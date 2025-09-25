# Roteiro de Linux para DevOps

## 1. [[Fundamentos do Linux]]
- Navegação: `ls`, `cd`, `pwd`
- Manipulação de arquivos: `touch`, `rm`, `mv`, `cp`, `cat`, `less`, `head`, `tail`

---

## 2. [[Gerenciamento do sistema]]
- Pacotes: `apt`, `yum`, `dnf`, `snap`
- Processos: `ps`, `top`, `htop`, `kill`, `killall`
- Serviços: `systemctl`, `service`
- Monitoramento: `df -h`, `du -sh`, `free -h`, `uptime`
- Logs: `journalctl`, diretório `/var/log/`

---

## 3. [[Shell Scripting]]
- Criar scripts em `bash`
- Variáveis: `VAR=value`, `$VAR`
- Estruturas de controle: `if`, `for`, `while`, `case`
- Entrada/saída: `read`, `echo`
- Redirecionamentos: `>`, `>>`, `<`, `|`
- Automação de tarefas (backup, limpeza de logs, deploy simples)

---

## 4. [[Rede e Conectividade]]
- Conexão remota: `ssh user@host`, `scp`, `sftp`
- Testes básicos: `ping`, `curl`, `wget`
- Inspeção de rede: `ip addr`, `ip route`, `netstat`, `ss`, `traceroute`
- DNS: `dig`, `nslookup`, edição de `/etc/hosts`
- Firewall básico: `ufw`, noções de `iptables`

---

## 5. [[Gerenciamento de Serviços e Processos]]
- Iniciar/parar/reiniciar: `systemctl start|stop|restart serviço`
- Habilitar no boot: `systemctl enable serviço`
- Ver status: `systemctl status serviço`
- Processos ativos: `ps aux`, `pgrep`, `htop`
- Encerrar processos: `kill -9 PID`

---

## 6. [[Gerenciamento de Usuários e Segurança]]
- Usuários: `useradd`, `userdel`, `passwd`
- Grupos: `groupadd`, `usermod -aG`
- Permissões: `chmod`, `chown`, `umask`
- Acesso root: `sudo`, `/etc/sudoers`
- Chaves SSH: `ssh-keygen`, `ssh-copy-id`
- Segurança básica: restringir login root via SSH, boas práticas de senha

---

## 7. [[Armazenamento e Filesystem]]
- Discos e partições: `lsblk`, `fdisk -l`
- Montagem: `mount`, `umount`, `/etc/fstab`
- Espaço em disco: `df -h`, `du -sh`
- Links: `ln` (hardlink), `ln -s` (symlink)
- Permissões no filesystem: leitura/escrita/execução para `user/group/others`