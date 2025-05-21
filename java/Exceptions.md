Methods in java use exceptions to tell the calling code that something bad had occurred, I failed. 

An exception is always thrown back to the caller, the caller must catch it and handle it. 

>If you can't recover from the exception then at least get a stack trace using the `printStackTrace` method.

The compiler checks for everything but `RuntimeExceptions`.

- Runtime exceptions are not checked by the compiler, they're known as unchecked exceptions. I can throw, catch and declare them but I don't have to and the compiler won't check because they are exceptions that are meant to occur during runtime, they are present flaws in my code and the code won't run properly at the present if they're not fixed. 


Try-with-resources exception handling is useful when reading os resources like files. 

If an exception is a runtime exception, I do not have to warn about throwing it on the method declaration.

I don't even have to worry about handling runtime exceptions. 

