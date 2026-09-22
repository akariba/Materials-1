Good — Git for Windows is installed, and PowerShell found it here:

C:\Users\ak54743\AppData\Local\CitiSoftware\CTC1029056_GITFORWINDOWSPORTABLE_2.45.0\cmd\git.exe

Now locate the bundled ssh.exe.

Run this exact PowerShell command:

Get-ChildItem "C:\Users\ak54743\AppData\Local\CitiSoftware\CTC1029056_GITFORWINDOWSPORTABLE_2.45.0" -Filter ssh.exe -Recurse -ErrorAction SilentlyContinue | Select-Object -ExpandProperty FullName

You will likely get something similar to:

C:\Users\ak54743\AppData\Local\CitiSoftware\CTC1029056_GITFORWINDOWSPORTABLE_2.45.0\usr\bin\ssh.exe

Then test the returned executable:

& "PASTE-THE-SSH-PATH-HERE" -V

For example:

& "C:\Users\ak54743\AppData\Local\CitiSoftware\CTC1029056_GITFORWINDOWSPORTABLE_2.45.0\usr\bin\ssh.exe" -V

If that prints an OpenSSH version, test Market Dev directly:

& "C:\Users\ak54743\AppData\Local\CitiSoftware\CTC1029056_GITFORWINDOWSPORTABLE_2.45.0\usr\bin\ssh.exe" ak54743@sd-f34e-972f.nam.nsroot.net

If that connects, configure VS Code with that exact executable path:

"remote.SSH.path": "C:\\Users\\ak54743\\AppData\\Local\\CitiSoftware\\CTC1029056_GITFORWINDOWSPORTABLE_2.45.0\\usr\\bin\\ssh.exe"

Then restart VS Code and use:

Remote-SSH: Connect to Host → market-dev → Linux

Run the Get-ChildItem ... ssh.exe command first and send me the result.
