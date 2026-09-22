Fix the Market Dev SSH authentication cleanly and safely.

Goal:
VS Code / Copilot should connect to Market Dev without repeatedly asking for the Unix password.

Current target:
Host: sd-f34e-972f.nam.nsroot.net
User: ak54743
Port: 22

Requirements:

1. Inspect the existing SSH setup first:
   - C:\Users\ak54743\.ssh
   - existing config
   - existing Market Dev RSA key pair
   - existing known_hosts
   - Git-for-Windows OpenSSH client

2. Do NOT delete existing Helix keys or unrelated SSH keys.

3. Verify the actual filename/path of the Market Dev public/private key instead of assuming it.

4. Use standard OpenSSH public-key authentication.
   - install ONLY the Market Dev public key into ~/.ssh/authorized_keys on Market Dev
   - set correct Unix permissions
   - never copy the private key to Unix

5. Configure C:\Users\ak54743\.ssh\config with a clean alias:

Host market-dev
    HostName sd-f34e-972f.nam.nsroot.net
    User ak54743
    Port 22
    IdentityFile <verified Market Dev private-key path>
    IdentitiesOnly yes

6. Configure VS Code Remote SSH to use the verified Git-for-Windows ssh.exe.

7. Test:
   ssh market-dev

The desired result is:
- no Unix password prompt
- host-key verification works
- VS Code Remote SSH works
- Copilot can execute remote commands without repeatedly requesting the Unix password

8. Do NOT store the Unix password in:
   - scripts
   - environment variables
   - VS Code settings
   - Copilot prompts
   - plaintext files

9. If corporate policy prevents public-key authentication, STOP and report the exact blocker rather than attempting an unsafe workaround.

Make the necessary safe configuration changes, test them, and report exactly what changed.
