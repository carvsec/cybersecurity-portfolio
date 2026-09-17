# Logs Fundamentals & Centralization — TryHackMe

**Data:** 09/08/2026 | **Categoria:** Defensive Security

## O que aprendi
- **Importância dos Logs:** os logs constituem a matéria-prima essencial de qualquer investigação em um centro de operações de segurança.
- **Centralização de Eventos:** sem a centralização de logs, torna-se inviável comprovar incidentes e correlacionar eventos vindos de fontes distintas.

## Prática
Examinei diretórios reais de logs no sistema Linux e executei comandos para filtrar eventos de autenticação e monitorar o sistema em tempo real:
```bash
cat /var/log/auth.log | grep "Failed password"
tail -f /var/log/syslog
```
Resultado: o comando permitiu isolar tentativas incorretas de login no arquivo de autenticação. Além disso, analisei logs de eventos do Windows e logs de acesso de servidores web para identificar padrões suspeitos de tentativas de acesso.

## Referência
https://tryhackme.com/room/logsfundamentals
