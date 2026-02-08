# Investment Aggregator — Spring Boot

REST API for managing investment accounts and associating assets (stocks), with integration to an external API to retrieve real-time prices.

The project follows good architectural practices, separation of responsibilities, and uses modern technologies from the Spring ecosystem.

---

## Technologies Used

- **Java**
- **Spring Boot**
- **Spring Web**
- **Spring Data JPA**
- **Spring Cloud OpenFeign**
- **Hibernate**
- **MySQL**
- **Maven**
- **JUnit 5 / Mockito**
- **External BRAPI API**

---

## API Routes
### **Users**
POST /v1/users
- Creates a new user in the system.

GET /v1/users
- Returns a list of all registered users.

GET /v1/users/{userId}
- Retrieves a specific user by its identifier.

PUT /v1/users/{userId}
- Updates the data of an existing user.

DELETE /v1/users/{userId}
- Deletes a user by its identifier.

### **Accounts**
POST /v1/users/{userId}/accounts
- Creates a new investment account associated with a specific user.

GET /v1/users/{userId}/accounts
- Returns all investment accounts associated with a specific user.

### **Account Stocks**
POST /v1/accounts/{accountId}/stocks
- Associates a stock with an investment account, storing the quantity owned for that stock.

GET /v1/accounts/{accountId}/stocks
- Returns all stocks associated with a specific account, including calculated investment values.

### **Stocks**
POST /v1/stocks
- Creates a new stock available to be associated with investment accounts.


---

## **Architecture**

- Controller: handles HTTP requests and responses
- Service: contains business logic
- Repository: handles persistence
- DTOs: define input and output contracts
- Entity: represents database model
---

## Data Modeling

### Main entities:

- **Account**
- **Stock**
- **AccountStock** (association table)

### Relationships:

- `Account` **1:N** `AccountStock`
- `Stock` **1:N** `AccountStock`
- `AccountStock` uses a **composite key** (`@EmbeddedId`)

---

## External API Integration (BRAPI)

The external API is consumed via **Feign Client** to fetch the current stock price.

### Usage example:
The total invested value in a stock is calculated dynamically:
- total = quantity × current_price

The API token is configured via an **environment variable**, ensuring security.

```env
BRAPI_TOKEN=your_token_here
```

**Tests**
- Unit tests using JUnit 5
- Dependency mocking with Mockito
- Focus on business rules in the service layer

**How to Execute the Project**
Requirements:
- Java 21+
- Maven
- MySQL
