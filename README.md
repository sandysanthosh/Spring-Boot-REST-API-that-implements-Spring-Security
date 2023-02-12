# Spring-Boot-REST-API-that-implements-Spring-Security

```
@RestController
@RequestMapping("/api")
public class ExampleController {

  @GetMapping("/protected")
  public ResponseEntity<String> protectedEndpoint() {
    return ResponseEntity.ok("Access granted to protected endpoint");
  }
}

@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

  @Override
  protected void configure(HttpSecurity http) throws Exception {
    http
        .authorizeRequests()
        .anyRequest().authenticated()
        .and()
        .httpBasic();
  }

  @Autowired
  public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {
    auth
        .inMemoryAuthentication()
        .withUser("user")
        .password("{noop}password")
        .roles("USER");
  }
}


```

In this example, all requests to the /api/protected endpoint are protected and require basic authentication. 

The configureGlobal method sets up an in-memory user with the username user and password password, and the configure method sets up basic authentication for all requests.


#### To test this in Postman, you can follow these steps:
```
Create a new request in Postman

Choose the GET method

Enter the URL of your endpoint (e.g. http://localhost:8080/api/protected)

In the Authorization tab, choose the Basic Auth type and enter the username and password for the in-memory user (e.g. user and password)

Send the request
```
If the credentials are correct, you should receive a 200 OK response with the message Access granted to protected endpoint.

If the credentials are incorrect, you should receive a 401 Unauthorized response.
