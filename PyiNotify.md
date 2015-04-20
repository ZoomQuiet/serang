StepByStep

这么简单就可以监控目录/文件变化了，真伟大

```
from pyinotify import *

import os, os.path  

flags = IN_CLOSE_WRITE|IN_CREATE|IN_Q_OVERFLOW|IN_IGNORED
dirs = {}  
base = "/home/serang/apps"
   
class PTmp(ProcessEvent):
    def process_IN_CREATE(self, event):
        print "Create: %s" %  os.path.join(event.path, event.name) 
    def process_IN_DELETE(self, event):
        print "Remove: %s" %  os.path.join(event.path, event.name) 
    def process_IN_IGNORED(self, event): 
        print "Remove1: %s" %  os.path.join(event.path, event.name) 
        
        
wm = WatchManager()  
notifier = Notifier(wm, PTmp())  
dirs.update(wm.add_watch(base, flags, rec=True, auto_add=True))  

notifier.loop()  

```