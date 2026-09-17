---
# Phishing Emails 5

**Data:** 17/09/2026 | **Categoria:** Phishing Analysis

## O que aprendi
- **Análise de Campanhas Phishing:** identificação de padrões em múltiplos emails de mesma campanha
- **Correlação de IOCs:** conexão entre diferentes indicadores de comprometimento de mesma origem
- **Técnicas de Evasão Avançada:** métodos usados para evitar detecção por ferramentas de segurança
- **Análise de Infraestrutura:** identificação de servidores, domínios e recursos usados em campanhas coordenadas
- **Técnicas de Atribuição:** análise para identificar possíveis grupos de atacantes ou origem geográfica

## Prática
Analisei campanhas coordenadas, correlacionei IOCs e investiguei infraestrutura de phishing:

```bash
# Análise de múltiplos emails de mesma campanha
grep -r "Subject:.*Invoice" phishing_samples/  # Padrões de assunto
grep -r "From:.*@same-domain.com" phishing_samples/  # Remetentes similares
find phishing_samples/ -type f -exec md5sum {} \; | sort  # Identificação de duplicados

# Correlação de IOCs
python3 ioc-extractor.py phishing_samples/ > iocs.txt
grep -oP '\b\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}\b' iocs.txt | sort -u > ips.txt
grep -oP '[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}' iocs.txt | sort -u > domains.txt

# Análise de infraestrutura
for ip in $(cat ips.txt); do
    whois $ip | grep -i "netname\|country\|organization"
    nslookup $ip | grep "name ="
done

for domain in $(cat domains.txt); do
    echo "=== $domain ==="
    dig $domain ANY +short
    whois $domain | grep -i "creation date\|registrar"
done

# Detecção de técnicas de evasão
grep -r "display:none\|visibility:hidden\|opacity:0" phishing_samples/  # Conteúdo oculto
grep -r "user-agent\|referer" phishing_samples/ | grep -v "common browsers"  # User agents falsos

# Análise temporal de campanha
find phishing_samples/ -type f -exec stat -c "%y %n" {} \; | sort  # Ordenação por data
python3 -c "from datetime import datetime; import sys; dates = [datetime.fromtimestamp(float(line.split()[0])) for line in open('timestamps.txt')]; print(f'Primeiro: {min(dates)}, Último: {max(dates)}')"

# Script para análise de campanha
#!/bin/bash
echo "=== Análise de Campanha Phishing ==="
echo "1. Total de amostras: $(find "$1" -type f | wc -l)"
echo "2. Assuntos únicos:"
grep -r "Subject:" "$1" | cut -d: -f3- | sort -u | head -10
echo "3. Domínios de remetente:"
grep -r "From:" "$1" | grep -oP '@\K[^>]+' | sort -u | head -10
echo "4. URLs encontradas:"
grep -roP 'https?://[^" <]+' "$1" | sort -u | wc -l

# Análise de headers X- para técnicas avançadas
grep -r "X-" phishing_samples/ | grep -v "X-Mailer: Microsoft" | sort -u

# Verificação de reputação em massa
python3 vt-bulk-check.py ips.txt
python3 abuseipdb-check.py ips.txt
```

Resultado: os comandos permitiram analisar múltiplos emails de mesma campanha identificando padrões de Subject e From, extrair e correlacionar IOCs como IPs e domínios, investigar infraestrutura com whois e dig, detectar técnicas de evasão como conteúdo oculto com CSS, analisar timeline da campanha, verificar reputação de IPs em massa com APIs como VirusTotal e AbuseIPDB, e identificar headers X- personalizados usados para técnicas avançadas de evasão.

## Referência
https://tryhackme.com/room/phishingemails5fgjlzxc