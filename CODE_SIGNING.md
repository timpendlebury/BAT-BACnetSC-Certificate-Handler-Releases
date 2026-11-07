# Installer verification and optional publisher trust

BAT BACnetSC Certificate Handler uses T. Pendlebury's self-signed Authenticode certificate. Confirm the publisher's identity and the fingerprint below through a channel you already trust. The public certificate is `T-Pendlebury-code-signing.cer`. Managed PCs may require IT approval for certificate trust and installation. Windows reputation checks and organisational policies still apply.

| Certificate property | Expected value |
| --- | --- |
| Subject | `CN=T. Pendlebury` |
| DER SHA-256 | `237BFA480A1489E23BAF28FF8A989F219DF6229FA59FA451D707C6D728919B13` |
| Windows thumbprint | `A2BD4071D5153B7C0E8849A95F47937810C6BA37` |

Download the public CER and the installer into the same folder. Check the fingerprint first.

```powershell
$certificate = Resolve-Path -LiteralPath './T-Pendlebury-code-signing.cer'
$expected = '237BFA480A1489E23BAF28FF8A989F219DF6229FA59FA451D707C6D728919B13'
if ((Get-FileHash -LiteralPath $certificate.Path -Algorithm SHA256).Hash -cne $expected) {
    throw 'Publisher certificate fingerprint mismatch.'
}
```

After independent verification, if you choose to trust this publisher for the current Windows user, import that exact public CER into the current user's **Trusted Root Certification Authorities** and **Trusted Publishers** stores.

```powershell
$null = Import-Certificate -FilePath $certificate.Path -CertStoreLocation 'Cert:/CurrentUser/Root'
$null = Import-Certificate -FilePath $certificate.Path -CertStoreLocation 'Cert:/CurrentUser/TrustedPublisher'
$signature = Get-AuthenticodeSignature -LiteralPath './BATBACnetSCCertificateHandler-stable-Setup.exe'
if ($signature.Status -ne 'Valid' -or -not $signature.TimeStamperCertificate -or
    $signature.SignerCertificate.Thumbprint -cne 'A2BD4071D5153B7C0E8849A95F47937810C6BA37') {
    throw 'The installer signature does not match the expected timestamped publisher signature.'
}
$signature | Format-List Status, StatusMessage
```

Run the installer after verification. This trust choice applies to software signed with the same publisher identity. The download is a public certificate. Installing the app requires only that public certificate if your Windows policy needs it.

[Microsoft Authenticode guidance](https://learn.microsoft.com/en-us/windows/win32/dxtecharts/authenticode-signing-for-game-developers)
