# Reverse SSH Tunnels

**-L** is a local tunnel (YOU <-- CLIENT). If a site was blocked, you can forward the traffic to a server you own and view it. For example, if imgur was blocked at work, you can do **ssh -L 9000:imgur.com:80 user@example.com.** Going to localhost:9000 on your machine, will load imgur traffic using your other server.

**-R** is a remote tunnel (YOU --> CLIENT). You forward your traffic to the other server for others to view. Similar to the example above, but in reverse.

If we run **ss -tulpn** it will tell us what socket connections are running

| Argument | Description         |
| -------- | ------------------- |
| -t       | Display TCP sockets |
| -u       | Display UDP sockets | 

-l

Displays only listening sockets

-p

Shows the process using the socket

-n

Doesn't resolve service names
