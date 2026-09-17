# REMnux: Getting Started — TryHackMe

**Data:** 2026 | **Categoria:** Defensive Security Tooling

## O que aprendi
- **Visão Geral:** o REMnux é uma distribuição Linux voltada para análise de malware, que reúne ferramentas como Volatility 3, YARA, Wireshark, oledump e INetSim.
- **Ambiente Seguro:** oferece um ambiente isolado para analisar softwares maliciosos sem expor a rede principal, sendo fundamental em investigações de incidentes.
- **Frentes de Atuação:** a prática cobriu a análise estática de documentos do Office, a simulação de serviços de rede para observar conexões externas e a análise de memória RAM em sistemas infectados.

## Prática

**Análise de documento Office com oledump:**
Listei e extraí os dados de um arquivo malicioso:
```bash
oledump.py -h
oledump.py agenttesla.xlsm
oledump.py -s 3 -v agenttesla.xlsm
```
Resultado: identifiquei os streams marcados com a letra M, que indicam a presença de código VBA, e extraí a macro maliciosa contida no arquivo.

**Simulação de rede com INetSim:**
Ajustei a configuração do INetSim para redirecionar o tráfego DNS para o endereço IP da máquina de análise e iniciei o serviço:
```bash
sudo nano /etc/inetsim/inetsim.conf
sudo inetsim
```
Em um segundo ambiente, simulei o download de um arquivo malicioso direcionado ao serviço fake:
```bash
sudo wget https://192.168.1.50/second_payload.zip --no-check-certificate
```
Após interromper a execução, analisei o relatório do simulador para identificar o método HTTP utilizado pela ameaça na requisição do arquivo.

**Análise de memória com Volatility 3:**
Executei plugins no dump de memória para mapear a estrutura do sistema:
```bash
vol3 -h
vol3 -f wcry.mem windows.pstree.PsTree
vol3 -f wcry.mem windows.pslist.PsList
vol3 -f wcry.mem windows.dlllist.DllList | grep "@WanaDecryptor@.exe"
vol3 -f wcry.mem windows.malfind.Malfind
```
Resultado: a análise em árvore de processos permitiu identificar o executável do WannaCry e localizar injeções de código em memória. Também utilizei o utilitário de strings com codificação de 16 bits em formato little-endian e big-endian para extrair textos legíveis do binário:
```bash
strings -e l arquivo_suspeito
strings -e b arquivo_suspeito
```

## Referência
https://tryhackme.com/room/remnuxgettingstarted
