# Checkpoint 3: Orquestração e Composição de Serviços

Função serverless desenvolvida em Go e executada no Google Cloud Functions (2ª geração). A função é acionada automaticamente sempre que uma nova mensagem é publicada no tópico **orders** do Google Cloud Pub/Sub.


## Provedor Utilizado
* GCP

## Como rodar localmente

### Pre-requisitos
* Goland
* git clone https://github.com/Doebber/Checkpoint-2.git

### Passo a passo
1. Clone o repositorio para sua maquina:
git clone https://github.com/Doebber/Checkpoint-3.git

2. Entre na pasta do projeto:
```bash
cd Checkpoint-3
```

3. Faça o deploy do workflow:

```bash
gcloud workflows deploy loan-workflow \
  --location=us-central1 \
  --source=workflow.yaml
```

4. Executar o Workflow:

```bash
gcloud workflows run loan-workflow \
  --location=us-central1 \
  --data='{
    "name":"Joao",
    "cpf":"12345678900",
    "amount":15000,
    "term":24
  }'
```

5. Verifique os logs da função para confirmar o processamento da mensagem:

```bash
gcloud functions logs read LoanHandlerPubSub \
  --gen2 \
  --region=us-central1 \
  --limit=20
```
