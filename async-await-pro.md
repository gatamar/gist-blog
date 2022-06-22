## "Modern Swift Concurrency book"

https://www.raywenderlich.com/books/modern-concurrency-in-swift/v1.0/

### Conspect 

Restart an HTTP server:
```
[ WARNING ] bind(descriptor:ptr:bytes:): Address already in use (errno: 48)
Swift/ErrorType.swift:200: Fatal error: Error raised at top level: bind(descriptor:ptr:bytes:): Address already in use (errno: 48)
zsh: trace trap  swift run
user@olha 00-book-server % sudo lsof -i:8080
Password:
COMMAND   PID         USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
Run     85028 user   15u  IPv4 0xabe903c74153566d      0t0  TCP localhost:http-alt (LISTEN)
user@olha 00-book-server % kill -9 85028
```

### Easy wins for refactoring the old code: wrappers/patterns/etc

### Rules/checklists for reviewing a new code
