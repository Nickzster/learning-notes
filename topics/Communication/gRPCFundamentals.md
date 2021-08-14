# gRPC Fundamentals

## Motivation

- **Problems**

  - Protocols like http, REST, GraphQL, and SOAP need client libraries to be implemented.
  - Need a library to understand the protocol you communicate with.
  - All parties need to "agree" on the protocol / how to communicate with.

- **How gRPC Solves these problems**

  - gRPC came around to "Standardize" everything.
  - Everything is built for you.
  - 1 library for all popular languages is generated.
  - Built on top of HTTP/2 so that the details of HTTP/2 is abstracted away.
  - When HTTP/3 is released, very easy to migrate.
  - Message format: Protocol buffers.

## Best Practices

- [Protobuf Best Practices](https://medium.com/@akhaku/protobuf-definition-best-practices-87f281576f31)
- Consistent naming -- easier to read
- Data structure enforcement at API layer -- use message & service constructs to enforce data quality.
- Unique messages for each RPC service.
- Use structs liberally, as it organizes & enforces data quality.
- Don't have fields influencing the meanings of others -- they should have independent contexts.
- Enum value 0's should be unknown, so leave them undefined.

## Pros and Cons

### Pros

- Fast & compact
- One client library (.proto)
- Progress feedback (due to streaming features)
- Cancel a request (since it's built on HTTP/2)
- Protobuf -- Binary payload

### Cons

- Need a schema: very opinionated, strict.
- Have to maintain the client library.
- Need proxies to be compatible with HTTP/1.2
- Doesn't support **all** languages -- only the most popular.
- Error handling
- No native browser support
- Timeouts (pub/sub)
  - Unary model: Have to wait for a response.
  - What if request takes too long? Have to manage it yourself.

### gRPC modes

- **Unary**: Request / Response model.
- **Server Streaming**: Expects a stream from the server (Web sockets)
- **Client Streaming**: Expects a stream from the client (uploading a file)
- **Bi-directional streaming**: Both client and server are streaming (playing an online multiplayer video game)

### The "Proto" syntax & libraries.

- The code that needs to be ran is geneated with `protoc`. However, there are libaries for languages that can read a `.proto` file without running the compiler.
- [The full proto3 language syntax can be found here.](https://developers.google.com/protocol-buffers/docs/proto3)

### Message Types

- Can be thought of as "structs". They're objects with properties.

```proto3
message Person {
  string name = 1;
  int32 age = 2;
  repeated string hobbies = 3;
}
```

- Property types include: `string`, `int32`, `repeats (array)`, `enum`, etc.

### Service

- gRPC service.
- Defined as a service block with interface functions.

```proto3
message TodoItem{ ... }
message TodoItems { repeated TodoItem items = 1;}
message myVoid { }

service ToDo {
  rpc createTodo(TodoItem) returns (TodoItem); //Unary
  rpc createTodoStream(stream TodoItem) returns (TodoItem); //Client streaming
  rpc readTodos(myVoid) returns (TodoItem); //Unary
  rpc readTodosStream(myVoid) returns(stream TodoItems); //Server streaming
  rpc updateTodosStream(stream TodoItem) returns (stream TodoItem); //Bidirectional
  rpc deleteTodo(TodoItem) returns (TodoItem); //Unary

}
```

### The protoc compiler, how to implement into application.

- [Each language has its own unique method to incorporate gRPC into code, which can be found here.](https://grpc.io/docs/languages/)
- Implement `.proto` file
- Use `protoc` to compile it.
