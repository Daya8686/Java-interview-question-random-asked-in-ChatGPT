# Best Way to Build a Complex User Object with Optional Parameters

The **Builder Pattern** is ideal for building complex objects with optional parameters. 
This pattern allows you to construct an object step-by-step, making it easier to manage multiple optional parameters without having 
a massive constructor with too many arguments.

### Example Using Builder Pattern:
```java
public class User {
    // Required parameters
    private String name;
    private String email;

    // Optional parameters
    private int age;
    private String phone;
    private String address;

    private User(UserBuilder builder) {
        this.name = builder.name;
        this.email = builder.email;
        this.age = builder.age;
        this.phone = builder.phone;
        this.address = builder.address;
    }

    // Builder Class
    public static class UserBuilder {
        private String name;
        private String email;
        
        private int age = 0;  // default value
        private String phone = "";  // default value
        private String address = "";  // default value

        public UserBuilder(String name, String email) {
            this.name = name;
            this.email = email;
        }

        public UserBuilder setAge(int age) {
            this.age = age;
            return this;
        }

        public UserBuilder setPhone(String phone) {
            this.phone = phone;
            return this;
        }

        public UserBuilder setAddress(String address) {
            this.address = address;
            return this;
        }

        public User build() {
            return new User(this);
        }
    }
}

```
### Usage:
```java
User user = new User.UserBuilder("John", "john@example.com")
                .setAge(30)
                .setPhone("1234567890")
                .build();

```

The builder pattern makes the code flexible and easy to read, especially when many optional parameters are involved.

