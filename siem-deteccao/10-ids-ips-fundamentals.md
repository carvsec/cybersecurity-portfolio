# IDS & IPS Fundamentals

**Data:** 10/08/2026 | **Categoria:** Security Solutions

## O que aprendi

**IDS vs. IPS:** O sistema de detecção de intrusão atua de forma passiva, identificando e gerando alertas sobre ameaças. O sistema de prevenção de intrusão atua de forma ativa, realizando o bloqueio das conexões em tempo real.

**Métodos de Detecção:** A detecção baseada em assinatura é rápida para ameaças conhecidas, mas ineficaz contra ataques de dia zero. A detecção por anomalia identifica novos padrões e ataques inéditos, porém apresenta maior índice de falsos positivos. O método híbrido combina ambas as abordagens.

**Modelos de Implantação:** Pode ser instalado no formato de host, monitorando um dispositivo específico, ou no formato de rede, cobrindo o tráfego completo com visão centralizada.

## Prática

Executei o Snort em modo de detecção de rede para capturar tráfego do protocolo ICMP na interface de loopback:

```bash
sudo snort -q -l /var/log/snort -i lo -A alert_fast -c /etc/snort/snort.lua
```

**Resultado:** a regra foi validada com sucesso após a geração do alerta de ping em loopback no arquivo de log.

Também utilizei o Snort para realizar a análise forense de um arquivo de captura de rede:

```bash
sudo snort -q -l /var/log/snort -r Task.pcap -A alert_fast -c /etc/snort/snort.lua
```

**Resultado:** a ferramenta inspecionou os pacotes históricos registrados no arquivo pcap e aplicou as regras de detecção pré-configuradas.

**Referência:** [tryhackme.com/room/idsfundamentals](https://tryhackme.com/room/idsfundamentals)
