---
title: How to Visualize your Python Project’s Dependency Graph - Gauge - Solving the monolith/microservices dilemma
source: https://www.gauge.sh/blog/how-to-visualize-your-python-projects-dependency-graph
author: 
published: 
created: 2025-03-21
description: How to Visualize your Python Project’s Dependency Graph. Gauge is solving the monolith/microservices dilemma. We’re building tools to untangle codebases through incremental modularization. Our open-source toolkit supports defining and enforcing rules for interfaces and dependencies. By focusing on high cohesion and loose coupling, you can unlock a codebase that your engineers and AI love to work in. Improve quality and developer velocity at the same time.
tags:
  - clippings
  - python
  - debugging
  - tutorial
  - tool
---
Understanding your project’s dependency graph is important for a number of reasons:

- Education ->Visualization helps new developers easily understand how things should be structured and where new functionality should go.
- Refactoring → Understanding how a certain module is used and what its dependencies are creates a clear path to modifying or removing it.
- Code Quality → Easily identify circular module level dependencies, poor design decisions, and weak points, such as tightly coupled modules.

With [Tach](https://github.com/gauge-sh/tach), you can easily visualize the set of dependencies that exist within your Python project.  Here’s how:

### 1\. Install Tach

`> pip install tach   `

The first step is straightforward - install `Tach` and make sure you’re on the latest version.

### 2\. Define module boundaries

`> tach mod   `

Next, we need to define the modules within your project that we want to visualize dependencies between. The `tach mod` command opens up an editor in which you can mark modules and your Python source root. Here are the commands you need:

- up/down/left/right arrow: navigate
- enter: mark directory or file as module
- Ctrl + a: Mark all files or directories at the current level as modules
- s: mark directory as Python source root
- Ctrl + s: save

We’ll use the [FastAPI repo](https://github.com/tiangolo/fastapi) as an example. Here’s what this looks like for FastAPI before saving:

![](https://cdn.prod.website-files.com/665a5f120c4c63df1944d627/67632a8c299027767879f67d_6684a5da6ceadfaa7137be95_fastapi_mod.png)

### 3\. Sync your dependencies to Tach

In order to correctly visualize your existing dependencies, Tach will [crawl the Python AST](https://www.gauge.sh/blog/parsing-python-asts-20x-faster-with-rust) to figure out which modules import from each other. This can be achieved by running:

`> tach sync   `

![](https://cdn.prod.website-files.com/665a5f120c4c63df1944d627/6789969dbc83993a9fc3d742_67899671f7d8eaca00a53ea2_Screenshot%25202025-01-16%2520at%252015.24.40.png)

Here’s a slice of what Tach found for the above configuration:

![](https://cdn.prod.website-files.com/665a5f120c4c63df1944d627/6789969dbc83993a9fc3d74e_67899625e126a75f4f09c2f6_Screenshot%25202025-01-16%2520at%252015.23.52.png)

### 4\. View your dependencies with Tach

The final step is the easiest. Run `tach show --web`, and click on the generated URL to view your dependency graph! You can also view a local version of the graph through GraphViz using the base command `tach show` .

![](https://cdn.prod.website-files.com/665a5f120c4c63df1944d627/6789969dbc83993a9fc3d752_678995d64206504d365d7365_Screenshot%25202025-01-16%2520at%252015.27.04.png)

[Here’s the link for FastAPI!](https://app.gauge.sh/show?uid=227d60d7-20b5-4999-9fbf-2b780a68eb9d)

You can also click and drag on modules/edges to learn more about their dependencies:

![](https://cdn.prod.website-files.com/665a5f120c4c63df1944d627/6789988a82ab5149905dbe24_678997e662d6b89cb77c3532_Screenshot%25202025-01-16%2520at%252015.35.05.png)

By following the above steps, you can easily visualize your project’s set of Python dependencies, and inform future architecture decisions.

Tach also enables you to [enforce boundaries](https://docs.gauge.sh/getting-started/getting-started#setup) between modules, as well as define [strict interfaces](https://docs.gauge.sh/usage/interfaces) for a given module. If there’s a feature you’d like to see in Tach, feel free to [drop an issue](https://github.com/gauge-sh/tach/issues) or join the discussion on [Discord](https://discord.gg/a58vW8dnmw)!

‍