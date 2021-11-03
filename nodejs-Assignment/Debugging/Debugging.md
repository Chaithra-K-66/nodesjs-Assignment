Debugging with nodejs

Debug Node.js application using various tools including following:

1.The Console Object

2.Node Inspector

3.Built-in debugger in IDEs

1)The Console Object
The simplest form of debugging is simple logging. The console is a global
object available in Node.js. It is intentionally designed to mimic the behavior
of a web browser’s console object. 

Simple Logging
The simplest behavior of console.log is that it will take any number of
arguments and call util.inspect (from the Node.js core util module)
on each of these, separated by a space and followed by a new line.

1)

If the first argument to console.log is a string and it
contains one of the placeholders, these placeholders are replaced (with
formatting) from the remaining arguments to console.log. The following
placeholders are supported (same as util.format function):
%s - String
%d - Number (both integer and float)
%j - JSON
A single percent sign ('%') in the absence of a category (s/d/j) does
not consume an argument. However, you can always double up the percent
sign ('%%') to prevent it from looking at the next character (which may or
may not be one of s/d/j) and print a single %.

2)

Simple Benchmark

There are two functions, console.time and console.timeEnd, that
can be used to instrument your code quickly and painlessly so you don’t waste
time looking at the wrong place. They simply take a label and on
console.timeEnd print out the label + the duration since the last moment
'console.time' was called with the same label. In the absence of a label,
undefined will get used socan use that as well for quick throwaway
tests.
3)

A Quick Way to Get the Call Stack

To get the stack trace to see why a particular function is being
called and by whom. You can get a quick printout of the call stack using the
console.trace function, which optionally takes a label to display for the
particular stack trace.
4)

Print to stderr

The console.log function outputs to the program’s stdout stream. The
console.error function has the same behavior as console.log
except that it prints to stderr.
The program as a function, then this function always returns an object with two values,
stdout and stderr. This makes stdout clear of any error messages and
safe to pipe between applications.
5)

Node’s Built-in Debugger

A quick debugging strategy is to insert a debugger statement in your code
where  want to break (and debug) and then start your node application by
passing in the debug argument to node:
		$ node debug yourscript.js
Note You pass arguments to node by mentioning them after node but
before your script name. We already saw a usage of this in the previous
chapter where we using the --harmony flag. Such arguments do not become
a part of 'process.argv' and therefore do not pollute your argument
processing logic inside your code. These are simply processed by node
internally.
Using the debug argument will do the following:
	> Start your application
	> Pause before executing the first line of your JavaScript
	> Give you a shell to control you application flow
The debugger shell has a bunch of commands, but since we are focused on
quick debugging in this section, all you need to know are the following:
a)Control flow
	c continue execution
	n next step (this is step over if you are familiar with traditional debuggers)
	restart restarts the script
b)Observe state
	watch(expression:string) adds a watch
	unwatch(expression:string) removes a watch
	repl open the Node.js REPL with current context. Press Ctrl+C to exit the REPL.
	bt backtrace, prints the call-stack
6)

Node-inspector

If all you need is a quick way to debug a Node.js application, we highly
recommend node-inspector. Node-inspector is a tool dedicated solely
to debugging Node.js applications. It is built on top of the chrome developer
tools platform, so if you are used to debugging browser applications using
chrome, you will feel right at home with it. First, you need to install it, which
is easily done using "npm install -g node-inspector".

To debug a script using node-inspector, you simply use nodedebug instead of node.
7)

Remote Debugging Node.js:

You can start a node process in debug mode using the --debug flag:
	$ node --debug yourfile.js
Additionally, if you use the --debug-brk flag, the node process starts
in debug mode with a break on the first line waiting for a debugger to connect
before it executes any JavaScript:
	$ node --debug-brk yourfile.js
Once you start a node process in debug mode, by default it listens on port
5858 to accept incoming connections for debugging (using the V8 TCP based
debugging protocol). You can change the port node listens on by passing an
optional value to –debug. For example, the following node process will
listen on port 3333 for a debugger to connect.
	$ node --debug=3333 yourfile.js
The same port option exits for --debug-brk (for example, --debugbrk=3333). The principle of remote debugging Node.js is the same in all
the debuggers. In other words, start the node process in debug mode and then
connect to it. 

