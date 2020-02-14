# spring-data-transactions

## Why Transaction Management ?

- This ensures data consistency and integrity.

### Types of Transactions

- Global Transactions
  - Typically this is managed at the server level.
  - This is used to manage multiple resources.
    - For Example, Message Queue, Relational Databases and more.
- Local Transactions
  - They are specifically related to a single resource.

## Why Spring Framework for Transaction management?

- Spring allows the the developer to manage the transactions using two different approaches:
  - Programmatic Approach
    - Developer writes custom code for this one.
  - Declarative Approach
    - Its taken care by the framework and its not part of the business logic code thats written by the developer.

## Handling Transactions using Declarative Approach - Using @Trasnsactional

### How it works ?

- Spring uses AOP behind the scenes to enable transaction management
- A proxy is created to hold the Transaction management code. There are four proxies:
  - EntityManager Proxy
    - Manages the entities that live in the data base
  - Persistence Context Proxy
    - Database transaction happens inside a persistence context
    - This is defined in Jpa.
    - This handles a set of entities that contain data to be persisted
    - This takes care of tracking and persisting the entities
  - Transactional Aspect
    - Manages the transaction for any method thats annotated with @Transactional
    - The Transaction interceptor basically intercepts the calls to the method thats annotated with @Transactional
    - This is invoked before and after the method call.
    - Two Main Responsibilities:
      - Determines if new transaction is needed.
      - Determines to Commit, rollback or leave
  - Transactional Manager
    - It uses Spring Platform Transaction Manager which is basically the **JPATransactionManager**
    - This is responsible for providing Begin, Commit and Rollback

### How to enable Transactions logging?

```
logging.level.org.springframework.transaction.interceptor=TRACE
```

-  Additional Logging

```
spring.jpa.show-sql: true
logging.level.org.hibernate.SQL: debug
logging.level.org.hibernate.type.descriptor.sql: trace
```

## Entity Manager vs DataBase Transaction vs Persistence Context

- EntityManager
  - This basically manages all the entities of your app.
  - Each entity will have its own EntityManager.
  - The EntityManager is the instance that takes care of interacting with the persistence context.
  - EntityManagerFactory holds the factory of EntityManager
- Persistence Context
  - This is defined in Jpa.
  - This handles a set of entities that contain data to be persisted
  - This takes care of tracking and persisting the entities
- DataBase Transaction  
  - @Transaction defines a single transaction in the scope of a persistence context.
  - Each EntityManager is associated with the persistence context
