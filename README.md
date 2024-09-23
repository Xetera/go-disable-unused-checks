Hate commenting out unused variables and then having to comment out the import it was using (that's now also unused) just to print a different variable for testing? Same here.

Sadly we need to fork the compiler and build it from source with patches just to get it to do the reasonable thing. Go doesn't have a concept of compiler warnings so this patch removes all mentions of unused variables entirely instead of turning them into warnings.

I'd only recommend this for development / prototyping.
It's helpful to have a standard go compiler in CI to catch any potential unused variable mistakes since the error is in there for a good reason... when building for production.

![image](https://github.com/user-attachments/assets/6e5fe848-aac5-4272-884e-ee68dcb54207)

(A proudly unused 🅱️ with no errors)

# Installing

1. Clone the [go compiler](https://github.com/golang/go)
2. Figure out if you're gonna blindly copy paste the command below or check the file first. It's not being piped into `bash` or anything, what's the worst that can happen right?
3. Apply the patches `curl -L https://raw.githubusercontent.com/Xetera/go-disable-unused-checks/refs/heads/main/bettergo.patch -o - | git apply --ignore-whitespace`
5. Follow the rest of the instructions to build it from source. Good luck, you'll need it.

## Tooling

If you don't want underlines for unused variables in your editor you'll also need to fork gopls. Thankfully once you've done the work of building the compiler, gopls builds incredibly quick so this is an easy step.

1. Clone [gopls](https://github.com/golang/tools.git)
2. `cd gopls && go build -o gopls`
3. If using vscode, update settings.json to point to the new alternate binaries. If you're using something else I'm sure there's a different way to swap out the language server.
```json
// settings.json
{
  "go.alternateTools": {
    "gopls": "/home/you/tools/gopls/gopls",
    "go": "/home/you/goroot/bin/go"
  }
}
```
