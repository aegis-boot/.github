# aegis-boot

**Signed boot. Any ISO. Your keys.**

A signed UEFI Secure Boot rescue environment that lets operators pick any ISO from a USB stick's data partition and `kexec` into it — without leaving the chain of trust.

## Repositories

- **[aegis-boot/aegis-boot](https://github.com/aegis-boot/aegis-boot)** — the operator CLI, initramfs, boot chain, and per-ISO verification. Written in Rust, targets UEFI Secure Boot *enforcing*.
- **[aegis-boot/aegis-hwsim](https://github.com/aegis-boot/aegis-hwsim)** — QEMU + OVMF + swtpm hardware-persona matrix harness. Exercises the signed-chain flow across ~100 firmware configurations without physical hardware.

## What makes aegis-boot different

Other multi-ISO USB tools (Ventoy, YUMI) either ask you to disable Secure Boot or trust their one shared MOK key for every kernel they boot. aegis-boot reuses the signed distro boot chain — shim (MS-signed) → GRUB (Canonical-signed) → distro kernel — and enforces `KEXEC_SIG` on the selected ISO. Unsigned ISO kernels are refused with a specific `mokutil --import` command for their signing key.

No firmware modification. No global MOK enrollment. No data collection.

## Install

```bash
# Linux
curl -sSfSL https://raw.githubusercontent.com/aegis-boot/aegis-boot/main/scripts/install.sh | sh

# macOS (Apple Silicon), or Linux via Homebrew
brew tap aegis-boot/aegis-boot https://github.com/aegis-boot/aegis-boot
brew install aegis-boot
```

Full operator docs: [aegis-boot/aegis-boot](https://github.com/aegis-boot/aegis-boot) → `docs/INSTALL.md`.

## Licensing

Dual-licensed under [Apache 2.0](https://github.com/aegis-boot/aegis-boot/blob/main/LICENSE-APACHE) OR [MIT](https://github.com/aegis-boot/aegis-boot/blob/main/LICENSE-MIT), operator's choice.

## Security reports

Private disclosure path is documented in [SECURITY.md](https://github.com/aegis-boot/aegis-boot/blob/main/SECURITY.md). Do not file public issues for vulnerabilities.
