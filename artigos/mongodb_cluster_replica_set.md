# Configuração de Cluster MongoDB Replica Set no Docker com mongosh

## Descrição

Este documento descreve os passos para configurar um cluster MongoDB Replica Set utilizando Docker, realizar testes de replicação e simular falhas, utilizando o `mongosh` para interagir com o cluster.

## Pré-requisitos

* Docker instalado e configurado no Windows.
* MongoDB Compass instalado (opcional, para visualização).

## Passo 1: Preparação do Ambiente

1.  **Verifique a Instalação do Docker:**
    * Certifique-se de que o Docker esteja instalado e funcionando corretamente.
2.  **Crie uma Rede Docker:**
    * Crie uma rede Docker para que os contêineres do MongoDB possam se comunicar.

    ```bash
    docker network create mongo-network
    ```

## Passo 2: Configuração do Replica Set MongoDB

1.  **Inicie os Contêineres MongoDB:**
    * Inicie quatro contêineres MongoDB, cada um com um nome e porta diferentes, e conecte-os à rede Docker criada.

    ```bash
    docker run -d -p 27017:27017 --name mongo1 --net mongo-network mongo --replSet rs0 --bind_ip 0.0.0.0
    docker run -d -p 27018:27017 --name mongo2 --net mongo-network mongo --replSet rs0 --bind_ip 0.0.0.0
    docker run -d -p 27019:27017 --name mongo3 --net mongo-network mongo --replSet rs0 --bind_ip 0.0.0.0
    docker run -d -p 27020:27017 --name mongo4 --net mongo-network mongo --replSet rs0 --bind_ip 0.0.0.0
    ```

2.  **Inicie o Replica Set:**
    * Conecte-se ao primeiro contêiner MongoDB usando `mongosh`:

    ```bash
    docker exec -it mongo1 mongosh
    ```

    * Dentro do shell do `mongosh`, execute os seguintes comandos:

    ```javascript
    rs.initiate({
    _id: "rs0",
    members: [
    { _id: 0, host: "mongo1:27017" },
    { _id: 1, host: "mongo2:27017" },
    { _id: 2, host: "mongo3:27017" },
    { _id: 3, host: "mongo4:27017" }
    ]
    })
    ```

3.  **Verifique o Status do Replica Set:**
    * Verifique se o Replica Set foi configurado corretamente.

    ```javascript
    rs.status()
    ```

    * Este comando exibirá o status do cluster, incluindo qual nó é o primário e quais são os secundários.

## Passo 3: Teste de Replicação

1.  **Conecte-se ao Nó Primário:**
    * Use o MongoDB Compass para se conectar ao nó primário (porta 27017) através da seguinte URL: `mongodb://localhost:27017`
2.  **Insira Dados:**
    * Crie um banco de dados e uma coleção, e insira alguns documentos.
3.  **Conecte-se aos Nós Secundários:**
    * Conecte-se aos nós secundários usando o MongoDB Compass, através das seguintes URLs:
        * Nó secundário 1 (porta 27018): `mongodb://localhost:27018`
        * Nó secundário 2 (porta 27019): `mongodb://localhost:27019`
        * Nó secundário 3 (porta 27020): `mongodb://localhost:27020`
    * Verifique se os dados inseridos no nó primário foram replicados para os nós secundários.

## Passo 4: Simulação de Falha de Nós Secundários

1.  **Pare um ou Dois Contêineres Secundários:**
    * Use o comando `docker stop` para parar um ou dois dos contêineres secundários.
    * Ex: `docker stop mongo2`
2.  **Verifique o Status do Replica Set:**
    * Conecte-se ao nó primário e execute `rs.status()` para verificar o status do cluster.
    * Verifique se o nó primário ainda está funcionando e aceitando inserções de dados.
3.  **Reinicie os Contêineres Secundários:**
    * Use o comando `docker start` para reiniciar os contêineres secundários.
    * Ex: `docker start mongo2`
4.  **Verifique a Recuperação do Cluster:**
    * Verifique se os nós secundários se reconectaram ao cluster e se a replicação foi retomada.

## Passo 5: Simulação de Falha do Nó Primário

1.  **Pare o Contêiner Primário:**
    * Use o comando `docker stop` para parar o contêiner primário.
2.  **Verifique o Status do Replica Set:**
    * Conecte-se a um dos nós secundários restantes e execute `rs.status()`.
    * Verifique se um dos nós secundários assumiu o papel de primário.
3.  **Insira Dados no Novo Nó Primário:**
    * Conecte-se ao novo nó primário e insira alguns dados.
4.  **Reinicie o Contêiner Primário Original:**
    * Use o comando `docker start` para reiniciar o contêiner primário original.
5.  **Verifique a Recuperação do Cluster:**
    * Verifique se o contêiner primário original se reconectou como um nó secundário e se a replicação está funcionando.

## Observações

* Este guia fornece os comandos básicos. Ajuste as configurações com base nos seus requisitos.
* Consulte a documentação oficial do MongoDB para informações detalhadas.
* Documente cada etapa com capturas de tela e logs.