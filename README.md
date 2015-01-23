# ezdaemon
`ezdaemon` makes Unix-y daemons real easy. Just import ezdaemon.daemonize
and call it before whatever you want the daemon to be. A couple
gotchas:

1. It will disconnect your python process from stdin and stdout, so any
   print calls will not show up. This is because daemons are disconnected
   from any controlling terminal.
2. Similarly, the working directory is changed to the root folder. This
   is to prevent lockup in case any virtual volumes are unmounted. Just make
   sure any IO uses the absolute path.

## Example
```python
from ezdaemon import daemonize

def do_daemony_stuff():
    # your code here
    logfile = open('/some/absolute/path.log').read()  # IO needs abspath

if __name__ == "__main__":
    print "before daemon"  # this will print
    daemonize()
    print "in daemon"  # this will go to /dev/null (aka not print)
    do_daemony_stuff()
```
