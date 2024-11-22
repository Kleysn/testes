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
