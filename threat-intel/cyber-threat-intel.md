---
# Cyber Threat Intel

**Data:** 21/09/2026 | **Categoria:** Threat Intelligence

## O que aprendi
- **Fundamentos de Threat Intelligence:** conceitos básicos de inteligência de ameaças, incluindo tipos (estratégica, operacional, técnica) e ciclo de vida
- **Plataformas de Análise de Ameaças:** utilização de ferramentas online para coleta e análise de indicadores de comprometimento (IOCs)
- **Análise de Hashes de Arquivos:** compreensão de como hashes criptográficos (MD5, SHA1, SHA256) são usados para identificação única de arquivos maliciosos
- **Classificação de Malware:** identificação de famílias de malware e técnicas de ataque com base em análise de comportamento
- **Correlação de IOCs:** técnicas para conectar diferentes indicadores (IPs, domínios, hashes) para entender campanhas de ataque completas

## Plataformas e Ferramentas de Threat Intelligence
Esta sala introduziu várias plataformas essenciais para análise de ameaças:

### 🔍 **VirusTotal**
- **Para que serve:** Análise de arquivos, URLs, IPs e domínios suspeitos
- **Recursos principais:** Detecção multi-antivírus, análise estática/dinâmica, relações entre IOCs
- **Uso prático:** Upload de arquivos suspeitos, verificação de hashes, análise de comportamento
- **Link:** https://www.virustotal.com

### 🛡️ **AlienVault OTX (Open Threat Exchange)**
- **Para que serve:** Compartilhamento colaborativo de indicadores de ameaças
- **Recursos principais:** Pulses (coleções de IOCs), feeds de ameaças, pesquisa por malware family
- **Uso prático:** Pesquisa de campanhas conhecidas, verificação se IOCs estão em listas públicas
- **Link:** https://otx.alienvault.com

### 💼 **IBM X-Force Exchange**
- **Para que serve:** Plataforma de inteligência de ameaças da IBM
- **Recursos principais:** Reputação de IPs/domínios, análise de malware, relatórios de ameaças
- **Uso prático:** Verificação de reputação, pesquisa de vulnerabilidades, análise de campanhas
- **Link:** https://exchange.xforce.ibmcloud.com

### 📊 **MISP (Malware Information Sharing Platform)**
- **Para que serve:** Plataforma open-source para compartilhamento de inteligência de ameaças
- **Recursos principais:** Armazenamento de IOCs, taxonomias, relacionamento entre eventos
- **Uso prático:** Compartilhamento em comunidades, correlação automática de eventos
- **Link:** https://www.misp-project.org

### 🎯 **Outras Plataformas Importantes:**
- **ThreatConnect:** Plataforma unificada de threat intelligence
- **Recorded Future:** Inteligência baseada em machine learning
- **Anomali ThreatStream:** Plataforma de gerenciamento de threat intelligence

## Fluxo de Trabalho Básico em Threat Intelligence
```bash
# 1. Coleta de IOCs (de logs, alertas, relatórios)
# Exemplo: Extrair hashes de arquivos suspeitos
md5sum arquivo_suspeito.exe
sha256sum arquivo_suspeito.exe

# 2. Verificação em múltiplas plataformas
# VirusTotal para arquivos
curl -X POST https://www.virustotal.com/api/v3/files/upload

# AlienVault OTX para pesquisa
curl -H "X-OTX-API-KEY: YOUR_KEY" https://otx.alienvault.com/api/v1/indicators

# 3. Análise de relações
# Verificar conexões entre diferentes IOCs
# - Arquivo X se comunica com IP Y
# - IP Y está associado ao domínio Z
# - Domínio Z foi usado em campanha W

# 4. Classificação e priorização
# Baseado em:
# - Severidade das detecções
# - Confiança das fontes
# - Relevância para o ambiente

# 5. Geração de relatórios
# Documentar:
# - IOCs identificados
# - Táticas, técnicas e procedimentos (TTPs)
# - Recomendações de mitigação
```

## Tipos de Threat Intelligence
- **Estratégica:** Alto nível, para tomadores de decisão (ex: relatórios de tendências)
- **Operacional:** Foco em campanhas específicas (ex: análise de grupos de ataque)
- **Técnica:** IOCs específicos (ex: hashes, IPs, domínios)

## MITRE ATT&CK Framework
- **Para que serve:** Conhecimento estruturado sobre táticas e técnicas de adversários
- **Uso:** Mapeamento de comportamentos observados para técnicas conhecidas
- **Link:** https://attack.mitre.org

Resultado: a sala proporcionou compreensão fundamental das plataformas de threat intelligence disponíveis, seus casos de uso específicos, e como integrá-las em um fluxo de trabalho de análise de segurança. Aprendi que cada plataforma tem suas especialidades: VirusTotal para análise técnica detalhada, AlienVault OTX para colaboração comunitária, IBM X-Force para reputação corporativa, e MISP para compartilhamento estruturado.

## Referência
https://tryhackme.com/room/cyberthreatintel
