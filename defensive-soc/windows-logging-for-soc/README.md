---
# Windows Logging for SOC

**Data:** 17/09/2026 | **Categoria:** Windows Security

## O que aprendi
- **Windows Event Logs:** logs do Windows registram eventos na execução do sistema para fornecer trilha de auditoria, essenciais para entender atividades de sistemas complexos
- **Localização de Logs:** diretório `C:\Windows\System32\winevt\Logs` contém todos os logs do Windows incluindo Security, System, Application
- **Interpretação de Logs:** analistas SOC precisam conhecer bem os logs - como se parecem, como interpretá-los e que ação maliciosa indicam
- **Fontes de Log Importantes:** monitoramento de fontes como Sysmon, PowerShell logs, e logs de autenticação para detecção de ameaças
- **Análise de Linha do Tempo:** entradas de log ajudam investigadores a ver timeline de eventos para determinar o que ocorreu no sistema

## Prática
Analisei logs de eventos do Windows, interpretei diferentes tipos de logs e pratiquei habilidades de análise em múltiplos datasets:

```bash
# Comandos para acesso e análise de logs do Windows
wevtutil qe Security /f:text /c:100
wevtutil qe System /q:"*[System[(Level=1 or Level=2)]]" /f:text
wevtutil qe Application /q:"*[System[(EventID=1000)]]" /f:text

# Consultas PowerShell para logs
Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4624,4625,4634,4648}
Get-WinEvent -FilterHashtable @{LogName='System'; ID=7036} | Select-Object -First 10
Get-WinEvent -LogName 'Microsoft-Windows-Sysmon/Operational' | Where-Object {$_.ID -eq 1}

# Análise de logs de autenticação
wevtutil qe Security /q:"*[System[(EventID=4624)]]" /f:text | findstr /i "logon"
wevtutil qe Security /q:"*[System[(EventID=4625)]]" /f:text | findstr /i "failure"

# Exportação de logs para análise
wevtutil epl Security C:\temp\security_logs.evtx
wevtutil epl System C:\temp\system_logs.evtx
wevtutil epl Application C:\temp\application_logs.evtx

# Consultas XPath para filtragem avançada
wevtutil qe Security /q:"*[System[(EventID=4688)]]" /f:text
Get-WinEvent -LogName Security -FilterXPath "*[System[(EventID=4688)]]"

# Análise de logs do Sysmon
Get-WinEvent -LogName "Microsoft-Windows-Sysmon/Operational" -FilterXPath "*[System[(EventID=1 or EventID=3 or EventID=10)]]"

# Script para análise automatizada
$events = Get-WinEvent -LogName Security -MaxEvents 1000
$events | Group-Object -Property ID | Sort-Object -Property Count -Descending
```

Resultado: os comandos permitiram consultar logs de Security para eventos de logon bem-sucedidos (ID 4624) e falhos (ID 4625), analisar logs do Sysmon para criação de processos (ID 1) e conexões de rede (ID 3), exportar logs para investigação offline, e usar consultas XPath para filtragem precisa de eventos específicos como execução de processos (ID 4688).

## Referência
https://tryhackme.com/room/windowsloggingforsoc