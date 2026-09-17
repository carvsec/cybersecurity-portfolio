---
# Linux Logging for SOC

**Data:** 17/09/2026 | **Categoria:** Linux Security

## O que aprendi
- **Sistema de Logs do Linux:** compreensão de syslog, journald, e arquivos de log específicos de aplicações em distribuições Linux
- **Localização de Logs Importantes:** `/var/log/` como diretório principal contendo auth.log, syslog, kern.log, secure, e logs de aplicações
- **Análise de Logs de Autenticação:** interpretação de logs de login bem-sucedidos e falhos, detecção de tentativas de brute force
- **Monitoramento de Sistema:** uso de logs do kernel para detecção de atividades de hardware, drivers, e eventos de baixo nível
- **Ferramentas de Análise:** grep, awk, sed, journalctl para análise eficiente de grandes volumes de logs

## Prática
Analisei logs do sistema Linux, interpretei diferentes tipos de logs e pratiquei técnicas de análise em ambientes Linux:

```bash
# Análise de logs de autenticação
grep "Failed password" /var/log/auth.log
grep "Accepted password" /var/log/auth.log | tail -20
grep "invalid user" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -nr

# Monitoramento de tentativas de brute force
cat /var/log/auth.log | grep "Failed password" | awk '{print $11}' | sort | uniq -c | sort -nr | head -10
fail2ban-client status sshd
lastb | head -20

# Análise de logs do sistema com journalctl
journalctl -u sshd --since "today"
journalctl -u apache2 --since "2 hours ago" -f
journalctl -k --since "yesterday"  # Kernel logs
journalctl --list-boots

# Análise de logs de aplicações web
tail -f /var/log/apache2/access.log
tail -f /var/log/nginx/access.log
grep -E "(404|500|403)" /var/log/apache2/access.log | awk '{print $1}' | sort | uniq -c

# Monitoramento de atividades de sistema
who /var/log/wtmp
last
w
uptime

# Análise de logs do kernel
dmesg | grep -i "error\|fail\|warning"
cat /var/log/kern.log | grep -i "firewall\|iptables\|drop"

# Ferramentas avançadas de análise de logs
logwatch --detail High --range Today --service All
goaccess /var/log/nginx/access.log -a
lnav /var/log/*.log

# Script para análise de segurança automatizada
#!/bin/bash
echo "=== Análise de Segurança Linux ==="
echo "1. Tentativas de login falhas:"
grep "Failed password" /var/log/auth.log | wc -l
echo "2. Logins bem-sucedidos recentes:"
last -n 10
echo "3. Processos em execução suspeitos:"
ps aux | grep -E "(nc|netcat|python.*-c|bash.*-i)"
echo "4. Conexões de rede ativas:"
netstat -tunap | grep -E "(4444|5555|6666|7777)"

# Configuração de monitoramento de logs em tempo real
tail -f /var/log/syslog | grep -E "(CRITICAL|ERROR|WARNING)"
watch -n 5 'netstat -tunap | grep ESTABLISHED'
```

Resultado: os comandos permitiram identificar tentativas de brute force SSH analisando "Failed password" em auth.log, monitorar logins bem-sucedidos com o comando last, analisar logs de aplicações web para erros HTTP 404/500, investigar atividades do kernel com dmesg, usar journalctl para logs de serviços específicos como sshd e apache2, implementar scripts de análise automatizada de segurança, e configurar monitoramento em tempo real de logs críticos do sistema.

## Referência
https://tryhackme.com/room/linuxloggingforsoc