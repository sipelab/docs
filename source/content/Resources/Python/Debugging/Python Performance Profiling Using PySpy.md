---
title: Python Performance Profiling Using PySpy
source: https://docs.squirro.com/en/latest/technical/admin/troubleshooting/python-profiling-pyspy.html
author:
  - "[[Squirro Documentation]]"
  - jgronemeyer
created: 2025-03-25
tags:
  - clippings
  - python
  - debugging
  - tool
---
## Python Performance Profiling Using PySpy#

In general: Any problem report to Support or Engineering related to performance or hangs will yield much faster results with a PySpy Top snapshot or a dump or a flamegraph.

## Installation

```python
pip install py-spy
```

## Before You Start

To begin, you’ll need a PID of a target process:

#underconstruction 

## Common Flags

```python
-p, --pid <pid>              PID of a running python program to spy on
--full-filenames Show full Python filenames
-r, --rate <rate>            The number of samples to collect per second [default: 100]
-s, --subprocesses           Profile subprocesses of the original process
-n, --native                 Collect stack traces from native extensions written in Cython, C or C++
```

## TOP#

Great for these situations:

- What is this service doing?
- Why is a service/process slow?

Output:

```python
Total Samples 991
GIL: 2.20%, Active: 19.78%, Threads: 16

  %Own   %Total  OwnTime  TotalTime  Function (filename:line)
  8.79%   8.79%   0.330s    0.330s   readinto (socket.py:586)
  4.40%   4.40%   0.150s    0.150s   run (topic/background.py:534)
  0.00%   0.00%   0.120s    0.120s   run (flup/server/threadedserver.py:76)
  0.00%   8.79%   0.000s    0.330s   _get_and_deliver (kombu/transport/virtual/base.py:406)
  0.00%   8.79%   0.000s    0.330s   _read_status (http/client.py:268)
  0.00%   8.79%   0.000s    0.330s   _delete_source_id (topic/background.py:116)
  0.00%   0.00%   0.000s    0.120s   run_flup_daemon (common/daemonlauncher.py:89)
  0.00%   4.40%   0.000s    0.080s   POST (topic/items.py:849)
  0.00%   8.79%   0.000s    0.330s   get (kombu/utils/scheduling.py:56)
  0.00%   4.40%   0.000s    0.080s   wrapped_f (common/__init__.py:142)
  0.00%   8.79%   0.000s    0.330s   delete (elasticsearch/client/__init__.py:596)
  0.00%   8.79%   0.000s    0.330s   consume (kombu/mixins.py:197)
```

Here we can see that a source is being deleted.

## Dump a Stacktrace#

Great for these situations:

A process is stuck:

Output:

```python
Thread 1614 (active): "local.3"
    readinto (socket.py:586)
    _read_status (http/client.py:268)
    begin (http/client.py:307)
    getresponse (http/client.py:1346)
    _make_request (urllib3/connectionpool.py:421)
    urlopen (urllib3/connectionpool.py:677)
    perform_request (elasticsearch/connection/http_urllib3.py:229)
    perform_request (elasticsearch/transport.py:362)
    perform_request (common/tracing/elasticsearch_tracing.py:84)
    delete (elasticsearch/client/__init__.py:596)
    _wrapped (elasticsearch/client/utils.py:92)
    retry (index/retry.py:57)
    delete_document (index/writer.py:183)
    delete_document (index/item/writer.py:152)
    update_item (topic/background.py:88)
    _delete_source_id (topic/background.py:116)
    _on_task_delete_source_items (topic/background.py:70)
    _on_task (common/queue.py:1071)
    on_task (common/queue.py:992)
    _process_task (common/queue.py:528)
    <listcomp> (kombu/messaging.py:590)
    receive (kombu/messaging.py:590)
    _receive_callback (kombu/messaging.py:624)
    _callback (kombu/transport/virtual/base.py:633)
    _deliver (kombu/transport/virtual/base.py:983)
    _get_and_deliver (kombu/transport/virtual/base.py:406)
    get (kombu/utils/scheduling.py:56)
    _poll (kombu/transport/virtual/base.py:402)
    drain_events (kombu/transport/virtual/base.py:745)
    _drain_channel (kombu/transport/virtual/base.py:1001)
    get (kombu/utils/scheduling.py:56)
    drain_events (kombu/transport/virtual/base.py:963)
    drain_events (kombu/connection.py:323)
    consume (kombu/mixins.py:197)
    run (kombu/mixins.py:175)
    run (common/background.py:174)
    _bootstrap_inner (threading.py:916)
    _bootstrap (threading.py:884)
```

The stack is reversed, you can see it’s on a network socket waiting for a response of an Elasticsearch `delete` command.

## Record#

Great for these situations:

- Investigate slow performance
- Understanding the bottlenecks during a load test
- Performance regression testing: New code vs old code
- Generally pinpointing where time is spent. *Note:* Time is not equal to CPU load.

```python
py-spy record -p 1529 -o /tmp/flamegraph.svg
Sampling process 100 times a second. Press Control-C to exit.
...
Stopped sampling because Control-C pressed
Wrote flamegraph data to '/tmp/flamegraph.svg'. Samples: 6864 Errors: 0
```

You can use `-f speedscope` for a more interactive experience and can analyze the output file on the [Speedscope Site](https://www.speedscope.app/).

**Output:**

Full View:

[![image1](https://s3.amazonaws.com/download.squirro.net/docs/migrated-attachments/2571011002/2571011035.png)](https://s3.amazonaws.com/download.squirro.net/docs/migrated-attachments/2571011002/2571011035.png)

Zoomed in, we can see that it’s spending a lot of time in the `delete item` function of Squirro, which in turn is waiting on Elastic due to many roundtrips:

[![image2](https://s3.amazonaws.com/download.squirro.net/docs/migrated-attachments/2571011002/2571011049.png)](https://s3.amazonaws.com/download.squirro.net/docs/migrated-attachments/2571011002/2571011049.png)

## Tips and Caveats#

- You need root privileges
- Start recording during a time of action. If you record with py-spy and do nothing on the server, the flamegraph will mostly show flup/kombu doing a whole lot of nothing.
- For the record, consider using the `--function` switch, it will show you the function instead of the line number. This can be easier to read if you’re not familiar with the codebase.
- Don’t forget the `--subprocesses` flag if you have multi-process services, e.g. topicd, datasourced, machinelearningd, data loader with parallel flag etc.
- Use the `--native` flag if C libraries are at play.