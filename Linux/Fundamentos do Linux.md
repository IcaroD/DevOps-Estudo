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
- `tail arquivo.log` → mostra as últimas linhas de um arquivo
- `cat arquivo.txt` → mostra o conteúdo de arquivos
- `head arquivo.log` → mostra o primeiras linhas de arquivos

---

## 2. Flags no Linux

As **flags** personalizam o comportamento dos comandos.  
- Podem ser **curtas** (`-a`, `-l`, `-r`) ou **longas** (`--all`, `--help`).  
- Muitas vezes a letra é uma **abreviação da função** (ex.: `-r` = *recursive*, `-l` = *list*).  
- É comum combinar várias flags curtas: `ls -alh` = `ls -a -l -h`.

Tabela resumida de flags comuns:

| Flag | Palavra (Inglês)       | Função / Significado                          | Exemplo |
|------|------------------------|-----------------------------------------------|---------|
| `-a` | all                    | Mostra todos arquivos, inclusive ocultos      | `ls -a` |
| `-l` | list                   | Lista detalhada (permissões, dono, tamanho)  | `ls -l` |
| `-h` | human-readable         | Tamanhos legíveis (KB, MB, GB)               | `ls -lh` |
| `-R` | recursive              | Aplica a ação em subdiretórios                | `ls -R` |
| `-r` | recursive              | Copia, remove ou aplica recursivamente       | `rm -r pasta/` |
| `-f` | force                  | Força execução sem pedir confirmação         | `rm -rf pasta/` |
| `-v` | verbose                | Mostra detalhes do que está acontecendo     | `cp -rv pasta1 pasta2` |
| `-n` | number                 | Numera linhas ou define quantidade           | `head -n 5 arquivo.txt` |
| `-c` | count                  | Define quantidade de execuções ou pacotes    | `ping -c 4 google.com` |
| `-p` | parents                | Cria diretórios pai automaticamente          | `mkdir -p projeto/src` |
| `-f` | follow                 | Acompanha arquivo em tempo real              | `tail -f arquivo.log` |
