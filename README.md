# Virtual Machine no Azure (Robusta) para Testes e Laboratórios

Usando terraform.
Baixe o repositorio com git clone...

---

## 1. Máquina

* **Size:** `Standard_D2s_v3` (General Purpose)
* **vCPUs:** 2
* **RAM:** 8 GB
* **OS:** Ubuntu Server 22.04 LTS (Jammy Jellyfish)
* **Image Publisher:** Canonical (`0001-com-ubuntu-server-jammy`)

---

## 2. Preparação do Ambiente Com AzureCLI

### 2.1. Atualizar e instalar dependências
```bash
### Atualizar e instalar dependências
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release
```
---
### 2.2. Baixar e adicionar a chave GPG da Microsoft
```bash
### Baixar e adicionar a chave GPG da Microsoft
sudo mkdir -p /etc/apt/keyrings
curl -sL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /etc/apt/keyrings/microsoft.gpg > /dev/null
```
---
### 2.3. Adicionar o repositório oficial do Azure CLI
```bash
### Adicionar o repositório oficial do Azure CLI
AZ_DIST=$(lsb_release -cs)
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/microsoft.gpg] https://packages.microsoft.com/repos/azure-cli/ $AZ_DIST main" | sudo tee /etc/apt/sources.list.d/microsoft.list
```
---
### 2.4. Atualizar o gerenciador de pacotes e instalar
```bash
### Atualizar o gerenciador de pacotes e instalar
sudo apt-get update
sudo apt-get install -y azure-cli
```
---
## 3. Preparação do Ambiente com Terraform
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y gnupg software-properties-common curl
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update
sudo apt install -y terraform
terraform -version
```
---
## 4. Rodando 
### 4.1. Login na Azure
```bash
az login --use-device-code --tenant <TenantID>
```
---
### 4.2. Rodando o Terraform
```bash
terraform init
terraform plan
terraform apply -auto-approve
terraform output user_credentials
```
---
### 4.3. Destruindo o Terraform
```bash
terraform destroy -auto-approve
```
---
