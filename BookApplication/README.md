# BookApplication

Simple Spring Boot application to manage a small book inventory using MongoDB.

## Technologies

- Java 17 (toolchain configured in Gradle)
- Spring Boot 3.5.5
- Spring Web (REST / MVC)
- Spring Data MongoDB
- Thymeleaf (server-side templates)
- Lombok (compile-time)
- Gradle (build tool)
- Bootstrap (frontend styling)

## Project structure (important folders)

- src/main/java - application sources
  - com.book.inventory.app.controller - Spring MVC controllers
  - com.book.inventory.app.domain - domain model (Book)
  - com.book.inventory.app.repo - Spring Data Mongo repository
- src/main/resources/templates - Thymeleaf templates (views)
- src/main/resources/static - static assets (JS/CSS/HTML used as static pages)
- build.gradle - project build and dependencies

## Dependencies

Main dependencies are declared in build.gradle (excerpt):

- org.springframework.boot:spring-boot-starter-web
- org.springframework.boot:spring-boot-starter-thymeleaf
- org.springframework.boot:spring-boot-starter-data-mongodb
- org.projectlombok:lombok (compileOnly + annotationProcessor)
- org.springframework.boot:spring-boot-devtools (developmentOnly)

Gradle will fetch these from Maven Central.

## Prerequisites

- Java 17 JDK installed
- Gradle wrapper is included (no global Gradle required)
- MongoDB server running and accessible (default: localhost:27017)

Notes about MongoDB configuration:
- By default Spring Boot's MongoDB auto-configuration will attempt to connect to localhost:27017.
- If your MongoDB is remote or requires authentication, set the connection string in
  `src/main/resources/application.properties` or via environment variables, e.g.: 

  spring.data.mongodb.uri=mongodb://username:password@host:port/database

## How to run

1. Start MongoDB (if not already running).
2. From the project root run using the included Gradle wrapper:
   - Run application in development mode:
     ./gradlew bootRun

   - Build runnable jar and run:
     ./gradlew bootJar
     java -jar build/libs/*.jar

3. Access the application in a browser at http://localhost:8080/

## Important endpoints (UI)

- GET /           -> Home (index)
- GET /addBook    -> Show add-book form (Thymeleaf template)
- POST /addBook   -> Submit form to create a Book (controller handles POST)
- GET /search     -> Search form
- POST /search    -> Search action
- GET /deleteBook -> Delete form
- POST /deleteBook-> Delete action
- GET /info       -> Info page (counts and totals)

Troubleshooting: if you see a "405 Method Not Allowed" when submitting a form, check that:
- Your form's `action` points to a controller endpoint (for example `/addBook`) and not to a static HTML file like `/addbook.html`.
- The controller has a matching @PostMapping for that endpoint.
- If you use a static page in `src/main/resources/static`, it will be served directly by the server and won't accept POST unless a controller handles that path.

## Tests

Run unit/integration tests with:

./gradlew test

## Notes

- Templates that use Thymeleaf attributes (th:*) must be placed under `src/main/resources/templates` so Spring's ThymeleafViewResolver can process them. Static HTML files under `src/main/resources/static` are served as-is and will not have server-side processing applied.
- If you add new Lombok-annotated classes and your IDE shows missing members, ensure annotation processing is enabled in the IDE.

If you want, I can also add example Docker configuration for MongoDB and the app, or update the application.properties with a sample connection string. Let me know which option you prefer.
