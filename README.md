

## Installation

yarn add react-native-fixed-rabbitmq
cd ios
pod install

## Usage
```
import { Connection, Exchange, Queue } from 'react-native-fixed-rabbitmq';

const config = {
    host:'',
    port:5672,
    username:'user',
    password:'password',
    virtualhost:'vhost',
    ttl: 10000 // Message time to live,
    ssl: true // Enable ssl connection, make sure the port is 5671 or an other ssl port
}

const rabbitServer = new Connection(config)

rabbitServer.on('error', (event) => {
    console.log('eventoErro', event)
})

rabbitServer.on('connected', (event) => {

    let queue = new Queue(rabbitServer, {
        name: '',
        passive: false,
        durable: false,
        exclusive: true,
        consumer_arguments: { 'x-priority': 1 }
    }, {

        });

    let exchange = new Exchange(this.rabbitServer, {
        name: 'app',
        type: 'fanout',
        durable: false,
        autoDelete: false,
        internal: false
    });

    queue.bind(exchange, '');
    queue.on('message', (data) => {
    	
    });
};

rabbitServer.connect();

```
