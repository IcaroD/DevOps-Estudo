
O **Shell Script** é usado para automatizar tarefas no Linux. Ele combina comandos comuns do terminal em arquivos `.sh` executáveis.

---
### 1. Criar scripts em `bash`

```bash
#!/bin/bash
echo "Olá, Shell Script!"
```

```bash
chmod +x script.sh   # dá permissão de execução
./script.sh          # executa o script
```

---
### 2. Saída com `echo`

O comando **`echo`** imprime textos e variáveis no terminal.  
É a forma mais básica de mostrar informações em um script.

- Exemplos simples:
```bash
#!/bin/bash
echo "Hello world!"
```

- Saída:
```bash
Hello world!
```

- Opções comuns:

| Opção         | Função                          | Exemplo              | Saída       |
| ------------- | ------------------------------- | -------------------- | ----------- |
| _(sem opção)_ | Imprime texto normal            | `echo "Linux é top"` | Linux é top |
| `-n`          | Não quebra linha no final       | `echo -n "Oi"`       | Oi%         |
| `-e`          | Interpreta escapes (`\n`, `\t`) | `echo -e "A\nB"`     | A  <br>B    |

---
### 3. Entrada com `read`

O comando **`read`** captura textos e variáveis no terminal.  

```bash
read -p "Digite seu nome: " nome
```

---
### 4. Variáveis

```bash
NOME="Fulano"
IDADE=25
echo "Meu nome é $NOME e tenho $IDADE anos."
```
- Variáveis de ambiente úteis:
```bash
echo $HOME   # diretório do usuário
echo $USER   # nome do usuário
echo $PWD    # diretório atual
```

---

### 5. Estruturas de controle

`if`
```bash
if [ $IDADE -ge 18 ]; then
  echo "Maior de idade"
else
  echo "Menor de idade"
fi
```
**principais operadores numéricos**:
- `-ge` significa **greater than or equal** (maior ou igual)  
- `-eq` significa **equal** (igual)  
- `-ne` significa **not equal** (diferente)  
- `-gt` significa **greater than** (maior que)  
- `-lt` significa **less than** (menor que)  
- `-le` significa **less than or equal** (menor ou igual) 
**operadores de comparação de strings**:
- `=` significa **equal** (igual)
- `!=` significa **not equal** (diferente)
- `-z` significa **string zero length** (string vazia)
- `-n` significa **string non-zero length** (string não vazia)

`for`
```bash
for i in 1 2 3; do
  echo "Número: $i"
done
```

Versões 3.0+ do bash permitem encurtar o intervalo (range) com “**. .**”
```bash
for i in {1. .5}
do
 echo "Hai $i"
done
```

Versões 4.0+ do bash permitem que você use a sintaxe **{INÍCIO. .FIM. .INCREMENTO}**
```bash
for i in {0. .8. .2}
do
 echo "Hai $i"
done
```

`while`
```bash
count=1
while [ $count -le 3 ]; do
  echo "Contando: $count"
  ((count++))
done
```
`case`
```bash
read -p "Digite uma opção (a/b): " opcao
case $opcao in
  a) echo "Você escolheu A" ;;
  b) echo "Você escolheu B" ;;
  *) echo "Opção inválida" ;;
esac
```

---

### 6. Redirecionamentos

Controlam entrada e saída dos comandos.

**`>`: Sobrescreve no arquivo**
```bash
echo "Log inicial" > log.txt
```
**`>>`: Adiciona no final do arquivo**
```bash
echo "Nova linha" >> log.txt
```
**`<`: usa arquivo como entrada**
```bash
sort < lista.txt
```
**`|`(pipe): Encadeia comandos**
```bash
ls -lh | grep ".txt"
```

---

### 7. Automação de tarefas (backup, limpeza de logs, deploy simples)

Shell scripts são muito usados para automação.

```bash
# Backup simples
tar -czf backup_$(date +%F).tar.gz /home/usuario/documentos

# Limpeza de logs
find /var/log -type f -name "*.log" -delete

# Deploy simples
git pull origin main
npm install
pm2 restart app
```
