### 1 Pacotes

Gerenciar software e atualizações com diferentes gerenciadores de pacotes:

| Gerenciador | Distribuição      | Comandos comuns                                                                                                                          |
| ----------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `apt`       | Debian, Ubuntu    | `sudo apt update` → atualiza lista de pacotes <br> `sudo apt upgrade` → atualiza pacotes <br> `sudo apt install pacote` → instala pacote |
| `yum`       | CentOS 7, RHEL 7  | `sudo yum update` <br> `sudo yum install pacote`                                                                                         |
| `dnf`       | Fedora, CentOS 8+ | `sudo dnf update` <br> `sudo dnf install pacote`                                                                                         |
| `snap`      | Todas (via Snap)  | `sudo snap install pacote` <br> `sudo snap remove pacote`                                                                                |

---

## Processos

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


