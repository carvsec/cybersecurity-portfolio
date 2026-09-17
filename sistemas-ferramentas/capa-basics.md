# CAPA: The Basics — TryHackMe

**Data:** 2026 | **Categoria:** Defensive Security Tooling

## O que aprendi
- **Finalidade do CAPA:** desenvolvido pela equipe FLARE e Mandiant, o CAPA identifica automaticamente as capacidades de arquivos executáveis em formatos como PE, ELF, .NET, shellcode e relatórios de sandbox. A ferramenta aplica regras que descrevem comportamentos maliciosos sem a necessidade de engenharia reversa manual.
- **Mapeamento de Ameaças:** os resultados obtidos são organizados com referências ao framework MITRE ATT&CK e ao catálogo de comportamentos de malware MBC.

## Prática
Acessei o diretório da ferramenta no terminal do PowerShell:
```powershell
cd C:\Users\Administrator\Desktop\capa
```
Executei o CAPA contra um arquivo suspeito:
```powershell
capa.exe cryptbot.bin
```
Explorei os parâmetros de linha de comando para ajustar o nível de detalhe:
```powershell
capa -h
capa -v
capa -vv
capa -j
```
Para otimizar o tempo de análise, consultei o resultado pré-processado diretamente no terminal:
```powershell
Get-Content .\cryptbot.txt
```
Resultado: identifiquei a técnica de arquivos ofuscados T1027 no MITRE ATT&CK e a sub-técnica de remoção de indicadores T1027.005. Essas técnicas confirmaram que o malware ocultava dados utilizando codificação em base64 e operação XOR.

## Referência
https://tryhackme.com/room/capabasics
