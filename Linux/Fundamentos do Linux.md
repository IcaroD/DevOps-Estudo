## 1. Navegação

Comandos básicos para se mover entre diretórios e manipular arquivos:

- `pwd` → mostra o diretório atual
- `ls` → lista arquivos e diretórios
- `cd pasta/` → entra em um diretório
- `cd ..` → sobe um nível
- `touch arquivo.txt` → cria um arquivo vazio
- `mkdir nova_pasta` → cria diretório
- `rm arquivo.txt` → remove arquivo
-  `cp arquivo1.txt arquivo2.txt` → copia arquivo
- `mv origem destino` → move arquivo para pasta

---

## 2. Permissões e usuários
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

