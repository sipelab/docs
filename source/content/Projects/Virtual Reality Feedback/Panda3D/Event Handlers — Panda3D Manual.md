---
title: "Event Handlers — Panda3D Manual"
source: "https://docs.panda3d.org/1.10/python/programming/tasks-and-events/event-handlers"
author:
published:
created: 2025-02-22
description:
tags:
  - "clippings"
  - "panda3d"
---
Events occur either when the user does something (such as clicking a [mouse](https://docs.panda3d.org/1.10/python/programming/hardware-support/mouse-support#mouse-support) or pressing a [key](https://docs.panda3d.org/1.10/python/programming/hardware-support/keyboard-support#keyboard-support)) or when sent by the script using [`messenger.send()`](https://docs.panda3d.org/1.10/python/reference/direct.showbase.Messenger#direct.showbase.Messenger.Messenger.send "direct.showbase.Messenger.Messenger.send")

## Defining a class that can Handle Events

The first step is to import the [`DirectObject`](https://docs.panda3d.org/1.10/python/reference/direct.showbase.DirectObject#module-direct.showbase.DirectObject "direct.showbase.DirectObject") module:

```
from direct.showbase import DirectObject
```

With DirectObject loaded, it is possible to create a subclass of DirectObject. This allows the class to inherit the messaging API and thus listen for events.

```
class myClassName(DirectObject.DirectObject):
```

```
class Hello(DirectObject.DirectObject):
    def __init__(self):
        self.accept('mouse1', self.printHello)

    def printHello(self):
        print('Hello!')

h = Hello()
```

## Event Handling Functions

An object may accept an event an infinite number of times or accept it only once. If checking for an accept within the object listening to it, it should be prefixed with self. If the accept command occurs outside the class, then the variable the class is associated with should be used.

```
myDirectObject.accept('Event Name', myDirectObjectMethod)
myDirectObject.acceptOnce('Event Name', myDirectObjectMethod)
```

Finally, there are some useful utility functions for debugging. The messenger typically does not print out when every event occurs. Toggling verbose mode will make the messenger print every event it receives

```
messenger.toggleVerbose()
print(messenger)
messenger.clear()
```

## Sending Custom Events

Custom events can be sent by the script using the code

```
messenger.send('Event Name')
```

## A Note on Object Management

When a DirectObject accepts an event, the messenger retains a reference to that DirectObject. To ensure that objects that are no longer needed are properly disposed of, they must ignore any messages they are accepting.

One solution (patterned after other parts of the Panda3D architecture) is to define a “destroy” method for any custom classes you create, which calls “ignoreAll” to unregister from the event-handler system.

```
import direct.directbase.DirectStart
from direct.showbase import DirectObject
from panda3d.core import *

class Test(DirectObject.DirectObject):
    def __init__(self):
        self.accept("FireZeMissiles", self._fireMissiles)

    def _fireMissiles(self):
        print("Missiles fired! Oh noes!")

    # function to get rid of me
    def destroy(self):
        self.ignoreAll()

foo = Test()  # create our test object
foo.destroy() # get rid of our test object

del foo

messenger.send("FireZeMissiles") # No missiles fire
base.run()
```

## Coroutine Event Handlers

It is permissible for any event handler to be a [coroutine](https://docs.panda3d.org/1.10/python/glossary#term-coroutine) (i.e. marked as an `async def`), which permits use of the `await` keyword inside the handler. Usage is otherwise identical to a regular event handler.

```
class Test(DirectObject):
    def __init__(self):
        self.accept('space', self.on_space)

    async def on_space(self):
        await Task.pause(1.0)
        print("The space key was pressed one second ago!")
```