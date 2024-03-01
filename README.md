# Tutorial de Apache Airflow

## Descrição dos arquivos
Para os exemplos do tutorial, estamos usando 3 containers Docker definidos no arquivo [./docker-compose.yml](docker-compose.yml):
- _postgres_: Esse é o banco de dados de metadados, ou o lugar onde o Airflow armazena diversos dados relativos aos processos como DAGs, execuções, variáveis, etc.
- _airflow-webserver_: Esse container possui as configurações para rodar a interface de usuário, é aonde a gente vai passar a maior parte do tempo interagindo com o Airflow.
- _airflow-scheduler_: Aqui é onde o Scheduler e o Executor (que roda dentro do scheduler) rodam, garantindo a execução das tarefas agendadas.

Além disso, temos também os arquivos:
- [./.env](.env): Arquivo de variáveis de ambiente, responsável por criar o banco de dados inicial no Postgres e definir algumas configurações do Airflow
- [./scripts/entrypoint.sh](entrypoint.sh): Arquivo que executa assim que o container `airflow-webserver` é criado, responsável por iniciar o banco de metadados do Airflow e criar o usuário `admin` para acessar a interface web
- Pasta `dags`: Aqui é onde vamos colocar todos os nossos DAGs no futuro

## Como criar o ambiente de desenvolvimento
Uma vez que se tenha o Docker e o Docker Compose instalado, basta executar os comandos abaixo:

`chmod +x ./scripts/entrypoint.sh` -> para dar permissão para o arquivo ser executado dentro do container

`docker-compose up -d` (ou `docker compose up -d`, dependendo da versão do seu Docker Compose) -> para criar o ambiente

## Como pausar / despausar o ambiente de desenvolvimento
Se você quiser pausar o ambiente, ou seja, parar os containers mas não perder as configurações de variáveis / conexões criadas por exemplo, é só executar o comando abaixo:

`docker-compose stop` (ou `docker compose stop`, dependendo da versão do seu Docker Compose)

E para continuar o trabalho no seu container de Airflow depois, basta executar:

`docker-compose start` (ou `docker compose start`)

## Como remover o ambiente de desenvolvimento
Para remover os containers criados e todas as configurações como variáveis e conexões, basta rodar o comando abaixo:

`docker-compose down -v` (ou `docker compose down -v`)

Isso vai eliminar os containers, redes e volumes criados pelo Docker Compose