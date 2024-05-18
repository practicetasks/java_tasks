# Квиз

Какие реализации методов  `hashCode()` и `equals()` для класса `User` написаны корректно (без багов).

`User`
```java
public class User {
    private Integer id;
    private String name;
    private String email;
    private String country;
}
```

<br>

A) 
```java
public boolean equals(User user) {
    return id.equals(user.id);
}

public int hashCode() {
    return id.hashCode();
}
```
<br>

B)
```java
public String toString() {
    return "User from country: " + country;
}

public boolean equals(User user) {
    return this.toString().equals(user.toString());
}

public int hashCode() {
    return this.toString().hashCode();
}
```
<br>

C)
```java
public boolean equals(User user) {
    return id.equals(user.id)
            && name.equals(user.name)
            && email.equals(user.email)
            && country.equals(user.country);
}

public int hashCode() {
    int result = id.hashCode();
    result = 31 * result + name.hashCode();
    result = 31 * result + email.hashCode();
    result = 31 * result + country.hashCode();
    return result;
}
```
<br>

D)
```java
public boolean equals(User user) {
    return true;
}

public int hashCode() {
    return id.hashCode();
}
```