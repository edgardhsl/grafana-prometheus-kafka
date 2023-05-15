# Grafana, Prometheus e Kafka Exporter com Docker Compose

Este repositório contém um arquivo `docker-compose.yml` que configura e inicia os serviços do Grafana, Prometheus e Kafka Exporter em contêineres Docker. O Grafana é usado como plataforma de visualização, o Prometheus para coletar métricas e o Kafka Exporter para exportar métricas do Kafka para o Prometheus.

## Pré-requisitos

Antes de começar, certifique-se de ter instalado o Docker e o Docker Compose em seu sistema. Você pode encontrar as instruções de instalação nos seguintes links:

- Docker: [https://docs.docker.com/get-docker/](https://docs.docker.com/get-docker/)
- Docker Compose: [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)

## Como usar

1. Clone este repositório para o seu sistema:

```
git clone https://github.com/seu-usuario/nome-do-repositorio.git
cd nome-do-repositorio
```

2. Edite o arquivo `prometheus.yml`:

Abra o arquivo `prometheus.yml` e ajuste os alvos (endereços e portas) conforme necessário. Certifique-se de configurar corretamente o endereço do Kafka Exporter.

```yaml
# prometheus.yml

scrape_configs:
  - job_name: 'kafka-exporter'
    static_configs:
      - targets: ['kafka-exporter:9308']  # Altere para o endereço correto do Kafka Exporter
```

3. (Opcional) Adicione os arquivos de dashboard do Grafana:

Se você tiver arquivos de dashboard personalizados para o Kafka Exporter, copie-os para o diretório `provisioning/dashboards` e certifique-se de que estejam no formato JSON.

4. Inicie os contêineres:

Execute o comando a seguir para iniciar os contêineres do Grafana, Prometheus e Kafka Exporter:

Copy code
docker-compose up -d
Isso iniciará os contêineres em segundo plano (`-d`), baixando as imagens necessárias e configurando os serviços.

5. Acesse o Grafana:

Abra o navegador e acesse `http://localhost:3000` para acessar o Grafana. Use as seguintes credenciais de login:

Login: admin
Senha: admin
Você será solicitado a alterar a senha após o primeiro login.

6. Configure o Prometheus como fonte de dados:

No Grafana, clique no ícone do menu lateral (canto superior esquerdo) e vá em "Configuration" -> "Data Sources".
Clique em "Add data source".
Selecione "Prometheus" como o tipo de fonte de dados.
Configure o nome do data source como "Prometheus" (ou qualquer nome de sua preferência).
No campo "URL", insira `http://prometheus:9090`.
Clique em "Save & Test" para salvar a configuração e testar a conexão com o Prometheus.

7. Explore os dashboards e crie painéis:
Agora você está pronto para explorar os dashboards pré-configurados (se você adicionou os arquivos de dashboard) ou criar seus próprios painéis no Grafana. Você
