
### 1. Usuários

- **`useradd nomeusuario`** → cria um novo usuário.  
  Exemplo: `sudo useradd usuario`

- **`passwd nomeusuario`** → define ou altera a senha de um usuário.  
  Exemplo: `sudo passwd usuario`

- **`userdel nomeusuario`** → remove um usuário (pode ser usado com `-r` para remover também o diretório home).  
  Exemplo: `sudo userdel -r usuario`

---

### 2. Grupos

- **`groupadd nomegrupo`** → cria um novo grupo.  
  Exemplo: `sudo groupadd devs`

- **`usermod -aG grupo usuario`** → adiciona o usuário a um grupo existente (`-aG` = append to Group).  
  Exemplo: `sudo usermod -aG devs usuario`

📌 Dicas:
- Um **usuário pode pertencer a vários grupos**.  
- Para verificar os grupos de um usuário:  
```bash
  groups usuario
```
- O arquivo **`/etc/passwd`** guarda informações dos usuários.
- O arquivo **`/etc/group`** guarda informações dos grupos.

---

### 3. Permissões

Cada arquivo/diretório tem permissões para:
- **Usuário (owner)**
- **Grupo (group)**
- **Outros (others)**

Exemplo com `ls -l`:
```bash
-rwxr-xr-- 1 usuario devops 1200 set 24 10:20 script.sh
```
- `r` = leitura, `w` = escrita, `x` = execução
- `usuario` = dono do arquivo
- `devops` = grupo

Comandos úteis:
- `chmod [permissão] arquivo` → define permissões
- `chown usuario arquivo.txt` → muda o dono
- `chgrp grupo arquivo.txt` → muda o grupo
- `whoami` → mostra usuário atual
- `id` → mostra UID, GID e grupos

Permissões:

| Número | Binário | Permissões | Significado                 |
| ------ | ------- | ---------- | --------------------------- |
| 0      | 000     | ---        | Sem permissão               |
| 1      | 001     | --x        | Somente execução            |
| 2      | 010     | -w-        | Somente escrita             |
| 3      | 011     | -wx        | Escrita e execução          |
| 4      | 100     | r--        | Somente leitura             |
| 5      | 101     | r-x        | Leitura e execução          |
| 6      | 110     | rw-        | Leitura e escrita           |
| 7      | 111     | rwx        | Leitura, escrita e execução |

Exemplos práticos de `chmod`:

| Comando | Significado |
|---------|-------------|
| `chmod 755 arquivo` | Dono: rwx, Grupo: r-x, Outros: r-x |
| `chmod 644 arquivo` | Dono: rw-, Grupo: r--, Outros: r-- |
| `chmod 700 arquivo` | Dono: rwx, Grupo: --- , Outros: --- |
| `chmod 600 arquivo` | Dono: rw-, Grupo: --- , Outros: --- |
| `chmod 777 arquivo` | Todos podem ler, escrever e executar (cuidado!) |

O **`umask`** (user file-creation mode mask) define quais **permissões padrão** NÃO serão dadas a arquivos e diretórios recém-criados.

### Como funciona
- Quando você cria um **arquivo**, o sistema dá permissão base de `666` (rw-rw-rw-).  
- Quando você cria um **diretório**, o sistema dá permissão base de `777` (rwxrwxrwx).  
- O valor do `umask` é **subtraído** dessa base para definir a permissão final.

### Exemplo prático

1. Ver o valor atual:
```bash
umask
```

2. Alterar o `umask`

- Para definir temporariamente:
```bash
umask 0007
```
Isso remove permissões para "others".  
Novo diretório criado terá permissão `770` (somente dono e grupo).

- Para definir permanentemente:  
    Adicionar no `~/.bashrc` ou `/etc/profile`:
```bash
umask 0022
```

---
### 4. Segurança e Acesso

### Acesso root
- **`sudo comando`** → executa um comando como superusuário (root).  
  Exemplo: `sudo apt update`
- Arquivo **`/etc/sudoers`** → define quem pode usar `sudo` e quais comandos pode executar.  
  - Editar com segurança: `sudo visudo`
  - Exemplo de linha no `/etc/sudoers`:
    ```
    icaro ALL=(ALL) NOPASSWD: ALL
    ```
    → Usuário `icaro` pode executar qualquer comando sem senha (⚠️ não recomendado em produção).

---
### Chaves SSH

- **Gerar chave SSH**:
  ```bash
  ssh-keygen -t rsa -b 4096 -C "email@example.com"
  ```
  - Cria chave pública e privada (`~/.ssh/id_rsa` e `~/.ssh/id_rsa.pub`).
- **Copiar chave para servidor remoto**:
```bash
ssh-copy-id user@host
```

---

### Segurança básica

- **Restringir login root via SSH**:
-  Editar `/etc/ssh/sshd_config` e alterar:
```nginx
PermitRootLogin no
```
- Reiniciar SSH: `sudo systemctl restart sshd`
- **Boas práticas de senha**:
	 - Usar senhas longas e únicas.   
    - Alterar periodicamente.
    - Usar `passwd usuario` para redefinir senhas.
- **Outras recomendações**:
    - Manter sistema atualizado (`sudo apt upgrade`).
    - Liberar somente portas necessárias no firewall.
    - Usar autenticação por chave SSH em vez de senha sempre que possível.