---
# Phishing Emails 3

**Data:** 17/09/2026 | **Categoria:** Phishing Analysis

## O que aprendi
- **Técnicas de Extração de Attachments:** métodos para obter attachments maliciosos de emails phishing para análise forense
- **Uso de Malware Sandboxes:** detonação de attachments em ambientes controlados para entender comportamento e funcionalidade
- **Análise de Payloads Maliciosos:** identificação de scripts, executáveis, documentos Office maliciosos e outros tipos de attachments
- **Deobfuscation Manual:** técnicas para desofuscar código JavaScript, VBA macros, e outros payloads ofuscados
- **Análise de Comportamento:** observação de atividades de rede, criação de arquivos, modificações de registro e outras ações maliciosas

## Prática
Extraí attachments maliciosos, detonei em sandboxes e analisei comportamentos de payloads:

```bash
# Extração de attachments de emails
munpack phishing_email.eml
ripmime -i phishing_email.eml -d attachments/
python3 -c "import email; msg = email.message_from_file(open('phishing_email.eml')); [open(p.get_filename(), 'wb').write(p.get_payload(decode=True)) for p in msg.get_payload() if p.get_filename()]"

# Análise de documentos Office maliciosos
oleid malicious_document.doc
olevba malicious_document.xls -c
python3 oletools/olevba.py malicious_document.ppt

# Detonação em sandboxes
curl -X POST -F "file=@malicious.exe" https://api.hybrid-analysis.com/v2/submit/file
python3 any.run-submit.py malicious_file.exe
cuckoo submit malicious_document.pdf

# Análise de scripts maliciosos
strings malicious_script.js | head -50
jsbeautifier malicious_script.js -o deobfuscated.js
python3 -m js2py malicious_script.js

# Ferramentas de análise estática
file malicious_attachment.exe
strings malicious_attachment.exe | grep -i "http\|https\|passw\|key\|token"
exiftool malicious_attachment.pdf
peframe malicious_attachment.exe

# Análise de comportamento em tempo real
strace -f -o strace.log ./malicious_binary
ltrace -f -o ltrace.log ./malicious_binary
procmon /accepteula -backingfile procmon.pml

# Script para análise automatizada de attachments
#!/bin/bash
echo "=== Análise de Attachments Phishing ==="
echo "1. Informações do arquivo:"
file "$1"
echo "2. Strings relevantes:"
strings "$1" | grep -E "(http|https|\.exe|\.dll|powershell|cmd\.exe)" | head -20
echo "3. Hash do arquivo:"
md5sum "$1"
sha256sum "$1"
echo "4. Verificação no VirusTotal:"
python3 vt-check.py $(sha256sum "$1" | awk '{print $1}')

# Análise de PDFs maliciosos
pdfid malicious.pdf
pdf-parser malicious.pdf
peepdf -i malicious.pdf

# Análise de arquivos RTF
rtfdump.py malicious.rtf
python3 oletools/rtfobj.py malicious.rtf
```

Resultado: os comandos permitiram extrair attachments de emails com munpack e ripmime, analisar documentos Office maliciosos com oletools (oleid, olevba), detonar arquivos em sandboxes como Hybrid Analysis e Cuckoo, desofuscar scripts JavaScript com jsbeautifier, analisar executáveis com strings e peframe, monitorar comportamento com strace e ltrace, verificar hashes em VirusTotal, e analisar arquivos PDF e RTF com ferramentas especializadas como pdfid e rtfdump.

## Referência
https://tryhackme.com/room/phishingemails3tryoe