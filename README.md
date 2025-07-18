# Shadow Credentials Attack Tool

A Python POC implementation for performing shadow credentials attacks against Active Directory machine accounts.

## Features

- ✅ Implements Microsoft's exact binary structure for KeyCredentials
- ✅ Supports both NTLM and Kerberos authentication
- ✅ Generates compliant certificates with Smart Card Logon EKU
- ✅ Preserves existing credentials when adding new ones
- ✅ Enforces LDAPS with certificate validation
- ✅ Secure memory cleanup of sensitive data

## Installation

```bash
git clone https://github.com/404tb/shadowcreds
cd shadowcreds
pip install -r requirements.txt
```

## Usage

### Basic Authentication
```bash
python3 shadowcreds.py -d dc01.corp.local -u username -p password -t TARGET$
```

### Kerberos Authentication
```bash
export KRB5CCNAME=/path/to/ticket.ccache
python3 shadowcreds.py -d dc01.corp.local -k -t TARGET$
```

### Remove Credentials
```bash
python3 shadowcreds.py -d dc01.corp.local -k -t TARGET$ --remove
```

## Command Line Arguments

| Argument          | Description                                      |
|-------------------|--------------------------------------------------|
| `-d`, `--domain`   | Domain controller hostname (required)            |
| `-u`, `--username` | Username for NTLM authentication                 |
| `-p`, `--password` | Password for NTLM authentication                 |
| `-k`, `--kerberos` | Use Kerberos authentication from ccache          |
| `-t`, `--target`   | Target machine name (with $ suffix)              |
| `-o`, `--output`   | Base filename for key material output            |
| `-r`, `--remove`   | Remove shadow credentials                        |
| `-v`, `--verbose`  | Enable verbose output                            |


## Defense Considerations

- 🔍 Monitor for unexpected modifications to `msDS-KeyCredentialLink`
- 🔒 Restrict write permissions on machine accounts
- ⚠️ Enable "PKINIT Freshness" protection (Windows Server 2019+)
- 📊 Review certificate authentication events

## References

- [Microsoft KeyCredential Documentation](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-adts/a90263c5-75c6-4d90-8f51-d3e8f6b69861)
- [Shadow Credentials Attack Explained](https://posts.specterops.io/shadow-credentials-abusing-key-trust-account-mapping-for-takeover-8ee1a53566ab)
- [Whisker - A tool for manipulating msDS-KeyCredentialLink](https://github.com/eladshamir/Whisker)

## Legal Disclaimer

This tool is provided for **authorized security testing** and **educational purposes** only. Unauthorized use against systems without explicit permission is illegal.
