# PowerShell

## Find things

```powershell
Get-ChildItem -Recurse -Filter *.ts | Select-String "TODO" -List
Get-Command gh
Get-Help Get-ChildItem -Examples
```

## Common traps

- `&&` is not available in Windows PowerShell 5.1 — use `;` or run separate commands.
- `mkdir a b` fails; `New-Item -ItemType Directory -Path a,b -Force` works.
- `ls -la` fails; use `Get-ChildItem -Force`.
- Check `$LASTEXITCODE` after native binaries — silence is not success.

## Processes

```powershell
Get-NetTCPConnection -LocalPort 3000 -State Listen |
  ForEach-Object { Stop-Process -Id $_.OwningProcess -Force }
```
