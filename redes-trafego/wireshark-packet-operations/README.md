---
# Wireshark Packet Operations

**Data:** 17/09/2026 | **Categoria:** Packet Analysis

## O que aprendi
- **Filtros de Exibição:** uso avançado de filtros com operadores lógicos (and, or, not) e funções para isolamento preciso de tráfego
- **Análise Estatística:** utilização do menu de estatísticas para análise de protocolos, distribuição de pacotes por endpoint e resumos de fluxo
- **Filtros de Captura:** configuração de filtros de captura para otimizar coleta de dados durante monitoramento em tempo real
- **Operações com Fluxos:** follow TCP stream e follow SSL stream para análise completa de comunicações entre cliente e servidor
- **Padrões de Tráfego:** reconhecimento de padrões como varredura SYN, conexões C2 e transferências de arquivo suspeitas

## Prática
Apliquei filtros de exibição avançados, analisei estatísticas de conversação e reconstruí fluxos de comunicação completos:

```bash
# Filtro para tráfego HTTP específico de host
http.host matches ".*rad.msn.com.*"

# Filtro combinado com operadores lógicos
ip.addr == 192.168.1.100 and tcp.port == 80

# Filtro para protocolo específico
tcp.port == 443 or ssl

# Filtro para conteúdo em payload
http contains "password" or ftp contains "USER"

# Estatísticas de conversação
Statistics -> Conversations -> TCP/UDP/Other tabs

# Follow TCP stream para análise completa
Analyze -> Follow -> TCP Stream
```

Resultado: os filtros permitiram isolar tráfego específico para investigação direcionada, as estatísticas identificaram endpoints com comunicação anormal, e a análise de fluxos reconstruiu comunicações completas entre cliente e servidor.

## Referência
https://tryhackme.com/room/wiresharkpacketoperations