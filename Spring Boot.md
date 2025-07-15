 ### 1. What is the difference between `antMatchers()` and `requestMatchers()`?

**Solution:** 

- `requestMatchers()` should be used when we want to apply matching to request URLs only.
- `antMatchers()` should be used when we want to apply matching to all requests including static resources.

Example:

```java
requestMatchers("/**").authenticated()
```
- `requestMatchers(“/**”)` matches all requests but applies to request URLs only. This means that static resources such as CSS, JavaScript, and image files are excluded from the matching and will not require authentication.

``` java
antMatchers(“/**”).authenticated()
```
	
- `antMatchers(“/**”)` matches all requests, including requests to static resources such as CSS, JavaScript, and image files. Therefore, if we use antMatchers(“/**”).authenticated(), even requests to static resources that do not require authentication will be intercepted and require authentication, resulting in a 403 error.
