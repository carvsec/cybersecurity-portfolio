# Pyramid of Pain

Data: 20/08/2026 | Categoria: Cyber Defence Frameworks

## O que aprendi

Estrutura da pirâmide: da base ao topo, os indicadores são IP addresses, Domain Names, Network artifacts, Host artifacts, Tools e TTPs, organizados pelo quanto custa pro atacante mudar cada um.
Lógica do nome Pyramid of Pain: quanto mais alto o indicador na pirâmide, mais dor causa ao atacante quando você o detecta e bloqueia, porque TTPs comportamento do atacante são muito mais difíceis e caros de mudar do que um simples endereço IP.
Aplicação prática: indicadores como hash de arquivo ou domínio comprado pra typo squatting ficam nas camadas inferiores, fáceis de trocar, enquanto o plano e objetivo do atacante TTP fica no topo, praticamente impossível de evitar sem mudar a estratégia inteira.

## Prática

Classifiquei corretamente seis descrições dentro dos níveis certos da pirâmide, incluindo identificar assinaturas usadas pra atribuir payloads a um autor como Tools, endereços usados pra identificar infraestrutura de campanha como IP addresses, e artefatos que podem se apresentar como tráfego de C2 como Network artifacts.

## Referência
https://tryhackme.com/room/pyramidofpain
