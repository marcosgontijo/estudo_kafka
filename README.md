<h1>Projeto de Estudo: - Arquitetura de Microsserviços: Padrão Saga Orquestrado</h1>

<p>Repositório contendo o projeto desenvolvido do curso <strong>Arquitetura de Microsserviços: Padrão Saga Orquestrado</strong></p>

<img src="https://github.com/user-attachments/assets/90f9b78f-63df-4055-a6d4-5b67cf1b8697" alt="Imagem Curso">

<h2>Sumário:</h2>
<ul>
  <li><a href="#tecnologias">Tecnologias</a></li>
  <li><a href="#ferramentas">Ferramentas utilizadas</a></li>
  <li><a href="#arquitetura">Arquitetura Proposta</a></li>
  <li><a href="#execucao">Execução do projeto</a></li>
</ul>

<h2 id="tecnologias">Tecnologias</h2>
<ul>
  <li>Java 17</li>
  <li>Spring Boot 3</li>
  <li>Apache Kafka</li>
  <li>API REST</li>
  <li>PostgreSQL</li>
  <li>MongoDB</li>
  <li>Docker</li>
  <li>docker-compose</li>
  <li>Redpanda Console</li>
</ul>

<h2 id="ferramentas">Ferramentas utilizadas</h2>
<ul>
  <li>IntelliJ IDEA Community Edition</li>
  <li>Docker</li>
  <li>Gradle</li>
</ul>

<h2 id="arquitetura">Arquitetura Proposta</h2>
<img src="https://github.com/user-attachments/assets/5a0c32cc-54a3-49c6-9547-d166591acb6f" alt="Arquitetura Proposta">

<p>Em nossa arquitetura, teremos 5 serviços:</p>
<ul>
  <li><strong>Order-Service:</strong> Responsável por gerar pedidos iniciais e receber notificações.</li>
  <li><strong>Orchestrator-Service:</strong> Orquestra todo o fluxo da Saga.</li>
  <li><strong>Product-Validation-Service:</strong> Valida produtos no pedido.</li>
  <li><strong>Payment-Service:</strong> Processa pagamentos.</li>
  <li><strong>Inventory-Service:</strong> Gerencia estoque.</li>
</ul>

<h2 id="execucao">Execução do projeto</h2>
<p>Para rodar as aplicações, será necessário ter instalado:</p>
<ul>
  <li>Docker</li>
  <li>Java 17</li>
  <li>Gradle 7.6 ou superior</li>
</ul>

<h3>01 - Execução geral via docker-compose</h3>
<pre><code>docker-compose up --build -d</code></pre>

<h3>02 - Execução geral via automação com script em Python</h3>
<pre><code>python build.py</code></pre>

<h3>03 - Executando os serviços de bancos de dados e Message Broker</h3>
<pre><code>docker-compose up --build -d order-db kafka product-db payment-db inventory-db</code></pre>

<h3>04 - Executando manualmente via CLI</h3>
<pre><code>gradle build -x test</code></pre>
<p>Para rodar:</p>
<pre><code>gradle bootRun</code></pre>
<p>Ou via JAR:</p>
<pre><code>java -jar nome_do_jar.jar</code></pre>


<h1>Acessando a aplicação</h1>
<p><a href="#inicio">Voltar ao início</a></p>

<p>Para acessar as aplicações e realizar um pedido, basta acessar a URL:</p>
<p><a href="http://localhost:3000/swagger-ui.html" target="_blank">http://localhost:3000/swagger-ui.html</a></p>

<p>Você chegará nesta página:</p>

![Documentacao](https://github.com/user-attachments/assets/61d5d387-cfd7-4d47-88b3-3a9ee8548176)

<img src="caminho/para/imagem.jpg" alt="Swagger UI" />

<p>As aplicações executarão nas seguintes portas:</p>
<ul>
  <li>Order-Service: 3000</li>
  <li>Orchestrator-Service: 8080</li>
  <li>Product-Validation-Service: 8090</li>
  <li>Payment-Service: 8091</li>
  <li>Inventory-Service: 8092</li>
  <li>Apache Kafka: 9092</li>
  <li>Redpanda Console: 8081</li>
  <li>PostgreSQL (Product-DB): 5432</li>
  <li>PostgreSQL (Payment-DB): 5433</li>
  <li>PostgreSQL (Inventory-DB): 5434</li>
  <li>MongoDB (Order-DB): 27017</li>
</ul>

<h2>Acessando tópicos com Redpanda Console</h2>
<p><a href="#inicio">Voltar ao início</a></p>

<p>Para acessar o Redpanda Console e visualizar tópicos e publicar eventos, basta acessar:</p>
<p><a href="http://localhost:8081" target="_blank">http://localhost:8081</a></p>

<p>Você chegará nesta página:</p>

![Redpanda Kafka](https://github.com/user-attachments/assets/c09f665d-842e-4123-bb5d-90257d433dbf)

<img src="caminho/para/imagem2.jpg" alt="Redpanda Console" />

<h2>Dados da API</h2>
<p><a href="#inicio">Voltar ao início</a></p>

<p>É necessário conhecer o payload de envio ao fluxo da saga, assim como os produtos cadastrados e suas quantidades.</p>

<h3>Produtos registrados e seu estoque</h3>
<p><a href="#nivel-anterior">Voltar ao nível anterior</a></p>

<ul>
  <li>COMIC_BOOKS (4 em estoque)</li>
  <li>BOOKS (2 em estoque)</li>
  <li>MOVIES (5 em estoque)</li>
  <li>MUSIC (9 em estoque)</li>
</ul>

<h3>Endpoint para iniciar a saga:</h3>
<p><a href="#nivel-anterior">Voltar ao nível anterior</a></p>

<p>POST <code>http://localhost:3000/api/order</code></p>

<p>Payload:</p>
<pre>
{
  "products": [
    {
      "product": {
        "code": "COMIC_BOOKS",
        "unitValue": 15.50
      },
      "quantity": 3
    },
    {
      "product": {
        "code": "BOOKS",
        "unitValue": 9.90
      },
      "quantity": 1
    }
  ]
}
</pre>

<p>Resposta:</p>
<pre>
{
  "id": "64429e987a8b646915b3735f",
  "products": [
    {
      "product": {
        "code": "COMIC_BOOKS",
        "unitValue": 15.5
      },
      "quantity": 3
    },
    {
      "product": {
        "code": "BOOKS",
        "unitValue": 9.9
      },
      "quantity": 1
    }
  ],
  "createdAt": "2023-04-21T14:32:56.335943085",
  "transactionId": "1682087576536_99d2ca6c-f074-41a6-92e0-21700148b519"
}
</pre>

<h3>Endpoint para visualizar a saga:</h3>
<p><a href="#nivel-anterior">Voltar ao nível anterior</a></p>

<p>É possível recuperar os dados da saga pelo orderId ou pelo transactionId, o resultado será o mesmo:</p>
<p>GET <code>http://localhost:3000/api/event?orderId=64429e987a8b646915b3735f</code></p>
<p>GET <code>http://localhost:3000/api/event?transactionId=1682087576536_99d2ca6c-f074-41a6-92e0-21700148b519</code></p>

<p>Resposta:</p>
<pre>
{
  "id": "64429e9a7a8b646915b37360",
  "transactionId": "1682087576536_99d2ca6c-f074-41a6-92e0-21700148b519",
  "orderId": "64429e987a8b646915b3735f",
  "payload": {
    "id": "64429e987a8b646915b3735f",
    "products": [
      {
        "product": {
          "code": "COMIC_BOOKS",
          "unitValue": 15.5
        },
        "quantity": 3
      },
      {
        "product": {
          "code": "BOOKS",
          "unitValue": 9.9
        },
        "quantity": 1
      }
    ],
    "totalAmount": 56.40,
    "totalItems": 4,
    "createdAt": "2023-04-21T14:32:56.335943085",
    "transactionId": "1682087576536_99d2ca6c-f074-41a6-92e0-21700148b519"
  },
  "source": "ORCHESTRATOR",
  "status": "SUCCESS",
  "eventHistory": [
    {
      "source": "ORCHESTRATOR",
      "status": "SUCCESS",
      "message": "Saga started!",
      "createdAt": "2023-04-21T14:32:56.78770516"
    },
    {
      "source": "PRODUCT_VALIDATION_SERVICE",
      "status": "SUCCESS",
      "message": "Products are validated successfully!",
      "createdAt": "2023-04-21T14:32:57.169378616"
    },
    {
      "source": "PAYMENT_SERVICE",
      "status": "SUCCESS",
      "message": "Payment realized successfully!",
      "createdAt": "2023-04-21T14:32:57.617624655"
    },
    {
      "source": "INVENTORY_SERVICE",
      "status": "SUCCESS",
      "message": "Inventory updated successfully!",
      "createdAt": "2023-04-21T14:32:58.139176809"
    },
    {
      "source": "ORCHESTRATOR",
      "status": "SUCCESS",
      "message": "Saga finished successfully!",
      "createdAt": "2023-04-21T14:32:58.248630293"
    }
  ],
  "createdAt": "2023-04-21T14:32:58.28"
}
</pre>

<h2>Acesso ao MongoDB</h2>
<p><a href="#inicio">Voltar ao início</a></p>

<p>Para conectar-se ao MongoDB via linha de comando (cli) diretamente do docker-compose, basta executar o comando abaixo:</p>

<pre>docker exec -it order-db mongosh "mongodb://admin:123456@localhost:27017"</pre>

<p>Para listar os bancos de dados existentes:</p>
<pre>show dbs</pre>

<p>Para selecionar um banco de dados:</p>
<pre>use admin</pre>

<p>Para visualizar as collections do banco:</p>
<pre>show collections</pre>

<p>Para realizar queries e validar se os dados existem:</p>
<pre>db.order.find()</pre>
<pre>db.event.find()</pre>
<pre>db.order.find(id=ObjectId("65006786d715e21bd38d1634"))</pre>
<pre>db.order.find({ "products.product.code": "COMIC_BOOKS" })</pre>



