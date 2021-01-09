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
```zsh
GOOS=js GOARCH=wasm go build -o main.wasm
```

HTML snippet:
```html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="wasm_exec.js"></script>
    <script>
        const go = new Go();
        WebAssembly.instantiateStreaming(fetch("main.wasm"), go.importObject).then((result)=>{
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

```zsh
goexec 'http.ListenAndServe(`:8080`, http.FileServer(http.Dir(`.`)))'
```

Finally
```zsh
Hello, world!
```

is written in the javascript-console in (e.g.) chrome.