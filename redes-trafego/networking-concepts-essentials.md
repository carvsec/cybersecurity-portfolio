# Networking Concepts & Essentials — TryHackMe

**Data:** 20/07/2026 | **Categoria:** Networking Basics

## O que aprendi
- **Modelos de Rede:** estudei as diferenças entre o modelo teórico OSI de 7 camadas e o modelo prático TCP/IP de 4 camadas.
- **Endereçamento:** analisei o endereço físico MAC na camada 2 e o endereço lógico IP na camada 3.
- **Portas Padrão:** mapeei portas essenciais de serviços, incluindo a porta 80 para HTTP, 443 para HTTPS e 22 para SSH.
- **Ativos de Rede:** diferenciei a função de um Switch, focado na conexão interna da rede local via endereço MAC, da função de um Roteador, focado na comunicação entre redes distintas via IP.

## Prática
Utilizei utilitários de linha de comando para testar conectividade, traçar rotas de rede e mapear endereços:
```bash
ping 8.8.8.8
tracert tryhackme.com
ipconfig /all
arp -a
telnet 192.168.1.1 80
```
Resultado: os comandos permitiram validar a comunicação com servidores externos, verificar o endereço de gateway local e mapear a tabela ARP da máquina.

## Referência
https://tryhackme.com/room/networkingconcepts
https://tryhackme.com/room/networkingessentials
