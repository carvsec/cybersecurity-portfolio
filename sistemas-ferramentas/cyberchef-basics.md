# CyberChef: The Basics — TryHackMe

**Data:** 2026 | **Categoria:** Defensive Security Tooling

## O que aprendi
- **Conceito:** desenvolvido pelo GCHQ, o CyberChef funciona como um utilitário web para manipulação e decodificação de dados diretamente no navegador.
- **Estrutura da Interface:** a plataforma é dividida em quatro áreas centrais: Operations, com o catálogo de funções; Recipe, onde as operações são encadeadas; Input, para inserção dos dados brutos; e Output, que exibe o resultado final após a execução.
- **Capacidades:** permite realizar desde conversões simples em Base64, XOR e código Morse até operações complexas de criptografia em AES e decriptação em RSA.

## Prática

**URL Decode:** decodifiquei uma URL codificada para obter o endereço em texto limpo.
```
Entrada: https%3A%2F%2Ftryhackme.com%2Fr%2Froom%2Fcyberchefbasics
Receita: URL Decode
Saída: https://tryhackme.com/r/room/cyberchefbasics
```

**From UNIX Timestamp:** converti um valor de timestamp Unix para o formato de data legível.
```
Entrada: 1725151258
Receita: From UNIX Timestamp
Saída: Data e hora convertidas
```

**From Base85:** decodifiquei uma cadeia de texto em codificação Base85.
```
Entrada: <+oue+DGm>Ap%u7
Receita: From Base85
Saída: Texto original decodificado
```

Resultado: também utilizei os extratores da plataforma para isolar endereços IP, URLs e e-mails contidos em um arquivo de log, identificando um endereço IP específico na análise.

## Referência
https://tryhackme.com/room/cyberchefbasics
