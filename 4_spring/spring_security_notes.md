### Spring security 

#### Form based security 
- After adding spring security starter pom, rest call asks for username & password (form based authentication) - From bowser
- Grab password from console. (Default username - user)
- to logout/kill from session - `localhost:8080/logout`

#### Basic Auth 
- Client sends request - username:password in header base64 encoded
- If auth fails - HTTP 401 
- To implement basic auth
```
@Configuration
@EnableWebSecurity
public class ApplicationSecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
                .authorizeRequests()
                .anyRequest()
                .authenticated()
                .and()
                .httpBasic();
    }

}
```

- Now, If you restart the app, Pop up appears in browser 
- If you enter - username & password (copied from console), Authentication will be performed
- No `localhost:8080/logout` is present. As username and password is apllied on every single request
- Postman - Select basicAuth
- To **whitelist** URL - Example index.html. Use `antMatchers()`
```
  @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
                .authorizeRequests()
                .antMatchers("/", "index", "/css/*", "/js/*")
                .anyRequest()
                .authenticated()
                .and()
                .httpBasic();
    }
```

### Application Users
- Users 
    - Must have username & It should be unique
    - Encoded password
    - Role/s 
    - Authorities (?) 
    - and more.. 
- Override - `protected UserDetailsService userDetailsService()`
    - This has many implementations - `CachingUserDetailsService, InMemoryUserDetailsService, JdbcDaoImpl, JdbcUserDetailsManager, UserDetailsManager`
    - In below example - `InMemoryUserDetailsManager` is used
- Password encoder
    - Declare bean & autowire it. (Otherwise - Logs password does not look like BCrypt)
    - Most popular - BCryptPasswordEncoder
```
 @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder(10);
    }
```
- ROLES 
    - ROLES has 0-n permissions
    - Refer ApplicationUserRole enum & ApplicationUserPermission
    - URL based role based auth - `.antMatchers("/api/**").hasRole(STUDENT.name()).antMatchers("/api/**").hasRole(STUDENT.name())`
    - Permission based Auth -     
```

@Configuration
@EnableWebSecurity
public class ApplicationSecurityConfig extends WebSecurityConfigurerAdapter {

    private final PasswordEncoder passwordEncoder;

    @Autowired
    public ApplicationSecurityConfig(PasswordEncoder passwordEncoder) {
        this.passwordEncoder = passwordEncoder;
    }

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
                .authorizeRequests()
                .antMatchers("/", "index", "/css/*", "/js/*").permitAll()
                .permitAll() // For above path, permit all 
                .anyRequest()
                .authenticated()
                .and()
                .httpBasic();
    }

    @Override
    @Bean
    protected UserDetailsService userDetailsService() {
        UserDetails annaSmithUser = User.builder()
                .username("annasmith")
                .password(passwordEncoder.encode("password")) //
                .roles(STUDENT.name()) // ROLE_STUDENT
                .build();

        UserDetails lindaUser = User.builder()
                .username("linda")
                .password(passwordEncoder.encode("password123"))
                .roles(ADMIN.name()) // ROLE_ADMIN
                .build();

        UserDetails tomUser = User.builder()
                .username("tom")
                .password(passwordEncoder.encode("password123"))
                .roles(ADMINTRAINEE.name()) // ROLE_ADMINTRAINEE
                .build();

        return new InMemoryUserDetailsManager(
                annaSmithUser,
                lindaUser,
                tomUser
        );

    }
}
```

```
public enum ApplicationUserPermission {
    STUDENT_READ("student:read"),
    STUDENT_WRITE("student:write"),
    COURSE_READ("course:read"),
    COURSE_WRITE("course:write");

    private final String permission;

    ApplicationUserPermission(String permission) {
        this.permission = permission;
    }

    public String getPermission() {
        return permission;
    }
}

public enum ApplicationUserRole {
    STUDENT(Sets.newHashSet()),
    ADMIN(Sets.newHashSet(COURSE_READ, COURSE_WRITE, STUDENT_READ, STUDENT_WRITE)),
    ADMINTRAINEE(Sets.newHashSet(COURSE_READ, STUDENT_READ));

    private final Set<ApplicationUserPermission> permissions;

    ApplicationUserRole(Set<ApplicationUserPermission> permissions) {
        this.permissions = permissions;
    }

    public Set<ApplicationUserPermission> getPermissions() {
        return permissions;
    }
}
```
 
### CSRF

- When PUT or POST, API fails with 403 forbidden 
- `csrf().disabled` - Now PUT , POST will work.
  
```
 @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
                .csrf().disabled
                ---
                ;
    }
```
- Permission based auth
  - `antMatchers(HttpMethod.DELETE, "/management/api/**").hasAuthority(ApplicationUserPermission.COURSE_WRITE.name())
    .antMatchers("/management/api/**").hasAnyRole(ADMIN.name(), STUDENT.name())`
  -
- Adding authorities to ROLE
  - 
```
 @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
                .csrf().csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse())
                .httpBasic();
    }
```
