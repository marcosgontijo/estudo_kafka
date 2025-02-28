<h1>Projeto: Curso Udemy - Arquitetura de Microsserviços: Padrão Saga Orquestrado</h1>

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
