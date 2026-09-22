Get-ChildItem `
  "C:\Windows\System32", `
  "C:\Program Files", `
  "C:\Program Files (x86)", `
  "C:\Users\ak54743\AppData\Local\CitiSoftware" `
  -Include ssh.exe,ssh*.exe `
  -File -Recurse -ErrorAction SilentlyContinue |
Select-Object -ExpandProperty FullName
