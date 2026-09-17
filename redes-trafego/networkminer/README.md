---
# NetworkMiner

**Data:** 17/09/2026 | **Categoria:** Network Forensics

## O que aprendi
- **NetworkMiner como NFAT:** ferramenta de análise forense de rede funcionando como sniffer passivo e parser de PCAPs
- **Extração de Artefatos:** sistemas operacionais detectados, sessões de comunicação, hostnames, portas abertas, arquivos transferidos
- **Reconstrução de Arquivos:** capacidade de remontar arquivos transferidos através da rede incluindo imagens, documentos, executáveis
- **Análise de Credenciais:** extração de credenciais em texto claro de protocolos como HTTP Basic Auth, FTP, outros
- **Interface Intuitiva:** apresentação de dados extraídos em interface gráfica simplificando análise e economizando tempo

## Prática
Usei NetworkMiner para carregar PCAPs, extrair informações forenses e reconstruir arquivos transferidos:

```bash
# Comandos básicos do NetworkMiner (modo linha de comando)
NetworkMiner.exe --open pcapfile.pcap
NetworkMiner.exe --extract-all pcapfile.pcap
NetworkMiner.exe --parse pcapfile.pcap --output-dir ./forensics

# Análise de PCAP com foco em artefatos específicos
NetworkMiner.exe --open case.pcap --hosts
NetworkMiner.exe --open case.pcap --sessions
NetworkMiner.exe --open case.pcap --files
NetworkMiner.exe --open case.pcap --credentials

# Extração de arquivos específicos por tipo
NetworkMiner.exe --open transfer.pcap --extract-images
NetworkMiner.exe --open transfer.pcap --extract-documents
NetworkMiner.exe --open transfer.pcap --extract-certificates

# Análise forense avançada
NetworkMiner.exe --open investigation.pcap --dns
NetworkMiner.exe --open investigation.pcap --parameters
NetworkMiner.exe --open investigation.pcap --keywords "password,login,secret"

# Integração com outras ferramentas forenses
tshark -r evidence.pcap -Y "http" | tee http_traffic.txt
zeek -r network.pcap
capinfos -T -z -e -u capture.pcap

# Scripting para análise automatizada
#!/bin/bash
for pcap in *.pcap; do
    NetworkMiner.exe --open "$pcap" --output-dir "./output_${pcap%.*}"
    echo "Analyzed: $pcap"
done
```

Resultado: os comandos permitiram carregar arquivos PCAP no NetworkMiner, extrair informações completas sobre hosts (sistemas operacionais, sessões, portas), reconstruir arquivos transferidos incluindo imagens e documentos, extrair credenciais de autenticação em texto claro, e automatizar análise de múltiplos arquivos PCAP para investigações forenses em larga escala.

## Referência
https://tryhackme.com/room/networkminer