---
# Phishing Emails 4

**Data:** 17/09/2026 | **Categoria:** Phishing Analysis

## O que aprendi
- **Técnicas Avançadas de Obfuscação:** métodos sofisticados usados por atacantes para esconder URLs maliciosas e payloads
- **Análise de URLs Encurtadas:** identificação de serviços de URL shortening usados para mascarar destinos maliciosos
- **Decodificação de Payloads:** técnicas para decodificar base64, hexadecimal, rot13 e outras codificações comuns em phishing
- **Análise de Redirecionamentos:** identificação de cadeias de redirecionamento usadas para evadir detecção
- **Verificação de Certificados SSL:** análise de certificados de domínios phishing para identificar fraudes

## Prática
Analisei técnicas avançadas de obfuscação, decodifiquei payloads e investiguei cadeias de redirecionamento:

```bash
# Desofuscação de URLs encurtadas
curl -I "https://bit.ly/suspicious-link"  # Seguir redirecionamentos
curl -s "https://api.unshorten.me?shortURL=https://bit.ly/suspicious-link"
python3 -c "import requests; print(requests.get('https://tinyurl.com/xyz').url)"

# Decodificação de payloads codificados
echo "base64_encoded_string" | base64 -d
echo "hex_encoded_string" | xxd -r -p
echo "rot13_encoded_string" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
python3 -c "import urllib.parse; print(urllib.parse.unquote('url%20encoded%20string'))"

# Análise de JavaScript ofuscado
node -e "console.log(eval('obfuscated_js_code'))"
js-beautify -r malicious.js
python3 -m js2py malicious.js

# Verificação de certificados SSL
openssl s_client -connect phishing-site.com:443 -servername phishing-site.com | openssl x509 -text -noout
nmap --script ssl-cert phishing-site.com -p 443
testssl.sh phishing-site.com

# Análise de cadeias de redirecionamento
curl -L -v "https://suspicious-url.com" 2>&1 | grep -i "location:"
python3 -c "import requests; r = requests.get('https://suspicious-url.com', allow_redirects=False); print(r.headers.get('Location'))"

# Ferramentas para análise de phishing
phish.ai analyze --url "https://suspicious-site.com"
urlscan.io search "domain:phishing-site.com"
virustotal -u "https://suspicious-url.com"

# Script para análise de obfuscação
#!/bin/bash
echo "=== Análise de Obfuscação Phishing ==="
echo "1. URL original: $1"
echo "2. Redirecionamentos:"
curl -L -v "$1" 2>&1 | grep -E "^< Location:|^> GET" | head -10
echo "3. Decodificação de parâmetros:"
echo "$1" | grep -oP '[?&][^=]+=\K[^&]*' | while read param; do
    echo "   Tentativa base64: $(echo "$param" | base64 -d 2>/dev/null || echo 'Falhou')"
    echo "   Tentativa URL decode: $(python3 -c "import urllib.parse; print(urllib.parse.unquote('$param'))")"
done

# Análise de iframes maliciosos
grep -oP '<iframe[^>]+src="\K[^"]+' phishing_page.html
python3 -c "from bs4 import BeautifulSoup; import sys; soup = BeautifulSoup(open(sys.argv[1]), 'html.parser'); [print(iframe['src']) for iframe in soup.find_all('iframe') if 'src' in iframe.attrs]" phishing_page.html

# Verificação de WHOIS para domínios recentes
whois phishing-domain.com | grep -i "creation date"
domaintools reverse-whois "phishing-domain.com"
```

Resultado: os comandos permitiram desofuscar URLs encurtadas seguindo redirecionamentos com curl -L, decodificar payloads base64, hex e rot13, analisar JavaScript ofuscado com js-beautify, verificar certificados SSL com openssl, investigar cadeias de redirecionamento, usar APIs como VirusTotal e URLScan.io para análise, extrair iframes maliciosos de páginas HTML, e verificar datas de criação de domínios através de WHOIS para identificar domínios recentemente registrados.

## Referência
https://tryhackme.com/room/phishingemails4gkxh