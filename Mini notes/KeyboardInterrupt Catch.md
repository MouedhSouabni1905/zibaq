**Tags:** [[Sysadmin]]

To catch a keyboard interrupt in python:
```
 try:
    some_process
except KeyboardInterrupt:
    print("\nKeyboard interrupt received, exiting.")
    sys.exit(0)
```

To catch a keyboard interrupt in bash (doesn't work on child processes, like if you call a python server script from a bash script like this one it would not work):
```
trap 'handle_interrupt' INT

handle_interrupt() {
  echo "Process finished"
  exit 1
}

some_process
```