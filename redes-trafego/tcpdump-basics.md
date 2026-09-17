# Tcpdump: The Basics — TryHackMe

**Data:** 31/07/2026 | **Categoria:** Network Analysis

## O que aprendi
- **Captura via Terminal:** explorei o tcpdump como utilitário em linha de comando nativo no Linux, essencial para a captura de pacotes em servidores remotos sem interface gráfica.
- **Parâmetros de Controle:** compreendi o uso de opções como -i para selecionar a interface de rede, -c para delimitar a quantidade de pacotes, além de -w e -r para salvar e ler arquivos no formato pcap. Também utilizei -n e -nn para desativar a resolução de nomes de domínio e portas.
- **Filtros BPF e Verbosidade:** estudei a aplicação de filtros Berkeley Packet Filter para isolar endereços IP, portas e protocolos específicos. Ajustei os níveis de verbosidade com -v, -vv e -vvv, e inspecionei o conteúdo dos dados com -A para exibição em ASCII e -X para formato hexadecimal.

## Prática
Capturei e filtrei pacotes diretamente na interface de rede via linha de comando:
```bash
sudo tcpdump -i eth0 -c 10 -nn
sudo tcpdump -i eth0 port 80 -w captura_web.pcap
tcpdump -r captura_web.pcap -A
sudo tcpdump -nn src 192.168.1.50 and dst port 22
```
Resultado: os comandos permitiram capturar dez pacotes sem resolver nomes, salvar todo o tráfego HTTP da porta 80 em um arquivo pcap, ler o arquivo exibindo os dados em modo texto e filtrar tentativas de conexão SSH originadas de um IP específico.

## Referência
https://tryhackme.com/room/tcpdump
