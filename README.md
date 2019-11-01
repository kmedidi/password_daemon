# password_daemon
Exploring the possibility: A daemon which saves ssh passwords in encrypted form

Two functions based on need:
1) Need: Lazy mode -> Store ssh passwords in a file and auto-populate when ssh command is entered
2) Need: Secure mode -> 1) Authenticate on log-in 2) Store ssh passwords in encrypted form 3) Prompt for authentication sometimes

Implementation
A) Lazy mode
1) Create a daemon service that runs on boot and listens for ssh commands being executed
2) Once ssh process is detected in the ps command output, observe if SSH authentication is successful.
3) If yes, use ssh-copy-id and copy the local public key to remote hosts.
4) If this isn't possible, intervene [and prompt for authentication (only first time)]
5) If authenticated, prompt for the ssh password and store it.
6) If ssh password for the host is already stored and authentication has been completed, intervene and provide ssh password.

