---
# Detecting Web Shells

**Data:** 17/09/2026 | **Categoria:** Web Security Forensics

## O que aprendi
- **Web Shells como Técnica Comum:** scripts maliciosos injetados em servidores web que fornecem acesso remoto para ganhar ponto de apoio inicial em sistemas alvo
- **Padrões de Comportamento:** requisição POST seguida por múltiplas GETs após upload bem-sucedido de web shell, indicando interação do atacante
- **Dificuldade de Detecção:** shells web são facilmente modificados por atacantes, frequentemente empregando criptografia, codificação e ofuscação
- **Métodos de Detecção Efetivos:** comparação de arquivos em servidor web de produção com versão conhecida como boa (fresh install)
- **Habilidade Essencial para SOC:** detecção de web shells é competência crítica para analistas SOC e respondedores de incidentes

## Prática
Analisei logs para detectar padrões de web shells, identifiquei arquivos suspeitos e apliquei técnicas de detecção avançada:

```bash
# Detecção de padrões de web shell em logs
grep -E "POST.*(upload|shell|cmd|exec)" /var/log/apache2/access.log
awk '$6 == "POST" && $7 ~ /upload/ {print $1, $6, $7}' access.log | head -20

# Identificação de requisições POST seguidas por GETs do mesmo IP
cat web_logs.txt | grep "POST.*\.php" | awk '{print $1}' | sort | uniq > post_ips.txt
cat web_logs.txt | grep "GET.*\.php" | awk '{print $1}' | sort | uniq > get_ips.txt
comm -12 <(sort post_ips.txt) <(sort get_ips.txt)

# Busca por funções perigosas de PHP em arquivos
find /var/www/html -name "*.php" -exec grep -l "eval(\|base64_decode(\|system(\|exec(\|passthru(\|shell_exec(" {} \;
grep -r "\\\$_GET\\\|\\\$_POST\\\|\\\$_REQUEST" /var/www/html --include="*.php"

# Análise de hashes de arquivos para detecção de modificações
find /var/www/html -type f -name "*.php" -exec md5sum {} \; > current_hashes.txt
diff baseline_hashes.txt current_hashes.txt

# Ferramentas especializadas para detecção de web shells
python3 webshell_detector.py -p /var/www/html
clamscan -r /var/www/html --include="*.php"
yara -r webshells.yar /var/www/html

# Monitoramento de atividades suspeitas em tempo real
inotifywait -m -r /var/www/html -e create,modify | grep "\.php"
auditctl -w /var/www/html -p war -k webshell_monitoring

# Análise de comportamento anormal
ps aux | grep -E "(wget|curl|nc|netcat|python.*-c|php.*-r)"
netstat -tunap | grep -E "(4444|5555|6666|7777|8888)"
```

Resultado: os comandos permitiram detectar padrões de requisições POST para uploads seguidos por múltiplas GETs do mesmo IP, identificar arquivos PHP contendo funções perigosas como eval() e system(), comparar hashes de arquivos com baseline para detectar modificações, e monitorar atividades suspeitas em tempo real como execução de comandos via PHP ou conexões de rede em portas não padrão.

## Referência
https://tryhackme.com/room/detectingwebshells