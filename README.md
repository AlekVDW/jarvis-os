# jarvis-os &nbsp; [![bluebuild build badge](https://github.com/alekvdw/jarvis-os/actions/workflows/build.yml/badge.svg)](https://github.com/alekvdw/jarvis-os/actions/workflows/build.yml)

Een eigen, herbouwbare Linux-desktop op basis van [Bazzite](https://bazzite.gg) (Fedora Atomic +
KDE Plasma), met een JARVIS-eigen opstartscherm en (later) een eigen bureaubladschil met een
ingebouwde AI-assistent. Gebouwd via [BlueBuild](https://blue-build.org) — elke push naar `main`
bouwt automatisch een nieuwe, ondertekende image.

Waarom Bazzite als basis in plaats van vanaf nul: kant-en-klare Proton/Steam-compatibiliteit,
atomic/veilig (read-only systeem, automatische rollback), en meetbaar lichter dan Windows (gemeten
in een test-VM: ~1,8GB RAM in rust tegenover Windows' 3,3-5GB).

## Installation

> [!WARNING]  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/alekvdw/jarvis-os:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/alekvdw/jarvis-os:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## ISO

If build on Fedora Atomic, you can generate an offline ISO with the instructions available [here](https://blue-build.org/how-to/generate-iso/#_top). These ISOs cannot unfortunately be distributed on GitHub for free due to large sizes, so for public projects something else has to be used for hosting.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/alekvdw/jarvis-os
```
