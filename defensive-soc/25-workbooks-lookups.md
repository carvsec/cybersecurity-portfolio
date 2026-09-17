# SOC Workbooks and Lookups

Data: 20/08/2026 | Categoria: SOC Team Internals

## O que aprendi

Papel dos workbooks: são fluxogramas de decisão que padronizam o processo de investigação de um analista N1, reduzindo a chance de pular uma etapa importante durante um incidente.
Estrutura em árvore de decisão: cada etapa do workbook leva a um ponto de decisão, e a resposta a essa pergunta define se o caso é escalado para L2 ou fechado como falso positivo.
Aplicação prática do processo: um workbook de e-mail externo com anexo suspeito guia o analista por sandbox de binários, revisão manual de scripts, análise do e-mail via ferramenta EML, e coleta de evidência antes de decidir o desfecho.

## Prática

Resolvi um laboratório com três workbooks disponíveis, Email Analysis, PowerShell Analysis e Network Analysis, focando no workbook de Email Analysis para o cenário External Email With Script or Binary Attachment. Organizei corretamente a sequência de seis etapas do fluxo, desde continuar a análise do anexo em sandbox até escrever um relatório de alerta para L2, chegando ao ponto de decisão se o anexo é malicioso, tem origem falsificada ou é inesperado para o papel do destinatário, direcionando corretamente para escalar a L2 quando sim, ou fechar como falso positivo quando não.

## Referência
https://tryhackme.com/room/socworkbooksandlookups
