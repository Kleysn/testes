Aqui está o passo a passo detalhado para instalar o Docker em sua instância EC2 na AWS:

---

### **Passo 1: Conectar-se à Instância EC2**

1. No seu terminal, conecte-se à instância usando SSH:
   ```bash
   ssh -i ~/server-root-key.pem ubuntu@<ENDEREÇO_DA_INSTÂNCIA>
   ```
   Substitua `<ENDEREÇO_DA_INSTÂNCIA>` pelo endereço público de sua máquina EC2.

---

### **Passo 2: Atualizar os Pacotes do Sistema**

2. Após se conectar à instância, atualize os pacotes existentes:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

---

### **Passo 3: Instalar Dependências Necessárias**

3. Instale pacotes adicionais necessários para adicionar o repositório Docker:
   ```bash
   sudo apt install -y ca-certificates curl gnupg lsb-release
   ```

---

### **Passo 4: Adicionar o Repositório Docker**

4. Adicione a chave GPG oficial do Docker:
   ```bash
   sudo mkdir -p /etc/apt/keyrings
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
   ```

5. Configure o repositório Docker:
   ```bash
   echo \
   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

---

### **Passo 5: Instalar o Docker**

6. Atualize novamente os pacotes para incluir o repositório Docker:
   ```bash
   sudo apt update
   ```

7. Instale o Docker Engine e seus componentes:
   ```bash
   sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
   ```

---

### **Passo 6: Verificar Instalação do Docker**

8. Confirme se o Docker foi instalado corretamente verificando sua versão:
   ```bash
   docker --version
   ```

---

### **Passo 7: Permitir Uso do Docker sem `sudo` (Opcional)**

9. Por padrão, o Docker requer permissões administrativas. Para usar o Docker sem `sudo`:
   - Adicione seu usuário ao grupo `docker`:
     ```bash
     sudo usermod -aG docker $USER
     ```
   - Faça logout e login novamente ou use o comando abaixo para aplicar a mudança:
     ```bash
     su - $USER
     ```

10. Teste se o Docker funciona sem `sudo`:
    ```bash
    docker run hello-world
    ```

---

### **Passo 8: Configurar o Docker para Iniciar Automaticamente**

11. Certifique-se de que o Docker será iniciado automaticamente após o boot da instância:
    ```bash
    sudo systemctl enable docker
    ```

---

Agora o Docker está instalado e pronto para uso em sua instância EC2!

--- 

Caso ao rodar o comando ```docker run hello-world ``` retorne o erro a seguir:

``` bash

docker: permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Head "http://%2Fvar%2Frun%2Fdocker.sock/_ping": dial unix /var/run/docker.sock: connect: permission denied.

```

Esse erro ocorre porque o usuário atual (`ubuntu`) não tem permissões para acessar o socket do Docker. Para resolver isso, siga os passos abaixo:

---

### **a): Verificar o Grupo do Docker**

1. O grupo do Docker geralmente é chamado `docker`. Confirme se ele existe:
   ```bash
   grep docker /etc/group
   ```

Se você vir algo como `docker:x:999:`, o grupo existe.

---

### **b): Adicionar o Usuário ao Grupo Docker**

2. Adicione o usuário `ubuntu` ao grupo `docker`:
   ```bash
   sudo usermod -aG docker $USER
   ```

3. Para aplicar a mudança sem reiniciar:
   ```bash
   newgrp docker
   ```

---

### **c): Testar o Docker**

4. Execute novamente o comando de teste:
   ```bash
   docker run hello-world
   ```

Se o comando funcionar, o problema está resolvido!

---

### **d): Garantir que o Docker Seja Iniciado com Permissões**

Se o problema persistir, tente os comandos abaixo para garantir que o serviço Docker esteja rodando com as permissões corretas:

5. Reinicie o serviço Docker:
   ```bash
   sudo systemctl restart docker
   ```

6. Verifique o status do serviço Docker:
   ```bash
   sudo systemctl status docker
   ```

Certifique-se de que ele está ativo e rodando.

---

### **e): Solução Temporária (Usar `sudo`)**

Se você não quiser alterar as permissões do usuário, pode executar os comandos Docker com `sudo`:
   ```bash
   sudo docker run hello-world
   ```

No entanto, é recomendável corrigir as permissões para evitar o uso contínuo de `sudo`.
