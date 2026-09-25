---
# File and Hash Threat Intel

**Data:** 21/09/2026 | **Categoria:** File Analysis

## O que aprendi
- **Análise de Hashes Criptográficos:** compreensão de como MD5, SHA1 e SHA256 são usados para identificação única de arquivos
- **Plataformas de Análise de Malware:** utilização de ferramentas especializadas para análise estática e dinâmica de arquivos suspeitos
- **Detecção de Packers e Obfuscadores:** identificação de técnicas usadas para esconder código malicioso em arquivos
- **Análise de Metadados:** extração de informações úteis de cabeçalhos de arquivos e estruturas internas
- **Correlação de Artefatos:** conexão de diferentes arquivos relacionados em uma campanha de ataque

## Plataformas e Ferramentas para Análise de Arquivos e Hashes
Esta sala focou em ferramentas específicas para análise de arquivos maliciosos:

### 🔬 **VirusTotal (Análise Avançada)**
- **Para que serve:** Análise multi-antivírus de arquivos, com recursos avançados
- **Recursos principais:**
  - **Detecção:** 70+ motores antivírus
  - **Análise Estática:** Extração de strings, metadados, cabeçalhos
  - **Análise Dinâmica:** Sandbox behavior analysis
  - **Relações:** Conexões com outros IOCs
- **Uso prático:** Upload de arquivos, verificação de hashes, análise de comportamento
- **API disponível:** Para automatização de verificações

### 🧪 **Hybrid Analysis**
- **Para que serve:** Sandbox avançada para análise de malware
- **Recursos principais:**
  - **Análise Comportamental:** Monitoramento de ações do malware
  - **Análise de Rede:** Captura de tráfego C2
  - **Dump de Memória:** Análise de processos em execução
  - **Anti-evasion:** Técnicas para bypass de detecção de sandbox
- **Uso prático:** Submissão de arquivos para análise automatizada
- **Link:** https://www.hybrid-analysis.com

### 🎯 **Any.Run**
- **Para que serve:** Sandbox interativa para análise de malware
- **Recursos principais:**
  - **Análise Interativa:** Controle manual durante execução
  - **Ambientes Específicos:** Windows, Linux, Android
  - **Gravação de Tela:** Captura visual do comportamento
  - **Análise em Tempo Real:** Monitoramento ao vivo
- **Uso prático:** Análise detalhada de comportamento suspeito
- **Link:** https://app.any.run

### 📦 **MalwareBazaar**
- **Para que serve:** Repositório colaborativo de amostras de malware
- **Recursos principais:**
  - **Banco de Dados:** Milhões de amostras de malware
  - **Busca por Características:** YARA rules, hashes, strings
  - **Download Seguro:** Amostras em containers protegidos
  - **Estatísticas:** Análise de tendências de malware
- **Uso prático:** Pesquisa de amostras similares, download para análise
- **Link:** https://bazaar.abuse.ch

### 🔍 **Joe Sandbox**
- **Para que serve:** Análise automatizada de malware em sandbox
- **Recursos principais:**
  - **Análise Profunda:** Static + dynamic + memory analysis
  - **Relatórios Detalhados:** PDF/HTML com análise completa
  - **Suporte Multi-OS:** Windows, macOS, Linux, Android
  - **API para Automação:** Integração com workflows
- **Uso prático:** Análise automatizada em escala
- **Link:** https://www.joesandbox.com

### 🛠️ **Ferramentas de Linha de Comando para Análise Inicial**
```bash
# Cálculo de hashes para identificação
md5sum arquivo_suspeito.exe
sha1sum arquivo_suspeito.exe
sha256sum arquivo_suspeito.exe

# Identificação do tipo de arquivo
file arquivo_suspeito.exe
exiftool arquivo_suspeito.exe  # Metadados

# Extração de strings para análise
strings arquivo_suspeito.exe | head -100
strings -n 8 arquivo_suspeito.exe | grep -i "http\|passw\|key"

# Análise de cabeçalhos PE (Windows executables)
peinfo arquivo_suspeito.exe
pestudio arquivo_suspeito.exe

# Verificação de packers/obfuscadores
peid arquivo_suspeito.exe
diec arquivo_suspeito.exe

# Script para análise inicial automatizada
#!/bin/bash
echo "=== Análise Inicial de Arquivo Suspeito ==="
echo "Arquivo: $1"
echo ""
echo "1. Tipo: $(file "$1")"
echo "2. Hashes:"
echo "   MD5:    $(md5sum "$1" | awk '{print $1}')"
echo "   SHA1:   $(sha1sum "$1" | awk '{print $1}')"
echo "   SHA256: $(sha256sum "$1" | awk '{print $1}')"
echo "3. Strings suspeitas:"
strings "$1" | grep -E "(http|https|\.exe|\.dll|CreateProcess|RegOpenKey)" | head -15
```

### 📊 **Fluxo de Trabalho para Análise de Arquivos**
```bash
# 1. Coleta do arquivo suspeito
# 2. Cálculo de hashes (identificação única)
# 3. Verificação em bases de dados (VirusTotal, MalwareBazaar)
# 4. Análise estática inicial (file, strings, metadados)
# 5. Submissão a sandboxes (Hybrid Analysis, Any.Run)
# 6. Análise de relatórios gerados
# 7. Correlação com outros IOCs
# 8. Classificação e documentação
```

### 🔗 **APIs para Automação**
```bash
# Exemplo: Verificar hash no VirusTotal via API
API_KEY="sua_chave_virustotal"
HASH="5d0509f68a9b7c415a726be75a078180e3f02e59866f193b0a99eee8e39c874f"

curl --request GET \
  --url "https://www.virustotal.com/api/v3/files/$HASH" \
  --header "x-apikey: $API_KEY"

# Exemplo: Submeter arquivo ao Hybrid Analysis
curl -X POST \
  -F "file=@malware.exe" \
  -F "environment_id=100" \
  -H "api-key: YOUR_API_KEY" \
  https://www.hybrid-analysis.com/api/v2/submit/file
```

### 🎯 **Indicadores de Arquivos Maliciosos**
- **Hashes em múltiplas bases de dados:** Sinal forte de maliciosidade
- **Detecção por múltiplos AVs:** Quanto mais detecções, mais confiança
- **Comportamento suspeito em sandbox:** Criar processos, modificar registro, rede
- **Metadados inconsistentes:** Informações falsas ou removidas
- **Uso de packers/obfuscadores:** Técnicas para esconder código

Resultado: a sala proporcionou compreensão prática das principais plataformas para análise de arquivos e hashes, desde ferramentas básicas de linha de comando até sandboxes avançadas. Aprendi que cada plataforma tem seu foco: VirusTotal para verificação rápida, Hybrid Analysis/Any.Run para análise comportamental detalhada, e MalwareBazaar para pesquisa de amostras similares. O fluxo de trabalho ideal combina análise estática inicial com submissão a sandboxes para compreensão completa do comportamento do malware.

## Referência
https://tryhackme.com/room/fileandhashthreatintel
