---
# Linux Threat Detection 2

**Data:** 17/09/2026 | **Categoria:** Linux Threat Detection

## O que aprendi
- **Técnicas de Persistência Linux:** métodos para manter acesso a sistemas Linux comprometidos incluindo cron jobs, services, startup scripts
- **Técnicas de Privilege Escalation Linux:** exploração de vulnerabilidades, abuso de sudoers, SUID binaries, e configurações incorretas de permissões
- **Detecção de Persistência:** monitoramento de cron jobs, systemd services, arquivos de inicialização, e backdoors
- **Identificação de Privilege Escalation:** análise de permissões SUID/GUID, configurações sudoers, capabilities do kernel, e vulnerabilidades conhecidas
- **Uso de Ferramentas de Análise:** find, ls, stat, auditd, chkconfig, systemctl para detecção de mecanismos de persistência e escalação

## Prática
Analisei técnicas de persistência e privilege escalation em Linux, detectei backdoors e tentativas de escalação de privilégios:

```bash
# Detecção de persistência via cron jobs
crontab -l
ls -la /etc/cron*
cat /etc/crontab
find /etc/cron* -type f -exec ls -la {} \;
systemctl list-timers --all

# Análise de serviços suspeitos (systemd)
systemctl list-units --type=service --state=running
systemctl list-unit-files --type=service | grep enabled
ls -la /etc/systemd/system/*.service /usr/lib/systemd/system/*.service 2>/dev/null

# Detecção de arquivos de inicialização suspeitos
ls -la /etc/init.d/
ls -la /etc/rc*.d/
ls -la ~/.bashrc ~/.bash_profile ~/.profile
ls -la /etc/profile.d/

# Identificação de privilege escalation via SUID binaries
find / -type f -perm /4000 -ls 2>/dev/null
find / -type f -perm /2000 -ls 2>/dev/null  # SGID
find / -type f -perm /6000 -ls 2>/dev/null  # Both

# Análise de configurações sudoers
cat /etc/sudoers
ls -la /etc/sudoers.d/
grep -r "NOPASSWD" /etc/sudoers*

# Detecção de capabilities perigosas
getcap -r / 2>/dev/null
# Busca por binários com capabilities como cap_setuid, cap_net_bind_service

# Análise de processos rodando como root
ps aux | grep "^root" | head -20
ps -ef | grep -v "\[" | awk '{if($1=="root") print $0}'

# Detecção de arquivos ocultos e diretórios suspeitos
find / -name ".*" -type f -exec ls -la {} \; 2>/dev/null | head -20
find /tmp /dev/shm /var/tmp -type f -exec ls -la {} \; 2>/dev/null | head -20

# Análise de vulnerabilidades conhecidas
uname -a
cat /etc/os-release
# Verificação para DirtyPipe, DirtyCow, outras vulnerabilidades específicas

# Script para detecção de persistência completa
#!/bin/bash
echo "=== Detecção de Persistência Linux ==="
echo "1. Cron jobs do usuário atual:"
crontab -l 2>/dev/null || echo "Nenhum cron job"
echo "2. Cron jobs do sistema:"
ls -la /etc/cron* 2>/dev/null
echo "3. Serviços systemd ativos:"
systemctl list-units --type=service --state=running | head -10
echo "4. Binários SUID:"
find / -type f -perm /4000 -ls 2>/dev/null | wc -l
echo "5. Configurações sudo sem senha:"
grep -r "NOPASSWD" /etc/sudoers* 2>/dev/null

# Monitoramento de auditoria com auditd
auditctl -l
ausearch -k persistence -i
ausearch -ts today -m EXECVE | head -20
```

Resultado: os comandos permitiram detectar persistência através de cron jobs suspeitos em /etc/cron* e crontab do usuário, identificar serviços systemd ativos e habilitados, analisar binários SUID que podem ser explorados para privilege escalation, verificar configurações sudoers com NOPASSWD, investigar capabilities perigosas com getcap, monitorar processos rodando como root, localizar arquivos ocultos e diretórios temporários suspeitos, e usar auditd para auditoria detalhada de execução de comandos e atividades de persistência.

## Referência
https://tryhackme.com/room/linuxthreatdetection2