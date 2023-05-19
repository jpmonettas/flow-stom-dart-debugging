# Debugging the compiler with FlowStorm

- Run clj -A:dev
- Start the debugger with :dbg (make sure recording is off)
- Run `((requiring-resolve 'cljd.build/-main) "flutter" "-d" "linux")`
- Debugging workflow loop
  - Clear debugger state
  - Start recording
  - Modify your src/acme/main.cljd
  - Debug
