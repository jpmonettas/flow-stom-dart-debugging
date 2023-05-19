# Debugging the compiler with FlowStorm

- Clone this repo
- Initialize the ClojureDart project by running `clj -M:cljd init`
- Run `clj -A:dev` to start a repl with ClojureDart and the debugger loaded
- Start the debugger by evaluating the `:dbg` keyword on the repl
- Run `((requiring-resolve 'cljd.build/-main) "flutter" "-d" "linux")` (or whatever arguments you normally give to flutter)
- Wait for the app window to show, so we know startup compilation finished
- Proposed debugging workflow
  - Start recording (hit the recording button at the top left bar)
  - LOOP
     - Clear debugger state (Ctrl-L) (so you don't get confused by previous recordings)
     - Modify your src/acme/main.cljd and save it (so we fire a recompilation and record everything)
	 - Open the main thread
     - Debug

# On debugging

While recording is on, because there is a thread that is constantly polling for changes
if you keep refreshing the tree tool you will see new invocations of cljd.build/compile-cli.compile-files.

There will be nothing interesting there until you capture a file compilation. Once you recompile a file you will
get some calls to compile-files that you can expand further.

I find much more useful in this case to jump to the functions tool (the last tab on the thread bottom left corner), so jump to it.

Lets say you are interested in understanding/debugging code emission. 

After you refresh the list (to be sure you have the latest captures), you can use the filter at the top to search for something like `emit-def`

If you double click on `cljd.compiler/emit-def` you should see on the right all calls to emit-def arguments.
You should see something like `[(def main (cljd.core/fn ...))]`. 

If you double click on it, it will take you to the code stepping tool, where you can use the keyboard, the mouse or the controls at the top to step over your
code, inspect values, locals, stack traces, define values for your repl, etc.

Take a look at the user guide or the tutorial for how to use
all those tools.

Happy debugging!

FlowStorm repo: https://github.com/jpmonettas/flow-storm-debugger 

FlowStorm user guide: https://jpmonettas.github.io/flow-storm-debugger/user_guide.html

