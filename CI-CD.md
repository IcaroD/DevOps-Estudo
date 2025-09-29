## CI/CD

### 1. O que é?
- **CI (Continuous Integration – Integração Contínua)**  
  - Prática onde desenvolvedores integram seu código frequentemente em um repositório central.  
  - Cada mudança dispara **builds automáticos e testes**, garantindo que o código continua funcionando.  
  - Objetivo: detectar erros cedo, evitar conflitos de integração.

- **CD (Continuous Delivery/Deployment – Entrega/Implantação Contínua)**  
  - Após a integração, o código é automaticamente **empacotado, testado e preparado para ir a produção**.  
  - Existem dois níveis:  
    - **Continuous Delivery** → entrega pronta, mas ainda precisa de alguém para apertar o "deploy".  
    - **Continuous Deployment** → o deploy é feito automaticamente em produção, sem intervenção manual.  

---

### 2. Benefícios
- Reduz falhas em produção.  
- Acelera ciclos de desenvolvimento.  
- Dá feedback rápido sobre mudanças no código.  
- Automatiza testes, builds e deploys.  

---

### 3. Ferramentas comuns
- **CI**: GitHub Actions, GitLab CI, Jenkins, CircleCI, TravisCI.  
- **CD**: ArgoCD, Spinnaker, FluxCD, além de integrações com Kubernetes e Docker.  

---

### 4. Eventos
   - Dispara pipelines em eventos diferentes, não só `push`/`pull_request`.  
   - Exemplos:  
     - `on: schedule` → rodar todo dia/semana (cron job).  
     - `on: issues` → automatizar ao abrir/fechar issues.  
     - `on: release` → quando cria uma release, faz deploy.  

---
### 5. Ambientes e Segredos
   - Usar **Secrets** (`secrets.MY_KEY`) para guardar senhas, tokens de API, chaves SSH.  
   - Definir **environments** (dev, staging, prod) com aprovações manuais.  

---
### 6. Matriz de jobs
   - Rodar testes em várias versões de linguagem/SO automaticamente:  
 ```yaml
 strategy:
   matrix:
	 node-version: [14, 16, 18]
 ```

---
### 7. Pipeline típico CI/CD

1. **Commit** → dev envia código para o repositório.  
2. **Build** → código é compilado, dependências instaladas.  
3. **Testes** → testes unitários, integração, segurança.  
4. **Empacotamento** → gera imagem Docker ou artefato.  
5. **Deploy** → envia para staging ou produção automaticamente.  

**Exemplo prático:**
```yml
name: CI/CD Pipeline

# Dispara a pipeline em push ou pull request na branch main
on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      # 1. Clona o repositório
      - name: Checkout do código
        uses: actions/checkout@vx

      # 2. Configura o Node.js (poderia ser Python, Java, etc.)
      - name: Configurar Node.js
        uses: actions/setup-node@vx
        with:
          node-version: 'xx'

      # 3. Instala dependências
      - name: Instalar dependências
        run: npm install

      # 4. Executa testes
      - name: Rodar testes
        run: npm test

      # 5. Build do projeto
      - name: Build do projeto
        run: npm run build

  deploy:
    runs-on: ubuntu-latest
    needs: build  # só roda se o build/test passar

    steps:
      - name: Deploy de exemplo
        run: echo "Fazendo deploy em produção 🚀"
        # Aqui você colocaria:
        # - upload para servidor via scp/rsync
        # - push para registry de Docker
        # - deploy em Kubernetes, etc.
```
### Como funciona:
1. Dispara em `push` ou `pull_request` na branch `main`.
2. Clona o repositório.
3. Instala dependências.
4. Roda os testes.
5. Faz o build.
6. Se tudo passar, executa o **deploy**.