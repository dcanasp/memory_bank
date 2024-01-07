#typescript #python
A [[Message Broker]] that allows to create queues. these queues live (by default) on a database, you can make them work you call these queues via the protocol [[amqp]].

They are really useful to maintain your data alive when the request are not sure to arrive and comeback instantly. There are two parts, the sender and receiver, each has it's unique code, but that is more amqp than RabbitMQ

there are multiple ways to do it, a simple one, where the message only goes (great for creating a register on the database or something like that). Or another where you wait for a response [[RPC]] (great for task that take some time but will work and you need the response)


It's important to understand that in it's core, RabbitMQ it's just a [[database]], so just treat it as such, the database lives on wherever you like. How you connect to the database it's your problem

To create it it's better on [[docker]] (local on windows it's a pain because of erlang), and to connect you need a library that speaks [[amqp]].


code on [[Node.js]]:

```typescript
const connection = await amqplib.connect(`amqp://${user}@${url}:5672`);
const channel = await connection.createChannel();
const q = await channel.assertQueue('', { exclusive: true });


channel.sendToQueue('rpc_queue', Buffer.from(texto), {

  correlationId: correlationId,

  replyTo: q.queue

});

const numero = await new Promise<string>((resolve) => {

	channel.consume(q.queue, (msg) =>  {
	
		let stringMsg = msg?.content.toString('utf8');
		
		if (msg?.properties.correlationId === correlationId) {
		
		  resolve( stringMsg! );
		
		}
	
	}, { noAck: true });

});
```

code on python:
```python
credentials = pika.PlainCredentials(username='trunews', password='password')

connection = pika.BlockingConnection(
    pika.ConnectionParameters(
        host=ip,
        port=5672,
        credentials=credentials
    )
)

channel = connection.channel() 
channel.queue_declare(queue='rpc_queue')

def on_request(ch, method, props, body):
    response = queue(body)
    ch.basic_publish(exchange='',
                     routing_key=props.reply_to,                     properties=pika.BasicProperties(correlation_id = \
  props.correlation_id),
                     body=str(response))
    ch.basic_ack(delivery_tag=method.delivery_tag)
channel.basic_qos(prefetch_count=1)
channel.basic_consume(queue='rpc_queue', on_message_callback=on_request)
print(" [x] Awaiting RPC requests")
channel.start_consuming()
```

