# BAT BACnetSC Certificate Handler — Releases

This is the public distribution repository for the Windows utility. Application development takes place in a separate private source repository.

> BAT BACnetSC Certificate Handler is an independent, unofficial third-party tool developed in a personal capacity. It carries no vendor affiliation, endorsement or support. The software is provided as is, without warranty. Review each certificate, its issuing authority and the deployment target before applying it to a live BACnet/SC system.

## Download and install

Installers will be published under [GitHub Releases](https://github.com/timpendlebury/BAT-BACnetSC-Certificate-Handler-Releases/releases). On Windows x64, choose `BATBACnetSCCertificateHandler-stable-Setup.exe` from the stable release and follow the [installer verification instructions](CODE_SIGNING.md). The installer includes the .NET runtime. The full Velopack package and `releases.stable.json` are distribution assets. For an upgrade, finish active work, close the application and run the newer signed installer.

The application uses OpenSSL. It can find an existing installation, let you browse to it, or offer an installation through WinGet.

## Supported certificate workflows

- **YABE** exports a password-protected P12 and a separate CA PEM.
- **SBR** exports the operational and CA PEMs, with the key retained in the protected request folder.
- **Desigo CC** exports a password-protected PFX and separate DER certificates, with a guided Windows certificate-store import.
- **Third-party** offers configurable key and TLS role settings, PEM and DER exports, and an optional password-protected P12.

ABT Site signs the requests. Use the built-in certificate workflows for Desigo Optic and ABT Go. The app supports resuming requests, tracking expiry and recording deployment after you test the connection.

## Publisher identity

The Windows installers use the same self-signed **T. Pendlebury** code-signing identity as the owner's other Windows tools. Download the [public certificate](T-Pendlebury-code-signing.cer) and independently verify its [SHA-256 checksum](CERTIFICATE-SHA256SUMS).
