#todo 

# maven 

./mvnw clean install
./mvnw spring-boot:run

si quiero que ser cargue en cada salvada en el pom en el area de dependencies agregar

```xml
<dependency> <groupId>org.springframework.boot</groupId> <artifactId>spring-boot-devtools</artifactId> <scope>runtime</scope> <optional>true</optional> </dependency>
```

# spring 

the framework that does everything. use the spring initilizer
this is how you set a route

```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class appStatus {    
    @GetMapping("/up")
    public boolean up() {
        return true;
    }
}
```
