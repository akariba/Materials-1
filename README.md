Next step — only verify Node on the Unix server

From the same PowerShell window, run these two commands separately using your working SSH executable:

& "C:\Users\ak54743\AppData\Local\CitiSoftware\CTC1829056_GITFORWINDOWSPORTABLE_2.45.0\usr\bin\ssh.exe" ak54743@sd-f34e-972f.nam.nsroot.net "node --version"

Then:

& "C:\Users\ak54743\AppData\Local\CitiSoftware\CTC1829056_GITFORWINDOWSPORTABLE_2.45.0\usr\bin\ssh.exe" ak54743@sd-f34e-972f.nam.nsroot.net "npm --version"
