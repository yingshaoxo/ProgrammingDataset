# Design Principle

## Important

* Make things done, don't let mess continue. Also, never let a project\(repository\) staying on unfinished.
* Use `assert` whenever you can. Because you'll never know if it's what you think unless you give it a check.
* Write tests for every function in your application. You don't want to check those functions again and again by yourself. Just let the machine do that job for you.
* Use a database to save users' data is better than using a JSON file \(JSON was meant to be used in server-client communication.\)

## Less important

* If you could design a package with binary, don't do it with codes \(unless it can compile to binary, like c, c++, golang, cython, rust\). You will gradually know that only binary files could be used at every platform or machine without too much worry about dependencies.
* Write logs for your application instead of just print it out: the logs must contain every information from the program start to program end.
* Use `Pipe` for multiprocessing communication, use `queue` for multithreading communication.

