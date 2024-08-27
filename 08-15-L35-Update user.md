## L35: Update user
1. Updating pre-added user
----

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
        return userService.get();
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

    public ArrayList<User> get(){
        return userRepo.get();
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


    public int add(User user){ // User - type; user - variable you provide in method
        users.add(user); // adds user addUser
        return users.size();
    }

    public ArrayList<User> get(){
        return users;
    }

}
```
*Method in UserService and UserController - better to have the same name.*

*We will use idex as an Array List*

**DTO** --> Data Transfer Object  
Transfers data from one layer to other  
Entity is like template for object  

Instead of updating user ourselves - User object, later in Repo, will be transferred to real object that is in database

Each layer has a similar method and they are daisy-chaining to get the DTO from one end to the other

It is like a temporary instance of the User class. It's only purpose is to carry the info needed to update a 'real' instance of User (ie a user that is registered in our list). The usefulness of putting info needed to update a User instance in the same format is evident.

![08-15-Screenshot 2024-08-15 185708](https://github.com/user-attachments/assets/77497c33-3cdf-4a60-b59b-a8c04e5a8806)

------
*To update an entity in database, we must use DTO that comes from payload  
DTO stands for data transfer object, an object, that transfers data from frontend to backend  
Database server IS NOT the same as repository server*  

#### TEAMWORK
------------

*Helsinki university offers a few free online courses:  
https://cybersecuritybase.mooc.fi/ 
java and python courses are both really good*
