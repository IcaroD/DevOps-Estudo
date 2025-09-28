### 1. Conexão remota
- **`ssh user@host`** → conecta-se de forma segura a outro computador/servidor via **Secure Shell**.  
  Exemplo: `ssh icaro@192.168.0.10`
- **`scp`** → copia arquivos de forma segura entre máquinas.  
  Exemplo: `scp arquivo.txt user@host:/caminho/`
- **`sftp`** → abre uma sessão de transferência de arquivos interativa (como FTP, mas via SSH).  

---

### 2. Testes básicos
- **`ping`** → testa a conectividade enviando pacotes ICMP.  
  Exemplo: `ping google.com`
- **`curl`** → faz requisições HTTP/HTTPS e mostra o conteúdo.  
  Exemplo: `curl -I https://example.com` (mostra apenas cabeçalhos).  
- **`wget`** → baixa arquivos da web.  
  Exemplo: `wget https://example.com/arquivo.zip`

---

### 3. Inspeção de rede
- **`ip addr`** → mostra interfaces de rede e seus endereços IP.  
- **`ip route`** → exibe a tabela de roteamento.  
- **`netstat -tulnp`** → lista conexões e portas abertas.  
- **`ss -tulnp`** → substituto moderno do `netstat`.  
- **`traceroute destino`** → mostra o caminho dos pacotes até o destino (saltos/roteadores).  

---

### 4. DNS
- **`dig dominio.com`** → consulta registros DNS (A, MX, etc.).  
- **`nslookup dominio.com`** → alternativa ao `dig`, mais simples.  
- **`/etc/hosts`** → arquivo local para mapear manualmente domínios a IPs.  
  - Exemplo de linha: `127.0.0.1   meuapp.local`

---

### 5. Firewall básico
- **`ufw`** (Uncomplicated Firewall) → gerencia regras de firewall de forma simples.  
  - `ufw enable` → ativa.  
  - `ufw allow 22` → libera porta 22 (SSH).  
  - `ufw status` → mostra regras ativas.  
- **`iptables`** → ferramenta mais avançada para controle de pacotes (baixo nível).  
  - Exemplo: `iptables -A INPUT -p tcp --dport 80 -j ACCEPT` (libera HTTP).
