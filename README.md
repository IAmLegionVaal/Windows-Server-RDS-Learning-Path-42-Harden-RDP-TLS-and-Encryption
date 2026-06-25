# Windows Server RDS Learning Path 42 — Harden RDP TLS and Encryption

**Level:** Advanced · **Module:** 42/70

## Goal
Enforce approved RDP security layer, encryption and certificate configuration.

## Setup
1. Record the current RDP listener settings and certificate binding.
2. In the RDS server GPO require the approved security layer and encryption level.
3. Confirm NLA remains enabled.
4. Bind the intended certificate where applicable.
5. Refresh policy and reconnect with an approved client.
6. Verify listener state and review Schannel/RDS events.

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' |
 Select-Object SecurityLayer,MinEncryptionLevel,UserAuthentication,SSLCertificateSHA1Hash
Get-ChildItem Cert:\LocalMachine\My | Select-Object Subject,Thumbprint,NotAfter
gpresult.exe /scope computer /r
```

## Evidence
Store listener settings before/after, certificate binding, successful trusted connection and Schannel/RDS events under `evidence/`.

## Troubleshooting
If clients fail after hardening, verify certificate name/trust, client updates and policy precedence rather than lowering security globally.

## Security
Use trusted TLS certificates and supported clients. Do not expose direct RDP to the Internet.

## Rollback
Restore the recorded listener/GPO baseline while maintaining console access.

## Next
`Windows-Server-RDS-Learning-Path-43-Configure-Windows-Firewall-for-RDS`
