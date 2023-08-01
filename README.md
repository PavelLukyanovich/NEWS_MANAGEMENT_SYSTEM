## News management system

To be realized: RESTfull web-service whit management control system for news and comments.

> ### Main entities:
> - ***news*** (contains: id, title, text, time, commentList)
> - ***comment*** (contains: id, userName, text, time, newsId)

### Requirements:

1. Use Spring Boot 3.x, Java 17, Gradle, PostgreSQL.
2. Develop API according to REST approaches:
   - CRUD for *news*
   - CRUD for *comment*
   - View news list with pagination
   - View news with own comments with pagination
   - Full text search for different parameters for news and comments
3. Place project on public git-repository
4. Code should be easy to read, use design patterns 
5. Realize connection to database with Spring @Profile (e.g test & prod)
6. Plug in Liquibase:
   - Scripts for production database put on when application is starting (tables are generating from one file and fill from another file)
   - Script for test database should execute when tests starting (third file)
7. Develop cache realization for save entities. Implement two algorithms **LRU** & **LFU**. **Algorithm** and **size** of collection should be reading from **application.yml** file
   - #### Algorithm for cache:
         - GET - look for in cache, else if no data, get from dao, save in cache and return
         - POST - save in dao, after than save in cache
         - DELETE - remove from dao, after than remove from cache
         - PUT - update/insertion in dao, after than update/insertion in cache
8. All code should be cover with unit-tests - 80%, service layer - 100%
9. Implement logging request-response with aspect stile (for controller layer), and also implement logging levels of application for the different layers of application using *logback*
10. Implement exception handling and interpret it according to the REST
11. All settings should be in .yml files
12. Code should be documented with @JavaDoc, and application properties, application description should be represented in README.md
13. Use Spring REST Docs or other tools automatic documentation for example *Swagger* or else (OpenAPI 3.0)
14. Use *testconteiners* in test for persistent layer
15. Develop integration tests
16. Use *WireMock* in tests for *client* layer
17. Use *Docker* (write Dockerfile - for Spring boot app, docker-compose.yml for up database and app in containers, set up relation among it)
### Additional tasks:
1. Switch up Redis cache provider in docker (@Profile to switching LRU/LFU/Redis)
2. Spring Security:
   - API for registering users with roles admin/journalist/subscriber
   - Administrator (role admin) can perform CRUD operations on all entities
   - Journalist (role journalist) can add and modify/delete only their news items
   - Subscriber (role subscriber) can add and modify/delete only their comments
   - Unregistered users can only view news and comments
   - Create a separate microservice with a relational database (postgreSQL) storing user/role information.
     From the main microservice (responsible for news) to request this information via REST using spring-cloud-
     feign-client.
3. Set up Spring Cloud Config (put into a separate service and customize the service under development to receive them depending on the profile
   )
4. Implementation of logging and exception handling should be placed in separate
   spring-boot-starters
5. Web interface entities (DTO) should be generated when building the project from .proto files (see https://github.com/google/protobuf-gradle-plugin)


