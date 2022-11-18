<h1 align="center">
    Node with RabbitMQ, MongoDB and Docker
</h1>

<p align="center">
  <img alt="Repo size" src="https://img.shields.io/github/repo-size/ricellicarvalho/node-rabbitmq-amqplib-docker">  
  <img alt="License" src="https://img.shields.io/badge/license-MIT-brightgreen">  
</p>

<br>

### **Preview the first application**

https://user-images.githubusercontent.com/38559002/202751117-d070dfee-0eb3-4254-985a-ab9197e3266f.mp4

### **Preview the second application**

https://user-images.githubusercontent.com/38559002/202749167-14683b87-18c6-4e15-9b55-169e68225756.mp4

## 🧪 Technologies

This project was developed with the following technologies:

- [Node.js](https://nodejs.org/en/)
- [TypeScript](https://www.typescriptlang.org/)
- [Express](https://expressjs.com/pt-br/)
- [Mongoose (MongoDB)](https://mongoosejs.com/)
- [amqplib (RabbitMQ)](https://amqp-node.github.io/amqplib/)
- [Socket.IO](https://socket.io/)
- [Docker](https://www.docker.com/)

## 🛠 Getting started

There are 2 applications in the project, being necessary to enter each one separately to run:
  * bitcoin-candle-generator - **RabbitMQ message publisher**
  * bitcoin-candle-api-with-mongodb - **RabbitMQ message consumer is responsible for saving to MongoDB**

>Tip: You must have docker and docker-compose installed on your machine
1. [Install Docker](https://docs.docker.com/engine/install/)
2. [Install Docker Compose](https://docs.docker.com/compose/install/)

Clone the project and access its folder.

```bash
$ git clone git@github.com:ricellicarvalho/node-rabbitmq-amqplib-docker.git
```
### **Running the first application**

```bash
# Enter the first application
$ cd bitcoin-candle-generator
```
**Open two consoles for this application, one to start RabbitMQ and one to run the project**

**First terminal:**
```bash
# Install dependencies
$ yarn

# To create the RabbitMQ container
$ docker-compose up
```

**Second terminal:**
```bash
# To run the application and watch the candles generation logs and publication in RabbitMQ
$ yarn start
```

A RabbitMQ client can be accessed at [`http://localhost:15672`](http://localhost:15672) with username and password: **admin/admin**

### **Running the second application**
```bash
# Enter the second application
$ cd bitcoin-candle-api-with-mongodb
```
**Open two consoles for this application, one to start MongoDB and one to run the project**

**First terminal:**
```bash
# Install dependencies
$ yarn

# To create the MongoDB container
$ docker-compose up
```

**Second terminal:**
```bash
# To run the application and see the logs being consumed from the database
$ yarn start
```

**To query the data in the database you can install Studio 3T: The Professional Client, IDE and GUI for MongoDB**[ Download Studio 3T](https://studio3t.com/)

## 🚀 Project

This project consists of two applications that communicate asynchronously through the RabbitMQ messaging system and consequently save the messages in the MongoDB database.

The first application (bitcoin-candle-generator) is a script responsible for making a call to the [CoinGecko](https://api.coingecko.com/api/v3/simple/price?ids=bitcoin&vs_currencies=usd) API to read/query the Bitcoin price quote every 5 minutes, thus generating candles with the price variation, where contains the opening price, lowest price, highest price and closing price of each candle. This information is queued in RabbitMQ to be consumed by the other application (bitcoin-candle-api-with-mongodb).

The second application (bitcoin-candle-api-with-mongodb) is an API that will read/consume the messages produced by the script in RabbitMQ and save them in MongoDB. Whenever a message is consumed the API will also issue a notification via Web Socket. These Web Socket notifications can be received and used by a third frontend application.

## 📝  License

This project is under the MIT license. See file [LICENSE](LICENSE.md) for more details.

---

<p align="center">Made with 💜 by Ricelli M. Carvalho</p>
