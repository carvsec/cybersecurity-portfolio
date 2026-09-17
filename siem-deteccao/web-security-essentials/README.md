---
# Web Security Essentials

**Data:** 17/09/2026 | **Categoria:** Web Security

## O que aprendi
- **OWASP Top 10:** compreensão das 10 vulnerabilidades web mais críticas incluindo injection, broken authentication, sensitive data exposure
- **Injeção SQL:** técnica onde entrada maliciosa é passada para consultas de banco de dados, permitindo acesso, modificação e exclusão de informações
- **Cross-Site Scripting (XSS):** execução de scripts maliciosos no contexto do navegador da vítima através de aplicações web vulneráveis
- **Controles de Acesso Quebrados:** vulnerabilidade que permite atacantes obter acesso não autorizado a recursos protegidos como contas de usuário, arquivos, funções administrativas
- **Prática de Exploração e Correção:** abordagem de explorar vulnerabilidades primeiro e aplicar correções depois para aprendizado completo

## Prática
Explorei vulnerabilidades OWASP Top 10, pratiquei técnicas de exploração e apliquei correções de segurança:

```bash
# Ferramentas para teste de segurança web
nmap -sV --script http-enum,http-security-headers target.com
nikto -h http://target.com -output nikto_scan.txt
dirb http://target.com /usr/share/wordlists/dirb/common.txt

# Teste de injeção SQL básica
sqlmap -u "http://target.com/page.php?id=1" --dbs
sqlmap -u "http://target.com/login.php" --data="username=admin&password=test" --level=3

# Detecção de XSS
xsstrike -u "http://target.com/search?q=test"
dalfox url http://target.com/search?q=test

# Análise de headers de segurança
curl -I http://target.com | grep -i "security\|x-"
testssl.sh target.com

# Teste de autenticação e sessão
burpsuite
zaproxy
hydra -l admin -P rockyou.txt http-get://target.com/login

# Verificação de configurações
whatweb target.com
wafw00f http://target.com
```

Resultado: os comandos permitiram identificar vulnerabilidades como injeção SQL em parâmetros de URL, detectar falta de headers de segurança como Content-Security-Policy, testar controles de acesso em páginas protegidas, e analisar configurações de servidor web para misconfigurações comuns.

## Referência
https://tryhackme.com/room/websecurityessentials