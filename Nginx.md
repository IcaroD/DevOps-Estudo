## Funções Essenciais do Nginx em DevOps

Em um ambiente conteinerizado (como Docker e Kubernetes), o Nginx é raramente usado para hospedar um site simples. Ele geralmente assume funções mais críticas e especializadas:

---

### 1. Reverse Proxy (Proxy Reverso)

Esta é a função mais comum no DevOps. O Nginx fica na "frente" da sua aplicação real (que pode ser um contêiner Node.js, Java, ou Python) e lida com todas as requisições da internet.

- **Como funciona:** Um cliente acessa `api.suaempresa.com`. O Nginx recebe essa requisição e a **encaminha** (faz _proxy_) para a porta interna do contêiner da sua API, escondendo a arquitetura interna.
- **Benefício:** Permite executar a aplicação real em portas internas (ex: 3000, 8080) e o Nginx cuida de expor o serviço na porta padrão 80 (HTTP) ou 443 (HTTPS).

---

### 2. Load Balancer (Balanceador de Carga)

Se você tem vários contêineres idênticos da sua aplicação rodando para lidar com o tráfego (o que é chamado de **escalabilidade horizontal**), o Nginx distribui as requisições entre eles.

- **Como funciona:** O Nginx gerencia uma lista de servidores _backend_ e usa algoritmos (como _Round-Robin_ ou _Least Connections_) para enviar cada nova requisição para o servidor menos ocupado, garantindo que nenhum contêiner fique sobrecarregado.
- **Benefício:** **Alta disponibilidade** e **performance**. Se um dos seus contêineres cair, o Nginx automaticamente para de enviar tráfego para ele.

---

### 3. TLS/SSL Termination (Gerenciamento de HTTPS)

É o Nginx que frequentemente lida com os certificados de segurança (SSL/TLS).

- **Como funciona:** Ele recebe a conexão criptografada (HTTPS) do usuário, descriptografa o tráfego e envia a requisição para o contêiner _backend_ em HTTP **não criptografado** (pois é uma comunicação interna e segura).
- **Benefício:** **Alivia a carga** do seu contêiner de aplicação. Sua aplicação não precisa gastar recursos com criptografia, focando apenas na lógica de negócios.

---

### 4. Servidor de Conteúdo Estático

Embora seja um Proxy, o Nginx é extremamente rápido para servir arquivos que não mudam (HTML, CSS, JavaScript, imagens).

- **Uso:** É comum configurar o Nginx para servir arquivos de _frontend_ estáticos (como um SPA em React ou Angular) e, ao mesmo tempo, atuar como proxy para o _backend_ da API.

---

## Guia de Execução: Aplicação Node.js com Nginx no Docker

Este procedimento é o _setup_ padrão para rodar uma aplicação Node.js atrás de um **Reverse Proxy** Nginx usando Docker Compose.

### 1. Configuração do Domínio Local (`/etc/hosts`)

O primeiro passo é garantir que seu computador consiga encontrar a aplicação pelo nome.

| Ação                    | Comando                        | Propósito                                                                                                                                         |
| ----------------------- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Adicionar a entrada** | **`127.0.0.1 www.nodejs.dvp`** | Mapeia o nome do domínio `www.nodejs.dvp` para o seu endereço local (`127.0.0.1`), permitindo que você acesse a aplicação pelo nome no navegador. |

> **Nota:** No Windows, o arquivo equivalente é `C:\Windows\System32\drivers\etc\hosts`. Você precisará de permissões de administrador para editar.

---

### 2. Construção da Imagem Docker

Você precisa criar o pacote de instalação da sua aplicação (a Imagem Docker) antes de executá-la.

|Ação|Comando|Propósito|
|---|---|---|
|**Build da Imagem**|**`./docker/build.sh`**|Executa o script que contém o **`docker build`**. Ele lê o `Dockerfile` e empacota seu código Node.js e todas as dependências em uma imagem customizada.|

---

### 3. Execução dos Contêineres (Docker Compose)

O **Docker Compose** inicia simultaneamente o contêiner Node.js e o contêiner Nginx (e quaisquer outros serviços) conforme o arquivo `docker-compose.yml`.

|Modo|Comando|Propósito|
|---|---|---|
|**Primeiro Plano**|**`docker-compose up`**|Inicia os serviços e anexa a saída de log ao seu terminal. Útil para **debug** inicial, pois você vê o que está acontecendo em tempo real.|
|**Segundo Plano (Daemon)**|**`docker-compose up -d`**|Inicia os serviços em modo _daemon_ (**detached**). Libera seu terminal para outras tarefas enquanto os contêineres continuam rodando.|

---

### 4. Confirmação e Debug (Navegador)

A etapa final é confirmar que o Nginx está funcionando como proxy reverso corretamente.

|Ação|Detalhe|Propósito|
|---|---|---|
|**Acessar o Site**|Abra **`http://www.nodejs.dvp/`**|O navegador envia a requisição para o `127.0.0.1`, que é o seu contêiner Nginx.|
|**Verificar Headers**|Abra as _DevTools_ (F12) e inspecione os cabeçalhos de resposta. Procure pela entrada: **`Server: nginx`**|Confirma que o Nginx recebeu a requisição, processou o _proxy_ para a aplicação Node.js, e foi o responsável por devolver a resposta ao cliente.|