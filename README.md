### Hello World in WebAssembly with GoLang

Hello world snippet:
```go
package main

import "fmt"

func main() {
	fmt.Println("Hello, world!")
}
```

Compile the go-code with:
```
GOOS=js GOARCH=wasm go build -o hello.wasm
```

HTML snippet (index.html):
```html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="wasm_exec.js"></script>
    <script>
        const go = new Go();
        WebAssembly.instantiateStreaming(fetch("hello.wasm"), go.importObject).then((result)=>{
            go.run(result.instance);
        });
    </script>
</head>
<body> 
    <h1>WebAssembly, hello world!</h1>
</body>
</html>
```

Copy $GOROOT/misc/wasm/wasm_exec.js to working directory.
Looking at the javascript code in vscode gives the message:
```
Complexity is 181 Bloody hell...
```
This is a sign that one should avoid writing programs in javascript;)

To serve the files write:
```
goexec 'http.ListenAndServe(`:8080`, http.FileServer(http.Dir(`.`)))'
```
You need to download the goexec:
```
go get -u github.com/shurcooL/goexec
```

Finally
```
Hello, world!
```
is written in the javascript-console in (e.g.) chrome.

This is the very simplest program you can write in WebAssembly with Golang.