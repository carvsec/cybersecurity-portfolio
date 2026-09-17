---
# Linux Threat Detection 3

**Data:** 17/09/2026 | **Categoria:** Linux Threat Detection

## O que aprendi
- **Técnicas de Defense Evasion Linux:** métodos para evitar detecção incluindo desativação de logs, ofuscação de comandos, uso de rootkits
- **Técnicas de Credential Access Linux:** roubo de credenciais via keyloggers, dump de memória, arquivos de senhas, e técnicas de harvesting
- **Detecção de Evasão de Defesa:** monitoramento de desativação de serviços de logging, modificação de arquivos de log, ofuscação de atividades
- **Identificação de Credential Access:** análise de tentativas de acesso a arquivos de senhas, memória de processos, e técnicas de keylogging
- **Uso de Ferramentas Avançadas:** strace, lsof, auditd, rkhunter, chkrootkit para detecção de técnicas sofisticadas de evasão

## Prática
Analisei técnicas de defense evasion e credential access em Linux, detectei tentativas de evasão e roubo de credenciais:

```bash
# Detecção de defense evasion via desativação de logs
systemctl status rsyslog auditd
journalctl --verify
ls -la /var/log/ | grep -E "(auth\.log|syslog|messages|secure)"
find /var/log -type f -size 0  # Logs vazios suspeitos
auditctl -l  # Regras de auditoria ativas

# Monitoramento de modificação de arquivos de log
auditctl -w /var/log/auth.log -p wa -k auth_log
auditctl -w /var/log/syslog -p wa -k syslog
ausearch -k auth_log -i | tail -10

# Detecção de ofuscação de comandos
history | grep -E "(base64|xxd|openssl.*enc|tr|rev)"
ps aux | grep -E "(python.*-c|perl.*-e|bash.*-i|sh.*-c)"
strings /tmp/* 2>/dev/null | grep -E "(passw|secret|key|token)"

# Identificação de rootkits e backdoors
rkhunter --check
chkrootkit
lsmod | grep -i "hidden\|rootkit"
find /lib/modules/$(uname -r) -type f -name "*.ko" | xargs modinfo | grep -i "description"

# Detecção de credential access via arquivos de senhas
lsof /etc/passwd /etc/shadow /etc/master.passwd 2>/dev/null
ausearch -k passwd_access -i
find / -name "*passwd*" -o -name "*shadow*" -o -name "*pwd*" 2>/dev/null | grep -v "/proc\|/sys"

# Análise de tentativas de dump de memória
ps aux | grep -E "(gcore|gdb|dd.*of=/proc/|cat /proc/.*/mem)"
lsof /proc/*/mem 2>/dev/null
auditctl -w /proc -p r -k proc_access

# Detecção de keyloggers
lsmod | grep -i "keylog"
find / -type f -name "*keylog*" -o -name "*klog*" 2>/dev/null
lsof /dev/input/* 2>/dev/null | grep -v "root"

# Monitoramento de acesso a arquivos de configuração SSH
auditctl -w /etc/ssh/sshd_config -p wa -k ssh_config
auditctl -w ~/.ssh/ -p wa -k ssh_keys
ausearch -k ssh_config -i | tail -5

# Análise de processos suspeitos com strace
ps aux | grep -E "(strace|ltrace)" | grep -v grep
# Uso de strace para monitorar processos suspeitos:
# strace -p <PID> -e trace=file,process

# Script para detecção de defense evasion
#!/bin/bash
echo "=== Detecção de Defense Evasion Linux ==="
echo "1. Status dos serviços de logging:"
systemctl is-active rsyslog auditd 2>/dev/null || echo "Serviços não encontrados"
echo "2. Arquivos de log modificados recentemente:"
find /var/log -type f -mtime -1 -exec ls -la {} \;
echo "3. Comandos ofuscados no history:"
history | tail -50 | grep -E "(base64|xxd|\\\\|eval)"
echo "4. Processos acessando arquivos sensíveis:"
lsof /etc/passwd /etc/shadow /etc/sudoers 2>/dev/null || echo "Nenhum acesso detectado"

# Análise de auditoria detalhada
ausearch -m ADD_USER,DEL_USER,ADD_GROUP,DEL_USER -i
ausearch -m EXECVE -sv no -i | grep -E "(passw|shadow|sudo)"
```

Resultado: os comandos permitiram detectar defense evasion através de desativação de serviços rsyslog e auditd, monitorar modificações de arquivos de log com auditctl, identificar ofuscação de comandos usando base64 e outras técnicas no history, detectar rootkits com rkhunter e chkrootkit, analisar tentativas de credential access a arquivos /etc/passwd e /etc/shadow, identificar processos acessando memória de outros processos para dump, detectar keyloggers através de módulos do kernel e acesso a /dev/input, monitorar modificações em configurações SSH, e usar strace para análise detalhada de processos suspeitos.

## Referência
https://tryhackme.com/room/linuxthreatdetection3