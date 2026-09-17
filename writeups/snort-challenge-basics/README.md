# Snort Challenge  Basics 

Writeup de laboratório prático sobre criação e depuração de regras IDS com **Snort**, cobrindo detecção de tráfego HTTP/FTP, identificação de arquivos por assinatura magic bytes, correção de sintaxe de regras e uso de regras externas contra exploits reais EternalBlue/MS17-010 e Log4Shell.

**Sala:** TryHackMe: Snort Challenge: The Basics
**Ferramentas:** Snort, tcpdump, base64

---

## Objetivo do laboratório

Praticar a escrita de regras Snort do zero, entender a anatomia de uma regra ação, protocolo, direção, opções e usar Snort em modo IDS contra arquivos `.pcap` para identificar tráfego malicioso ou suspeito, desde tráfego bruto até exploração de vulnerabilidades conhecidas.

---

## 1. Comandos essenciais do Snort

| Objetivo | Comando |
|---|---|
| Rodar regras contra um PCAP, saída no console | `sudo snort -c local.rules -r arquivo.pcap -A console` |
| Rodar regras e salvar logs no diretório atual | `sudo snort -c local.rules -r arquivo.pcap -A console -l .` |
| Modo verboso dump de pacotes/cabeçalhos | `snort -r arquivo.pcap -X -v` |
| Ler um log já gerado pelo Snort | `snort -r snort.log.<timestamp> -X` |

---

## 2. Escrevendo regras  por task

### Task 2  Tráfego HTTP
Detectar todo tráfego TCP na porta 80, em qualquer direção:

```
alert tcp any any <> any 80 (msg:"HTTP Traffic Detected"; sid:1000001; rev:1;)
```

### Task 3  Tráfego e autenticação FTP
Detectar todo tráfego TCP na porta 21:

```
alert tcp any any <> any 21 (msg:"FTP Traffic"; sid:1000001; rev:1;)
```

Detectar tentativa de login falha código de resposta FTP 530:

```
alert tcp any 21 -> any any (msg:"FTP Failed Login"; content:"530"; sid:1000002; rev:1;)
```

Detectar login bem-sucedido código 230:

```
alert tcp any 21 -> any any (msg:"FTP Successful Login"; content:"230"; sid:1000003; rev:1;)
```

Detectar usuário válido aguardando senha código 331:

```
alert tcp any 21 -> any any (msg:"FTP Valid User"; content:"331"; sid:1000004; rev:1;)
```

> **Aprendizado:** os códigos de resposta do protocolo FTP 230, 331, 530 aparecem em texto claro no payload, então dá pra usar `content` para identificar o estado exato da tentativa de autenticação  sem isso, o analista só veria "houve tráfego FTP", não *o que aconteceu* na conexão.

### Task 4 Identificação de arquivos por assinatura magic bytes
Arquivos têm uma assinatura binária fixa nos primeiros bytes, independente do nome ou extensão  é isso que a regra procura.

Detectar arquivo PNG:

```
alert tcp any any -> any any (msg:"PNG File Detected"; content:"|89 50 4E 47 0D 0A 1A 0A|"; sid:1000001; rev:1;)
```

Detectar arquivo GIF:

```
alert tcp any any -> any any (msg:"GIF File Detected"; content:"GIF89a"; sid:1000002; rev:1;)
```

### Task 5 Torrent Metafile
Detectar arquivo `.torrent` pelo tipo MIME transmitido:

```
alert tcp any any -> any any (msg:"Torrent Metafile Detected"; content:"application/x-bittorrent"; sid:1000001; rev:1;)
```

### Task 6  Depurando erros de sintaxe
Comando usado para validar as regras contra um PCAP de teste:

```
sudo snort -c local-X.rules -r mx-1.pcap -A console
```

Erros mais comuns encontrados e corrigidos:
- Falta de `;` no final de opções (`msg`, `sid`, `content`)
- Strings de `content` sem aspas
- Direção da regra incompatível (`->` vs `<>`)
- Valores de `sid` duplicados entre regras

### Task 7  Regras externas: EternalBlue/MS17-010 SMB
Execução com conjunto de regras externas:

```
sudo snort -c local.rules -r ms-17-010.pcap -A console
```

Regra para detectar tentativa de acesso ao compartilhamento administrativo `IPC$`:

```
alert tcp any any -> any any (msg:"SMB IPC$ Share Access"; content:"\IPC$"; sid:1000001; rev:1;)
```

### Task 8  Regras externas: Log4Shell
Detecção por tamanho de payload, já que o exploit tem uma faixa de tamanho característica:

```
alert tcp any any -> any any (msg:"Log4j Payload Size Match"; dsize:770<>855; sid:1000001; rev:1;)
```

---

## 3. Utilitários auxiliares de investigação

Cruzar Snort com `tcpdump` ajuda a confirmar manualmente o que a regra encontrou:

```bash
# Procura por strings específicas no PCAP e mostra contexto (cabeçalho IP acima)
tcpdump -nn -vvv -r log4j.pcap | grep -B 10 "Base64"

# Filtra tráfego de um IP específico
tcpdump -vv -r log4j.pcap 'host 45.155.205.233'
```

Decodificação de payload malicioso capturado em Base64:

```bash
echo "<STRING_BASE64_AQUI>" | base64 -d
```

---

## Principais aprendizados

- Anatomia de uma regra Snort: `ação | protocolo | IP/porta origem | direção | IP/porta destino (opções)`.
- Diferença entre detectar **tráfego de um protocolo** e detectar **um evento específico dentro do protocolo** 
- Identificação de arquivos por **magic bytes**, útil quando extensão/nome não são confiáveis.
- Regras podem ser usadas tanto para tráfego genérico quanto para **exploração ativa de vulnerabilidades conhecidas** EternalBlue, Log4Shell, cruzando `content` e `dsize`.
- Fluxo de troubleshooting de regras: validar sintaxe → testar contra PCAP → cruzar com `tcpdump` pra confirmar manualmente.

---

