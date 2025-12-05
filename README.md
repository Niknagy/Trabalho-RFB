# Trabalho-RFB
Trabalho de banco de dados Relacional - Não Relacional.

# Dados Publicos CNPJ

A Receita Federal do Brasil disponibiliza bases com os dados públicos do cadastro nacional de pessoas jurídicas (CNPJ).

De forma geral, nelas constam as mesmas informações que conseguimos ver no cartão do CNPJ, quando fazemos uma consulta individual, acrescidas de outros dados de Simples Nacional, sócios e etc. Análises muito ricas podem sair desses dados, desde econômicas, mercadológicas até investigações.

--------------------------------------------------------------------------------------------------------------------------

# Infraestutura necessária

E usada:

-Python 3.14.0

-MySQL Workbench 8.0.44 

 (ou MySQLInstaller Web Community)
 

***Pelo menos 50gb livres no HD***

---------------------------------------------------------------------------------------------------------------------------

**Nesse repositório consta um ETL que:**

**I)** Baixa os arquivos necessários

**II)** Descompacta os arquivos

**III)** Lê os arquivos

**IV)** Tratas os Arquivos

**V)** Insere no MySQL

*Todo o processo vária de 7 a + de 16 horas (como o meu caso)*

-----------------------------------------------------------------------------------------------------------------------------

# Como usar:

Com o WorkBench instalado, inicie a instância do servidor (pode ser local) e crie o banco de dados conforme o arquivo *banco_de_dados.sql.*

Crie um arquivo ``````.env`````` no diretório code, conforme as variáveis de ambiente do seu ambiente de trabalho (localhost). 

Utilize como referência o arquivo .env_template. Você pode também, por exemplo, renomear o arquivo de .env_template para apenas .env e então utilizá-lo:

*(no meu caso usei o .env na pasta code)*

``````OUTPUT_FILES_PATH:`````` diretório de destino para o donwload dos arquivos

``````EXTRACTED_FILES_PATH:`````` diretório de destino para a extração dos arquivos .zip

``````DB_USER:`````` usuário do banco de dados criado pelo arquivo banco_de_dados.sql

``````DB_PASSWORD:`````` senha do usuário do BD

**Este passo do DB_PASSWORD no meu caso o VSCODE/Python deu erro em buscar a senha por conta de caracteres especiais no final** 
como @, ai ele entendia por @@localhost, portanto um dos erros que vier a ser é ele pedir a senha por conta de haver caracteres especiais

``````DB_HOST:`````` host da conexão com o BD

``````DB_PORT:`````` porta da conexão com o BD

``````DB_NAME:`````` nome da base de dados na instância (Dados_RFB - conforme arquivo banco_de_dados.sql)



Instale as bibliotecas necessárias, disponíveis em **requirements.txt:**

``````pip install -r requirements.txt``````

Execute o arquivo ETL_coletar_dados_e_gravar_BD.py e aguarde a finalização do processo.



*Os arquivos são grandes. Dependendo da infraestrutura isso deve levar pelo menos 7 horas para conclusão, aqui levou mais de 16 horas.*

**Arquivos de 14/11/2025: 6,70 GB compactados e 68,9 GB descompactados.**

------------------------------------------------------------------------------------------------------------------------------

# Tabelas geradas no MYSQL:

``````empresa:`````` dados cadastrais da empresa em nível de matriz

``````estabelecimento:`````` dados analíticos da empresa por unidade / estabelecimento (telefones, endereço, filial, etc)

``````socios:`````` dados cadastrais dos sócios das empresas

``````simples:`````` dados de MEI e Simples Nacional

``````cnae:`````` código e descrição dos CNAEs

``````quals:`````` tabela de qualificação das pessoas físicas - sócios, responsável e representante legal.

``````natju:`````` tabela de naturezas jurídicas - código e descrição.

``````moti:`````` tabela de motivos da situação cadastral - código e descrição.

``````pais:`````` tabela de países - código e descrição.

``````munic:`````` tabela de municípios - código e descrição.

Pelo volume de dados, as tabelas empresa, estabelecimento, socios e simples possuem índices para a coluna cnpj_basico, que é a principal chave de ligação entre elas.
