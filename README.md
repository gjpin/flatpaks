# Personal Flatpak repo

These Flatpaks are for personal use.
Please use official releases as recommended by the developers.

1. Generate GPG key for deployment (see below)
2. Create GitHub Actions secrets:
   - GPG_PRIVATE_KEY
   - GPG_PASSPHRASE
3. Add Flatpak repo: `flatpak remote-add --if-not-exists private https://gjpin.github.io/flatpaks/index.flatpakrepo`

# GPG key
```bash
# Create directory to store GPG keys
mkdir flatter
chmod 700 flatter

# Create GPG key
gpg --homedir flatter --quick-gen-key ghaction@github.io

# List all keys
KEY_ID=$(gpg --homedir flatter --list-secret-keys --with-colons \
  | awk -F: '/^sec/ {print $5; exit}')

# Export private key
gpg --homedir flatter --armor --export-secret-key ghaction@github.io

# Export public key
gpg --homedir flatter --armor --export ghaction@github.io
```

# References
- [flatter](https://github.com/andyholmes/flatter)
- [flatpak-github-actions](https://github.com/flatpak/flatpak-github-actions)