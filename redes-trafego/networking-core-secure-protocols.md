# Networking Core & Secure Protocols — TryHackMe

**Data:** 25/07/2026 | **Categoria:** Networking Basics

## O que aprendi
- **Serviços de Infraestrutura:** analisei o protocolo DHCP, responsável pela atribuição automática de endereços IP, e o DNS, responsável por traduzir nomes de domínios em endereços IP.
- **Camada de Transporte:** comparei o protocolo TCP, orientado à conexão com verificação via 3-Way Handshake, ao protocolo UDP, focado em alta velocidade e baixa latência.
- **Migração para Protocolos Seguros:** compreendi a substituição de protocolos legados em texto puro como FTP, HTTP, Telnet e POP3 pelos seus equivalentes seguros SFTP, HTTPS, SSH e SMTPS, com uso de criptografia TLS/SSL e cadeia de confiança de certificados digitais.

## Prática
Realizei consultas de registros de DNS e testei conexões criptografadas inspecionando certificados de segurança via terminal:
```bash
nslookup instagram.com
dig instagram.com
openssl s_client -connect instagram.com:443
```
Resultado: as ferramentas retornaram os registros A do domínio e exibiram os detalhes da cadeia de validação do certificado SSL do servidor.

## Referência
https://tryhackme.com/room/networkingcoreprotocols
https://tryhackme.com/room/networkingsecureprotocols
