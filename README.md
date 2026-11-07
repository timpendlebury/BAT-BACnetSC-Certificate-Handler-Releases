# BAT BACnetSC Certificate Handler — Releases

BAT BACnetSC Certificate Handler is a Windows utility for requesting, deploying and renewing BACnet/SC host certificates. ABT Site signs the requests with the project CA. Application source is maintained in a separate private repository.

> BAT BACnetSC Certificate Handler is an independent, unofficial third-party tool developed in a personal capacity. It is not an official Siemens product and is not affiliated with, sponsored, endorsed or supported by Siemens AG or any other vendor or manufacturer. To the extent permitted by applicable law, the software is provided "as is", without warranty of any kind, express or implied. No ongoing support, updates or maintenance are promised. Use of the tool is at the user's own risk. Users should maintain appropriate project backups and independently review and validate all outputs and changes before applying them.

## Supported certificate workflows

- **YABE** exports a password-protected P12 and a separate CA PEM.
- **SBR** exports the operational and CA PEMs, with the key retained in the protected request folder.
- **Desigo CC** exports a password-protected PFX and separate DER certificates, with a guided Windows certificate-store import.
- **Third-party** offers configurable key and TLS role settings, PEM and DER exports, and an optional password-protected P12.

Use the built-in certificate workflows for Desigo Optic and ABT Go. The app supports resuming requests, tracking expiry and recording deployment after you test the connection.

## Download and install

Signed installers will be published on the [GitHub Releases page](https://github.com/timpendlebury/BAT-BACnetSC-Certificate-Handler-Releases/releases). When a stable release is available, download `BATBACnetSCCertificateHandler-stable-Setup.exe`, verify its signature using the steps below, then run it. The installer includes the .NET runtime.

## Prerequisites

- A Windows x64 PC.
- OpenSSL 3 or later. The app detects existing installations. Use **Browse for OpenSSL** to select an existing `openssl.exe` or **Install with WinGet** if WinGet is available.
- Access to the ABT Site project administrator to sign the CSR and provide the public project CA certificate.

## Updates

Select **Releases** in the app to open the stable downloads page. To upgrade, download and verify the newer signed installer, finish any active work, close the app and run the installer.

## Repository contents

- [Disclaimer](Disclaimer.md)
- [Code-signing and optional publisher trust instructions](CODE_SIGNED.md)
- [Public publisher certificate](T-Pendlebury-code-signing.cer) and its [SHA-256 checksum](CERTIFICATE-SHA256SUMS)

GitHub Releases will carry the Windows installer, the Velopack `.nupkg` package and the `releases.stable.json` feed.

## Signed installer verification

The Windows installers use the same self-signed **T. Pendlebury** code-signing identity as the publisher's other Windows tools. Independently confirm the [public certificate fingerprint](CERTIFICATE-SHA256SUMS), then follow the [installer verification and optional trust instructions](CODE_SIGNED.md) before running Setup.
