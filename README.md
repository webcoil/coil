# Coil
`Coil` is a simple HTTP abstraction for Common Lisp.

Inspired by Pump, Ring, WAI, Plug and other interface specifications.

## Summary
Your `app` is just a function that takes a`environment` - a property list with request information and returns a `response` - a property list of three keys `status`, `headers` and `body`. Additional capabilities could be added to app using `middlewares`.

## Specification 

### environment
`environment` is a property list representing web request. In addition, environment may also contain `coil` specific headers prefixed with `coil-`.
```lisp
(:server-port "80"
 :server-name "localhost"
 :headers ( :host "localhost:8000"
            :connection "keep-alive"))
```

### response
`response` is a property list with `status`, `headers` and `body`. 

Value of `status` is one of the http status codes, such as 200, 404, 500, 303 etc. 

`headers` is a property list, with keys and values as string, except for multiple header values, where the value is a list of strings. Applications can send `coil-` prefixed directive headers to web servers, which should not be sent to the client.

`body` should be string, file, list or anything that can be represented by a string.

 ```lisp
 (:status 200
  :headers (:content-type "text/plain")
  :body "Hello")
 ```
### app
`app` is a function that takes `environment` and returns a `response`.
```lisp
(lambda (environment)
  `(:status 200 
    :headers (:content-type "text/plain") 
    :body "Hello, World"))
```
### middleware
`middleware` is a higher order function that adds additional capabilities to the `app`.
```lisp
(lambda (app)
  (lambda (environment)
    (format t "Logged")
    (app environment)))
```
