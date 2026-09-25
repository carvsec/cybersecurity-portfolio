---
# IP and Domain Threat Intel

**Data:** 21/09/2026 | **Categoria:** Network Intelligence

## O que aprendi
- **Análise de Reputação de IPs:** técnicas para determinar se um endereço IP está associado a atividades maliciosas
- **Investigação de Domínios:** métodos para analisar registros de domínio e identificar sites de phishing ou C2
- **Plataformas de Threat Intelligence para Rede:** ferramentas especializadas para análise de infraestrutura de ataque
- **Geolocalização de Ameaças:** identificação da origem geográfica de IPs maliciosos
- **Correlação de Infraestrutura:** conexão de diferentes elementos (IPs, domínios, ASNs) para mapear campanhas

## Plataformas e Ferramentas para Análise de IPs e Domínios
Esta sala focou em ferramentas específicas para análise de infraestrutura de rede:

### 🌐 **AbuseIPDB**
- **Para que serve:** Banco de dados colaborativo de IPs reportados por abuso
- **Recursos principais:**
  - **Relatórios de Abuso:** Spam, brute force, exploits, scanning
  - **Pontuação de Confiança:** 0-100 (quanto maior, mais malicioso)
  - **Histórico de Relatórios:** Timeline de atividades reportadas
  - **API para Consultas:** Verificação programática de IPs
- **Uso prático:** Verificar se IP aparece em ataques conhecidos
- **Link:** https://www.abuseipdb.com

### 🔍 **Talos Intelligence (Cisco)**
- **Para que serve:** Reputação de IPs e domínios da Cisco
- **Recursos principais:**
  - **Reputação em Tempo Real:** Classificação de IPs/domínios
  - **Análise de Malware:** Relacionamento com amostras conhecidas
  - **Feed de Ameaças:** Atualizações constantes de IOCs
  - **Pesquisa Avançada:** Filtros por tipo de ameaça, país, etc.
- **Uso prático:** Verificação de reputação corporativa
- **Link:** https://talosintelligence.com

### 🕵️ **Shodan**
- **Para que serve:** Motor de busca para dispositivos conectados à internet
- **Recursos principais:**
  - **Scanning de Serviços:** Identificação de serviços expostos
  - **Banners de Serviço:** Informações de versão e configuração
  - **Filtros Específicos:** país, cidade, organização, porta
  - **Vulnerabilidades Conhecidas:** Serviços com falhas conhecidas
- **Uso prático:** Identificar infraestrutura exposta, encontrar C2 servers
- **Link:** https://www.shodan.io

### 🔬 **Censys**
- **Para que serve:** Plataforma de pesquisa de ativos na internet
- **Recursos principais:**
  - **Inventário Completo:** Hosts, domínios, certificados SSL/TLS
  - **Análise de Certificados:** Validade, emissor, assinatura
  - **Monitoramento Contínuo:** Mudanças na infraestrutura
  - **APIs para Pesquisa:** Consultas programáticas
- **Uso prático:** Mapeamento de infraestrutura, pesquisa de certificados suspeitos
- **Link:** https://search.censys.io

### 📋 **Whois**
- **Para que serve:** Consulta de informações de registro de domínios
- **Recursos principais:**
  - **Registrante:** Informações sobre quem registrou o domínio
  - **Datas:** Criação, expiração, última atualização
  - **Nameservers:** Servidores DNS responsáveis
  - **Status:** Ativo, suspenso, etc.
- **Uso prático:** Identificar donos de domínios suspeitos
- **Comando:** `whois dominio.com`

### 🎯 **DNS Tools**
```bash
# Consulta básica de DNS
nslookup dominio.com
dig dominio.com

# Consulta de tipos específicos de registro
dig dominio.com MX      # Servidores de email
dig dominio.com TXT     # Registros TXT (SPF, DMARC)
dig dominio.com NS      # Nameservers

# Verificação de histórico DNS
# Usar serviços como SecurityTrails ou DNSHistory

# Consulta reversa de IP (PTR)
nslookup 192.168.1.1
dig -x 192.168.1.1

# Script para análise DNS rápida
#!/bin/bash
echo "=== Análise DNS de $1 ==="
echo ""
echo "1. Resolução A:"
dig +short $1 A
echo ""
echo "2. Nameservers:"
dig +short $1 NS
echo ""
echo "3. Registro MX:"
dig +short $1 MX
echo ""
echo "4. Registro TXT:"
dig +short $1 TXT
```

### 🌍 **Geolocalização de IPs**
```bash
# Ferramentas para geolocalização
# MaxMind GeoIP, IP2Location, etc.

# Usar API de geolocalização
curl ipinfo.io/8.8.8.8
# Retorna: país, cidade, provedor, coordenadas

# Script para análise de IP
#!/bin/bash
echo "=== Análise de IP: $1 ==="
echo ""
echo "1. Geolocalização:"
curl -s "https://ipinfo.io/$1/json" | jq '.country, .city, .org'
echo ""
echo "2. Reputação (AbuseIPDB):"
# Necessário API key do AbuseIPDB
echo ""
echo "3. Consulta reversa:"
dig +short -x $1
```

### 🔗 **Análise de Infraestrutura de C2 (Command & Control)**
```bash
# Indicadores de servidores C2:
# 1. IPs com alta taxa de detecção em VirusTotal
# 2. Domínios com vida curta (DGAs ou disposable)
# 3. Certificados SSL auto-assinados ou de baixa qualidade
# 4. Servidores respondendo em portas incomuns
# 5. Similaridade com infraestrutura conhecida

# Exemplo: Verificar IP no VirusTotal
curl -X GET "https://www.virustotal.com/api/v3/ip_addresses/8.8.8.8" \
  -H "x-apikey: YOUR_API_KEY"

# Exemplo: Verificar domínio
curl -X GET "https://www.virustotal.com/api/v3/domains/example.com" \
  -H "x-apikey: YOUR_API_KEY"
```

### 📊 **Plataformas Adicionais para Análise de Rede**
- **SecurityTrails:** Histórico DNS, subdomínios, dados passivos
- **RiskIQ:** Inteligência de ameaças digital
- **GreyNoise:** Ruído de internet, scanners e bots
- **BinaryEdge:** Exposição de dados na internet
- **ZoomEye:** Similar ao Shodan, foco em dispositivos IoT

### 🎯 **Indicadores de IPs/Domínios Maliciosos**
- **Alta contagem de relatórios** no AbuseIPDB
- **Detecção por múltiplas fontes** no VirusTotal/Talos
- **Histórico de associação** com malware conhecido
- **Geolocalização incomum** para o serviço
- **Domínios recém-registrados** (menos de 30 dias)
- **Registrante genérico/privacy-protected**
- **Nameservers suspeitos** ou compartilhados com domínios maliciosos

### 🔄 **Fluxo de Trabalho para Análise**
```bash
# 1. Coleta do IP/domínio suspeito
# 2. Verificação básica (nslookup/dig)
# 3. Consulta WHOIS (informações de registro)
# 4. Verificação de reputação (AbuseIPDB, Talos)
# 5. Análise no VirusTotal (relações com malware)
# 6. Geolocalização (origem do IP)
# 7. Pesquisa em Shodan/Censys (serviços expostos)
# 8. Correlação com outros IOCs
# 9. Documentação dos resultados
```

Resultado: a sala proporcionou compreensão prática das principais plataformas para análise de IPs e domínios, desde ferramentas básicas como whois e dig até plataformas avançadas como AbuseIPDB, Shodan e Talos Intelligence. Aprendi que cada ferramenta tem seu propósito específico: AbuseIPDB para relatórios de abuso, Shodan para infraestrutura exposta, WHOIS para informações de registro, e Talos para reputação corporativa. A análise combinada dessas fontes permite identificar com confiança se um IP ou domínio está envolvido em atividades maliciosas.

## Referência
https://tryhackme.com/room/ipanddomainthreatintel
