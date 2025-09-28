### 1. Pacotes

Gerenciar software e atualizações com diferentes gerenciadores de pacotes:

| Gerenciador | Distribuição      | Comandos comuns                                                                                                                          |
| ----------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `apt`       | Debian, Ubuntu    | `sudo apt update` → atualiza lista de pacotes <br> `sudo apt upgrade` → atualiza pacotes <br> `sudo apt install pacote` → instala pacote |
| `yum`       | CentOS 7, RHEL 7  | `sudo yum update` <br> `sudo yum install pacote`                                                                                         |
| `dnf`       | Fedora, CentOS 8+ | `sudo dnf update` <br> `sudo dnf install pacote`                                                                                         |
| `snap`      | Todas (via Snap)  | `sudo snap install pacote` <br> `sudo snap remove pacote`                                                                                |

---

### 2. Processos

Processos são **programas em execução** no sistema. Cada processo possui um **PID (Process ID)** e consome recursos (CPU, memória). Gerenciar processos é essencial para manter o servidor estável.

- **`ps`** – lista processos:
```bash
ps aux          # lista todos os processos com detalhes
ps -ef          # outra forma de listar todos os processos
```
- **`top`** – monitora processos em tempo real:
```bash
top             # mostra CPU, memória, uso de swap e lista de processos ativos
```
- **`htop`** – versão interativa e colorida do top (mais fácil de visualizar e filtrar):
```bash
htop
```
	Use as setas para navegar e F9 para finalizar processos.
- **`kill`** – finaliza processos pelo PID:
```bash
kill 1234       # envia sinal padrão (TERM) para o processo 1234
kill -9 1234    # força encerramento imediato (KILL)
```
- **`killall`** – finaliza processos pelo nome:
```bash
killall nginx   # encerra todos os processos chamados nginx
```

---

### 3. Serviços

Serviços são **programas que rodam em segundo plano** (daemons). Eles iniciam no boot ou manualmente e oferecem funcionalidades contínuas (ex.: web server, banco de dados).

- **`systemctl`** – sistemas modernos com systemd:
```bash
sudo systemctl start nginx      # iniciar serviço
sudo systemctl stop nginx       # parar serviço
sudo systemctl restart nginx    # reiniciar serviço
sudo systemctl status nginx     # verificar status
sudo systemctl enable nginx     # habilitar inicialização automática
sudo systemctl disable nginx    # desabilitar inicialização automática
```
- **`service`** – sistemas antigos ou compatibilidade:
```bash
sudo service nome_servico start
sudo service nome_servico stop
sudo service nome_servico restart
sudo service nome_servico status
```

---

### 4 Monitoramento do sistema

Verificar **uso de disco, memória, CPU e tempo de atividade**:

| Comando                 | Função                                                    |
| ----------------------- | --------------------------------------------------------- |
| `df -h`                 | Mostra uso do disco em formato legível (GB, MB)           |
| `du -sh pasta/`         | Mostra tamanho de um diretório específico                 |
| `free -h`               | Mostra uso de memória (RAM e swap)                        |
| `uptime`                | Mostra tempo de atividade do sistema e carga média da CPU |

- **Cron jobs**: automatizam tarefas recorrentes
```bash
crontab -e       # editar tarefas do usuário
crontab -l       # listar tarefas
```
- Exemplo: rodar script todo dia às 3h:
```bash
0 3 * * * /home/usuario/backup.sh
```

---

### 5. Logs: `journalctl` e `/var/log/`

- **`journalctl`**
  - Comando para visualizar os logs do **systemd**.
  - Exemplos:
    - `journalctl -xe` → mostra os últimos logs em detalhes (com erros).
    - `journalctl -f` → segue os logs em tempo real (similar ao `tail -f`).
    - `journalctl -u nginx` → mostra logs de um serviço específico (ex.: `nginx`).
    - `journalctl --since "2025-09-25 10:00"` → logs a partir de um horário específico.
    - `journalctl --since yesterday` → logs do último dia.

- **Diretório `/var/log/`**
  - Pasta onde ficam a maioria dos logs tradicionais do Linux.
  - Arquivos importantes:
    - `/var/log/syslog` ou `/var/log/messages` → logs gerais do sistema.
    - `/var/log/auth.log` → tentativas de login e autenticação.
    - `/var/log/dmesg` → mensagens do kernel (útil para drivers/hardware).
    - `/var/log/nginx/` ou `/var/log/apache2/` → logs de servidores web.
    - `/var/log/apt/` → histórico de instalações/atualizações de pacotes.
  - Para acompanhar em tempo real:
    - `tail -f /var/log/syslog`
    - `less /var/log/auth.log`