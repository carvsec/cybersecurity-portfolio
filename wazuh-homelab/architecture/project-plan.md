# 📋 Plano do Projeto Wazuh Homelab

## 🎯 Objetivos do Projeto

### Objetivo Principal:
Criar um ambiente de SOC completo com Wazuh SIEM para desenvolvimento de habilidades práticas em Defensive Security e servir como portfólio técnico.

### Objetivos Específicos:
1. **Aprendizado Técnico:**
   - Dominar instalação e configuração do Wazuh SIEM
   - Implementar monitoramento em sistemas heterogêneos (Windows/Linux)
   - Desenvolver regras personalizadas de detecção
   - Analisar logs e eventos de segurança

2. **Portfólio Profissional:**
   - Demonstrar habilidades em SIEM/SOC operations
   - Mostrar capacidade de documentação técnica
   - Criar casos de uso reais para recrutadores
   - Desenvolver projetos complexos do zero

3. **Preparação para Mercado:**
   - Simular ambiente corporativo de SOC
   - Desenvolver mentalidade analítica de segurança
   - Praticar resposta a incidentes
   - Preparar para entrevistas técnicas

## 🗓️ Timeline do Projeto

### FASE 1: Planejamento (Outubro 2024)
**Duração:** 2 semanas
**Tarefas:**
- [x] Definir objetivos e escopo
- [x] Planejar arquitetura técnica
- [x] Documentar requisitos de hardware/software
- [ ] Criar checklist de instalação
- [ ] Configurar ambiente de virtualização

**Entregáveis:**
- Documentação de planejamento completa
- Diagrama de arquitetura
- Checklist de instalação

### FASE 2: Instalação e Configuração Básica (Novembro 2024)
**Duração:** 3 semanas
**Tarefas:**
- [ ] Instalar Wazuh Server (Ubuntu)
- [ ] Configurar Wazuh Manager e Indexer
- [ ] Instalar Wazuh Dashboard (Kibana)
- [ ] Configurar acesso e autenticação
- [ ] Testar instalação básica

**Entregáveis:**
- Wazuh Server funcionando
- Dashboard acessível
- Documentação de instalação

### FASE 3: Agentes e Integração (Dezembro 2024)
**Duração:** 3 semanas
**Tarefas:**
- [ ] Instalar agente no Windows 10
- [ ] Configurar Sysmon no Windows
- [ ] Instalar agente no Ubuntu
- [ ] Configurar logs do sistema Linux
- [ ] Testar comunicação agent-server

**Entregáveis:**
- 2+ sistemas monitorados
- Logs sendo coletados
- Dashboard com dados reais

### FASE 4: Regras e Detecção (Janeiro 2025)
**Duração:** 4 semanas
**Tarefas:**
- [ ] Configurar regras padrão do Wazuh
- [ ] Desenvolver regras personalizadas
- [ ] Criar alertas e notificações
- [ ] Desenvolver dashboards no Kibana
- [ ] Otimizar configurações

**Entregáveis:**
- Regras personalizadas funcionando
- Dashboards informativos
- Sistema de alertas configurado

### FASE 5: Simulação e Análise (Fevereiro 2025)
**Duração:** 3 semanas
**Tarefas:**
- [ ] Simular ataques básicos
- [ ] Analisar detecções geradas
- [ ] Criar relatórios de incidentes
- [ ] Ajustar regras baseado em resultados
- [ ] Otimizar performance

**Entregáveis:**
- Relatórios de simulação
- Análises de detecção
- Regras otimizadas

### FASE 6: Documentação Final (Março 2025)
**Duração:** 2 semanas
**Tarefas:**
- [ ] Completar toda documentação
- [ ] Criar guias passo a passo
- [ ] Desenvolver tutoriais específicos
- [ ] Documentar lições aprendidas
- [ ] Preparar apresentação do projeto

**Entregáveis:**
- Documentação completa
- Guias e tutoriais
- Apresentação do projeto

## 🖥️ Requisitos de Hardware

### Mínimo (Funcional):
- **CPU:** 4 cores (Intel i5/Ryzen 5 ou superior)
- **RAM:** 16GB DDR4
- **Armazenamento:** 256GB SSD
- **Virtualização:** Suporte VT-x/AMD-V habilitado

### Recomendado (Performance):
- **CPU:** 8 cores (Intel i7/Ryzen 7 ou superior)
- **RAM:** 32GB DDR4
- **Armazenamento:** 512GB+ SSD NVMe
- **Rede:** Gigabit Ethernet

### Especificações por VM:
1. **Wazuh Server:**
   - CPU: 4 cores
   - RAM: 8GB
   - Storage: 80GB
   - OS: Ubuntu 22.04 LTS Server

2. **Windows 10 Client:**
   - CPU: 2 cores
   - RAM: 4GB
   - Storage: 60GB
   - OS: Windows 10/11 Pro

3. **Ubuntu Client:**
   - CPU: 2 cores
   - RAM: 2GB
   - Storage: 40GB
   - OS: Ubuntu 22.04 Desktop

4. **Metasploitable 3:**
   - CPU: 2 cores
   - RAM: 2GB
   - Storage: 40GB
   - OS: Ubuntu-based vulnerable distro

## 📦 Requisitos de Software

### Virtualização:
- **Opção 1:** Proxmox VE 7/8 (recomendado)
- **Opção 2:** VirtualBox 7.0+
- **Opção 3:** VMware Workstation Player
- **Opção 4:** Hyper-V (Windows)

### Sistemas Operacionais:
- Ubuntu 22.04 LTS Server ISO
- Windows 10/11 Pro ISO
- Metasploitable 3 OVA

### Ferramentas de Segurança:
- Wazuh 4.7+
- Sysmon com configuração SwiftOnSecurity
- Elastic Stack (incluso no Wazuh)
- Kibana (incluso no Wazuh)

### Utilitários:
- SSH Client (PuTTY, OpenSSH)
- RDP Client (para Windows)
- Navegador moderno (Chrome, Firefox)
- Editor de texto/código (VS Code)

## 🔗 Dependências do Projeto

### Conhecimentos Prévios Necessários:
1. **Linux Básico:**
   - Terminal/Shell básico
   - Gerenciamento de pacotes (apt)
   - Configuração de rede
   - Permissões de arquivos

2. **Redes Básicas:**
   - Endereçamento IP
   - Subnets e gateways
   - Portas e protocolos
   - Conceitos de firewall

3. **Segurança Básica:**
   - Conceitos de SIEM/SOC
   - Tipos de logs e eventos
   - Ameaças comuns
   - Princípios de detecção

### Recursos de Aprendizado (Pré-requisito):
- [TryHackMe: Linux Fundamentals](https://tryhackme.com/module/linux-fundamentals)
- [TryHackMe: Introductory Networking](https://tryhackme.com/module/introductory-networking)
- [Wazuh Documentation](https://documentation.wazuh.com/)

## 📊 Métricas de Sucesso

### Técnicas:
| Métrica | Valor Alvo | Como Medir |
|---------|------------|------------|
| Sistemas Monitorados | 3+ | Agentes conectados no dashboard |
| Regras Personalizadas | 10+ | Regras ativas no Wazuh |
| Tempo de Instalação | < 8h | Tempo do primeiro commit ao funcionamento |
| Detecção de Ataques Simulados | 80%+ | Ataques detectados vs. simulados |
| Tempo de Resposta | < 30 min | Incidente detectado à análise inicial |

### Profissionais:
| Métrica | Valor Alvo | Como Medir |
|---------|------------|------------|
| Documentação Completa | 100% | Todas as fases documentadas |
| Commits no GitHub | 50+ | Histórico de desenvolvimento |
| Issues Resolvidas | 10+ | Problemas encontrados e resolvidos |
| Feedback da Comunidade | 3+ | Comentários/estrelas no GitHub |
| Visitas ao Repositório | 100+ | GitHub insights |

## ⚠️ Riscos e Mitigações

### Riscos Técnicos:
1. **Compatibilidade de versões:**
   - **Risco:** Versões incompatíveis do Wazuh/Elastic
   - **Mitigação:** Seguir versões testadas na documentação oficial

2. **Performance do sistema:**
   - **Risco:** Hardware insuficiente para múltiplas VMs
   - **Mitigação:** Começar com configuração mínima, escalar conforme necessário

3. **Complexidade de configuração:**
   - **Risco:** Configurações erradas causam falhas
   - **Mitigação:** Documentar cada passo, fazer backups de configuração

### Riscos de Tempo:
1. **Estimativas otimistas:**
   - **Risco:** Subestimar tempo necessário
   - **Mitigação:** Adicionar 30% de buffer em todas as estimativas

2. **Conflito com outros estudos:**
   - **Risco:** Google Certificate + THM + Wazuh simultaneamente
   - **Mitigação:** Priorizar, dedicar horas específicas para cada

### Riscos de Aprendizado:
1. **Curva de aprendizado íngreme:**
   - **Risco:** Desmotivação com complexidade
   - **Mitigação:** Começar simples, celebrar pequenas vitórias

2. **Falta de suporte:**
   - **Risco:** Problemas técnicos sem ajuda
   - **Mitigação:** Participar de comunidades (Discord, Reddit)

## 📈 Critérios de Aceitação

O projeto será considerado **COMPLETO** quando:

### Funcional:
1. ✅ Wazuh Server instalado e funcionando
2. ✅ 3+ agentes conectados e enviando logs
3. ✅ Dashboard Kibana acessível com dados
4. ✅ 10+ regras personalizadas funcionando
5. ✅ Simulações de ataque detectadas e documentadas

### Documental:
1. ✅ README completo e profissional
2. ✅ Guias de instalação passo a passo
3. ✅ Documentação de configuração
4. ✅ Relatórios de simulação e análise
5. ✅ Lições aprendidas documentadas

### Profissional:
1. ✅ Repositório GitHub organizado e profissional
2. ✅ Commits regulares demonstrando progresso
3. ✅ Projeto mencionável em entrevistas
4. ✅ Habilidades demonstradas através do projeto
5. ✅ Feedback positivo da comunidade

## 🔄 Processo de Trabalho

### Metodologia:
- **Iterativo:** Pequenos passos, feedback contínuo
- **Documentado:** Tudo é documentado desde o início
- **Versionado:** Git para controle de versão
- **Testado:** Cada fase testada antes de avançar

### Fluxo de Trabalho Diário:
1. **Planejamento:** 15 min - O que fazer hoje
2. **Execução:** 2-3h - Trabalho técnico
3. **Documentação:** 30 min - Documentar o feito
4. **Commit:** 15 min - Git commit com mensagem descritiva
5. **Revisão:** 15 min - Revisar progresso, planejar amanhã

### Controle de Qualidade:
- Cada configuração testada imediatamente
- Screenshots de etapas importantes
- Backups de arquivos de configuração
- Revisão por pares (se possível) ou auto-revisão

## 🎯 Próximos Passos Imediatos

### Esta Semana:
1. [ ] Finalizar planejamento de arquitetura
2. [ ] Configurar ambiente de virtualização
3. [ ] Baixar ISOs necessários
4. [ ] Criar VMs base
5. [ ] Documentar processo inicial

### Próxima Semana:
1. [ ] Instalar Ubuntu Server no Wazuh VM
2. [ ] Configurar rede básica
3. [ ] Instalar pré-requisitos do Wazuh
4. [ ] Iniciar instalação do Wazuh
5. [ ] Documentar cada passo

---

**📅 Próxima Atualização:** 01/10/2024  
**📊 Progresso Atual:** 5% (Planejamento inicial)

*Documento vivo - atualizado conforme progresso do projeto*
