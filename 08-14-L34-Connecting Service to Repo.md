## L34: Practical side of connecting Service to Repo
1. Connecting UserService with UserRepo
2. Adding a method for UserRepo to add a new User to ArrayList
3. Making sure the User get's added to fake DB by returning the size of ArrayList
----
**Repository** --> Responsible for communication btw Service/Business Logic and Database. Doing only 1 thing. Like a gate keeper.

**API** --> waiter/waitress, asking, bring me some food
**Service** --> you, bring me some food (?)
**Repo** --> is bringing you food, when it is ready (person who goes and brings)

If the waiter is API, kitchen's chef is the Service (knows how to prep all the food), restaurant's food storage supervisor is like Repo (goes to check if all the ingredients are available) and DB is the food storage space at the restaurant

**CRUD controller, CRUD repository**

1. CreateController (triggers constructor, creates new UserService)  
	2. Create UserService (creates new UserRepository)  
		 3. Create UserRepository  

<img width="766" alt="08-14" src="https://github.com/user-attachments/assets/1148977e-92ec-471a-88f0-5230e5f8aa26">

#### UserService.java
```java
package com.datorium.Datorium.API.Services;

import com.datorium.Datorium.API.DTOs.User;
import com.datorium.Datorium.API.Repo.UserRepo;

public class UserService {
    private UserRepo userRepo;
    
    public UserService(){
        userRepo = new UserRepo();
    }
    
    public int add(User user){
        return userRepo.add(user);
    }
}
```

#### UserRepo.java
```java
package com.datorium.Datorium.API.Repo;

import com.datorium.Datorium.API.DTOs.User;

public class UserRepo {

    public int add(User user){
        return 0;
    }
}
```
**Encapsulation** - Private vs Public  
- Encapsulation in Java is the principle of bundling data (fields) and methods (functions) into a single unit (class) and restricting access to the internal state of the object by making fields private.
- It uses getter and setter methods to control access to these fields, allowing for validation and protection of the data.
- Encapsulation improves code maintainability, security, and flexibility by hiding the internal workings of a class and exposing only a controlled interface to the outside world.

---------

#### UserController.java
```java
package com.datorium.Datorium.API.Controllers; // belongs to package created

import com.datorium.Datorium.API.DTOs.User;
import com.datorium.Datorium.API.Services.UserService;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/user")
public class UserController {

    // This code runs first, when creating UserController object

    private UserService userService;
    public UserController(){
        userService = new UserService();
    }

    //CRUD
    //AddUser
    //UpdateUser
    //GetUser
    //DeleteUser

    @PostMapping("/add") //localhost:8080/test -> localhost:8080/user/test
    public int add(@RequestBody User user){
        return userService.add(user);

    }
}
```

#### UserRepo.java
```java
package com.datorium.Datorium.API.Repo;

import com.datorium.Datorium.API.DTOs.User;

import java.util.ArrayList;

public class UserRepo {

    private ArrayList<User> users = new ArrayList<>();


    public int add(User user){
        users.add(user); // adds user addUser
        return users.size();
    }
}
```

#### UserService.java
```java
package com.datorium.Datorium.API.Services;

import com.datorium.Datorium.API.DTOs.User;
import com.datorium.Datorium.API.Repo.UserRepo;


public class UserService {
    private UserRepo userRepo;
    public UserService(){
        userRepo = new UserRepo(); // creates new object each time when UserService is accessed

    }
    public int add(User user){
        return userRepo.add(user);

    }
}
```

#### TEAMWORK
---------
Create a GET method for users

1. Create UserController endpoint to get all users
2. Create a UserService method to get all users
3. Create a userRepository method to get all users
4. Add user with a postman
5. Try to get all the users with GET method
6. Repeat step 4 and 5

#### User.java
```java
package com.datorium.Datorium.API.DTOs;

public class User {
    public String name;

}
```

#### UserController.java
```java
package com.datorium.Datorium.API.Controllers; // belongs to package created

import com.datorium.Datorium.API.DTOs.User;
import com.datorium.Datorium.API.Services.UserService;
import org.springframework.web.bind.annotation.*;

import java.util.ArrayList;

@RestController
@RequestMapping("/user")
public class UserController {

    // This code runs first, when creating UserController object

    private UserService userService;
    public UserController(){
        userService = new UserService();
    }

    //CRUD
    //AddUser
    //UpdateUser
    //GetUser
    //DeleteUser

    @PostMapping("/add") //localhost:8080/test -> localhost:8080/user/test
    public int add(@RequestBody User user){
        return userService.add(user);

    }

    @GetMapping("/get")
    public ArrayList<User> get(){
        return userService.getUsers();
    }
}

```
#### UserService.java
```java
package com.datorium.Datorium.API.Services;

import com.datorium.Datorium.API.DTOs.User;
import com.datorium.Datorium.API.Repo.UserRepo;

import java.util.ArrayList;


public class UserService {
    private UserRepo userRepo;
    public UserService(){
        userRepo = new UserRepo(); // creates new object each time when UserService is accessed

    }
    public int add(User user){
        return userRepo.add(user);

    }

    public ArrayList<User> getUsers(){
        return userRepo.getUsers();
    }
}
```

#### UserRepo.java
```java
package com.datorium.Datorium.API.Repo;

import com.datorium.Datorium.API.DTOs.User;

import java.util.ArrayList;

public class UserRepo {

    private ArrayList<User> users = new ArrayList<>();


    public int add(User user){
        users.add(user); // adds user addUser
        return users.size();
    }

    public ArrayList getUsers(){ // not static list
        return users;
    }

}
```
