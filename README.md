# Jax-RX

### Step 1: Set Up IntelliJ IDEA
1. **Download and Install IntelliJ IDEA**: Visit the JetBrains website to download IntelliJ IDEA Community or Ultimate edition based on your preference. Follow the installation instructions for your operating system.

2. **Create a New Java Project**:
   - Open IntelliJ IDEA and select "Create New Project" from the welcome screen.
   - Choose "Java" from the list of project types and click "Next."
   - Configure your project settings (e.g., project name, location) and click "Finish" to create the project.

### Step 2: Add Jersey Dependency
1. **Open `pom.xml`**:
   - In the project view, locate the `pom.xml` file under your project's root directory.
   - Double-click on `pom.xml` to open it in the editor.

2. **Add Jersey Dependency**:
   - Inside the `<dependencies>` section of the `pom.xml` file, add the following dependency for Jersey:

   ```xml
   <dependency>
       <groupId>org.glassfish.jersey.containers</groupId>
       <artifactId>jersey-container-servlet</artifactId>
       <version>2.35</version>
   </dependency>
   ```

   Make sure to save the changes (`Ctrl + S` or `Cmd + S`).

### Step 3: Create a JAX-RS Resource Class
1. **Create a New Java Class**:
   - Right-click on your source folder in the Project view.
   - Choose "New" -> "Java Class" from the context menu.
   - Name the class `HelloWorldResource` and click "OK."

2. **Add Resource Class Code**:
   - Copy and paste the provided `HelloWorldResource.java` code into the newly created class file.

  
### Step 4: Add Additional Methods to HelloWorldResource

```java
import javax.ws.rs.*;
import javax.ws.rs.core.*;

@Path("/hello")
public class HelloWorldResource {

    @GET
    @Produces(MediaType.TEXT_PLAIN)
    public String getHello() {
        return "Hello, World!";
    }

    @GET
    @Path("/{name}")
    @Produces(MediaType.TEXT_PLAIN)
    public String getHelloWithName(@PathParam("name") String name) {
        return "Hello, " + name + "!";
    }

    @POST
    @Consumes(MediaType.TEXT_PLAIN)
    @Produces(MediaType.TEXT_PLAIN)
    public Response postMessage(String message) {
        // Logic to process the received message
        return Response.status(Response.Status.CREATED)
                .entity("Received message: " + message)
                .build();
    }

    @PUT
    @Path("/{id}")
    @Consumes(MediaType.TEXT_PLAIN)
    @Produces(MediaType.TEXT_PLAIN)
    public Response putMessage(@PathParam("id") String id, String message) {
        // Logic to update the message with the given ID
        return Response.ok("Updated message with ID " + id + ": " + message).build();
    }

    @DELETE
    @Path("/{id}")
    @Produces(MediaType.TEXT_PLAIN)
    public Response deleteMessage(@PathParam("id") String id) {
        // Logic to delete the message with the given ID
        return Response.ok("Deleted message with ID " + id).build();
    }
}
```

### Step 5: Test the Additional HTTP Verbs

1. **POST Request**: Use a tool like Postman to send a POST request to `http://localhost:8080/your-app-context/hello` with a plain text message in the request body. You should receive a response indicating that the message was received.

2. **PUT Request**: Similarly, send a PUT request to `http://localhost:8080/your-app-context/hello/{id}` with a plain text message in the request body. Replace `{id}` with an actual ID value. You should receive a response indicating that the message was updated.

3. **DELETE Request**: Send a DELETE request to `http://localhost:8080/your-app-context/hello/{id}`. Replace `{id}` with the ID of the message you want to delete. You should receive a response indicating that the message was deleted.

### Step 6: Configure Jersey Servlet
1. **Create a New Java Class for Configuration**:
   - Right-click on your source folder in the Project view.
   - Choose "New" -> "Java Class" from the context menu.
   - Name the class `AppConfig` and click "OK."

2. **Add Configuration Code**:
   - Copy and paste the provided `AppConfig.java` code into the newly created class file.

3. **Create Servlet Configuration**:
   - Right-click on the `AppConfig` class and select "Create 'AppConfig'".
   - In the dialog, choose "Create Servlet 3.0 'web.xml'" and click "OK."

### Step 7: Run the Application
1. **Run Configuration**:
   - Right-click on the `AppConfig` class.
   - Choose "Run 'AppConfig.main()'".

2. **Verify Application Startup**:
   - Look for console output indicating that the application has started successfully.

### Step 8: Test the RESTful Web Service
1. **Use REST Client**:
   - Open a web browser or a REST client tool like Postman.

2. **Send HTTP Requests**:
   - Send GET requests to `http://localhost:8080/your-app-context/hello` and `http://localhost:8080/your-app-context/hello/{name}` to test the `GET` methods.
   - Send POST, PUT, and DELETE requests to appropriate endpoints to test the corresponding methods.

3. **Verify Responses**:
   - Verify that you receive the expected responses for each request.

