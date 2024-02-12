#typescript
is a protocol that one program can use to **request** a **service** from **another program** located on another computer in a network. RPC abstracts the networking aspect, making the [[network]] communication process appear as a simple function call.

- In RPC, calling a function on a remote server **feels like** calling a **local function**. The complexity of the network communication is hidden from the developer.

- The client makes a **request to the server**, which performs the required operation and sends back a response.

- RPC can be **synchronous**, where the client waits for the server's response, or **asynchronous**, where the client proceeds without waiting.

### How It Works

mainly with 2 stubs, a client and a server stub. That make the process seamless. This is the process:

1. The **client** has a **stub** that provides the interface of the remote functions.
2. When the client calls the function, the stub **packages** the **function** parameters into a message and makes a system call to send the message.
3. The **server** has a similar **stub** that unpacks the message and calls the function on the server.
4. The server's response is sent back to the client, where it's unpacked by the client stub, returning the result to the client.
# gRPC
## Theory
### Basics
gRPC is an open-source remote procedure call (RPC) system initially developed by Google. It uses Protocol Buffers (protobuf) as its interface definition language to define the service methods and their message types.
I find very important to note, that to date. gRPC is **NOT SUPPORTED** on [[web browser]]

- **Protocol Buffers**: A language-neutral, platform-neutral, extensible way of serializing structured data.
- Uses `.proto` files to define service methods and their request and response message types.
- gRPC provides automatic code generation for multiple languages, enabling easy implementation of client and server applications.

### gRPC vs REST

#### Protocol
- **gRPC** Uses HTTP/2 which allows for features like streaming, multiplexing, and smaller message sizes.
- **REST** Typically uses HTTP/1.1. Does not inherently support streaming and often uses JSON for message format, which can be larger.
#### Communication Model
- **gRPC** Supports Unary (single request/response), server **streaming**, client streaming, and bi-directional streaming.
- **REST** Primarily based on request/response model. Streaming has to be implemented separately.

#### Use Cases

- gRPC is ideal for high-performance, low-latency applications like microservices, real-time communication, and inter-service communication in distributed systems.
- Once again. gRPC is **NOT SUPPORTED** on web browsers
- REST is more suitable for web APIs, public-facing services, and when human readability of messages is important.

### Why is gRPC Fast?

- **Efficient Message Encoding** with Protobuf, the binary format, is more efficient than JSON or XML in terms of both size and speed of encoding/decoding.
- **HTTP/2 Capabilities** like header compression, multiplexing, and server push contribute to reduced latency and improved speed.
- HTTP/2 allows to **reuse  connections**, reducing the overhead of setting up new connections for each request.

## Practice

#### create the protocol buffer
```protobuf
syntax = "proto3";

package bookPackage;
service Book {
  rpc allBooks(voidNoParam) returns (bookItems);
  rpc createBook(bookItem) returns (bookItem);
  rpc readBook(bookId) returns (bookItem);
  rpc updateBook(bookId) returns (bookItem);
  rpc DeleteBook(bookId) returns (bookItem);
}
message voidNoParam {}
message bookItem {
  int32 id = 1;
  string title = 2;
  string author = 3;
  string content = 4;
}  
message bookItems {
  repeated bookItem items = 1;
}
 
message bookId {
  int32 id = 1;
}
```


#### convert the proto to buffer 
the .proto is a serilized object, so you must create some code that manages this, or you can use [protoc](https://protobuf.dev/) or [buf](https://buf.build/solutions/generate-sdks)  (protoc is better)

if you are using typescript there is no out of the box compatibility. so you have to use `ts-protoc-gen`. Or just don't do it and leave a lot of optimization lost

The command is something like this for the [[Go]] language `protoc --go_out=. --go_opt=paths=source_relative --go-grpc_out=. --go-grpc_opt=paths=source_relative proto/videoQueue.proto`
#### Create the server and client
after that you finally create a server and client. They can be on different languages and will always expect your protocol buffer. The packages that you use will manage the files that you just created.

if you want to see a full example. Look at the project [[YoutubeClone]]

##### examples

###### typescript server without authentication
```typescript
import { loadPackageDefinition, Server, status, ServerCredentials, Call, requestCallback } from "@grpc/grpc-js";
import { loadSync } from "@grpc/proto-loader";
import { VideoService } from "./video.service";
import { logger } from "../utils/logger";
import { Database } from "../db";
 
const packageDef = loadSync("./src/proto/videoQueue.proto", {});
const grpcObject = loadPackageDefinition(packageDef);
const videoPackage: any = grpcObject.videoPackage;
  
const main = async () => {
    const db = new Database();
    await db.connect();
 
    //instance Server
    const server = new Server();
	server.addService(videoPackage.Video.service,
        {
            "UpdateVideoStatus": UpdateVideoStatus,
        });
   server.bindAsync("127.0.0.1:50000", ServerCredentials.createInsecure(), (error, port) => {
        server.start();
        console.log(`listening on port ${port}`);
    });

}
main();
async function UpdateVideoStatus(call: any, callback: any) {
	//yourCode
    callback(null, response); //how the response is structured
}
```


## Common errors

#### Bad response
when you return an invalid object, it will actually return the default response, with 0 on its values (0 for int, false for boolean, "" for strings ... ). So for example, if you have this code:
```typescript
const response = {success:true,err:"porsiaca" };
callback(null, { response });
```
It looks okay, but you actually have { { `your actual object` } }. This is an invalid response, so it will return 
```json
{"success": false,
"err": ""}
```
even though everything seams perfect

