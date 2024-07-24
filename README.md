# exemplo-builder-java
Exemplo do Builder Design Pattern feito em Java

No Bootcamp de Backend com Java, oferecido pela DIO em parceria com o Santander, pude aprender sobre os design patterns estabelecidos pela GoF (Gang of Four) no livro "Design Patterns: Elements of Reusable Object-Oriented Software".

Em Java, é possível criar um Builder facilmente utilizando a anotação `@Builder` da biblioteca Lombok:
```java
import lombok.Builder;

@Builder
public class UserEntity {
    private String username;
    private String password;
}
```
E o objeto pode então ser criado da seguinte forma:
```java
UserEntity.builder().username("julio").password("senha").build();
```
Mas eu queria saber o que acontece por debaixo dos panos... Por isso, analisando a criação do objeto, decidi criar o meu próprio Builder:
```java
public class UserEntity {
    private String username;
    private String password;

    private UserEntity(String username, String password) {
        this.username = username;
        this.password = password;
    }

    public static UserEntityBuilder builder() {
        return new UserEntityBuilder();
    }

    public static class UserEntityBuilder {
        private String username;
        private String password;

        public UserEntityBuilder username(String username) {
            this.username = username;
            return this;
        }
        public UserEntityBuilder password(String password) {
            this.password = password;
            return this;
        }

        public UserEntity build() {
            return new UserEntity(username, password);
        }
    }
}
```
---
Consegui o efeito desejado, a criação de objeto funciona normalmente. Porém, mesmo com toda essa complexidade, esse código ainda não substitui totalmente o Builder do Lombok; que exigiria ainda mais trabalho. Como não tenho a intenção de reinventar a roda, o melhor a se fazer é continuar utilizando o Lombok... mas cumpri meu objetivo, entender o que tem por trás de um Builder e, com isso, desmistificar o Builder Design Pattern.

Na [Documentação Oficial do Lombok](https://projectlombok.org/features/Builder) é disponibilizado um trecho de como o Builder pode ser criado com Java "puro" (ou "vanilla"). 
