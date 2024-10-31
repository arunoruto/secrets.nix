# SOPS secrets manager using Nix

## Update sops file

Add the wanted keys to the `secrets.yaml` file
and then then run the following command to encrypt the data.

```sh
sops updatekeys secrets.yaml
```

And commit + push to the private repo

## Update flake

```sh
nix flake lock --update-input secrets
```

## Hangup on home-manager switch

1. Try a refresh command:

```sh
home-manager switch --refresh --flake .#mirza
```

2. Use `systemctl` to reload failed services:

```sh
systemctl --user reset-failed
```

## Keys

Add these keys to `.sops.yaml`.

### Standalone

Create a standalone key for the user to be used.
Reference it in the `users` section after creating it.

```sh
mkdir -p ~/.config/sops/age
age-keygen -o ~/.config/sops/age/keys.txt
```

### Host Key

Create an `age` key from the hosts SSH key found in `/etc/ssh`.
Please use the ed25519 key or something stronger in the future :)
Add the key to the `hosts` sections.

```sh
cat /etc/ssh/ssh_host_ed25519_key.pub | ssh-to-age
```
