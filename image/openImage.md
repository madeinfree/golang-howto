# Open Image

how to open image ?

before decode image must be add image register.

- png magic number "\x89PNG\r\n\x1a\n"
- jpg maigc number "\xff\xd8"

```go
path := "./img.png"
file, err := os.Open(path)
if err != nil {
  panic(err)
}
defer file.Close()
img, err := png.Decode(file)
if err != nil {
  panic(err)
}
fmt.Println(img)
```
