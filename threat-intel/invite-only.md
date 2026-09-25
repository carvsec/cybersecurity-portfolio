---
# Invite Only

**Data:** 21/09/2026 | **Categoria:** Threat Intelligence Practice

## O que aprendi
- **Análise Prática de Threat Intelligence:** aplicação real de conceitos de TI em cenário de SOC (Security Operations Center)
- **Uso do VirusTotal para Investigação:** análise detalhada de hashes e IPs usando a plataforma TryDetectThis2.0 (simulação do VirusTotal)
- **Identificação de Famílias de Malware:** reconhecimento de padrões específicos de malware como AsyncRAT
- **Correlação de Indicadores:** conexão entre diferentes IOCs (hashes, IPs, arquivos) para entender campanhas completas
- **Investigação de Campanhas de Ataque:** reconstrução de cadeias de execução e infraestrutura de ataque
- **Pesquisa de Relatórios de Ameaças:** uso de Google e fontes abertas para encontrar relatórios originais sobre campanhas

## Cenário da Sala
Você é um analista de SOC na TrySecureMe investigando dois indicadores sinalizados por um analista L1:
- **IP sinalizado:** 101.99.76.120
- **Hash SHA256 sinalizado:** 5d0509f68a9b7c415a726be75a078180e3f02e59866f193b0a99eee8e39c874f

## Plataformas Utilizadas na Investigação

### 🎯 **TryDetectThis2.0 (Simulação do VirusTotal)**
- **Para que serve:** Plataforma de threat intelligence simulada para análise prática
- **Recursos utilizados:**
  - **Análise de Hashes:** Identificação de arquivos por hash SHA256
  - **Relações entre IOCs:** Conexões entre arquivos, IPs, domínios
  - **Cadeias de Execução:** Parent/child relationships de processos
  - **Arquivos Droppados:** Arquivos criados durante execução
- **Uso prático:** Investigação passo a passo dos indicadores fornecidos

### 🔍 **VirusTotal Real (para confirmação)**
- **Para que serve:** Confirmação de descobertas e análise adicional
- **Recursos utilizados:**
  - **Communication Files:** Arquivos que se comunicaram com IP suspeito
  - **Malware Family Detection:** Identificação da família de malware
  - **Community Intelligence:** Informações compartilhadas por pesquisadores
- **Link:** https://www.virustotal.com

### 📚 **Google Search (OSINT)**
- **Para que serve:** Encontrar relatórios de pesquisa sobre campanhas
- **Recursos utilizados:**
  - **Pesquisa por Hashes:** Encontrar menções específicas
  - **Relatórios de Threat Intelligence:** Documentação formal de campanhas
  - **Artigos de Pesquisa:** Análises detalhadas de grupos de ataque
- **Uso prático:** Localizar o relatório "From Trust to Threat: Hijacked Discord Invites Used for Multi-Stage Malware Delivery"

## Passo a Passo da Investigação

### **1. Análise do Hash SHA256 (5d0509f68a9b7c415a726be75a078180e3f02e59866f193b0a99eee8e39c874f)**
```bash
# No TryDetectThis2.0 (VirusTotal simulado):
# 1. Pesquisar o hash
# 2. Identificar o arquivo: syshelpers.exe
# 3. Verificar tipo: Win32 EXE
```

### **2. Análise das Relações (Relations Tab)**
```bash
# 1. Execution Parents (pais de execução):
#    - 361GJX7J (hash: 047c5eec0445746862710d20e50a5dd04510b7e625fa5c1f5d48ce078001c0de)
#    - installer.exe (hash: fa102d4e3cfbe85f5189da70a52c1d266925f3efd122091cdc8fe0fc39033942)

# 2. Dropped Files (arquivos criados):
#    - Aclient.exe (hash: dd02c105809e4ca41a5489e585ba025eddb89a91703b73a566c9903e6406a08c)
```

### **3. Investigação do Segundo Parent (installer.exe)**
```bash
# 1. Pesquisar hash fa102d4e3cfbe85f5189da70a52c1d266925f3efd122091cdc8fe0fc39033942
# 2. Analisar Dropped Files:
#    - searchhost.exe
#    - syshelpers.exe
#    - nat.vbs
#    - runsys.vbs
```

### **4. Análise do IP 101.99.76.120**
```bash
# 1. Pesquisar IP no TryDetectThis2.0
# 2. Ir para aba "Relations"
# 3. Analisar "Communication Files" (arquivos que se comunicaram com este IP)
# 4. Verificar malware family em múltiplos arquivos
```

### **5. Descoberta da Família de Malware**
```bash
# Todos os arquivos que se comunicam com 101.99.76.120 têm o mesmo rótulo:
# MALWARE FAMILY: AsyncRAT
```

### **6. Pesquisa do Relatório Original**
```bash
# 1. Usar Google para pesquisar os hashes ou IP
# 2. Encontrar relatório da Check Point Research:
#    "From Trust to Threat: Hijacked Discord Invites Used for Multi-Stage Malware Delivery"
```

## Respostas das Questões

1. **syshelpers.exe** - Nome do arquivo do hash sinalizado
2. **Win32 EXE** - Tipo do arquivo
3. **361GJX7J,installer.exe** - Execution parents em ordem cronológica
4. **Aclient.exe** - Arquivo droppado pelo syshelpers.exe
5. **searchhost.exe,syshelpers.exe,nat.vbs,runsys.vbs** - Arquivos maliciosos droppados pelo installer.exe
6. **asyncrat** - Família de malware que conecta os arquivos ao IP
7. **From Trust to Threat: Hijacked Discord Invites Used for Multi-Stage Malware Delivery** - Título do relatório original
8. **ChromeKatz** - Ferramenta para roubo de cookies do Chrome
9. **ClickFix** - Técnica de phishing utilizada
10. **Discord** - Plataforma usada para redirecionar usuários

## AsyncRAT - A Família de Malware Identificada

### 🐀 **O que é AsyncRAT?**
- **Tipo:** Remote Access Trojan (RAT) open-source
- **Propósito:** Controle remoto completo de sistemas comprometidos
- **Características:**
  - Keylogging
  - Captura de tela
  - Webcam access
  - File transfer
  - Shell access
  - Persistence mechanisms

### 🔗 **Infraestrutura C2 (Command & Control)**
- **IP 101.99.76.120:** Servidor C2 para múltiplas instâncias do AsyncRAT
- **Arquivos relacionados:** Todos se comunicam com este IP para receber comandos
- **Campanha:** Distribuição via Discord invites comprometidos

## Ferramentas e Técnicas Identificadas

### 🛠️ **ChromeKatz**
- **Para que serve:** Roubo de cookies e credenciais do Google Chrome
- **Funcionalidade:** Extrai cookies de sessão para bypass de autenticação
- **Uso pelos atacantes:** Acesso a contas sem necessidade de senhas

### 🎣 **ClickFix**
- **Para que serve:** Técnica de phishing específica
- **Funcionalidade:** Envolve correção falsa de problemas para instalar malware
- **Uso pelos atacantes:** Engana usuários para executar código malicioso

### 💬 **Discord como Vetor**
- **Para que serve:** Plataforma de distribuição inicial
- **Funcionalidade:** Invites comprometidos redirecionam para sites maliciosos
- **Uso pelos atacantes:** Aproveita confiança na plataforma para distribuição

## Aprendizados Chave de Threat Intelligence

### 🔄 **Cadeia de Comprometimento Completa**
1. **Vetor inicial:** Discord invites comprometidos
2. **Downloader:** installer.exe
3. **Dropped files:** Múltiplos componentes maliciosos
4. **RAT principal:** AsyncRAT via syshelpers.exe
5. **C2 server:** 101.99.76.120
6. **Tooling adicional:** ChromeKatz para roubo de credenciais

### 🎯 **Valor da Correlação**
- Um único IP pode conectar múltiplos arquivos maliciosos
- Hashes diferentes podem pertencer à mesma campanha
- Relatórios públicos fornecem contexto valioso

### 📊 **Fluxo de Trabalho de SOC**
```bash
# 1. Receber alerta/indicador (L1 analyst)
# 2. Pesquisar em plataformas de TI (VirusTotal, etc.)
# 3. Analisar relações e conexões
# 4. Identificar família de malware
# 5. Pesquisar relatórios relevantes
# 6. Documentar descobertas
# 7. Criar regras de detecção (se aplicável)
```

Resultado: a sala proporcionou experiência prática completa em análise de threat intelligence, desde a investigação inicial de hashes e IPs até a identificação de famílias de malware e descoberta de relatórios de pesquisa relevantes. Aprendi como conectar diferentes indicadores para reconstruir campanhas completas de ataque, e como usar múltiplas fontes (plataformas de TI, pesquisa na web) para obter uma compreensão abrangente das ameaças.

## Referência
https://tryhackme.com/room/invite-only
