## PM2 – Gerenciamento de Processos Node.js

O **PM2** é um gerenciador de processos para Node.js que ajuda a manter aplicações rodando, reiniciar automaticamente em caso de falhas e facilitar deploys.

---
### Instalação
```bash
npm install -g pm2
```

---
### Comandos básicos

- **Iniciar uma aplicação**
```bash
pm2 start app.js
```
- **Listar processos**
```bash
pm2 list
```
- **Parar uma aplicação**
```bash
pm2 stop app
```
- **Reiniciar uma aplicação**
```bash
pm2 restart app
```
- **Reiniciar automaticamente em caso de mudança de código**
```bash
pm2 start app.js --watch
```
- **Ver logs da aplicação**
```bash
pm2 logs
```
- **Salvar configuração de processos para reinício automático do sistema**
```bash
pm2 save
pm2 startup
```
O comando `pm2 startup` gera o script necessário para iniciar o PM2 e suas aplicações automaticamente no boot do sistema.

---

## Recursos importantes

- **Cluster Mode** → permite rodar múltiplas instâncias de uma aplicação Node.js para usar melhor os núcleos do processador.
```bash
pm2 start app.js -i max
```
- **Monitoramento em tempo real** → gráficos de CPU, memória e status dos processos:
```bash
pm2 monit
```

---

## Integração com logs e deploy

O PM2 facilita o **monitoramento de logs** e pode ser integrado em pipelines de CI/CD para **deploy automático ou reinício de aplicações**.
#### Logs

- PM2 centraliza logs da aplicação, separando **stdout** e **stderr**:
```bash
pm2 logs          # mostra todos os logs
pm2 logs app      # mostra logs de uma aplicação específica
pm2 flush         # limpa os logs
```
- É possível redirecionar logs para arquivos customizados:
```bash
pm2 start app.js --log /var/log/app-completo.log
```

---

#### Deploy automático

- PM2 possui **deploy system** para servidores remoto (Node.js):
```bash
pm2 deploy ecosystem.config.js production setup
pm2 deploy ecosystem.config.js production
```
Exemplo de `ecosystem.config.js`:
```bash
module.exports = {
  apps: [
    {
      name: "app",
      script: "./app.js",
      watch: true
    }
  ],
  deploy : {
    production : {
      user : "ubuntu",
      host : "meu-servidor.com",
      ref  : "origin/main",
      repo : "git@github.com:usuario/repo.git",
      path : "/var/www/app",
      'post-deploy' : 'npm install && pm2 reload ecosystem.config.js --env production'
    }
  }
}
```
- Como funciona:
	1. PM2 conecta no servidor remoto via SSH.
	2. Faz o pull do repositório.
	3. Instala dependências (npm install).
	4. Reinicia a aplicação automaticamente com PM2.
