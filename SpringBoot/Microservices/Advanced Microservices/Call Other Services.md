### 1.RestTemplate
![[Pasted image 20251007153830.png]]
![[Pasted image 20251007151447.png]]
## 1️⃣ **RestTemplate Methods**

`RestTemplate` is synchronous and blocking. Some common methods:

|Method|Usage|Returns|
|---|---|---|
|`getForObject(String url, Class<T> responseType, Object... uriVariables)`|GET request|Directly returns the response body mapped to `responseType`|
|`getForEntity(String url, Class<T> responseType, Object... uriVariables)`|GET request|Returns `ResponseEntity<T>` (body + status + headers)|
|`postForObject(String url, Object request, Class<T> responseType, Object... uriVariables)`|POST request|Returns the response body|
|`postForEntity(String url, Object request, Class<T> responseType, Object... uriVariables)`|POST request|Returns `ResponseEntity<T>`|
|`put(String url, Object request, Object... uriVariables)`|PUT request|No return (void)|
|`delete(String url, Object... uriVariables)`|DELETE request|No return|
|`exchange(String url, HttpMethod method, HttpEntity<?> requestEntity, Class<T> responseType)`|Any HTTP method|Returns `ResponseEntity<T>` (most flexible)

### 2.WebClient
- Add webflux dependency
![[Pasted image 20251007152157.png]]

## 2️⃣ **WebClient Methods**

`WebClient` is reactive and non-blocking. Common patterns:

| Method                  | Usage                                | Returns                 |
| ----------------------- | ------------------------------------ | ----------------------- |
| `.get()`                | Start GET request                    | `RequestHeadersUriSpec` |
| `.post()`               | Start POST request                   | `RequestBodyUriSpec`    |
| `.put()`                | Start PUT request                    | `RequestBodyUriSpec`    |
| `.delete()`             | Start DELETE request                 | `RequestHeadersUriSpec` |
| `.retrieve()`           | Execute and prepare to extract body  | `ResponseSpec`          |
| `.bodyToMono(Class<T>)` | Extract single object                | `Mono<T>`               |
| `.bodyToFlux(Class<T>)` | Extract list/stream                  | `Flux<T>`               |
| `.exchangeToMono(...)`  | Low-level access to `ClientResponse` | `Mono<T>`               |
