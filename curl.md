# curl
Options to use as a REST client
* `-s`, `--silent`: Don't show progress meter or error messages.
* `-X`, `--request` <METHOD>: Specifies the request method GET, POST, etc.
* `-H`: Extra header to include in the request.
    * To clear a header use "<header name>:". Example ("Host:")
    * To send a custom header with no value use "<custom-header;>". Example ("X-Custom-Header;").
* `-d`, `--data`: To send data (body) with POST or `params` when used with GET and -G

## Example using GET
`curl -s -X GET 'https://jsonplaceholder.typicode.com/todos'`

# Example using POST
`curl -s -X POST 'https://jsonplaceholder.typicode.com/todos' \
  -H 'Content-Type: application/json' \
  -d '{ "title": "fooBatch", "completed": false, "userId": 1 }'`

# Example using GET with query `params`
`curl -s -X GET -G 'https://jsonplaceholder.typicode.com/todos' \
  -d 'userId=1'`

