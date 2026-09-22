Stop here. The key is fine; the command has a path typo.

You used something equivalent to:

$HOME.ssh\id_rsa_marketdev.pub

It needs the backslash:

$HOME\.ssh\id_rsa_marketdev.pub

Run only this now:

Test-Path "$HOME\.ssh\id_rsa_marketdev.pub"

Expected result:

True

Do not enter your password again yet. If it returns True, send me that result and I’ll give you the single next command to install the public key on Market Dev.
