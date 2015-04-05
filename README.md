# coil
Web application interface for Common Lisp.

Inspired by WSGI, Rack, Plack, Ring, WAI, Plug and other interface specifications.

## Application

A `coil` application is a function, that takes single argument `environment` and returns a list of `status`, `headers` and `body`.

```lisp
(lambda (environment)
  `(200 (:content-type "text/plain") "Hello, World"))
```
### environment

`environment` is a property list of CGI-like headers such as `REQUEST_METHOD`, `SCRIPT_NAME`, `PATH_INFO`, `QUERY_STRING`, `SERVER_NAME`, `SERVER_PORT`, `HTTP_ Variables` etc. In addition, environment may also contain `coil` specific headers prefixed with `coil-`.

### response

#### status
Is one of the http status codes, such as 200, 404, 500, 303 etc.

#### headers
Is a property list, with keys and values as string, except for multiple header values, where the value is a list of strings. Applications can send `coil-` prefixed directive headers to web servers, which should not be sent to the client.

#### body
Should be string, file, list or anything that can be represented by a string.
