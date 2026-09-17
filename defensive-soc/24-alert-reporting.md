# SOC L1 Alert Reporting

Data: 20/08/2026 | Categoria: SOC Team Internals

## O que aprendi

Diferença entre triagem e reporting: triagem decide o que fazer com o alerta, reporting documenta a decisão de forma clara o suficiente pra outro analista L2 ou L3 entender o caso sem precisar reinvestigar do zero.
Estrutura de um bom comentário de alerta: horário, quem, ação, o que foi afetado e o veredito final, sem informação solta ou ambígua.
Importância da escrita técnica objetiva: um relatório mal escrito atrasa a resposta do time inteiro, então clareza e precisão valem mais do que texto longo.

## Prática

Analisei o dashboard com cinco alertas, incluindo Spike of Domain Discovery Commands severidade média, que investiguei e documentei em um comentário formal identificando um reverse shell revshell.exe gerado a partir do processo IIS worker w3wp.exe no host DMZ MSEXCHANGE 2013, seguido de uma sequência de comandos de reconhecimento de domínio Active Directory whoami, net group, nltest executados sob o contexto NT AUTHORITY SYSTEM, com veredito de verdadeiro positivo indicando comprometimento bem sucedido do servidor web. Também revisei outros dois alertas já escalados e em investigação por E.Fleming L2, Web Scanning of Corporate Resources e Sensitive Document Share to External, ambos marcados como verdadeiro positivo, e um alerta fechado como falso positivo por S.Todd L1, Fast Beaconing to Untrusted Domain.

## Referência
https://tryhackme.com/room/soclvlonealertreporting
