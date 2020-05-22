# Using Yubico as sudo auth

## Configuring Slot 2 as Challenge Response

```bash
ykman otp chalresp --touch --generate 2 
```

## Necessary Packages

```bash
sudo add-apt-repository ppa:yubico/stable
sudo apt update
sudo apt install \
    libpam-yubico \
    yubikey-personalization
```

## Configure /etc/pam.d/sudo

Insert the following line before `@include common-auth`.

```
auth       sufficient   pam_yubico.so mode=challenge-response chalresp_path=/var/yubico
```

## Confgiure pam_yubico

Make a directory for the mappings.

```bash
sudo mkdir /var/yubico
sudo chown root:root /var/yubico
sudo chmod 700 root:root /var/yubico
```

## Enroll the yubico key

As the user to enroll insert the yubico

```
ykpamcfg -2 -v
sudo mv ~/.yubico/challenge-... /var/yubico/"$(whoami)"}-...
chmod 600 /var/yubico/*
chown root:root /var/yubico/*
```
