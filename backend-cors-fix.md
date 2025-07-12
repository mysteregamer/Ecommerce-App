To fix the CORS issue in your Java backend (assuming Spring Boot), you can add the following configuration:

1. Global CORS configuration using a WebMvcConfigurer bean:

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class WebConfig {

    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/api/**")
                        .allowedOrigins("http://localhost:3001") // your frontend origin
                        .allowedMethods("GET", "POST", "PUT", "DELETE", "OPTIONS")
                        .allowedHeaders("*")
                        .allowCredentials(true);
            }
        };
    }
}
```

2. Alternatively, use @CrossOrigin annotation on your controller class or methods:

```java
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.RestController;

@CrossOrigin(origins = "http://localhost:3001")
@RestController
public class ProductController {
    // your endpoints
}
```

After adding this configuration, restart your backend server. This will allow your frontend running on http://localhost:3001 to access the backend APIs without CORS errors.

Please apply this fix in your backend project in Eclipse and test again.

---

Testing Checklist:

- Frontend:
  - Test product listing page loads products without errors.
  - Test navigation to add product page.
  - Test adding a product successfully.
  - Test navigation back to product list and product appears.

- Backend:
  - Test API endpoints for products (GET, POST).
  - Test CORS headers are present in responses.

Please confirm if you want me to assist with any further frontend or backend testing or improvements.
