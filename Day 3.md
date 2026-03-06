# Day 3 – CRUD Operations using Spring Boot and Postman

## Overview
On Day 3, we continued developing the **Product Management System** using **Spring Boot**.  
The focus of this session was understanding and implementing **CRUD operations** and testing APIs using **Postman**.

The application follows a **layered architecture** commonly used in Spring Boot projects.
Controller → Service → DAO → Repository → Model → Application


Each layer has a specific responsibility:
- **Controller** – Handles HTTP requests and responses.
- **Service** – Contains business logic.
- **DAO (Data Access Object)** – Communicates with the repository.
- **Repository** – Interacts with the database using Spring Data JPA.
- **Model** – Represents the database entity.

---

# Project Structure
```

com.pratap
│
├── controller
│ └── ProductController.java
│
├── service
│ └── ProductService.java
│
├── dao
│ └── ProductDao.java
│
├── repository
│ └── ProductRepository.java
│
├── model
│ └── Product.java
│
└── PmsApplication.java

```
---

# Controller Layer

`ProductController.java`

The controller handles incoming HTTP requests from the client.

## Features
- Fetch all products
- Add new products

```java
package com.pratap.controller;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import com.pratap.model.Product;
import com.pratap.service.ProductService;

@RestController
@RequestMapping("/Product")
public class ProductController {

    @Autowired
    ProductService service;

    @GetMapping("/getProduct")
    public List<Product> getProduct() {
        return service.getProduct();
    }

    @PostMapping("/addProduct")
    public List<Product> addProduct(@RequestBody List<Product> product) {
        return service.addProduct(product);
    }
}
```
Service Layer

ProductService.java

The service layer contains the business logic and communicates with the DAO layer.
```java
package com.pratap.service;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.pratap.dao.ProductDao;
import com.pratap.model.Product;

@Service
public class ProductService {

    @Autowired
    ProductDao dao;

    public List<Product> getProduct() {
        return dao.getProduct();
    }

    public List<Product> addProduct(List<Product> product) {
        return dao.addProduct(product);
    }
}
```
DAO Layer

ProductDao.java

The DAO layer interacts with the repository layer to access the database.
```java
package com.pratap.dao;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Repository;

import com.pratap.model.Product;
import com.pratap.repository.ProductRepository;

@Repository
public class ProductDao {

    @Autowired
    ProductRepository repo;

    public List<Product> getProduct() {
        return repo.findAll();
    }

    public List<Product> addProduct(List<Product> product) {
        return repo.saveAll(product);
    }
}
```
Repository Layer

ProductRepository.java

This interface communicates with the database using Spring Data JPA.

Note: No changes were required in this file.

Model Layer

Product.java

This class represents the Product entity and maps to the Product table in MySQL.

Note: No modifications were required.

Running the Application

Start the Spring Boot application from:

PmsApplication.java
Testing API using Postman
Step 1

Open Postman

Step 2

Select:
```
Method: POST
URL: http://localhost:8080/Product/addProduct
```
Step 3

Go to:

Body → Raw → JSON

Example JSON data:
```json
[
  {
    "Category": "hello",
    "Description": "123",
    "inStock": true,
    "name": "Laptop",
    "price": 55000,
    "stockQuantity": 10
  },
  {
    "Category": "hello",
    "Description": "4356",
    "inStock": true,
    "name": "Laptop",
    "price": 55000,
    "stockQuantity": 10
  },
  {
    "Category": "hello",
    "Description": "john",
    "inStock": true,
    "name": "Laptop",
    "price": 55000,
    "stockQuantity": 10
  }
]
```
Explanation

@RequestBody converts JSON data into Java objects automatically.

Verifying Data in MySQL

Open MySQL and run:
```
use ProductManagementSystem;

select * from Product;
```
This will display the products inserted using the API.

Learning Outcome

By completing this task, I learned:

- Implementation of CRUD operations in Spring Boot
- Understanding of layered architecture
 - Sending JSON data using Postman
- Using @RequestBody for request data mapping
- Storing and retrieving data from MySQL database

Tools & Technologies

Java
Spring Boot
Spring Data JPA
MySQL
Postman
Maven


✅ You can **save this as `README.md`** and upload it to your GitHub repository.

If you want, I can also help you create a **professional GitHub README with badges, API endpoints table, and screenshots** so your project looks **much more impressive for recruiters.**
