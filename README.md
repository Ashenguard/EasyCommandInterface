### Github

![](https://img.shields.io/github/license/Ashenguard/EasyCommandInterface)
![](https://img.shields.io/github/v/release/Ashenguard/EasyCommandInterface)
![](https://img.shields.io/github/downloads/Ashenguard/EasyCommandInterface/total)
***

### PYPI

![Downloads](https://static.pepy.tech/personalized-badge/EasyCommandInterface?period=total&units=international_system&left_color=grey&right_color=red&left_text=downloads)
![Downloads](https://static.pepy.tech/personalized-badge/EasyCommandInterface?period=month&units=international_system&left_color=grey&right_color=red&left_text=this+month)
![Downloads](https://static.pepy.tech/personalized-badge/EasyCommandInterface?period=week&units=international_system&left_color=grey&right_color=red&left_text=this+week)
***

### Discord

[![Discord](https://img.shields.io/discord/690930221930643467?label=Discord+(Click+to+join))](https://discord.gg/6exsySK)
***

# EasyCommandInterface

Sometimes running a project like flask or a discord bot will remove the flexibility of using console to send commands, This library will revive that with just a simple setup.

## How to install

To install just use following command

```shell
pip install EasyCommandInterface
```

If you are looking for latest beta/alpha, you can use following command

```shell
pip install --upgrade git+https://github.com/Ashenguard/EasyCommandInterface.git
```

# Example

```py
from EasyCommandInterface import CommandInterface

# Only one Interface is allowed, If you try to create another one CommandInterfaceError will be raised.
interface = CommandInterface()


# A simple command, All the arguments are passed as string.
# Example input: test 1 Hi "Hello World!"
# Result: TEST COMMAND: ('1', 'Hi', 'Hello world!')
@interface.command('test')
def _test(*args):
    print('TEST COMMAND:', args)


# Another command with fixed arguments! If 2 arguments is not passed, It will raise CommandExecutionError
# Example input: sum 5 5.5
# Result: 10.5
@interface.command('sum')
def _sum(a, b):
    print(float(a) + float(b))


# As default, All commands will be executed inside a separate thread, But if you set `thread` to `False`, Command will be executed inside the interface thread
# Example input: sleep
# Result: Nothing - Except for that the interface will not accept another command before this one ends.
@interface.command('sleep', thread=False)
def _sleep(*args):
    from time import sleep

    sleep(10)
    
# There is a known issue (Fetal Python Error) when the program ends if the interface is waiting for another command.
# So we recommend using the `stop` method inside a not threaded command to stop the input thread as soon as it receives the command.
# Calling this method outside will stop the thread AFTER it received another command.
@interface.command('exit', thread=False)
def _exit():
    interface.stop()

# To start the interface, just say START! 
interface.start()

# Since the interface will read all inputs as soon as it starts, If you need an input just use following method. Using `input` might not work as intended
value = interface.get_input('Input something: ')
print("Input received:", value)

# You should keep the program alive since as soon as main program ends, Interface will be closed.
# You can use other projects like a flask or discord bot or ... instead
while interface.is_alive():
    pass
```

***

### ??? There will be more tutorials and examples at [Wiki](https://git.agmdev.xyz/EasyCommandInterface/wiki) ???
