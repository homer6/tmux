# Set up multiple windows and panes to multiple servers with tmux

If you ever find yourself needing to ssh into multiple machines and run commands on each of them at the same time, you can use this template to tailor a tmux session with multiple windows.

This script will create a tmux session that you can customize to your specific servers.
Once customized, you can place in github/gitlab to share with your team (and keep in sync when there are changes).

See the included ~/.tmux.conf for a few useful bindings.



## Create new session and attach
```
tmux new-session -d -s my_session_name -n first_window_name "ssh user@server001"

tmux split-window -h -t my_session_name:0 "ssh user@server002"
tmux split-window -h -t my_session_name:0 "ssh user@server003"
tmux split-window -h -t my_session_name:0 "ssh user@server004"
tmux select-layout -t my_session_name:0 tiled > /dev/null
tmux split-window -h -t my_session_name:0 "ssh user@server005"
tmux split-window -h -t my_session_name:0 "ssh user@server006"
tmux split-window -h -t my_session_name:0 "ssh user@server007"
tmux select-layout -t my_session_name:0 tiled > /dev/null
tmux select-pane -t my_session_name:0
tmux set-window-option -t my_session_name:0 synchronize-panes on > /dev/null

tmux new-window -d -t my_session_name:1 -n second_window_name "ssh user@server001"
tmux select-window -t my_session_name:1
tmux split-window -v -t my_session_name:1 "ssh user@server002"
tmux split-window -v -t my_session_name:1 "ssh user@server003"
tmux select-layout -t my_session_name:1 even-vertical > /dev/null

tmux a -t my_session_name





# delete session
CTRL-b :kill-session
```



## Detach session
```
CTRL-b d
```


## Delete session
```
CTRL-b :kill-session
```


## Delete window
```
CTRL-b &
```


## Delete pane
```
CTRL-b x
```


## List sessions
```
tmux ls
```



## Supported Layouts
```
     even-horizontal
             Panes are spread out evenly from left to right across the window.

     even-vertical
             Panes are spread evenly from top to bottom.

     main-horizontal
             A large (main) pane is shown at the top of the window and the remaining panes are spread from left to right in the leftover space at the bottom.  Use the main-pane-height window option to specify the height of the top pane.

     main-vertical
             Similar to main-horizontal but the large pane is placed on the left and the others spread from top to bottom along the right.  See the main-pane-width window option.

     tiled   Panes are spread out as evenly as possible over the window in both rows and columns.
```




## Links

http://hyperpolyglot.org/multiplexers

https://tmuxcheatsheet.com/