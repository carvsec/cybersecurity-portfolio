---
# Snort

**Data:** 17/09/2026 | **Categoria:** Intrusion Detection

## O que aprendi
- **Snort como IPS:** principal sistema open source de prevenção de intrusão usando regras para definir atividade maliciosa e gerar alertas
- **Funcionalidade NIDS/NIPS:** sistema baseado em regras que analisa tráfego de rede e identifica padrões indicativos de ataques
- **Estrutura de Regras:** ações (alert, block, drop, log), protocolos (TCP, UDP, ICMP, IP), operadores bidirecionais, opções (msg, sid, rev)
- **Desenvolvimento:** criado por Martin Roesch, mantido por contribuidores open source e equipe Cisco Talos
- **Aplicação Prática:** investigação de dados de tráfego para parar atividades maliciosas em diferentes cenários

## Prática
Compreendi estrutura de regras, escrevi regras básicas e executei Snort em diferentes modos:

```bash
# Comandos básicos do Snort
snort -c local.rules -r arquivo.pcap -A console
snort -c local.rules -r arquivo.pcap -A console -l .
snort -r arquivo.pcap -X -v
snort -r snort.log.<timestamp> -X

# Exemplos de regras Snort
alert tcp any any <> any 80 (msg:"HTTP Traffic Detected"; sid:1000001; rev:1;)
alert tcp any any <> any 21 (msg:"FTP Traffic"; sid:1000002; rev:1;)
alert tcp any 21 -> any any (msg:"FTP Failed Login"; content:"530"; sid:1000003; rev:1;)
alert tcp any any -> any any (msg:"PNG File Detected"; content:"|89 50 4E 47 0D 0A 1A 0A|"; sid:1000004; rev:1;)
alert tcp any any -> any any (msg:"Torrent Metafile Detected"; content:"application/x-bittorrent"; sid:1000005; rev:1;)

# Regras para vulnerabilidades conhecidas
alert tcp any any -> any any (msg:"SMB IPC$ Share Access"; content:"\\IPC$"; sid:1000006; rev:1;)
alert tcp any any -> any any (msg:"Log4j Payload Size Match"; dsize:770<>855; sid:1000007; rev:1;)

# Validação de regras
snort -c local.rules -T
snort -c /etc/snort/snort.conf --plugin-check

# Modos de operação
snort -i eth0 -c local.rules -A fast
snort -D -c /etc/snort/snort.conf -i eth0
```

Resultado: os comandos permitiram executar Snort em modo IDS contra arquivos PCAP, validar sintaxe de regras, detectar tráfego HTTP/FTP, identificar arquivos por magic bytes, e criar regras para vulnerabilidades como EternalBlue e Log4Shell.

## Referência
https://tryhackme.com/room/snort