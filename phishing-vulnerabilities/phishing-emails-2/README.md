---
# Phishing Emails 2

**Data:** 17/09/2026 | **Categoria:** Phishing Analysis

## O que aprendi
- **Táticas de Ataque Phishing:** métodos que atacantes usam para espelhar comunicações legítimas através de amostras reais de emails
- **Identificação de Nuances Sutis:** diferenciação entre notificações de rotina e tentativas sofisticadas de harvesting de credenciais
- **Análise de Headers de Email:** inspeção de arquivos de email raw para identificar origem verdadeira e intenção de mensagens suspeitas
- **Técnicas de Social Engineering:** como atacantes manipulam usuários para revelar informações sensíveis, clicar em links maliciosos ou executar attachments
- **Indicadores de Comprometimento (IOCs):** identificação de headers maliciosos, payloads, e infraestrutura usada em campanhas de phishing

## Prática
Analisei amostras realistas de phishing emails, identifiquei técnicas de engenharia social e examinei headers e payloads maliciosos:

```bash
# Ferramentas para análise de headers de email
curl -I "https://mail.google.com"  # Verificação de headers HTTP
nslookup suspicious-domain.com
dig suspicious-domain.com MX

# Análise de arquivos .eml raw
cat phishing_email.eml
grep -i "from:\|to:\|subject:\|reply-to:" phishing_email.eml
grep -i "received:" phishing_email.eml | head -5

# Extração de URLs de emails phishing
grep -oP '(http|https)://[^" <]+' phishing_email.eml
strings phishing_email.eml | grep -E "http://|https://" | sort -u

# Análise de attachments
file malicious_attachment.doc
oledump.py malicious_attachment.doc
olevba malicious_attachment.doc

# Verificação de domínios suspeitos
whois suspicious-domain.com
dig suspicious-domain.com ANY
host suspicious-domain.com

# Ferramentas especializadas de análise
phishdetect -f phishing_email.eml
urlscan.io submit --url "https://suspicious-link.com"
virustotal -f phishing_email.eml

# Análise de headers SMTP
python3 -c "import email; msg = email.message_from_file(open('phishing_email.eml')); print(msg.items())"

# Script para análise automatizada
#!/bin/bash
echo "=== Análise de Email Phishing ==="
echo "1. Headers principais:"
grep -E "^(From:|To:|Subject:|Date:)" "$1"
echo "2. IPs no caminho de entrega:"
grep -i "received:" "$1" | grep -oE "\b([0-9]{1,3}\.){3}[0-9]{1,3}\b"
echo "3. URLs no corpo:"
grep -oE "https?://[^[:space:]]+" "$1" | sort -u
echo "4. Domínios suspeitos:"
grep -oE "@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" "$1" | sort -u
```

Resultado: os comandos permitiram extrair e analisar headers From, To, Subject e Reply-To de emails .eml, identificar IPs no caminho de entrega através dos headers Received, extrair URLs maliciosas do corpo do email, verificar domínios suspeitos com whois e dig, analisar attachments maliciosos com ferramentas como oledump e olevba, e usar APIs como VirusTotal e URLScan.io para análise mais profunda de IOCs.

## Referência
https://tryhackme.com/room/phishingemails2rytmuv