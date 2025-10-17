# encbackup

A lightweight Bash utility to compress and encrypt or decrypt and extract directories and files using tar, lz4, and gpg.  
It is intended for simple, secure, and scriptable backups without leaving unencrypted data on disk.

---

## Features

- Strong AES-256 symmetric encryption via GnuPG.
- Fast lz4 compression before encryption.
- Works with both files and directories.
- Reads passphrases from a file or environment variable for non-interactive use.
- Minimal dependencies: only bash, tar, lz4, and gpg.

---

## Usage

    encbackup [options] (-e | --encrypt | -d | --decrypt) source destination

### Modes
- -e, --encrypt — Compress and encrypt a file or directory.
- -d, --decrypt — Decrypt and extract a previously encrypted archive.

### Arguments
| Argument | Description |
|-----------|-------------|
| source | The directory or file to encrypt, or the encrypted file to decrypt. |
| destination | The output file (for encryption) or extraction directory (for decryption). |

### Options
| Option | Description |
|---------|-------------|
| -h, --help | Show help and exit. |
| --passphrase-file FILE | Read passphrase from a file. |
| --passphrase VAR | Read passphrase from an environment variable. |

---

## Examples

### Encrypt a directory
    encbackup --encrypt /path/to/source /path/to/backup.gpg

### Decrypt an archive
    encbackup --decrypt /path/to/backup.gpg /path/to/restore/

### Use a passphrase file
    encbackup --encrypt --passphrase-file ~/.encbackup-pass secret-data/ secret-data.gpg

### Use an environment variable
    export BACKUP_KEY="s3cur3p4ss"
    encbackup --decrypt --passphrase BACKUP_KEY archive.gpg ./restored/

---

## How it works

- Encryption:  
  tar collects files, lz4 compresses them, and gpg encrypts using AES-256.  
  Produces a single .gpg file.

- Decryption:  
  gpg decrypts, lz4 decompresses, and tar restores the files.

---

## Dependencies

| Tool | Purpose |
|------|----------|
| tar | Create and extract archives |
| lz4 | High-speed compression |
| gpg | Encryption and decryption |

Install on Debian/Ubuntu:
    sudo apt install tar lz4 gpg

Install on Fedora/Redhat:
    sudo dnf install tar lz4 gpg

---

## Security notes

- Uses AES-256 symmetric encryption.
- Passphrases can be interactive, read from a file, or taken from environment variables.
- Passphrases are cleared from memory after use.
- Protect passphrase files with strict permissions (chmod 600 file).

---

## License

Licensed under the GNU General Public License v3 or later (GPLv3+).  
See the LICENSE file for details.
