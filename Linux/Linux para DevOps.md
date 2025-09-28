# Roteiro de Linux para DevOps

## 1. [[Fundamentos do Linux]]
- Navegação: `ls`, `cd`, `pwd`
- Manipulação de arquivos: `touch`, `rm`, `mv`, `cp`, `cat`, `less`, `head`, `tail`, `grep`

---

## 2. [[Shell Scripting]]
- Criar scripts em `bash`
- Variáveis: `VAR=value`, `$VAR`
- Estruturas de controle: `if`, `for`, `while`, `case`
- Entrada/saída: `read`, `echo`
- Redirecionamentos: `>`, `>>`, `<`, `|`
- Automação de tarefas (backup, limpeza de logs, deploy simples)

---

## 3. [[Gerenciamento do sistema]]
- Pacotes: `apt`, `yum`, `dnf`, `snap`
- Processos: `ps`, `top`, `htop`, `kill`, `killall`
- Serviços: `systemctl`, `service`
- Monitoramento: `df -h`, `du -sh`, `free -h`, `uptime`
- Logs: `journalctl`, diretório `/var/log/`

---

## 4. [[Rede e Conectividade]]
- Conexão remota: `ssh user@host`, `scp`, `sftp`
- Testes básicos: `ping`, `curl`, `wget`
- Inspeção de rede: `ip addr`, `ip route`, `netstat`, `ss`, `traceroute`
- DNS: `dig`, `nslookup`, edição de `/etc/hosts`
- Firewall básico: `ufw`, noções de `iptables`

---

## 5. [[Gerenciamento de Usuários e Segurança]]
- Usuários: `useradd`, `userdel`, `passwd`
- Grupos: `groupadd`, `usermod -aG`
- Permissões: `chmod`, `chown`, `umask`
- Acesso root: `sudo`, `/etc/sudoers`
- Chaves SSH: `ssh-keygen`, `ssh-copy-id`
- Segurança básica: restringir login root via SSH, boas práticas de senha