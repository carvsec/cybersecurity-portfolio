# FlareVM: Arsenal of Tools

**Data:** 2026 | **Categoria:** Defensive Security Tooling

## O que aprendi

**Visão Geral:** O FlareVM é uma máquina virtual Windows desenvolvida pela equipe FLARE para reunir ferramentas de engenharia reversa, análise de malware e perícia forense em um único ambiente isolado.

**Uso Operacional:** A plataforma é utilizada em laboratórios de malware, centros de operações de segurança e resposta a incidentes para investigar arquivos suspeitos com segurança, sem comprometer o sistema principal.

**Ferramentas Gráficas:** A análise estática de arquivos no formato PE conta com o PEStudio e o CFF Explorer. Para depuração de binários em 32 e 64 bits, é utilizado o x64dbg. A inspeção de memória e processos é realizada pelo Process Hacker, Process Explorer e Procmon. Para análise hexadecimal e aquisição de imagem de disco, utilizam-se o HxD e o FTK Imager.

**Ferramenta em Linha de Comando:** O utilitário FLOSS é empregado para extrair e desofuscar cadeias de texto de programas maliciosos.

## Prática

Acessei a pasta do laboratório pelo terminal do PowerShell:

```powershell
cd C:\Users\Administrator\Desktop\Sample
```

Executei a ferramenta FLOSS contra o arquivo executável suspeito e redirecionei a saída para um arquivo de texto:

```powershell
FLOSS.exe .\windows.exe > windows.txt
```

Em seguida, utilizei o conjunto de ferramentas gráficas para aprofundar a investigação:

- **PEStudio:** Importei o binário para extrair o hash SHA256 e analisar a contagem de funções.
- **CFF Explorer:** Gerador do hash MD5 e inspetor das propriedades do cabeçalho DOS.
- **Process Explorer:** Mapeamento da hierarquia entre processos pai e filho em execução no sistema.

**Referência:** [tryhackme.com/room/flarevmarsenaloftools](https://tryhackme.com/room/flarevmarsenaloftools)
