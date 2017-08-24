# Developing Your Block

After cloning the [block template](block-template.md) repository, you are ready to develop your block.

A good resource for new block development is the {{ book.product }} base block along with other blocks that have functionality similar to the one you would like to develop.

The basic elements of a block that you will define are its [properties](#properties), [commands](#commands), and [inputs and outputs](#inputs-and-outputs).

Any required Python dependencies for your block can be added to your `requirements.txt` file and will be automatically installed when your block is installed.

Other elements of a block to keep in mind include [block patterns](block-patterns.md), the [nio framework](framework.md) (including [discoverability](framework.md#discoverability)), and [mixins](mixins.md).

## Base Block Class

All {{ book.product }} blocks inherit from the base block class. The first import in the block template's `example_block.py` is `nio.block.base`. If you explore the code inside `nio.block.base`, you'll find explanatory docstrings for each method—including methods to override in your custom block—along with higher-level context.

An important principle to remember when developing your block is that [signals are passed as lists](/service-design-patterns/understanding-signals.md#lists-of-signals).

### Methods to Override

The following methods from the base block are designed to be overridden:

#### life cycle management
  * `configure`: at the end of the `configure` method, the block is ready to receive signals. If an exception is raised during configure, the service will not start.
  * `start`: during start, a block begins to send out signals. This method needs to eventually return so that the block status can change to “started”. For this reason, anything that runs continuously, should be run in a new thread.
  * `stop`: after stop, the block stops sending out signals and cancels jobs.

#### signaling
  * `process_signals(<list of signals>, input_id)`: receives input signals.
  * `notify_signals(<list of signals>, output_id)`: emits signals from the block. This method isn't intended to be overridden, but should be called by the block to send out signals. For example, you will usually call `notify_signals` at the end of your `process_signals` method.

## Current {{ book.product }} Blocks

An additional resource for developing your custom block is the [nio-blocks library](https://github.com/nio-blocks). Search the nio-blocks library for a block that has similar functionality to the block you need. Explore its properties, methods, commands, inputs, outputs, [mixins](mixins.md), and any modules imported from the [framework](framework.md).

## Properties

Block properties are declared as class attributes and have a [property type](#property-types). For example, to declare a configurable speed property as an `IntProperty` type
```python
speed = IntProperty(title='Speed', default=30)
```
And in the _File Reader_ block type a `file` property is declared with a `FileProperty` type.
```python
file = FileProperty(title='File', default='/tmp/file.txt')
```
To obtain the value of a block property, call the property with a function invocation. For example, you can get the value of the speed property defined above with
```python
 self.setSpeed(self.speed())
 ```
If you want to use the `$` syntax to refer to your signal, pass in `signal` when you call the property. The _File Reader_ block accesses the value of the `file` property with
```python
 file = self.file(signal).value
 ```

### Property Types

Block properties can include the following types:

- **BoolProperty**<br>One of two mutually exclusive options.

- **StringProperty**<br>A valid Python string.

- **IntProperty**<br>A Python integer.

- **FloatProperty**<br>A Python float.

- **FileProperty**<br>A file stream.

- **ListProperty**<br>List properties hold a list of object types which contain properties themselves or can be {{ book.product }} types such as IntType.

- **ObjectProperty**<br>Object types contain properties themselves.

- **SelectProperty**<br>Select properties enumerate a list of options.

- **TimeDeltaProperty**<br>A duration property expressing the difference between two date, time, or datetime instances.

- **VersionProperty**<br>A version property with the format `(major.minor.build)`.

- **Property**<br>A property that can assume any type.

## Commands

Commands are declared as decorators.
  ```python
  from nio.block.base import Block
  from nio.command import command

  @command("emit")
  class MyBlock(Block):
    # properties and block methods here…

    # emit method that will be invoked when the "emit" command is received
    def emit(self, foo=None):
          self._emit_job(foo) # where you have set up your own _emit_job method…
  ```

## Inputs and Outputs

Inputs and outputs are declared as decorators.
  ```python
  from nio.block.base import Block
  from nio.block import output

  @output('false', label='False')
  @output('true', label='True')
  class MyBlock(Block):
    # properties and block methods here…

    def process_signals(self, signals):
      true_result, false_result = self._filter_signals(signals) # where you have set up your own _filter_signals method…

      # add any other functionality to process_signals

      self.notify_signals(true_result, 'true')
      self.notify_signals(false_result, 'false')
  ```