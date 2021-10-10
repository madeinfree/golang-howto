# Open File

how to open file ?

- read all file content

```go
path := "path/filename"
file, err := os.Open(path)
if err != nil {
  panic(err)
}
defer file.Close()
content, err := ioutil.ReadAll(file)
fmt.Println(string(content))
```
