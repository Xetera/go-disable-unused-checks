Hate commenting out unused variables and then having to comment out the import it was using (that's now also unused) just to print a different variable for testing? Same here.

Sadly we need to fork the compiler and build it from source with patches just to get it to do the reasonable thing. Go doesn't have a concept of compiler warnings so this patch removes all mentions of unused variables entirely instead of turning them into warnings.

I'd only recommend this for development / prototyping.
It's helpful to have a standard go compiler in CI to catch any potential unused variable mistakes since the error is in there for a good reason... when building for production.

![image](https://github.com/user-attachments/assets/994c0528-e772-4051-b2f8-45aafe6d6b12)

# Installing

1. Clone the [go compiler](https://github.com/golang/go)
2. Figure out if you're gonna blindly copy paste the command below or check the file first. It's not being piped into `bash` or anything, what's the worst that can happen right?
3. Apply the patches `curl -L https://raw.githubusercontent.com/Xetera/go-disable-unused-checks/refs/heads/main/bettergo.patch -o - | git apply --ignore-whitespace`
4. Follow the rest of the instructions to build it from source. Good luck, you'll need it.
