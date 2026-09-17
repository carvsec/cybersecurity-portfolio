---
# Detecting Web DDoS

**Data:** 17/09/2026 | **Categoria:** DDoS Protection

## O que aprendi
- **Ataques DDoS na Camada de Aplicação:** técnicas onde múltiplos bots (botnet) inundam website ou serviço com requisições HTTP e tráfego para sobrecarregar recursos
- **Objetivo Primário DDoS:** desligar ou bloquear acesso a sistema através de sobrecarga de recursos de rede com tráfego de múltiplas fontes
- **Detecção Rápida e Precisa:** processo contínuo de monitoramento de telemetria de rede, identificação de anomalias que correspondem a assinaturas de ataque
- **Desafios de Detecção:** dificuldade de distinguir tráfego legítimo de ataque quando distribuído em centenas/milhares de fontes de origem
- **Mitigação Proativa:** redução de superfície de ataque, monitoramento de ameaças e ferramentas escaláveis de mitigação DDoS

## Prática
Analisei padrões de ataques DDoS, detectei anomalias em logs e implementei técnicas de mitigação:

```bash
# Detecção de DDoS em logs de acesso web
awk '{print $1}' /var/log/nginx/access.log | sort | uniq -c | sort -nr | head -20
tail -f /var/log/apache2/access.log | awk '{print $1}' | sort | uniq -c | sort -nr

# Identificação de SYN floods em capturas de pacotes
tshark -r attack.pcap -Y "tcp.flags.syn == 1 and tcp.flags.ack == 0" | wc -l
tcpdump -nn 'tcp[13] & 2 != 0' -c 1000 | awk '{print $3}' | cut -d. -f1-4 | sort | uniq -c

# Monitoramento de taxa de requisições
netstat -ntu | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -n
iftop -i eth0 -f 'port 80 or port 443'
vnstat -l -i eth0

# Configuração de limites de taxa no Nginx
# Adicionar ao nginx.conf:
# limit_req_zone $binary_remote_addr zone=one:10m rate=10r/s;
# limit_req zone=one burst=20 nodelay;

# Configuração de limites no Apache
# ModSecurity rules para rate limiting
SecAction "id:9001,phase:1,nolog,pass,initcol:ip=%{REMOTE_ADDR},col:rate=1/60"
SecRule IP:rate "@gt 100" "id:9002,phase:1,deny,status:429,msg:'Rate limit exceeded'"

# Ferramentas especializadas de detecção DDoS
ddosify -t http://target.com -n 1000 -d 60
slowhttptest -c 1000 -H -i 10 -r 200 -t GET -u http://target.com -x 24 -p 3

# Análise de tráfego anormal
tshark -i eth0 -Y "http.request" -T fields -e http.host -e http.request.uri | sort | uniq -c | sort -nr
tcpdump -nn -i eth0 'port 80' -c 1000 | awk '{print $3}' | cut -d. -f1-4 | sort | uniq -c | sort -nr

# Mitigação com iptables
iptables -A INPUT -p tcp --dport 80 -m limit --limit 100/min --limit-burst 200 -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -j DROP
iptables -A INPUT -p tcp --syn -m limit --limit 10/s --limit-burst 20 -j ACCEPT
```

Resultado: os comandos permitiram identificar IPs fazendo milhares de requisições por segundo (SYN floods), monitorar taxa de tráfego HTTP em tempo real, configurar limites de taxa no Nginx/Apache para prevenir sobrecarga, analisar padrões de tráfego anormal com ferramentas especializadas, e implementar regras iptables para mitigação básica de ataques DDoS na camada de rede.

## Referência
https://tryhackme.com/room/detectingwebddos