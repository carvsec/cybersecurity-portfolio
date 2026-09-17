---
# Windows Threat Detection 2

**Data:** 17/09/2026 | **Categoria:** Windows Threat Detection

## O que aprendi
- **Técnicas de Persistência:** métodos que atacantes usam para manter acesso a sistemas comprometidos após obtenção de acesso inicial
- **Técnicas de Execução:** mecanismos para executar código malicioso em sistemas alvo, muitas vezes disfarçados como processos legítimos
- **Detecção de Persistência:** identificação de entradas de registro, serviços, tarefas agendadas e outros mecanismos usados para manter acesso
- **Análise de Execução de Código:** monitoramento de criação de processos, injeção de código e execução através de mecanismos legítimos
- **Uso de Logs do Sysmon:** análise detalhada de eventos do Sysmon para detecção de técnicas avançadas de persistência e execução

## Prática
Analisei técnicas de persistência e execução, detectei mecanismos avançados de manutenção de acesso:

```bash
# Detecção de persistência via Registry Run keys
Get-WinEvent -LogName 'Microsoft-Windows-Sysmon/Operational' -FilterXPath "*[System[(EventID=12 or EventID=13 or EventID=14)]]" | Where-Object {$_.Properties[4].Value -match "Run\\|RunOnce\\"}
reg query "HKCU\Software\Microsoft\Windows\CurrentVersion\Run"
reg query "HKLM\Software\Microsoft\Windows\CurrentVersion\Run"

# Análise de serviços suspeitos
Get-WinEvent -FilterHashtable @{LogName='System'; ID=7045} | Where-Object {$_.Properties[6].Value -notmatch "SYSTEM|LOCAL SERVICE|NETWORK SERVICE"}
sc query state= all | findstr /i "SERVICE_NAME"
Get-WmiObject -Class Win32_Service | Where-Object {$_.StartName -notmatch "LocalSystem|NT AUTHORITY"}

# Detecção de tarefas agendadas suspeitas
schtasks /query /fo LIST /v
Get-ScheduledTask | Where-Object {$_.Principal.UserId -notmatch "SYSTEM|LOCAL SERVICE"} | Select-Object TaskName, Principal

# Análise de persistência via Startup folder
Get-ChildItem "C:\Users\*\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup" -Recurse -Force
Get-ChildItem "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup" -Recurse -Force

# Detecção de injeção de código e execução suspeita
Get-WinEvent -LogName 'Microsoft-Windows-Sysmon/Operational' -FilterXPath "*[System[(EventID=8)]]"  # Remote thread creation
Get-WinEvent -LogName 'Microsoft-Windows-Sysmon/Operational' -FilterXPath "*[System[(EventID=10)]]"  # Process access

# Análise de WMI para persistência
Get-WmiObject -Namespace root\Subscription -Class __EventFilter
Get-WmiObject -Namespace root\Subscription -Class __EventConsumer
Get-WmiObject -Namespace root\Subscription -Class __FilterToConsumerBinding

# Detecção de fileless malware e execução na memória
Get-WinEvent -LogName 'Microsoft-Windows-PowerShell/Operational' | Where-Object {$_.Message -match "Invoke-Expression|IEX|DownloadString"}
Get-Process | Where-Object {$_.Modules.ModuleName -match "amsi\.dll"} | Select-Object ProcessName, Id

# Script para análise de persistência completa
$persistenceMethods = @()
$persistenceMethods += Get-ItemProperty "HKLM:\Software\Microsoft\Windows\CurrentVersion\Run" -ErrorAction SilentlyContinue
$persistenceMethods += Get-ScheduledTask | Where-Object {$_.State -eq "Ready"}
$persistenceMethods | Format-Table -AutoSize
```

Resultado: os comandos permitiram detectar entradas suspeitas em Registry Run keys através do Sysmon (Event IDs 12-14), identificar serviços não executados como SYSTEM ou serviços do Windows, analisar tarefas agendadas com usuários incomuns, investigar injeção de código remota (Sysmon ID 8), detectar fileless malware via PowerShell (logs operacionais), e analisar uso de WMI para persistência através de subscriptions e event consumers.

## Referência
https://tryhackme.com/room/windowsthreatdetection2