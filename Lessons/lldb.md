<!-- .slide: data-background="./Images/header.svg" data-background-repeat="none" data-background-size="40% 40%" data-background-position="center 10%" class="header" -->
# Debugging
<!-- Put a link to the slides so that students can find them -->

➡️ [**Slides**](/MOB-2.9-Technical-Seminar-MOB/Slides/lldb.html':ignore')

<!-- > -->

## Learning Objectives

By the end of this lesson, you should be able to...

- Describe the steps to follow when debugging
- Identify the debugging panels in Xcode
- Manipulate different types of breakpoints
- Write lldb commands to inspect an app state

<!-- > -->

## Debugging

The process of identifying and removing errors from software.

- Reproducing the error
- Identify the cause
- Making a hypothesis
- Implementing a solution
- Testing the solution

<!-- > -->

## Techniques

Once we reproduce the state in our app that has the issue we can:

- Check variables
- Observe behavior
- Turn on logging
- Manipulate state on the fly

All of these can be done with the help of breakpoints, LLDB  and other tools that come with Xcode.

<!-- > -->

## Breakpoints - a deeper dive

A breakpoint is a location in our program where we would like to halt execution.

We add breakpoints by clicking on a line number in the code editor.

Then we can find it in the **Breakpoint Navigator**

**WE DO:** *Test it out in sample app*

<!-- > -->

With a right click on the breakpoint we can disable, delete and edit a breakpoint.

**Editing**

- Define conditions
- Ignore x times before stopping
- Adding actions
- Continue after evaluating options

**WE DO:** *Test it out in sample app*

<!-- > -->

## Symbolic Breakpoints

If we know the name of the function we want to break on, we can use this type of breakpoint.

1. Press "+"
1. Enter this as symbol: `-[UIViewController viewDidLoad]`

**WE DO:** *Test it out in sample app*

<!-- > -->

## LLDB

We are familiar with the `po` command. Something interesting is that it not only serves to print out objects in the debug console but also lets us change values at runtime.

```
po view.backgroundColor = [UIColor purpleColor]
```

**YOU DO:** *Test it out in sample app, change cell's background color*

<!-- > -->

Changing values at runtime is useful when we have trouble reproducing the error in our app.

It's also useful when we need to get to code that's hard to reach (an example if an error check turn out to be != nil). Using LLDB we can manually make our error to be non-nil to test that path.

<!-- > -->

### What if we don't know the variable name?

As long as we have the memory address, we can use it in the debugger.

`[((UIView *)0x123456) setBackgroundColor: [UIColor purpleColor]] `

*The visual tool helps finding the memory address*

**YOU DO:** *Test it out in sample app, change table's background color*

<!-- > -->

## Inspecting code after a breakpoint

`(lldb) thread backtrace`

`(lldb) frame info`

This matches what we see in the Debug Navigator.

`(lldb) frame select 19`

**WE DO:** *Test it out in sample app*

<!-- > -->

## Stepping Over

Stepping over allows you to step to the next code statement (usually, the next line) in the context where the debugger is currently paused.

If the current statement is calling another function, LLDB will run until this function has completed and returned.

`(lldb) run` - relaunches the program without recompiling 😯

`(lldb) next`

**WE DO:** *Test it out in sample app*

<!-- > -->

## Stepping in

If the next statement is a function call, the debugger will move into the start of that function and then pause again.

`(lldb) step`

**WE DO:** *Test it out in sample app*

<!-- > -->

## Stepping out

Stepping out means a function will continue for its duration then stop when it has returned. From a stack viewpoint, execution continues until the stack frame is popped off.

`(lldb) finish`

**WE DO:** *Test it out in sample app*

<!-- > -->

## Examining data

`(lldb) frame variable`

Dumps the variables available to the current stack frame and line of code.

This matches the content found in the Variables View

**WE DO:** *Test it out in sample app*

<!-- > -->

## Additional Resources

[Guide to breakpoints](https://www.bugsee.com/blog/advanced-guide-using-breakpoints-xcode/)<br>
Book: Swift for Good Vol.I<br>
Book: Advanced Apple Debugging<br>
[Apple Docs on debugging](https://developer.apple.com/support/debugging)
