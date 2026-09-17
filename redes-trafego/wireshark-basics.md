# Wireshark: The Basics — TryHackMe

**Data:** 30/07/2026 | **Categoria:** Network Analysis

## O que aprendi
- **Análise de Protocolos:** estudei o uso do Wireshark para captura de pacotes em tempo real e análise pós-incidente com arquivos nos formatos pcap e pcapng.
- **Filtros de Exibição:** dominei a criação de Display Filters com base em endereços IP como ip.addr, portas e protocolos como icmp e http, combinando operadores lógicos and, or e not.
- **Recursos de Investigação:** explorei a funcionalidade Follow Stream para reconstruir sessões completas e utilizei os painéis de estatística Protocol Hierarchy e Endpoints para mapear a distribuição do tráfego.

## Prática
Apliquei filtros de exibição avançados no Wireshark para isolar tráfego web, resoluções de nomes e excluir o tráfego de loopback local:
```
http.request.method == "GET" or http.request.method == "POST"
dns
ip.addr == 192.168.1.50 and not ip.src == 127.0.0.1
```
Resultado: os filtros isolaram apenas as requisições HTTP dos métodos GET e POST, as consultas DNS e o tráfego do IP informado, removendo pacotes locais desnecessários da visualização.

## Referência
https://tryhackme.com/room/wiresharkthebasics
