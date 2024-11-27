# Example 1 : Serialization and Deserialization using Java API

## Step 1 : implement the Serializable interface
```java
import java.io.Serializable;

public class Person implements Serializable {
    private static final long serialVersionUID = 1L; // recommended for Serializable classes
    private String name;
    private int age;
    private String address;
    public Person(String name, int age, String address) {
        this.name = name;
        this.age = age;
        this.address = address;
    }

    public String getName() {
        return name;
    }
    public int getAge() {
        return age;
    }
    public String getAddress() {
        return address;
    }
    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + ", address='" + address + "'}";
    }
}
```

### Step 2 : Serialize (write) the Serializable object to a file
```java
import java.io.FileOutputStream;
import java.io.ObjectOutputStream;
import java.io.IOException;

public class SerializeExample {
    public static void main(String[] args) {
        Person person = new Person("Alice", 30, "123 Main St, Wonderland");

        try (FileOutputStream fileOut = new FileOutputStream("person.ser");
             ObjectOutputStream out = new ObjectOutputStream(fileOut)) {

            out.writeObject(person);
            System.out.println("Person object has been serialized to person.ser");

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
### Step 3 : Deserialize (read) the object from the file 
```java
import java.io.FileInputStream;
import java.io.ObjectInputStream;
import java.io.IOException;

public class DeserializeExample {
    public static void main(String[] args) {
        try (FileInputStream fileIn = new FileInputStream("person.ser");
             ObjectInputStream in = new ObjectInputStream(fileIn)) {

            Person person = (Person) in.readObject();
            System.out.println("Deserialized Person object: " + person);

        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```


# Example 2 : Serialization and Deserialization using external libraries e.g. Jackson

```java
// User.java
public class User {
    private String id;
    private String name;
    private int age;
    // Constructors
    public User() {
    }
    public User(String id, String name, int age) {
        this.id = id;
        this.name = name;
        this.age = age;
    }
    // Getters and Setters
    public String getId() {
        return id;
    }
    public void setId(String id) {
        this.id = id;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
    @Override
    public String toString() {
        return "name=" + name + ", id=" + id + ", age=" + age;
    }
}

// Jackson.java
import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;

public class Jackson {
    public static void main(String[] args) {
        ObjectMapper objectMapper = new ObjectMapper();
        User user = new User("1", "Mahtab Alam", 31);
        try {
            String jsonAsString = objectMapper.writeValueAsString(user);
            System.out.println(jsonAsString);
            System.out.println(jsonAsString.length());

            String str = "{\"id\":\"1\",\"name\":\"Mahtab Alam\",\"age\":31}";
            System.out.println("STR :" + str);
            System.out.println(str.length());

            System.out.println(jsonAsString.equals(str));
        } catch (JsonProcessingException e) {
            e.printStackTrace();
        }
    }
}

```
