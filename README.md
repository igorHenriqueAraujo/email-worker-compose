# email-worker-compose
Aplicação para treinamento de docker e docker-compose.

Aplicação possui backend (connector em python), frontend (formulário simples executando no nginx), fila(serviço mq redis) e serviços (workers em python) que simulam um envio de email com conexão e armazenamento das informações em banco de dados postgreSQL.  

Ambiente criado para treinamento de utilização de docker e docker-compose.  

Para executar basta clonar esse repositório e executar:  
`docker-compose up -d`  
Basta acessar http://localhost no seu browser e visualizará o formulário.  
Os logs para verificação do funcionamento podem ser acessados da seguinte forma:  
`docker-compose logs -f -t`  
Dessa forma é possível acompanhar as execuções de todos os serviços, também é possível visualizar os logs de um único serviço informando logo a frente como no exemplo abaixo.  
`docker-compose logs -f -t worker`  

Também é possível escalar algum serviço, como os worker por exemplo, basta executar o comando up do docker-compose informando a flag --scale como no exemplo abaixo:  
`docker-compose up -d --scale worker=3`  
Aqui estamos dizendo para inicar três containers para o serviço worker.  

Para verificar se os dados estão sendo armaznados no banco de dados basta utilizar o comando exec do docker-compose acessando o serviço db do banco de dados e passando o comando que você quer executar como no exemplo abaixo:  
`docker-compose exec db psql -U postgres -d email_sender -c 'select * from emails'`
