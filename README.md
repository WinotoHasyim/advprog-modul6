# AdvProg-Modul6

> #### Winoto Hasyim - 2206025243 - Pemrograman Lanjut B

## Module 6 - Pemrograman Lanjut 2023/2024 Genap

### Commit 1 Reflection notes

#### What does `handle_connection` do?

0. We import `std::io::prelude` and `std::io::BufReader` to use features that help in reading from and writing to the network stream.

1. In the `handle_connection` function, mutable reference to the `stream` are wrapped with the help of a new `BufReader` instance.

2. A variable named `http_request` is created to read the incoming request line by line and collect these lines into a vector.

3. If there’s an error while reading (like invalid data or a problem with the stream), the program stops.

4. The browser signals the end of an HTTP request by sending two newline characters in a row. The function reads lines until it gets an empty line, which signifies the end of the HTTP headers.

5. The function prints out the contents of `http_request`.

### Commit 2 Reflection notes

#### What does the new `handle_connection` do?

The `handle_connection` function now reads the contents of an HTML file and includes it in the HTTP response. 

1. Firstly, we prepare an HTTP response. It starts with a status line indicating a successful response (`HTTP/1.1 200 OK`).

2. The `contents` variable reads the contents of the file `hello.html` into a string.

3. After that, we try to get the contents' length, which will be used to set the `Content-Length` header in the HTTP response.

4. The function then creates the full HTTP response. It includes the status line, a Content-Length header indicating the size of the response body, and the contents of `hello.html` as the body of the response.

5. Finally, the function writes the response to the `TcpStream`.

![Commit 2 screen capture](/assets/images/commit2.png)

### Commit 3 Reflection notes

#### How to split between response

To split between responses based on what the request looks like, we use the `if` and `else` blocks.

1. Make a variable to read the first line of the HTTP request. The first `unwrap` handles the `Option` returned by `next`. This `unwrap` will stop the program if the iterator has no items. The second `unwrap` handles the `Result` returned by `lines`.

2. The function then checks if the request line is a `GET` request for the root path (`/`). If it is, it sets the `status_line` to `HTTP/1.1 200 OK` and `filename` to `hello.html`. If it doesn't, it sets the `status_line` to `HTTP/1.1 404 NOT FOUND` and `filename` to `404.html`.

3. After that, the function reads the contents of the file specified by `filename` into a string. It then creates the full HTTP response, including the `status_line`, a `Content-Length` header indicating the size of the response body, and the file contents as the body of the response.

4. Finally, the function writes the response to the `TcpStream`.

![Commit 2 screen capture](/assets/images/commit3-1.png)

#### Why do we refactor

In the `handle_connection` function above, the `if` and `else` blocks have a lot of repetition. Notice that the only thing that differentiates between the two blocks are the status line and the filename. Thus, we can refactor the code so that we use the `if` and `else` blocks only to assign values of the status line and the filename. The contents of the response will be based on the status line and the filename that has already been assigned by a value.

![Commit 2 screen capture](/assets/images/commit3-2.png)

