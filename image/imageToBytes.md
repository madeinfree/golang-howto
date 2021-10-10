# Image to Buffer

how convert image to bytes type ?

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

// alloc buffer
buf := new(bytes.Buffer)
err = png.Encode(buf, img)
if err != nil {
  panic(err)
}
```
