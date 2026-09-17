# Writeups de Estudo, Segurança Defensiva e SOC

Registro dos meus estudos práticos em segurança, seguindo trilhas do TryHackMe e
laboratórios próprios.

👤 Autor: Pedro Carvalho · [LinkedIn](https://www.linkedin.com/in/pedroalvesc/)
🎯 Objetivo: Analista de SOC evoluindo para Cyber Security Engineer

---

## ⭐ Destaques, comece por aqui

| Writeup | O que demonstra | MITRE ATT&CK |
|---|---|---|
| [Snort Challenge, criação e debug de regras IDS](writeups/snort-challenge-basics) | Escrita de regras Snort, detecção de exploits reais, troubleshooting | T1210 EternalBlue MS17-010, T1190 Log4Shell |

Neste laboratório escrevi regras de IDS com Snort do zero, cobrindo detecção de tráfego HTTP e FTP, identificação de arquivos por magic bytes e correção de erros de sintaxe. Depois apliquei regras contra capturas de exploits como EternalBlue e Log4Shell, cruzando os alertas com tcpdump e base64 pra confirmar manualmente o que cada regra encontrou. O foco foi entender a anatomia de uma regra e a diferença entre detectar um protocolo e detectar um evento específico dentro dele.

## 🛡️ Defensive Security e SOC
- [SOC L1, Alert Triage](defensive-soc/23-alert-triage.md)
- [SOC L1, Alert Reporting](defensive-soc/24-alert-reporting.md)
- [Logs Fundamentals](defensive-soc/07-logs-fundamentals.md)
- [Introdução a EDR](defensive-soc/17-intro-edr.md)
- [Introdução a SOAR](defensive-soc/18-intro-soar.md)
- [SOC Metrics](defensive-soc/26-soc-metrics.md) · [Workbooks e Lookups](defensive-soc/25-workbooks-lookups.md)

## 🔎 SIEM e Detecção
- [Introdução a SIEM](siem-deteccao/08-siem.md)
- [Splunk Basics](siem-deteccao/21-splunk-basics.md)
- [Elastic Stack Basics](siem-deteccao/22-elastic-stack-basics.md)
- [IDS e IPS Fundamentals](siem-deteccao/10-ids-ips-fundamentals.md)
- [Firewall](siem-deteccao/09-firewall.md)

## 🧠 Frameworks
- [Pyramid of Pain](frameworks/19-pyramid-of-pain.md)
- [Cyber Kill Chain](frameworks/20-cyber-kill-chain.md)

## 🌐 Redes e Análise de Tráfego
- [Networking, Concepts e Essentials](redes-trafego/networking-concepts-essentials.md)
- [Networking, Core e Secure Protocols](redes-trafego/networking-core-secure-protocols.md)
- [Wireshark Basics](redes-trafego/wireshark-basics.md) · [tcpdump Basics](redes-trafego/tcpdump-basics.md) · [Nmap Basics](redes-trafego/nmap-basics.md)

## 🐧 Sistemas e Ferramentas
- [Linux Fundamentals](sistemas-ferramentas/11-linux-fundamentals.md) · [Linux Shells](sistemas-ferramentas/12-linux-shells.md)
- [Criptografia e Public Key](sistemas-ferramentas/03-cryptography-e-public-key.md) · [Hashing Basics](sistemas-ferramentas/07-hashing-basics-github.md)
- [CyberChef](sistemas-ferramentas/cyberchef-basics.md) · [CAPA](sistemas-ferramentas/capa-basics.md) · [REMnux](sistemas-ferramentas/remnux-getting-started.md) · [FLARE VM](sistemas-ferramentas/13-flarevm-arsenal-of-tools.md)

## 🔓 Phishing e Vulnerabilidades
- [Introdução a Phishing](phishing-vulnerabilidades/27-intro-phishing.md)
- [Vulnerability Management](phishing-vulnerabilidades/11-vulnerability-management.md)

---
_Em construção: writeups do meu home lab de detecção com Sysmon, SIEM e simulação de ataques._
