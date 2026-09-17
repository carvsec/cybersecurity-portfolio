---
# Windows Threat Detection 3

**Data:** 17/09/2026 | **Categoria:** Windows Threat Detection

## O que aprendi
- **Técnicas de Privilege Escalation:** métodos para obter privilégios mais altos em sistemas comprometidos, frequentemente de usuário para administrador
- **Técnicas de Defense Evasion:** mecanismos para evitar detecção por ferramentas de segurança, incluindo desativação de logging e ofuscação
- **Detecção de Escalação de Privilégios:** identificação de uso abusivo de ferramentas como PowerShell, exploração de vulnerabilidades e abuso de mecanismos legítimos
- **Análise de Evasão de Defesa:** monitoramento de desativação de logs, remoção de indicadores, uso de ferramentas living-off-the-land
- **Uso de Técnicas MITRE ATT&CK:** aplicação de framework ATT&CK para categorização e detecção de técnicas avançadas de ataque

## Prática
Analisei técnicas de privilege escalation e defense evasion, detectei tentativas de evasão e escalação de privilégios:

```bash
# Detecção de privilege escalation via UAC bypass
Get-WinEvent -LogName Security -FilterXPath "*[System[(EventID=4688)]]" | Where-Object {$_.Properties[5].Value -match "consent\.exe|fodhelper\.exe|eventvwr\.exe"}
Get-WinEvent -LogName 'Microsoft-Windows-Sysmon/Operational' -FilterXPath "*[System[(EventID=1)]]" | Where-Object {$_.Properties[10].Value -match "consent\.exe|fodhelper\.exe"}

# Análise de abuso de serviços para privilege escalation
Get-WinEvent -FilterHashtable @{LogName='System'; ID=7045} | Where-Object {$_.Properties[6].Value -match "LocalSystem" -and $_.Properties[0].Value -match "suspect"}
sc query | findstr /i "SERVICE_NAME.*STATE.*:.*RUNNING"
Get-WmiObject -Class Win32_Service | Where-Object {$_.StartMode -eq "Auto" -and $_.State -eq "Running"} | Select-Object Name, StartName, PathName

# Detecção de defense evasion via desativação de logs
Get-WinEvent -LogName Security -FilterXPath "*[System[(EventID=1102)]]"  # Log clear
auditpol /get /category:* | findstr /i "Failure Success"
wevtutil gl Security | findstr /i "enabled"

# Análise de remoção de indicadores (file deletion)
Get-WinEvent -LogName 'Microsoft-Windows-Sysmon/Operational' -FilterXPath "*[System[(EventID=23)]]"  # FileDelete
Get-WinEvent -LogName Security -FilterXPath "*[System[(EventID=4663) and (EventData/Data[@Name='AccessMask']='0x10000')]]"  # DELETE access

# Detecção de ofuscação de PowerShell
Get-WinEvent -LogName 'Microsoft-Windows-PowerShell/Operational' | Where-Object {$_.Message -match "FromBase64String|Invoke-Expression|IEX|\.Replace"}
Get-WinEvent -LogName 'Microsoft-Windows-PowerShell/Operational' -FilterXPath "*[System[(EventID=4104)]]"  # Script block logging

# Análise de abuso de ferramentas legítimas (living-off-the-land)
Get-WinEvent -LogName 'Microsoft-Windows-Sysmon/Operational' -FilterXPath "*[System[(EventID=1)]]" | Where-Object {$_.Properties[10].Value -match "bitsadmin\.exe|certutil\.exe|regsvr32\.exe|rundll32\.exe"}
Get-Process | Where-Object {$_.ProcessName -match "wmic|regsvr32|rundll32"} | Select-Object ProcessName, Id, CommandLine

# Detecção de modificação de Registry para persistence/evasion
Get-WinEvent -LogName 'Microsoft-Windows-Sysmon/Operational' -FilterXPath "*[System[(EventID=12 or EventID=13 or EventID=14)]]" | Where-Object {$_.Properties[4].Value -match "Policies\\System\\|Control\\Session Manager\\"}

# Script para análise de atividades suspeitas de privilege escalation
$suspiciousEvents = @()
$suspiciousEvents += Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4672}  # Special privileges assigned
$suspiciousEvents += Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4673}  # Privileged service called
$suspiciousEvents += Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4674}  # Operation attempted on privileged object
$suspiciousEvents | Group-Object -Property ID | Select-Object Count, Name
```

Resultado: os comandos permitiram detectar tentativas de UAC bypass através de consent.exe e fodhelper.exe, identificar abuso de serviços executando como LocalSystem, monitorar desativação de logs (Event ID 1102), analisar remoção de arquivos suspeitos (Sysmon ID 23), detectar ofuscação de PowerShell com FromBase64String e Invoke-Expression, identificar uso de ferramentas living-off-the-land como bitsadmin e certutil, e investigar modificações suspeitas no Registry relacionadas a policies do sistema.

## Referência
https://tryhackme.com/room/windowsthreatdetection3