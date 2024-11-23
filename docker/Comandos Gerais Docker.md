Principais comandos do Docker separados por categorias:

---

### **1. Comandos Gerais**
- `docker version`: Exibe a versão do Docker instalada.
- `docker info`: Exibe informações detalhadas sobre o Docker instalado e seu ambiente.
- `docker help`: Mostra ajuda geral sobre os comandos do Docker.

---

### **2. Gerenciamento de Imagens**
- **Listar imagens:**
  - `docker images`: Lista todas as imagens disponíveis localmente.
- **Baixar imagens:**
  - `docker pull <image_name>:<tag>`: Faz o download de uma imagem do Docker Hub ou outro repositório.
- **Remover imagens:**
  - `docker rmi <image_id>`: Remove uma imagem localmente.
- **Criar imagens:**
  - `docker build -t <image_name>:<tag> .`: Cria uma nova imagem com base no `Dockerfile`.

---

### **3. Gerenciamento de Contêineres**
- **Executar contêineres:**
  - `docker run <image_name>`: Inicia um contêiner baseado em uma imagem.
  - `docker run -d <image_name>`: Inicia um contêiner em segundo plano (modo `detached`).
  - `docker run -it <image_name> /bin/bash`: Inicia um contêiner em modo interativo.
- **Listar contêineres:**
  - `docker ps`: Lista contêineres em execução.
  - `docker ps -a`: Lista todos os contêineres, incluindo os parados.
- **Parar e reiniciar contêineres:**
  - `docker stop <container_id>`: Para um contêiner em execução.
  - `docker restart <container_id>`: Reinicia um contêiner.
- **Remover contêineres:**
  - `docker rm <container_id>`: Remove um contêiner parado.
  - `docker rm -f <container_id>`: Força a remoção de um contêiner em execução.
- **Inspecionar contêiner:**
  - `docker inspect <container_id>`: Exibe informações detalhadas de um contêiner.
  - `docker logs <container_id>`: Mostra os logs de um contêiner.

---

### **4. Gerenciamento de Volumes**
- **Criar volumes:**
  - `docker volume create <volume_name>`: Cria um volume.
- **Listar volumes:**
  - `docker volume ls`: Lista todos os volumes.
- **Remover volumes:**
  - `docker volume rm <volume_name>`: Remove um volume.
- **Inspecionar volumes:**
  - `docker volume inspect <volume_name>`: Exibe informações detalhadas de um volume.

---

### **5. Gerenciamento de Redes**
- **Criar redes:**
  - `docker network create <network_name>`: Cria uma nova rede.
- **Listar redes:**
  - `docker network ls`: Lista todas as redes disponíveis.
- **Conectar contêineres a uma rede:**
  - `docker network connect <network_name> <container_id>`: Conecta um contêiner a uma rede.
- **Desconectar contêineres de uma rede:**
  - `docker network disconnect <network_name> <container_id>`: Desconecta um contêiner de uma rede.
- **Remover redes:**
  - `docker network rm <network_name>`: Remove uma rede criada.

---

### **6. Comandos Relacionados a Docker Compose**
- `docker-compose up`: Inicia os serviços definidos no arquivo `docker-compose.yml`.
- `docker-compose down`: Para e remove os contêineres definidos no `docker-compose.yml`.
- `docker-compose ps`: Lista os contêineres gerenciados pelo Compose.
- `docker-compose logs`: Mostra os logs dos serviços gerenciados pelo Compose.
- `docker-compose build`: Constrói as imagens definidas no `docker-compose.yml`.

---

### **7. Gerenciamento de Configurações e Recursos**
- **Limpeza de recursos:**
  - `docker system prune`: Remove recursos não utilizados (contêineres parados, imagens órfãs, volumes não utilizados).
  - `docker volume prune`: Remove volumes não utilizados.
  - `docker image prune`: Remove imagens não utilizadas.
- **Limpar tudo (cuidado!):**
  - `docker system prune -a --volumes`: Remove tudo que não está sendo usado.

---
