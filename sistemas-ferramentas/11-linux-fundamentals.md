# Linux Fundamentals

**Data:** 10/07/2026 | **Categoria:** Linux Basics

## O que aprendi

**Navegação e Manipulação:** Dominei a navegação no sistema de arquivos com os comandos `pwd`, `ls` e `cd`, além da leitura e inspeção de conteúdo com `cat`, `head` e `tail`.

**Permissões e Elevação:** Estudei a estrutura de permissões de leitura, escrita e execução, além da elevação de privilégios com o utilitário `sudo`.

**Gestão de Sistema:** Compreendi o gerenciamento de processos com `ps` e `top`, controle de serviços com `systemctl`, monitoramento de espaço em disco e memória com `df` e `free`, e automação de tarefas com o `cron`.

## Prática

Identifiquei o usuário ativo, listei os arquivos do diretório em detalhes e consultei a lista de contas do sistema:

```bash
whoami
ls -la
cat /etc/passwd
```

**Resultado:** os comandos confirmaram a identidade do usuário logado, exibiram arquivos ocultos e permissões, e mapearam as contas registradas no sistema.

Executei buscas por arquivos confidenciais e inspeção de logs restritos:

```bash
find / -name flag.txt 2>/dev/null
grep -r "password" /var/log/
sudo cat /etc/shadow
```

**Resultado:** a busca localizou o arquivo contendo a chave, o filtro identificou termos sensíveis nos logs e a leitura com privilégios exibiu os hashes das senhas cadastradas.

Gerenciei serviços ativos, verifiquei o espaço de armazenamento e consultei o agendador de tarefas:

```bash
ps aux | grep apache2
systemctl status ssh
df -h
crontab -l
```

**Resultado:** verifiquei a execução do servidor web, o estado de funcionamento do serviço SSH, a capacidade das partições de disco e as tarefas agendadas no cron.

**Referência:**
[tryhackme.com/room/linuxfundamentalspart1](https://tryhackme.com/room/linuxfundamentalspart1) · [Parte 2](https://tryhackme.com/room/linuxfundamentalspart2) · [Parte 3](https://tryhackme.com/room/linuxfundamentalspart3)
