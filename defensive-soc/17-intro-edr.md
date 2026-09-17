# Introduction to EDR

Data: 20/08/2026 | Categoria: Security Solutions

## O que aprendi

Papel do EDR: monitora hosts continuamente e detecta atividade maliciosa que passa despercebida por antivírus tradicional, cobrindo execução de processo, persistência e movimentação lateral.
Dashboard de EDR: reúne métricas centrais como hosts ativos, novas detecções, fontes de detecção anomalia, comportamento e threat intel, além do histórico de malware prevenido por host.
Triagem de alerta: cada detecção listada traz severidade, tipo, host afetado e status, servindo de ponto de partida pra investigação do analista.

## Prática

Investiguei um alerta de acesso inicial via documento malicioso do Office no host DESKTOP HR01. Identifiquei que CURL.exe foi a ferramenta lançada pelo CMD.exe pra baixar o payload, e localizei o caminho absoluto do malware baixado em C:\Users\Public\install.exe. Também investiguei um alerta separado de dumping de credenciais via acesso à memória LSASS no host WIN ENG LAPTOP03, localizando o caminho absoluto do syncsvc.exe suspeito.

## Referência
https://tryhackme.com/room/introtoedr
