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