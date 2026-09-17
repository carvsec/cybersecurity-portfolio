# Elastic Stack: The Basics

Data: 20/08/2026 | Categoria: Security Solutions

## O que aprendi

Elastic Stack como SIEM: reúne Elasticsearch, Logstash e Kibana pra ingestão, armazenamento e visualização de logs, com o Kibana funcionando como a interface de investigação pro analista.
Discover view: permite explorar os eventos brutos de um índice, filtrar por campo e ajustar o intervalo de tempo pra localizar exatamente os dados relevantes.
Dashboards e visualizações: agregam dados em tabelas e gráficos configuráveis, facilitando identificar padrões que seriam difíceis de perceber olhando evento por evento.

## Prática

Explorei o índice vpn_connections no Discover do Kibana, contendo 2861 eventos com campos como timestamp, action, Source_ip, Source_Country, UserName e port. Apliquei filtros de data e de campo pra isolar eventos específicos, e criei um dashboard com tabelas e visualizações a partir desses dados filtrados.

## Referência
https://tryhackme.com/room/elasticstackbasics
