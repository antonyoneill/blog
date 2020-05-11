
# Using Yubico for LUKS

## Configuring Slot 2 as Challenge Response

If not already done so:

```bash
ykpersonalize -2 -ochal-resp -ochal-hmac -ohmac-lt64 -oserial-api-visible
```

## Necessary Packages

```bash
sudo apt install \
    yubikey-luks
```

## Configure LUKS

Check for a free LUKS slot
```
sudo cryptsetup luksDump <device>
```

Enroll yubikey & choose passphrase. You will need to confirm an existing passphrase
```
sudo yubikey-luks-enroll -s <slot> -d <device>
```

Note: The --test-passphrase functionality does not work with the yubikey-luks program.

# References
- https://blog.mimacom.com/fde-with-yubikey/

