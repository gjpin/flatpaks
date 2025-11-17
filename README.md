# Personal Flatpak repo

These Flatpaks are for personal use.
Please use official releases as recommended by the developers.

1. Generate GPG key for deployment (see below)
2. Create GitHub Actions secrets:
   - GPG_PRIVATE_KEY
   - GPG_PASSPHRASE

# GPG key
```bash
# Create directory to store GPG keys
mkdir flatter
chmod 700 flatter

# Create GPG key
gpg --homedir flatter --quick-gen-key username@github.io

# List all keys
KEY_ID=$(gpg --homedir flatter --list-secret-keys --with-colons \
  | awk -F: '/^sec/ {print $5; exit}')

# Export only subkey
gpg --homedir flatter --export-secret-subkeys --armor $KEY_ID > gpg-private-sub-key.asc

# Get private sub key
cat gpg-private-sub-key.asc
```

# References
- [flatter](https://github.com/andyholmes/flatter)
- [flatpak-github-actions](https://github.com/flatpak/flatpak-github-actions)