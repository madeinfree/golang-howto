# how to ues dotenv file

how to use local .env file ?

deps: [godotenv](https://github.com/joho/godotenv)

`.env`

```
LOCAL_KEY=qwerty
```

`main.go`

```go
func main() {
  godotenv.Load()
}
```
