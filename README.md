Next step only

Open Windows PowerShell and run:

$ssh = "C:\Users\ak54743\AppData\Local\CitiSoftware\CTC1829056_GITFORWINDOWSPORTABLE_2.45.0\usr\bin\ssh.exe"

Get-Content "$HOME\.ssh\id_rsa_marketdev.pub" |
& $ssh ak54743@sd-f34e-972f.nam.nsroot.net `
'umask 077; mkdir -p ~/.ssh; cat >> ~/.ssh/authorized_keys; chmod 700 ~/.ssh; chmod 600 ~/.ssh/authorized_keys'

It should ask for your Market Dev password one final time.

After it completes, test the new key explicitly:

& $ssh -i "$HOME\.ssh\id_rsa_marketdev" ak54743@sd-f34e-972f.nam.nsroot.net

Expected result: it should connect without asking for the Market Dev password. If you created the key with a passphrase, it may ask for the key passphrase instead; we can automate that safely with ssh-agent next.
