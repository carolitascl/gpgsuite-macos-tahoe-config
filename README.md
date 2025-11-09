## 1. Download and Install GPG Suite

```bash
https://gpgtools.org/
```

## 2. Install 'gnupg' from homebrew

```bash
brew install gnupg
```
   
## 3. Install 'pinentry-mac' from homebew

```bash
brew install pinentry-mac
```
   
## 4. Create symlinks

```bash
# Create symlinks so GPG Keychain finds Homebrew's tools
# Keep GPG Keychain installed but it will now use Homebrew's binaries

sudo mkdir -p /usr/local/MacGPG2/bin
sudo ln -sf /opt/homebrew/bin/gpg /usr/local/MacGPG2/bin/gpg
sudo ln -sf /opt/homebrew/bin/gpg-agent /usr/local/MacGPG2/bin/gpg-agent
sudo ln -sf /opt/homebrew/bin/dirmngr /usr/local/MacGPG2/bin/dirmngr
sudo ln -sf /opt/homebrew/bin/gpgconf /usr/local/MacGPG2/bin/gpgconf
 ```

## 5. Create or modify this hidden files in your computer under the home folder


### ~/.gnupg/gpg.conf
---

```bash
# Default key for signing/encryption

### Change the Xs with the default gpg
default-key XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

# Keyserver configuration
keyserver hkps://keys.openpgp.org
auto-key-retrieve

# Display options
keyid-format 0xlong
with-fingerprint
list-options show-uid-validity
verify-options show-uid-validity

# Algorithm preferences (strongest first)
personal-cipher-preferences AES256 AES192 AES
personal-digest-preferences SHA512 SHA384 SHA256
personal-compress-preferences ZLIB BZIP2 ZIP Uncompressed
default-preference-list SHA512 SHA384 SHA256 AES256 AES192 AES ZLIB BZIP2 ZIP Uncompressed

# Certificate digest algorithm
cert-digest-algo SHA512

# Charset
charset utf-8

# Don't include version in output
no-emit-version

# Don't include comments in signatures
no-comments

# Disable photo viewer
list-options no-show-photos
verify-options no-show-photos

# Trust model
trust-model tofu+pgp

# Use agent for passphrases
use-agent

# Timeout for keyserver operations (seconds)
keyserver-options timeout=10

```

### ~/.gnupg/gpg-agent.conf
---

```bash
# Pinentry program (GUI password prompt)
pinentry-program /opt/homebrew/bin/pinentry-mac

# Cache settings - balance security and convenience
default-cache-ttl 600        # 10 minutes of inactivity
max-cache-ttl 3600           # 1 hours maximum

# SSH support (if using GPG for SSH keys)
enable-ssh-support

# Logging (comment out in production, useful for debugging)
# log-file /Users/admin/.gnupg/gpg-agent.log
# debug-level basic

# Allow unattended passphrase entry (for scripts)
allow-preset-passphrase

# Grab keyboard/mouse during passphrase entry (security)
grab

# Ignore requests from other users
no-allow-external-cache

# Don't allow mark as trusted on first use
no-allow-mark-trusted

```

### ~/.gnupg/dirmngr.conf
---

```bash
# Keyserver configuration
keyserver hkps://keys.openpgp.org

# Fallback keyserver
# keyserver hkps://keyserver.ubuntu.com

# Use system resolver instead of internal
standard-resolver

# Disable IPv6 if having connectivity issues
# disable-ipv6

# Honor HTTP proxy from environment
# honor-http-proxy

# OCSP responder (for certificate validation)
allow-ocsp

# Logging (comment out in production)
# log-file /Users/admin/.gnupg/dirmngr.log
# debug-level basic
```
