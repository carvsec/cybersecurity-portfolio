---
# Snapped Phishing Line

**Data:** 17/09/2026 | **Categoria:** Phishing Investigation

## O que aprendi
- **Investigação Completa de Casos Phishing:** análise de incidentes do início ao fim incluindo triagem, análise e resposta
- **Técnicas de Triage:** priorização de emails suspeitos baseada em severidade e impacto potencial
- **Análise Forense de Email:** reconstrução de cadeia de ataque a partir de evidências em emails
- **Resposta a Incidentes:** procedimentos para conter, erradicar e recuperar de ataques phishing bem-sucedidos
- **Documentação de IOCs:** criação de listas completas de indicadores para compartilhamento com equipes e ferramentas

## Prática
Conduzi investigação completa de caso phishing, desde triagem inicial até resposta a incidentes:

```bash
# Triage inicial de emails suspeitos
python3 phishing-triage.py inbox/ --output triage_results.csv
grep -l "urgent\|invoice\|payment\|password\|verify" inbox/*.eml | head -10

# Análise forense detalhada
python3 email-forensics.py malicious_email.eml --output forensic_report.json
strings malicious_email.eml | grep -E "(passw|key|token|secret)" -i

# Extração e documentação de IOCs
python3 ioc-extractor.py case_emails/ > case_iocs.txt
md5sum case_attachments/* > attachment_hashes.txt
sha256sum case_attachments/* >> attachment_hashes.txt

# Verificação de IOCs em ferramentas de segurança
for hash in $(cat attachment_hashes.txt | awk '{print $1}'); do
    python3 vt-check.py $hash
    python3 malshare-check.py $hash
done

for ip in $(grep -oP '\b\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}\b' case_iocs.txt | sort -u); do
    python3 abuseipdb-report.py $ip
    whois $ip | grep -i "country\|netname"
done

# Análise de cadeia de ataque
echo "=== Cadeia de Ataque ==="
echo "1. Vetor inicial: $(grep 'Subject:' initial_email.eml)"
echo "2. Payload: $(file malicious_attachment.exe)"
echo "3. C2: $(strings malicious_attachment.exe | grep -oP 'https?://[^[:space:]]+' | head -1)"
echo "4. Infraestrutura: $(whois $(dig +short c2-domain.com) | grep -i 'country\|organization' | head -2)"

# Script para resposta a incidentes
#!/bin/bash
echo "=== Resposta a Incidente Phishing ==="
echo "1. Usuários afetados:"
grep -r "To:" case_emails/ | grep -oP '<\K[^>]+' | sort -u > affected_users.txt
cat affected_users.txt
echo "2. Ações de contenção:"
echo "   - Bloquear IPs maliciosos"
for ip in $(cat malicious_ips.txt); do
    echo "   iptables -A INPUT -s $ip -j DROP"
done
echo "   - Bloquear domínios"
for domain in $(cat malicious_domains.txt); do
    echo "   echo '0.0.0.0 $domain' >> /etc/hosts"
done
echo "3. Notificação aos usuários:"
python3 notify_users.py affected_users.txt --template "phishing_alert_template.html"

# Documentação para compartilhamento
python3 generate-ioc-report.py case_iocs.txt --format "misp" > case_report.misp.json
python3 generate-ioc-report.py case_iocs.txt --format "stix" > case_report.stix.xml
python3 generate-ioc-report.py case_iocs.txt --format "csv" > case_report.csv

# Análise pós-incidente
echo "=== Lições Aprendidas ==="
echo "1. Gap de detecção: $(grep 'missed_by' detection_log.txt | wc -l) emails não detectados"
echo "2. Tempo de resposta: $(python3 calculate_response_time.py timeline.log)"
echo "3. Recomendações:"
echo "   - Implementar treinamento adicional em phishing"
echo "   - Atualizar regras de detecção do email gateway"
echo "   - Melhorar processos de resposta a incidentes"
```

Resultado: os comandos permitiram realizar triagem inicial de emails suspeitos baseada em palavras-chave, conduzir análise forense detalhada extraindo strings sensíveis, documentar IOCs com hashes de arquivos, verificar reputação em APIs de segurança como VirusTotal e AbuseIPDB, reconstruir cadeia de ataque identificando vetor inicial, payload e infraestrutura C2, implementar ações de resposta como bloqueio de IPs e domínios, gerar relatórios em formatos padrão (MISP, STIX, CSV), e conduzir análise pós-incidente identificando gaps de detecção e recomendações de melhoria.

## Referência
https://tryhackme.com/room/snappedphishingline