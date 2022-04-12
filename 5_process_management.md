# 5. Process management
- a process is a unit for provisioning system resources
- it is any program, application, or command that runs on the system
- is created in memory in its own address space when a program, application, or command is initiated
- each process has a parent process that spawns it
- a single parent process may have one or many child processes and passes many of its attributes to them at the time of their creation
- each process is assigned a unique identification number, known as the process identifier (PID), which is used by the kernel to manage and control the process through its lifecycle
- when a process completes its lifecycle or is terminated, this event is reported back to its parent process, and all the resources provisioned to it are then freed and the PID is removed

```Don't root and drink!```

## Cheat sheet
```bash
ps aux    # list all processes
ps auxww  # list all processes in extra wide format
          # useful to display long commands that are trimmed by default
ps auxf   # hierarchy list all processes

kill PID    # terminate process
kill -9 PID # forcefully terminate process

pgrep -f "keyword"  # returns a list of PIDs that have "keyword" in command field
pkill -f "keyword"  # terminates all PIDs that have "keyword" in command field

command &        # run "command" and send it in background
nohup command &  # detach command from tty and run it in background

jobs             # display commands sent to run in background
fg               # bring last command send to background in foreground
bg               # resume commands paused with CTRL-Z

top, htop        # alternatives for process info
```

```Thou shalt not kill -9```
