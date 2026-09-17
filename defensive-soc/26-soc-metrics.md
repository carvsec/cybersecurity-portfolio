# SOC Metrics and Objectives

Data: 20/08/2026 | Categoria: SOC Team Internals

## O que aprendi

Papel das métricas em um SOC: métricas como Time to Detect, Time to Respond e Time to Acknowledge medem a eficiência real do time e ajudam a identificar gargalos no processo antes que virem problema recorrente.
Ligação entre métrica ruim e causa raiz: um incidente demorado geralmente aponta pra uma métrica específica falhando, e não pra um problema genérico de time, o que muda completamente o tipo de ação corretiva necessária.
Melhoria orientada a dados: toda melhoria de processo em um SOC deve estar ligada a uma métrica concreta e a um responsável designado, não apenas a uma boa intenção vaga.

## Prática

Resolvi três cenários de solicitação da alta gestão do MDR, Unhappy Customer, Delayed Alert e Tired Analysts, identificando em cada um a métrica problemática, propondo uma tarefa de melhoria e definindo o responsável por executá la. No cenário Unhappy Customer, envolvendo o cliente OpenDoor Inc cujo e mail do CFO e conta Entra ID foram comprometidos, levando seis horas pra remover o invasor da caixa de e mail e cinco horas pra resetar a senha e o MFA da vítima, identifiquei que o Time to Respond estava excessivamente alto, com tempo demais gasto contendo o ataque.

## Referência
https://tryhackme.com/room/socmetricsandobjectives
