# Homelab Wazuh SIEM - Ambiente SOC

Status: Em desenvolvimento  
Última atualização: Setembro 2026  
Autor: Pedro Carvalho  
LinkedIn: https://www.linkedin.com/in/pedroalvesc/

## Objetivo do Projeto

Criar um ambiente completo de Centro de Operações de Segurança utilizando SIEM open-source Wazuh para monitoramento, detecção e resposta a incidentes. Este projeto serve como laboratório prático para desenvolvimento de habilidades em Segurança Defensiva e funciona como portfólio técnico.

### Objetivos de Aprendizado
Implementar e configurar SIEM de nível empresarial usando Wazuh
Monitorar sistemas heterogêneos incluindo Windows e Linux
Desenvolver regras personalizadas para detecção de ameaças
Simular ataques reais e analisar detecções
Criar dashboards e relatórios de segurança
Documentar processos para portfólio técnico

## Arquitetura do Ambiente

Internet
    |
Firewall com UFW
    |
Servidor Wazuh           Estações de Trabalho
Ubuntu 22.04 LTS       Sistemas Monitorados
    |                       |
Elastic Stack           Windows 10
Gerenciador Wazuh           Sysmon
Indexer Wazuh               Agente Wazuh
Dashboard Wazuh             Aplicações de Teste
                        |
                        Ubuntu 22.04
                            Agente Wazuh
                            Serviços Comuns
                            Logs do Sistema
                        |
                        Metasploitable 3
                            Vulnerabilidades
                            Agente Wazuh
                            Serviços Vulneráveis

## Roteiro do Projeto

### Fase 1: Planejamento e Instalação, Outubro 2026
Duração: 2 semanas
Tarefas
Definir objetivos e escopo
Planejar arquitetura técnica
Documentar requisitos de hardware/software
Criar checklist de instalação
Configurar ambiente de virtualização

Entregáveis
Documentação de planejamento completa
Diagrama de arquitetura
Checklist de instalação

### Fase 2: Instalação e Configuração Básica, Novembro 2026
Duração: 3 semanas
Tarefas
Instalar Wazuh Server no Ubuntu
Configurar Gerenciador e Indexer Wazuh
Instalar Dashboard Wazuh com Kibana
Configurar acesso e autenticação
Testar instalação básica

Entregáveis
Servidor Wazuh funcional
Dashboard acessível
Documentação de instalação

### Fase 3: Integração de Agentes, Dezembro 2026
Duração: 3 semanas
Tarefas
Instalar agente Wazuh no Windows 10
Configurar Sysmon no Windows
Instalar agente Wazuh no Ubuntu
Configurar logs do sistema Linux
Testar comunicação agente-servidor

Entregáveis
2+ sistemas monitorados
Coleta de logs ativa
Dashboard com dados reais

### Fase 4: Regras e Detecção, Janeiro 2027
Duração: 4 semanas
Tarefas
Configurar regras padrão do Wazuh
Desenvolver regras personalizadas
Criar alertas e notificações
Desenvolver dashboards no Kibana
Otimizar configurações

Entregáveis
Regras personalizadas funcionando
Dashboards informativos
Sistema de alertas configurado

### Fase 5: Simulação e Análise, Fevereiro 2027
Duração: 3 semanas
Tarefas
Simular ataques básicos
Analisar detecções geradas
Criar relatórios de incidentes
Ajustar regras baseado em resultados
Otimizar performance

Entregáveis
Relatórios de simulação
Análises de detecção
Regras otimizadas

### Fase 6: Documentação Final, Março 2027
Duração: 2 semanas
Tarefas
Completar toda documentação
Criar guias passo a passo
Desenvolver tutoriais específicos
Documentar lições aprendidas
Preparar apresentação do projeto

Entregáveis
Documentação completa
Guias e tutoriais
Apresentação do projeto

## Tecnologias Utilizadas

### Sistemas Operacionais
- Servidor Wazuh: Ubuntu 22.04 LTS
- Cliente Windows: Windows 10 ou 11 Pro
- Cliente Linux: Ubuntu 22.04 LTS
- Alvo: Metasploitable 3

### Ferramentas de Segurança
- SIEM: Wazuh 4.7 ou superior
- Monitoramento de Endpoint: Agente Wazuh, Sysmon
- Visualização: Kibana com Dashboard Wazuh
- Gerenciamento de Logs: Elastic Stack

### Virtualização
- Proxmox VE, VirtualBox, ou VMware
- Vagrant para automação opcional

### Documentação
- Markdown para documentação
- PlantUML para diagramas
- Screenshots e gravações

## Estrutura do Repositório

wazuh-homelab
    README.md
    arquitetura
        diagrama-rede.puml
        requisitos-sistema.md
        checklist-instalacao.md
    instalacao
        wazuh-server
        windows-agent
        linux-agent
        config-sysmon
    configuracao
        wazuh
        regras
        alertas
        dashboards
    simulacao
        cenarios-ataque
        analise-deteccao
        relatorios-incidente
    documentacao
        guias
        tutoriais
        lições-aprendidas
    scripts
        setup
        monitoramento
        analise

## Começando

### Pré-requisitos
1. Hardware
   - CPU: 4 ou mais núcleos, 8 recomendados
   - RAM: 16GB ou mais, 32GB recomendado
   - Armazenamento: 100GB ou mais SSD
   - Virtualização habilitada

2. Software
   - Virtualizador como Proxmox, VirtualBox ou VMware
   - ISO Ubuntu 22.04
   - ISO Windows 10
   - OVA Metasploitable 3

3. Conhecimento
   - Terminal Linux básico, pacotes, serviços
   - Redes básicas incluindo IP, subnets, firewall
   - Conceitos básicos de segurança

### Guia Rápido de Instalação
1. Instalar Ubuntu Server
2. Instalar Wazuh usando script oficial
   curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
   sudo bash wazuh-install.sh --generate-config-files
3. Instalar agentes em sistemas monitorados
   Windows: Executar instalador .msi
   Linux: curl mais apt install

## Métricas do Projeto

| Métrica | Valor Alvo | Como Medir |
|---------|------------|------------|
| Sistemas Monitorados | 3 ou mais | Agentes conectados no dashboard |
| Regras Personalizadas | 10 ou mais | Regras ativas no Wazuh |
| Tempo de Instalação | Menos de 8 horas | Primeiro commit ao sistema funcional |
| Detecção de Ataques Simulados | 80% ou mais | Ataques detectados versus simulados |
| Tempo de Resposta | Menos de 30 minutos | Detecção à análise inicial |

## Casos de Uso Implementados

### 1. Detecção de Força Bruta SSH
- Regras para múltiplas tentativas de login SSH
- Alertas após 5 tentativas falhas em 5 minutos
- Bloqueio automático via integração com firewall

### 2. Monitoramento de Processos Maliciosos
- Detecção de executáveis suspeitos no Windows
- Monitoramento de criação de processos
- Alertas para processos maliciosos conhecidos

### 3. Análise de Logs Windows
- Monitoramento de Event IDs críticos
- Detecção de mudanças no registro
- Alertas para atividades suspeitas de usuário

### 4. Monitoramento de Integridade de Arquivos
- FIM em diretórios críticos
- Detecção de mudanças não autorizadas
- Linha de base de integridade do sistema

## Resultados Esperados

### Técnicos
1. Ambiente SOC funcional com monitoramento em tempo real
2. Dashboard com visibilidade completa do ambiente
3. Regras de detecção cobrindo ataques comuns
4. Processo de resposta a incidentes documentado

### Profissionais
1. Portfólio técnico demonstrável para recrutadores
2. Experiência prática com SIEM de nível empresarial
3. Habilidades de análise de logs e detecção de ameaças
4. Documentação demonstrando capacidade técnica

## Contribuição

Este é um projeto de aprendizado pessoal, mas sugestões são bem-vindas. Se você
- Encontrou erros na documentação
- Tem sugestões de melhorias
- Conhece ferramentas ou tecnologias que poderiam ser adicionadas

Por favor, abra uma issue ou contate via LinkedIn.

## Recursos Úteis

### Documentação Oficial
- Documentação Wazuh: https://documentation.wazuh.com/
- Guia Elasticsearch: https://www.elastic.co/guide/
- Guia do Usuário Kibana: https://www.elastic.co/guide/kibana/

### Tutoriais e Guias
- Guia de Instalação Wazuh: https://documentation.wazuh.com/current/installation-guide/
- Configuração Sysmon: https://github.com/SwiftOnSecurity/sysmon-config
- Framework MITRE ATT&CK: https://attack.mitre.org/

### Comunidades
- Discord Wazuh: https://discord.gg/wazuh
- Reddit r/Wazuh: https://www.reddit.com/r/Wazuh/
- Stack Overflow Tag Wazuh: https://stackoverflow.com/questions/tagged/wazuh

## Licença

Este projeto é para fins educacionais e de portfólio. Todo conteúdo é fornecido sob licença MIT.

## Próximos Passos
1. Configurar ambiente de virtualização
2. Instalar Wazuh Server
3. Documentar processo de instalação
4. Começar configuração de agentes

Progresso Atual: Planejamento inicial, 5% completo

Última atualização: Setembro 2026 - Fase de planejamento