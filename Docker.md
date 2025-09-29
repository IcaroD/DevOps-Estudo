## Docker

O uso de containers Docker garante que o ambiente de desenvolvimento seja idêntico ao de teste e produção, tornando os resultados dos testes mais confiáveis.

| Fase do DevOps               | Uso do Docker                                                                                                                                                                                   | Benefício em Testes                                                                                                                                                  |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Desenvolvimento**          | Usar **Docker Compose** para configurar o ambiente local com o backend, banco de dados (ex: PostgreSQL), cache (ex: Redis), etc.                                                                | O desenvolvedor testa em um ambiente que espelha exatamente a produção, capturando bugs de ambiente antes do _commit_.                                               |
| **Integração Contínua (CI)** | O pipeline (ex: GitHub Actions, Jenkins) usa um **Dockerfile** para construir a imagem da aplicação e executa testes unitários/de segurança **dentro do contêiner**.                            | Isolamento e Reprodutibilidade. O teste roda com o sistema operacional e as bibliotecas exatas definidas, garantindo que a falha não seja devido a um ambiente sujo. |
| **Testes de Integração/E2E** | Utiliza **Docker Compose** para subir um ambiente efêmero com o _serviço a ser testado_ e quaisquer **serviços de apoio** (bancos de dados temporários com **TestContainers**, APIs simuladas). | Velocidade e Limpeza. Após os testes, o ambiente (incluindo dados) é destruído instantaneamente, garantindo que o próximo teste comece do zero.                      |
| **Entrega Contínua (CD)**    | A **Imagem Docker** (que passou por todos os testes) é o artefato final que será enviado para o Registro (ex: Docker Hub, ACR) e implantado no ambiente de produção (ex: Kubernetes).           | Consistência. O que foi testado é exatamente o que é implantado.                                                                                                     |

## Comandos Fundamentais do Docker

|Categoria|Comando|Descrição|
|---|---|---|
|**Imagens (Build)**|`docker build -t <nome> .`|**CRIA/CONSTRÓI** uma nova imagem a partir do **`Dockerfile`** no diretório atual (`.`).|
|**Imagens (Pull)**|`docker pull <nome-da-imagem>`|**BAIXA** uma imagem (camadas) de um registro (ex: Docker Hub) para o seu computador.|
|**Imagens (Gestão)**|`docker images`|Lista todas as imagens armazenadas localmente.|
|**Imagens (Gestão)**|`docker rmi <nome-da-imagem>`|Remove uma imagem localmente.|
|**Contêineres (Run)**|`docker run -d -p 8080:80 --name <nome> <imagem>`|**CRIA** e **INICIA** um novo contêiner em background (`-d`), mapeando portas (`-p`).|
|**Contêineres (Run)**|`docker run -it <imagem> /bin/bash`|Cria um contêiner e executa um comando de forma **interativa** (`-it`). Ótimo para **debug rápido**.|
|**Contêineres (Gestão)**|`docker ps`|Lista os contêineres que estão **em execução**.|
|**Contêineres (Gestão)**|`docker ps -a`|Lista **todos** os contêineres (em execução e parados).|
|**Contêineres (Ciclo de Vida)**|`docker stop <nome-do-contêiner>`|Para um contêiner em execução de forma segura.|
|**Contêineres (Ciclo de Vida)**|`docker start <nome-do-contêiner>`|**REINICIA** um contêiner que foi parado.|
|**Contêineres (Ciclo de Vida)**|`docker rm <nome-do-contêiner>`|Remove um contêiner parado.|
|**Orquestração (Compose)**|**`docker compose up`**|**INICIA** seu aplicativo e todos os seus serviços definidos no arquivo **`docker-compose.yml`** (incluindo redes e volumes).|
|**Orquestração (Compose)**|`docker compose down`|Para e **REMOVE** todos os contêineres, redes e volumes (se não especificado) criados pelo `up`.|
|**Logs & Debug**|`docker logs -f <nome-do-contêiner>`|Exibe os logs de um contêiner (o `-f` segue em tempo real).|
|**Logs & Debug**|`docker exec -it <nome> /bin/bash`|Executa um comando (**`/bin/bash`**) dentro de um contêiner em execução.|
|**Inspeção**|`docker inspect <nome-do-contêiner>`|Exibe informações detalhadas em formato JSON (IP, volumes, configurações). **Fundamental para debug**.|
|**Visualização**|`docker stats <nome-do-contêiner>`|Mostra em tempo real o uso de **CPU, Memória e Rede** pelo contêiner.|
|**Limpeza**|`docker system prune`|Remove contêineres parados, redes, imagens sem tag e cache. **Use com cautela!**|
|**Volumes**|`docker volume ls`|Lista todos os **volumes** que estão armazenando dados persistentes.|

## Exemplos Práticos de Fluxo de Debug:

1. Verifica a configuração e status exato do contêiner que falhou
```bash
docker inspect meu-api-fail
```

2. Busca a causa do erro de execução
```bah
docker logs meu-api-fail
```

3. Entra no contêiner para ver arquivos, variáveis, etc.
```bash
docker exec -it meu-api-fail /bin/bash
```

4. Limpeza do Ambiente (Após o debug):
```bash
# Para e remove o contêiner
docker stop meu-api-fail 
docker rm meu-api-fail 
```

Estes comandos, combinados com o `docker run`,` build`, `pull` e `ps`, cobrem praticamente 90% das suas necessidades com Docker em um ambiente de desenvolvimento e CI/CD.