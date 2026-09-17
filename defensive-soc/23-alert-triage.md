# SOC L1 Alert Triage

Data: 20/08/2026 | Categoria: SOC Team Internals

## O que aprendi

Fluxo de triagem: cada alerta no dashboard traz horário, nome, severidade, status e veredito, e o analista precisa se atribuir ao alerta, mover pra In Progress e investigar antes de decidir o desfecho.
Critério de decisão: nem todo alerta vira incidente. Parte do trabalho de N1 é reconhecer quando a evidência aponta pra comportamento legítimo e fechar como falso positivo, e quando realmente precisa escalar pra L2.
Papel da severidade: alertas críticos e de alta severidade como Potential Data Exfiltration e Double Extension File Creation pedem prioridade de investigação em relação a alertas de baixa severidade como downloads de repositórios conhecidos.

## Prática

Revisei o dashboard com cinco alertas atribuídos, incluindo Double Extension File Creation severidade alta, Potential Data Exfiltration severidade crítica e Download from GitHub Repository severidade baixa, todos aguardando ação. Também analisei dois alertas já fechados como referência de bom encerramento, Unusual VPN Login Location fechado como falso positivo por T.Ross L1, e Bruteforce Attack from External fechado como verdadeiro positivo por J.Adams L2. Pratiquei o ciclo completo de atribuir o alerta a mim, mover para In Progress, investigar a evidência disponível e decidir entre fechar como falso positivo ou escalar para L2.

## Referência
https://tryhackme.com/room/soclvlonealerttriage
