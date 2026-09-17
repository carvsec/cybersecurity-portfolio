---
# Linux Threat Detection 1

**Data:** 17/09/2026 | **Categoria:** Linux Threat Detection

## O que aprendi
- **Técnicas de Initial Access Linux:** métodos comuns para obter acesso inicial a sistemas Linux incluindo SSH brute force, exploração de serviços web
- **Técnicas de Discovery Linux:** atividades de reconhecimento após acesso inicial para mapear sistema, usuários, processos e rede
- **Detecção de Acesso Inicial:** análise de logs de autenticação SSH, monitoramento de tentativas de conexão, detecção de exploração de serviços
- **Identificação de Atividades de Discovery:** monitoramento de comandos de enumeração, varredura de arquivos, listagem de processos e usuários
- **Uso de Ferramentas Nativas Linux:** análise com commands como ps, netstat, lsof, find, who, w para detecção de atividades suspeitas

## Prática
Analisei técnicas de initial access e discovery em Linux, detectei atividades de reconhecimento e acesso suspeito:

```bash
# Detecção de brute force SSH
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -nr | head -10
cat /var/log/auth.log | grep "Failed password" | awk '{if($9 == "invalid") print $11; else print $9}' | sort | uniq -c | sort -nr
fail2ban-client status

# Análise de logins SSH bem-sucedidos suspeitos
grep "Accepted password" /var/log/auth.log | tail -20
last | head -20
who

# Detecção de atividades de discovery via comandos de enumeração
history | grep -E "(whoami|id|uname|hostname|ifconfig|ip addr|netstat|ps aux|ls -la|find /)"
cat ~/.bash_history | grep -E "(\.\./|passwd|shadow|sudoers|/etc/)"

# Monitoramento de processos suspeitos
ps aux | grep -E "(nc|netcat|nmap|python.*-c|perl.*-e|bash.*-i)"
ps aux --sort=-%cpu | head -10
ps aux --sort=-%mem | head -10

# Análise de conexões de rede suspeitas
netstat -tunap | grep -E "(4444|5555|6666|7777|8888)"
netstat -tunap | grep ESTABLISHED | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -nr
lsof -i :22  # Conexões SSH

# Detecção de varredura de arquivos e diretórios
find / -name "*.php" -exec grep -l "eval(" {} \; 2>/dev/null
find / -name "*.sh" -perm /u=x,g=x,o=x 2>/dev/null | head -20
find /tmp /dev/shm -type f -exec file {} \; 2>/dev/null | grep -i "executable"

# Análise de usuários e grupos suspeitos
cat /etc/passwd | grep -E "(/bin/bash|/bin/sh)"
cat /etc/shadow | cut -d: -f1
getent group sudo
grep -E "(sudo|wheel)" /etc/group

# Monitoramento de arquivos de configuração sensíveis
ls -la /etc/passwd /etc/shadow /etc/sudoers
stat /etc/passwd
stat /etc/shadow

# Script para detecção de atividades de initial access
#!/bin/bash
echo "=== Detecção de Initial Access Linux ==="
echo "1. Tentativas SSH falhas nas últimas 24h:"
grep "Failed password" /var/log/auth.log --since="24 hours ago" | wc -l
echo "2. IPs com mais tentativas falhas:"
grep "Failed password" /var/log/auth.log --since="24 hours ago" | awk '{if($9 == "invalid") print $11; else print $9}' | sort | uniq -c | sort -nr | head -5
echo "3. Logins bem-sucedidos suspeitos:"
last -n 10 | grep -v "reboot\|wtmp"
```

Resultado: os comandos permitiram detectar ataques de brute force SSH analisando padrões de "Failed password" em auth.log, identificar logins bem-sucedidos suspeitos através do comando last, monitorar atividades de discovery como enumeração de sistema com whoami, id, uname, detectar processos suspeitos como netcat e reverse shells, analisar conexões de rede em portas não padrão, identificar varredura de arquivos PHP contendo eval(), e monitorar modificações em arquivos sensíveis como /etc/passwd e /etc/shadow.

## Referência
https://tryhackme.com/room/linuxthreatdetection1