# Linux Shells

**Data:** 15/07/2026 | **Categoria:** Command Line

## O que aprendi

**Conceito de Shell:** A shell atua como a interface que interpreta os comandos inseridos no terminal e os envia ao sistema operacional.

**Tipos de Interpretadores:** Existem variações como Bash, Zsh e Sh, sendo o Bash o padrão na maioria das distribuições Linux. O comando `echo` exibindo a variável `SHELL` indica o interpretador ativo na sessão.

**Filtragem de Dados:** O uso do utilitário `grep` para localizar termos dentro de arquivos extensos é uma habilidade fundamental para análise de logs.

**Automação com Scripts:** Um script em Bash deve ser iniciado com o cabeçalho shebang indicando o caminho do interpretador, salvo com extensão `.sh` e configurado com permissão de execução.

## Prática

Consultei o interpretador em uso, naveguei pelos diretórios e filtrei uma expressão específica dentro de um arquivo de texto:

```bash
echo $SHELL
pwd
ls -la
grep "THM" arquivo_grande.txt
```

**Resultado:** a consulta confirmou o uso do Bash e a busca isolou os registros contendo o padrão pesquisado.

Desenvolvi um script em Bash para autenticação de usuário e validação de PIN:

```bash
#!/bin/bash
echo "Enter your Username: "
read username
echo "Enter your Company name: "
read company
echo "Enter your PIN: "
read pin

if [ "$pin" == "1234" ]; then
  echo "Access Granted!"
else
  echo "Authentication Denied!!"
fi
```

Concedi permissão de execução ao arquivo e executei o script no terminal:

```bash
chmod +x locker_script.sh
./locker_script.sh
```

**Resultado:** o script solicitou as entradas de dados, comparou o valor digitado com a regra condicional e exibiu a mensagem de acesso liberado.

**Referência:** [tryhackme.com/room/linuxshells](https://tryhackme.com/room/linuxshells)
