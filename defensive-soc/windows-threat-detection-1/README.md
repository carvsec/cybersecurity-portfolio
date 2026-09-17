---
# Windows Threat Detection 1

**Data:** 17/09/2026 | **Categoria:** Windows Threat Detection

## O que aprendi
- **Initial Access MITRE ATT&CK:** técnicas que atacantes usam para ganhar ponto de apoio inicial dentro de sistema, rede ou ambiente
- **Discovery Técnicas:** ocorre após initial access, quando atacante começa a coletar informações sobre ambiente, identificar usuários, localizar sistemas/dados valiosos
- **Detecção com Windows Event Logs:** uso apenas de logs de eventos do Windows, fonte de log mais comum para times SOC do mundo real
- **Técnicas Comuns de Acesso:** phishing, exploração de vulnerabilidades públicas, uso de credenciais válidas, hardcoded credentials
- **Análise de Logs para Foothold:** detecção de sinais sutis de intrusão mesmo quando atores de ameaça acabaram de violar perímetros

## Prática
Analisei técnicas de Initial Access e Discovery, detectei comportamentos anormais usando apenas logs do Windows:

```bash
# Detecção de tentativas de acesso inicial via PowerShell logs
Get-WinEvent -LogName 'Microsoft-Windows-PowerShell/Operational' | Where-Object {$_.ID -eq 4103} | Select-Object -First 20
wevtutil qe 'Microsoft-Windows-PowerShell/Operational' /q:"*[System[(EventID=4103)]]" /f:text

# Análise de eventos de execução de processo suspeito
Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4688} | Where-Object {$_.Properties[5].Value -like "*powershell*"} 
Get-WinEvent -FilterHashtable @{LogName='Microsoft-Windows-Sysmon/Operational'; ID=1} | Where-Object {$_.Properties[10].Value -match "cmd\.exe|powershell\.exe"}

# Detecção de atividades de discovery
Get-WinEvent -LogName Security -FilterXPath "*[System[(EventID=4661)]]"  # Object access
Get-WinEvent -LogName Security -FilterXPath "*[System[(EventID=4663)]]"  # File access

# Consultas para atividades de reconhecimento de rede
Get-WinEvent -LogName 'Microsoft-Windows-Sysmon/Operational' -FilterXPath "*[System[(EventID=3)]]" | Where-Object {$_.Properties[4].Value -match "445|139"}  # SMB
Get-WinEvent -LogName Security -FilterXPath "*[System[(EventID=5140)]]"  # Network share access

# Análise de logs de autenticação para acesso suspeito
wevtutil qe Security /q:"*[System[(EventID=4625) and TimeCreated[@SystemTime>='2026-01-01T00:00:00']]]" /f:text
Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4624} | Where-Object {$_.Properties[8].Value -eq 10}  # Remote logon

# Script para análise de eventos de criação de serviço
$services = Get-WinEvent -FilterHashtable @{LogName='System'; ID=7045}
$services | ForEach-Object { Write-Host "Serviço criado: $($_.Properties[0].Value) por $($_.Properties[6].Value)" }
```

Resultado: os comandos permitiram detectar execução suspeita de PowerShell (Event ID 4103), identificar processos criados via cmd.exe ou powershell.exe através do Sysmon (ID 1), analisar tentativas de acesso a objetos e arquivos (IDs 4661, 4663), monitorar conexões de rede SMB (Sysmon ID 3), e investigar logons remotos (Security ID 4624 com Logon Type 10) e criação de serviços suspeitos (System ID 7045).

## Referência
https://tryhackme.com/room/windowsthreatdetection1