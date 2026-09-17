---
# Detecting Web Attacks

**Data:** 17/09/2026 | **Categoria:** Web Security Monitoring

## O que aprendi
- **Técnicas Comuns de Ataque Web:** visão geral de ataques frequentes antes de aprender a detectá-los através de logs e capturas de pacotes
- **Análise de Logs de Servidor Web:** logs como mina de ouro para detecção de tentativas de intrusão, permitindo isolamento rápido de requisições suspeitas
- **Padrões de Comportamento Suspeito:** identificação de padrões comuns em logs de sistemas Linux e assinaturas de ataque conhecidas
- **Reconhecimento de Ataques Aplicação:** foco em camada de aplicação onde técnicas tradicionais de análise de tráfego têm limitações
- **Técnicas de Análise Forense Web:** triagem de incidentes, identificação de hosts comprometidos, extração e decodificação de payloads

## Prática
Analisei logs de servidor web, identifiquei padrões de ataque e apliquei técnicas de detecção forense:

```bash
# Análise de logs de acesso Apache/Nginx para ataques
grep -E "(union.*select|select.*from|1=1|' OR '1'='1)" /var/log/apache2/access.log
grep -E "(\.\./|\.\.\\|etc/passwd|bin/sh)" /var/log/nginx/access.log
awk '{print $1}' /var/log/apache2/access.log | sort | uniq -c | sort -nr

# Detecção de tentativas de injeção SQL
cat web_logs.txt | grep -i "union\|select\|insert\|update\|delete\|drop\|create\|alter"
grep -E "%27|%20OR%20|%20AND%20|%3D%3D" access.log

# Identificação de ataques XSS
grep -E "<script>|javascript:|alert\(|onload=|onerror=" access.log
cat logs.txt | grep -i "eval\|document\.cookie\|window\.location"

# Análise de parâmetros suspeitos
zegrep "(cmd=|exec=|system=|passthru=|shell_exec=)" /var/log/httpd/*
grep -E "(php://|data://|expect://|input://)" access.log

# Ferramentas especializadas para análise de logs
goaccess /var/log/apache2/access.log -a
lnav /var/log/nginx/*
logwatch --detail High --service httpd

# Análise de payloads em tráfego web
tshark -r web_traffic.pcap -Y "http.request.method == POST" -T fields -e http.file_data
tcpdump -nn -A -s0 -r attack.pcap 'port 80' | grep -E "(passwd|shadow|config)"
```

Resultado: os comandos permitiram identificar tentativas de injeção SQL com padrões "union select" e "1=1", detectar payloads XSS contendo tags <script> e chamadas javascript:, analisar parâmetros suspeitos com wrappers PHP maliciosos, e isolar requisições POST contendo dados sensíveis em capturas de tráfego.

## Referência
https://tryhackme.com/room/detectingwebattacks