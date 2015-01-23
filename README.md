# daemonize
Daemonize makes Unix-y daemons real easy. Just import daemonize.daemonize
and call the function before whatever you want the daemon to be. A couple
gotchas:

    1. It will disconnect your python process from stdin and stdout, so any
       print calls will not show up. This is because daemons are disconnected
       from any controlling terminal.

    2. Similarly, the working directory is changed to the root folder. This
       is to prevent lockup in case any virtual volumes are unmounted. Just make
       sure any IO uses the absolute path.
