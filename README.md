
# Guia de Estudos - Faculdade Infnet

Este projeto é uma aplicação web para gerenciamento de estudos, implantada em um cluster Docker Swarm na AWS com monitoramento via Prometheus, cAdvisor e Grafana.

## 📦 Tecnologias Utilizadas

- [Docker](https://www.docker.com/)
- [Docker Swarm](https://docs.docker.com/engine/swarm/)
- [Prometheus](https://prometheus.io/)
- [cAdvisor](https://github.com/google/cadvisor)
- [Grafana](https://grafana.com/)
- [MySQL](https://www.mysql.com/)
- [Next.js](https://nextjs.org/)

---

## 🚀 Como subir o projeto

### 1. Clonar o repositório

```bash
git clone https://github.com/tassioauad/infnet-guia.git
cd infnet-guia
```

---

### 2. Criar volumes de dados

Crie as pastas de persistência para os serviços:

```bash
sudo mkdir -p /mnt/data/prometheus_data/data
sudo mkdir -p /mnt/data/grafana_data
sudo mkdir -p /mnt/data/mysql_data

# Permissões
sudo chown -R 65534:65534 /mnt/data/prometheus_data
sudo chmod -R 777 /mnt/data/prometheus_data

sudo chown -R 472:472 /mnt/data/grafana_data
sudo chown -R ec2-user:ec2-user /mnt/data/mysql_data
```

---

### 3. Subir o stack Docker Swarm

```bash
docker stack deploy -c docker-composer-deploy.yaml infnet-guia
```

Verifique os serviços:

```bash
docker stack services infnet-guia
```

---

### 4. Acesso à aplicação

- **Frontend da aplicação**: http://[IP-PÚBLICO]:80
- **Grafana**: http://[IP-PÚBLICO]:3000  
  Login: `admin` | Senha: `grafana`

> ❗ Certifique-se de liberar as portas 80 e 3000 no grupo de segurança da sua instância EC2.

---

## 📊 Monitoramento

O sistema de monitoramento foi configurado com:

- **Prometheus**: coleta de métricas dos containers via cAdvisor
- **cAdvisor**: exporta métricas para o Prometheus
- **Grafana**: dashboards e visualização

O Prometheus já está configurado para descobrir automaticamente os nodes do Swarm via DNS interno AWS.

---

## 🛠️ Manutenção

Para atualizar o código:

```bash
git pull --all
docker stack rm infnet-guia
docker stack deploy -c docker-composer-deploy.yaml infnet-guia
```

---


## 📃 Licença

Projeto desenvolvido para fins educacionais no contexto da Faculdade Infnet. Todos os direitos reservados.
