Banking App API
Uma API RESTful para um sistema bancário simples desenvolvida com Spring Boot.

📋 Descrição
Esta API permite o gerenciamento completo de contas bancárias, incluindo operações financeiras básicas como depósitos, saques, transferências entre contas e consulta de histórico de transações.

🚀 Funcionalidades
Gestão de Contas
Criação de contas: Cria novas contas bancárias com nome do titular e saldo inicial

Consulta de contas: Obter detalhes de uma conta específica ou listar todas as contas

Exclusão de contas: Remover contas do sistema

Operações Financeiras
Depósitos: Adicionar fundos a uma conta existente

Saques: Retirar fundos de uma conta (com validação de saldo suficiente)

Transferências: Transferir valores entre duas contas diferentes

Histórico e Extratos
Consulta de transações: Visualizar todo o histórico de movimentações de uma conta

Ordenação por data: Transações listadas da mais recente para a mais antiga

🏗️ Estrutura do Projeto


PASTA PRINCIPAL (banking-app)


pom.xml → Lista de ferramentas e bibliotecas que o projeto precisa para funcionar


PASTA DE CÓDIGO (src/main/java/net/vbonilha/banking_app/)


BankingAppApplication.java → Motor principal que inicia o aplicativo bancário


PASTA CONTROLLER (controller)


AccountController.java → Recebe as solicitações dos usuários (como criar conta ou fazer transferências)


PASTA DTO (dto) → Formulários padrão para organizar os dados que entram e saem do sistema:


AccountDto.java → Formulário de dados da conta bancária


TransactionDto.java → Formulário de dados de transações


TransferFundDto.java → Formulário específico para transferências


PASTA ENTITY (entity) → Tabelas do banco de dados em formato Java:


Account.java → Modelo de como uma conta bancária é armazenada


Transaction.java → Modelo de como uma transação é armazenada


PASTA EXCEPTION (exception) → Gerenciamento de erros:


AccountException.java → Erros específicos da conta


ErrorDetails.java → Modelo de como os erros são exibidos


GlobalExceptionHandler.java → Central de tratamento de erros


PASTA MAPPER (mapper)


AccountMapper.java → Tradutor que converte dados entre diferentes formatos


PASTA REPOSITORY (repository) → Armazenamento de dados:


AccountRepository.java → Operaçōes de salvar/buscar contas


TransactionRepository.java → Operaçōes com transações


PASTA DE CONFIGURAÇÕES (src/main/resources)


application.properties → Configuraçōes do aplicativo (como senha do banco de dados)


🔄 Fluxo de Operações
Criação de Conta
Recebe dados do titular e saldo inicial via POST

Valida e persiste a nova conta no banco de dados

Retorna os dados da conta criada com ID único

Operações de Depósito/Saque
Identifica a conta pelo ID

Valida o valor da operação

Atualiza o saldo da conta

Registra a transação no histórico

Transferência entre Contas
Valida existência das contas de origem e destino

Verifica saldo suficiente na conta de origem

Executa débito na conta de origem e crédito na conta de destino

Registra duas transações (uma para cada conta)

Consulta de Transações
Busca todas as transações associadas a uma conta

Ordena resultados por data decrescente

Retorna lista formatada com detalhes de cada operação

🛡️ Tratamento de Erros
Conta não encontrada: Retorna erro 404 com mensagem específica

Saldo insuficiente: Impede saques e transferências sem fundos

Erros internos: Tratamento genérico com respostas padronizadas

📊 Modelo de Dados
Account
ID único, nome do titular, saldo atual

Transaction
ID único, referência à conta, valor, tipo (DEPOSIT/WITHDRAWAL), data/hora

🔌 Endpoints Disponíveis
POST /api/accounts - Criar conta

GET /api/accounts - Listar todas as contas

GET /api/accounts/{id} - Consultar conta específica

DELETE /api/accounts/{id} - Excluir conta

PUT /api/accounts/{id}/deposit - Realizar depósito

PUT /api/accounts/{id}/withdraw - Realizar saque

POST /api/accounts/transfer - Transferir entre contas

GET /api/accounts/{id}/transactions - Consultar transações

⚙️ Instalação e Configuração
Pré-requisitos
Java 17 ou superior

MySQL 8.0 ou superior

Maven 3.6 ou superior

Git para clonar o repositório

Passo a Passo para Instalação
Clone o repositório

bash
git clone <url-do-repositorio>
cd banking-app
Configure o banco de dados MySQL

sql
-- Conecte-se ao MySQL como root ou usuário com privilégios
CREATE DATABASE banking_app;
CREATE USER 'your_username'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON banking_app.* TO 'your_username'@'localhost';
FLUSH PRIVILEGES;
Configure a aplicação
Edite o arquivo src/main/resources/application.properties se necessário:

properties
# Altere se usar configurações diferentes do MySQL
spring.datasource.url=jdbc:mysql://localhost:3306/banking_app
spring.datasource.username=your_username
spring.datasource.password=your_password
Compile o projeto

bash
mvn clean compile
Execute a aplicação

bash
mvn spring-boot:run
A aplicação estará disponível em: http://localhost:8080

🐛 Solução de Problemas
Erro de conexão com MySQL:

Verifique se o MySQL está rodando

Confirme usuário e senha no application.properties

Porta 8080 ocupada:

Altere a porta em application.properties: server.port=8081

Erros de compilação:

Verifique a versão do Java: java -version

Limpe e recompile: mvn clean compile

📝 Próximos Passos
Implementar autenticação e autorização

Adicionar documentação Swagger/OpenAPI

Criar testes de integração abrangentes

Implementar paginação nas consultas

Adicionar cache para melhor performance

Desenvolvido com Spring Boot - Uma aplicação robusta e escalável para demonstração de conceitos bancários básicos.
