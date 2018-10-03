This wiki documents the basic usage of API implemented.

We use [API-Platform](https://api-platform.com/) for API access and [lexik/jwt-authentication-bundle](https://github.com/lexik/LexikJWTAuthenticationBundle/blob/master/Resources/doc/index.md#installation) for JWT token authentication.

Swagger: https://gettingmarried.ampdev.co/api/

# Authentication

Demo: http://recordit.co/Pnb2D1CPUv

```bash
$ curl -X POST -H "Content-Type: application/json" \
  https://gettingmarried-local.ampdev.co/api/login_check \
  -d '{"username":"admin","password":"admin"}'

{"token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE1Mzg0NzA3OTQsImV4cCI6MTUzODQ3NDM5NCwicm9sZXMiOlsiUk9MRV9TVVBFUl9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6ImFkbWluIn0.hY0138l1Xz_UFyL_qI7TcKzjCNh2rltFIxBuXdTZRrUT2HnvOkSYyjPF8QAg0epO-84dgpuvEHstNH3VXCp0o4pbEsBJjRUY7549YWS1icFYO1R-LsJjoyE7gxQU90f6znWI-6FXe-siJb10jx1108CMhG9h1AHeTBeiEI1wi0BFhhxmgbwmBwJBxpR05AWSuP9pHx94FW6FvnZORSHSZNaSPFfakhX2fNo80pZJzNuRwaD7k3vOjKFue8vQRXhR36TAJgiyhcDwF9cIB8AXpKkFh1UewP9DboJh5zjOcv-f_-gxntBWglUBN3qBUWZ-3VkYFoT1NpdlVtWKq3wQyUAHpq2hkXfnZMRWG9po4TvKZainXV1VAbK-q4FoDNplBpUwYXo6qyCTA8Aqtj7EIc436Ei37m23nW11zuqFFmFaGHimxBfsIwlD2Wy4U7CgXdZfBG0uIXXwHQFef-IQrzHHkRo_icb31D-q11TUfVuc53VOzgzx0TLh0iV3qphJYaBMhaO83qWQvGxeyLcQQCyhu88sSicz7hs0PDBZh7Twm31dtN9hINA2RqPL2_oMiTmLjvVWPoKwUO5lhoetJlOq09CFgnkvkOcXILYK4gmwXiwRNOx9rdAwO6vzqPYH4Y2KjaPU9g-Hmbh6zl1Q5Evur9HcF2cj27rZCjI0SbA"}
```

Use token on request for single sign on (SSO):

```bash
$ curl -X GET -H "Accept: application/json" \
  -H "Authorization: Bearer {token}" \
  https://gettingmarried-local.ampdev.co/api/weddings

[{"id":1,"users":[{"id":1,"wedding":"\/api\/weddings\/1"},{"id":2,"wedding":"\/api\/weddings\/1"}],"weddingEvents":...
```

Replace `{token}` with the token value `eyJ0eXAiO...` returned from auth request