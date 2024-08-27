## L33: Flow of data from client to db and file organisation, practical side
1. What business logic contains
2. What is a package
3. What is a module
4. What's behind imports
5. Practical side of using business logic service for API
-----
#### DatoriumApiApplication.java

```java
package com.datorium.Datorium.API;

import com.datorium.Datorium.API.DTOs.Book;
import com.datorium.Datorium.API.DTOs.Credentials;
import com.datorium.Datorium.API.DTOs.User;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.*;

@SpringBootApplication
@RestController
@CrossOrigin
public class DatoriumApiApplication { // Main class (to configure)

	public static void main(String[] args) { // This is the only thing supposed to be here
		System.out.println("asd"); // just for testing
		SpringApplication.run(DatoriumApiApplication.class, args); // initializes Spring application
	}
	
	@GetMapping("/ping")
	public String ping() {
		return "pong";
	}

	@GetMapping("/hello")
	public String hello(@RequestParam(value = "name", defaultValue = "World") String name) {
		return String.format("Hello %s!", name); // "Hello " + name + "!";
	}

	@GetMapping("/getbook") // http://localhost:8080/getbook mapping for endpoint
	public Book getBook(){
		var book = new Book();
		book.title = "book title";
		book.author = "book author";

		return book;

	}

	@PostMapping("/postexample")
	public Book addBook(@RequestBody Book book){
		book.title = book.title.toUpperCase();
		return book;
	}

	// We want user to be able to authorize, by using username and password
	// And then we provide a profile of the user (name, surname, age, email)

	@PostMapping("/authorize")
	public User authorize(@RequestBody Credentials credentials) { // username + password
		if(credentials.username.equals("okklv") && credentials.password.equals("Password123")){
			var user = new User();
			user.name = "Oskars";
			return user;
		}
		return null;
	}

}
```
![08-08](https://github.com/user-attachments/assets/59efdfbb-1086-4d5c-8d04-0ccad21bc871)

import of outside packages --> folder with classes  
Module - functions

MODULE (packages inside)  
Package - classes inside  
Package - classes inside  
Package - classes inside  

Separate module for API, data, controller etc.

#### UserController.java

```java
package com.datorium.Datorium.API.Controllers; // belongs to package created

import org.springframework.web.bind.annotation.GetMapping; // importing outside packages
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/user")
public class UserController {
    //CRUD
    //AddUser
    //UpdateUser
    //GetUser
    //DeleteUser

    @GetMapping("/test") //localhost:8080/test -> localhost:8080/user/test
    public String test(){
        return "testy testy";
    }
}
```
Dependency injection -->  
Dependency Injection (DI) is a design pattern in Java (and other programming languages) that helps to decouple the creation of objects from their usage. It is a form of Inversion of Control (IoC), where the control of creating objects and managing dependencies is shifted from the class itself to an external framework or container.

E.g. Constructor Injection: Dependencies are provided through the class constructor.

#### UserController.java


```java
package com.datorium.Datorium.API.Controllers;

import com.datorium.Datorium.API.DTOs.User;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/user")
public class UserController {

    private UserService _userService;
    public UserController(){
        
    }
    //CRUD
    //AddUser
    //UpdateUser
    //GetUser
    //DeleteUser

    @GetMapping("/add") //localhost:8080/test -> localhost:8080/user/test
    public int add(@RequestBody User user){

    }
}
```
#### UserService.java

```java
package com.datorium.Datorium.API.Services;

import com.datorium.Datorium.API.DTOs.User;


public class UserService {

    public int add(User user){
        return 0;
    }
}
```

POST in Postman

{
    "username": "okklv",
    "password": "Password123"

}

#### FINAL
----

#### Controllers --> UserController.java

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

#### Services --> UserService.java

```java
package com.datorium.Datorium.API.Services;

import com.datorium.Datorium.API.DTOs.User;

public class UserService {

    public int add(User user){
        return 0;
    }
}
```

WE ARE CONNECTING CONTROLLERS TO SERVICE AT THE MOMENT.

ENDPOINT -->  
A specific path where a particular resource or set of operations can be accessed. It usually corresponds to an HTTP method (like GET, POST, PUT, DELETE) combined with a URL.  
An endpoint in Java refers to a specific URL or URI that represents a point of interaction for a client to access a resource or service

#### TEAMWORK
----------

1. Create MessageController.java  
2. Create MessageService.java  
3. Create Message.java --> DTO  
4. In message controller, create an endpoint, which uses both MessageService and Message.java  
5. HELP YOUR TEAMMATES TO GET EVERYTHING WORKING pls (including UserController/Service etc)  
-----

**Payload** is a part of web request, where it's possible to put data. Usually in JSON format, but it can come in various formats. Including byte array (images, songs etc.)

**POST method** is a WEB API request method, used to send data by using http.

Usually in databases passwords are saved in **hashed format**, just so if a hacker get's into the database, then it's not possible to immediately access every account



