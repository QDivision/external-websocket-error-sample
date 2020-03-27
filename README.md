Proxy External Websocket Demo
---

## Expected Behavior
Able to proxy websocket requests to external services with spring cloud gateway.

## Actual Behavior
Unable to proxy websocket requests to external services with spring cloud gateway.


# How to exercise

## Prerequisites

- Java 11
- [Websocat](https://github.com/vi/websocat) cli websocket tool

## Not Working Flow
1. Open terminal and navigate to `not-working-external-websocket`
1. Run gateway service `./mvnw clean spring-boot:run`
1. Repeat Step one
1. Attempt to establish websocket connection with this command:
                    
        websocat 'ws://localhost:8869/websocket/echo' -H 'Pragma: no-cache' -H 'Origin: http://localhost:8869' -H 'Accept-Language: en-US,en;q=0.9' -H 'Sec-WebSocket-Key: vBAeZp3K1b+6iCx6rQSlew==' -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.122 Safari/537.36 OPR/67.0.3575.53' -H 'Upgrade: websocket' -H 'Sec-WebSocket-Extensions: permessage-deflate; client_max_window_bits' -H 'Cache-Control: no-cache' -H 'Connection: Upgrade' -H 'Sec-WebSocket-Version: 13'
1. Type `foo` and hit enter 
1. Type `bar` and hit enter

### Expected output
```
foo
foo
bar
bar
```

### Actual Output
```$xslt
foo
bar
```

## Working Flow (with built changes)
1. Make sure the code with the fix is published to maven local and the `pom.xml` has the correct version with the local changes in the `working-external-websocket` project.
1. Open terminal and navigate to `working-external-websocket`
1. Run gateway service `./mvnw clean spring-boot:run`
1. Repeat Step one
1. Attempt to establish websocket connection with this command:
                    
        websocat 'ws://localhost:8870/websocket/echo' -H 'Pragma: no-cache' -H 'Origin: http://localhost:8870' -H 'Accept-Language: en-US,en;q=0.9' -H 'Sec-WebSocket-Key: vBAeZp3K1b+6iCx6rQSlew==' -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.122 Safari/537.36 OPR/67.0.3575.53' -H 'Upgrade: websocket' -H 'Sec-WebSocket-Extensions: permessage-deflate; client_max_window_bits' -H 'Cache-Control: no-cache' -H 'Connection: Upgrade' -H 'Sec-WebSocket-Version: 13'
1. Type `foo` and hit enter 
1. Type `bar` and hit enter

### Expected output
```
foo
foo
bar
bar
```

### Actual output
```
foo
foo
bar
bar
```