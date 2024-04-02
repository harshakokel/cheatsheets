
## Basic

| Description 				| Command 				|
|---------------------------------------|---------------------------------------|
| Start a new session with session name | `screen -S <session_name>`		|
| List running sessions / screens	      | `screen -ls`				|
| Attach to a running session		        | `screen -x`				|
| Attach to a running session with name	| `screen -r <session_name>`		|
| Detach a running session		          | `screen -d <session_name>`		|
| Kill a running session                | `screen -X -S [session # you want to kill] kill` |
| Kill an attached session                | `exit` |
| Rename a session                | `screen -S <session_name> -X sessionname <new_name>` |
| Accessing a screen that is already attached | `screen -r -d [session name]` |
| Enable/disable vertical scrolling mode* in a running session		| `Ctrl-a ESC`		|

