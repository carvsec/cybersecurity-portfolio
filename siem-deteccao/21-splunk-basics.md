# Splunk: The Basics

Data: 20/08/2026 | Categoria: Security Solutions

## O que aprendi

Fluxo de upload de dados: subir um log no Splunk segue cinco etapas, selecionar a fonte, definir o source type, configurar o índice de destino e o hostname, revisar as configurações e concluir o upload.
Formato de log JSON delimitado por linha: exige usar o assistente de upload do Splunk pra que cada linha seja tratada como um evento separado, e o comando spath após a busca base quando os campos não aparecem automaticamente nos resultados.
Uso da ferramenta pra investigação: depois do upload, o analista usa Search and Reporting pra consultar os eventos, filtrando por usuário, IP, país ou período de tempo.

## Prática

Fiz o upload do arquivo VPN_logs disponível na AttackBox, criei o índice VPN_Logs e confirmei que o arquivo continha 2862 eventos no total. Identifiquei que 60 eventos foram capturados pela usuária Maleena, que o username associado ao IP 107.14.182.38 era Smith, que 2814 eventos tinham origem em países diferentes da França, e que 14 eventos de VPN estavam associados ao IP 107.3.206.58.

## Referência
https://tryhackme.com/room/splunkbasics
