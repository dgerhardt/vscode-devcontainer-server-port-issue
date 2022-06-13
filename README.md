# Visual Studio Code Devcontainer SERVER\_PORT issue

## Reproduction Steps

1. Open this project in Visual Studio Code as a Devcontainer

    You should notice that some extensions are not running correctly:

    > Couldn't start client Language Support for Java  
    > Source: Language Support for Java(TM) by Red Hat (Extension)

2. Try to run the Spring application with Maven:

    `mvn spring-boot:run`

    It will fail to start because both Spring Boot and Extension Host use the port set via `SERVER_PORT` (`8123`).

3. Run `ss -tulpen`.

    Result:

    ```
    Netid              State               Recv-Q              Send-Q                           Local Address:Port                           Peer Address:Port             Process                                                                                                 
    tcp                LISTEN              0                   511                                  127.0.0.1:9999                                0.0.0.0:*                 users:(("node",pid=171,fd=18)) uid:1000 ino:32977355 sk:c001 cgroup:unreachable:7f14d <->              
    tcp                LISTEN              0                   511                                          *:8123                                      *:*                 users:(("node",pid=546,fd=33)) uid:1000 ino:32957332 sk:c002 cgroup:unreachable:7f14d v6only:0 <->
    ```
