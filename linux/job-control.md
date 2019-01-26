Ctl + z   # can suspend forground jobs 
bg # will make the suspended forground process background.
ps  # show now working process 
kill PID  # ps will return PID of every process, use kill to kill the process
(1) ps to get PID
(2) kill command for that PID
(3) if not response, send increasingly harsh signals to terminate it.
ps x | grep program_u_want_find
-SIGINT  2   # Interrupt signal.  Ctl-c is this case. 
kill -SIGTERM 2931  or kill -15 2931  # 终止 kill command 默认的signal, handle by program
kill -SIGKILL 2931  or  kill -9 2931   # 终止 Linux Kernel, not handle by program

