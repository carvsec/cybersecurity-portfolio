# Nmap: The Basics — TryHackMe

**Data:** 03/08/2026 | **Categoria:** Reconnaissance

## O que aprendi
- **Mapeamento e Varredura:** estudei o Nmap para auditorias de segurança e reconhecimentos de rede.
- **Mapeamento de Ativos vs. Portas:** diferenciei a descoberta de hosts ativos da varredura de portas. Compreendi técnicas como SYN Scan com o parâmetro -sS, TCP Connect com -sT, UDP Scan com -sU e a desativação da checagem de ping com a opção -Pn.
- **Detecção e Scripts:** explorei a detecção de versões de serviços com -sV, identificação de Sistema Operacional com -O, execução de scripts do NSE com -sC e varreduras agressivas com -A.
- **Gerenciamento da Varredura:** aprendi a definir intervalos de portas com -p, ajustar a velocidade de envio com perfis de timing de -T0 a -T5 e exportar relatórios nos formatos -oN e -oX.

## Prática
Executei comandos de varredura rápida de portas com detecção de versão e scans agressivos completos:
```bash
sudo nmap -sS -sV 10.10.10.10 -T4
sudo nmap -A -Pn -p- 10.10.10.10 -oN resultado_nmap.txt
```
Resultado: o primeiro comando identificou as portas abertas e as versões dos serviços rodando no host de forma acelerada, enquanto o segundo realizou uma varredura completa em todas as portas sem enviar ping prévio, salvando a análise detalhada em arquivo de texto.

## Referência
https://tryhackme.com/room/nmap
