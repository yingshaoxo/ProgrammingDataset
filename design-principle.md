1. Use a database to save users data is better than using a JSON file (JSON was meant to be used in server-client communication)

2. Make things done, don't let mess continuous. Also, never let a project(repository) unfinished.

3. If you could design a package with binary, don't do it with codes (unless it can compile to binary, like c, c++, golang, cython). You will gradually know that only binary file could be used at every platform or machine without much worry.

4. Write logs for your application instead of just print it out: the logs must contain every information from program start to program end.

5. Write tests for every function in your application. You don't want to check those function again and again by yourself. Just let the machine do that job for you. 