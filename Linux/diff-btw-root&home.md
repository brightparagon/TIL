## touch

> basically, used to modify date or time info of files

* create a file of which size is zero
  ```
  touch file-name-to-be-created
  ```
* update time info of a file with the system time
  ```
  touch -c file-name
  ```
* update time info of a file
  ```
  touch -t YYYYMMDDhhmm file-name
  ```
* apply time info of file-A to file-B
  ```
  touch -r file-A file-B
  ```
