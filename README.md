# SOPS secrets manager using Nix

## Update sops file

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

```sh
mkdir -p ~/.config/sops/age
age-keygen -o ~/.config/sops/age/keys.txt
```

### From host key

```sh
cat /etc/ssh/ssh_host_ed25519_key.pub | ssh-to-age
```
