# 🔧 Wazuh SIEM Homelab - SOC Environment

**Status:** 🚧 Em construção | **Última atualização:** 25/09/2026  
**Autor:** Pedro Carvalho | **LinkedIn:** [pedroalvesc](https://www.linkedin.com/in/pedroalvesc/)

## 🎯 Objetivo do Projeto

Criar um ambiente completo de Security Operations Center (SOC) utilizando Wazuh SIEM open-source para monitoramento, detecção e resposta a incidentes de segurança. Este projeto serve como laboratório prático para desenvolvimento de habilidades em Defensive Security.

### 🎓 Objetivos de Aprendizado:
1. Implementar e configurar um SIEM enterprise-grade (Wazuh)
2. Monitorar múltiplos sistemas (Windows, Linux, Docker)
3. Desenvolver regras personalizadas para detecção de ameaças
4. Simular ataques reais e analisar detecções
5. Criar dashboards e relatórios de segurança
6. Documentar processos para portfólio técnico

## 🏗️ Arquitetura do Ambiente

```
                    🌐 Internet
                        |
                🔒 Firewall (UFW)
                        |
        ┌───────────────┴───────────────┐
        │                               │
    🖥️ Wazuh Server                 🖥️ Workstations
    (Ubuntu 22.04 LTS)              (Monitoradas)
        │                               │
        ├── 📊 Elastic Stack            ├── 🪟 Windows 10
        ├── 🛡️ Wazuh Manager            │   ├── Sysmon
        ├── 🔍 Wazuh Indexer            │   ├── Wazuh Agent
        └── 🎨 Wazuh Dashboard          │   └── Aplicações teste
                                        │
                                        ├── 🐧 Ubuntu 22.04
                                        │   ├── Wazuh Agent
                                        │   ├── Serviços comuns
                                        │   └── Logs de sistema
                                        │
                                        └── 🐳 Metasploitable 3
                                            ├── Vulnerabilidades
                                            ├── Wazuh Agent
                                            └── Serviços vulneráveis
```

## 📋 Roadmap do Projeto

### FASE 1: PLANEJAMENTO E INSTALAÇÃO (Outubro 2024)
- [x] **S1.1** - Planejamento de arquitetura e requisitos
- [ ] **S1.2** - Configuração de VMs (Proxmox/VirtualBox)
- [ ] **S1.3** - Instalação do Wazuh Server (Ubuntu)
- [ ] **S1.4** - Configuração básica do Wazuh

### FASE 2: CONFIGURAÇÃO DE AGENTES (Novembro 2024)
- [ ] **S2.1** - Instalação do Wazuh Agent no Windows 10
- [ ] **S2.2** - Instalação do Wazuh Agent no Ubuntu
- [ ] **S2.3** - Configuração do Sysmon no Windows
- [ ] **S2.4** - Integração de logs do sistema

### FASE 3: REGRAS E DETECÇÃO (Dezembro 2024)
- [ ] **S3.1** - Configuração de regras padrão do Wazuh
- [ ] **S3.2** - Desenvolvimento de regras personalizadas
- [ ] **S3.3** - Configuração de alertas e notificações
- [ ] **S3.4** - Criação de dashboards no Kibana

### FASE 4: SIMULAÇÃO E ANÁLISE (Janeiro 2025)
- [ ] **S4.1** - Simulação de ataques básicos
- [ ] **S4.2** - Análise de logs e detecções
- [ ] **S4.3** - Criação de relatórios de incidentes
- [ ] **S4.4** - Otimização de regras baseada em resultados

### FASE 5: DOCUMENTAÇÃO FINAL (Fevereiro 2025)
- [ ] **S5.1** - Documentação completa do ambiente
- [ ] **S5.2** - Guias de instalação e configuração
- [ ] **S5.3** - Casos de uso e exemplos práticos
- [ ] **S5.4** - Lições aprendidas e próximos passos

## 🛠️ Tecnologias Utilizadas

### 💻 Sistemas Operacionais:
- **Wazuh Server:** Ubuntu 22.04 LTS
- **Windows Client:** Windows 10/11 Pro
- **Linux Client:** Ubuntu 22.04 LTS
- **Target:** Metasploitable 3

### 🔧 Ferramentas de Segurança:
- **SIEM:** Wazuh 4.7+
- **Endpoint Monitoring:** Wazuh Agent, Sysmon
- **Visualização:** Kibana (Wazuh Dashboard)
- **Log Management:** Elastic Stack

### ⚡ Virtualização:
- Proxmox VE / VirtualBox / VMware
- Vagrant para automação (opcional)

### 📝 Documentação:
- Markdown para documentação
- PlantUML para diagramas
- Screenshots e gravações

## 📁 Estrutura do Repositório

```
wazuh-homelab/
├── 📄 README.md                          # Este arquivo
├── 📁 architecture/                      # Diagramas e planejamento
│   ├── network-diagram.puml             # Diagrama de rede
│   ├── system-requirements.md           # Requisitos do sistema
│   └── installation-checklist.md        # Checklist de instalação
├── 📁 installation/                      # Guias de instalação
│   ├── wazuh-server/                    # Instalação do servidor
│   ├── windows-agent/                   # Agente Windows
│   ├── linux-agent/                     # Agente Linux
│   └── sysmon-config/                   # Configuração do Sysmon
├── 📁 configuration/                     # Arquivos de configuração
│   ├── wazuh/                           # Configurações do Wazuh
│   ├── rules/                           # Regras personalizadas
│   ├── alerts/                          # Configuração de alertas
│   └── dashboards/                      # Dashboards do Kibana
├── 📁 simulation/                        # Simulações de ataque
│   ├── attack-scenarios/                # Cenários de ataque
│   ├── detection-analysis/              # Análise de detecções
│   └── incident-reports/                # Relatórios de incidentes
├── 📁 documentation/                     # Documentação completa
│   ├── guides/                          # Guias passo a passo
│   ├── tutorials/                       # Tutoriais específicos
│   └── lessons-learned/                 # Lições aprendidas
└── 📁 scripts/                          # Scripts de automação
    ├── setup/                           # Scripts de setup
    ├── monitoring/                      # Scripts de monitoramento
    └── analysis/                        # Scripts de análise
```

## 🚀 Começando

### Pré-requisitos:
1. **Hardware:**
   - CPU: 4+ cores (8+ recomendado)
   - RAM: 16GB+ (32GB recomendado)
   - Storage: 100GB+ SSD
   - Virtualization enabled (VT-x/AMD-V)

2. **Software:**
   - Virtualizador (Proxmox, VirtualBox, VMware)
   - Ubuntu 22.04 ISO
   - Windows 10 ISO
   - Metasploitable 3 OVA

3. **Conhecimentos:**
   - Linux básico (terminal, pacotes, serviços)
   - Redes básicas (IP, subnets, firewall)
   - Conceitos básicos de segurança

### Instalação Rápida (Guia Resumido):
```bash
# 1. Instalar Ubuntu Server
# 2. Instalar Wazuh via script oficial
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh --generate-config-files

# 3. Instalar agentes nos sistemas monitorados
# Windows: Executar installer .msi
# Linux: curl + apt install
```

## 📊 Métricas do Projeto

| Métrica | Valor Alvo | Status |
|---------|------------|---------|
| Sistemas Monitorados | 3+ | ⏳ |
| Regras Personalizadas | 10+ | ⏳ |
| Simulações Realizadas | 5+ | ⏳ |
| Detecções Efetivas | 90%+ | ⏳ |
| Tempo de Resposta | < 1 hora | ⏳ |
| Documentação Completa | 100% | ⏳ |

## 🎯 Casos de Uso Implementados

### 1. **Detecção de Brute Force SSH**
- Regras para múltiplas tentativas de login SSH
- Alertas após 5 tentativas falhas em 5 minutos
- Bloqueio automático via integração com firewall

### 2. **Monitoramento de Processos Maliciosos**
- Detecção de executáveis suspeitos no Windows
- Monitoramento de criação de processos
- Alertas para processos conhecidos como maliciosos

### 3. **Análise de Logs do Windows**
- Monitoramento de Event IDs críticos
- Detecção de alterações no registro
- Alertas para atividades suspeitas de usuários

### 4. **Monitoramento de Integridade de Arquivos**
- FIM (File Integrity Monitoring) em diretórios críticos
- Detecção de alterações não autorizadas
- Baseline de integridade do sistema

## 📈 Resultados Esperados

### Técnicos:
1. Ambiente SOC funcional com monitoramento em tempo real
2. Dashboard com visibilidade completa do ambiente
3. Regras de detecção cobrindo ataques comuns
4. Processo de resposta a incidentes documentado

### Profissionais:
1. Portfólio técnico demonstrável para recrutadores
2. Experiência prática com SIEM enterprise-grade
3. Habilidades em análise de logs e detecção de ameaças
4. Documentação que demonstra capacidade técnica

## 🤝 Contribuição

Este é um projeto pessoal de aprendizado, mas sugestões são bem-vindas! Se você:
- Encontrou um erro na documentação
- Tem uma sugestão de melhoria
- Conhece uma ferramenta/tecnologia que poderia ser adicionada

Sinta-se à vontade para abrir uma issue ou entrar em contato via LinkedIn.

## 📚 Recursos Úteis

### Documentação Oficial:
- [Wazuh Documentation](https://documentation.wazuh.com/)
- [Elasticsearch Guide](https://www.elastic.co/guide/)
- [Kibana User Guide](https://www.elastic.co/guide/kibana/)

### Tutoriais e Guias:
- [Wazuh Installation Guide](https://documentation.wazuh.com/current/installation-guide/)
- [Sysmon Configuration](https://github.com/SwiftOnSecurity/sysmon-config)
- [MITRE ATT&CK Framework](https://attack.mitre.org/)

### Comunidades:
- [Wazuh Discord](https://discord.gg/wazuh)
- [Reddit r/Wazuh](https://www.reddit.com/r/Wazuh/)
- [Stack Overflow - Wazuh Tag](https://stackoverflow.com/questions/tagged/wazuh)

## 📄 Licença

Este projeto é para fins educacionais e de portfólio. Todo o conteúdo é disponibilizado sob a licença MIT - veja o arquivo [LICENSE](LICENSE) para detalhes.

---

**🚀 Próximos Passos:** 
1. Configurar ambiente de virtualização
2. Instalar Wazuh Server
3. Documentar processo de instalação
4. Iniciar configuração de agentes

**📅 Progresso Atual:** Planejamento inicial - 5% completo

*Última atualização: 25/09/2026 - Fase de planejamento*
