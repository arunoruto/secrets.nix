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
