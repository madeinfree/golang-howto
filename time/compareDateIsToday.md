# Compare date is today

how to compare date is same today?

```go
func isToday(compareTime time.Time) bool {
	compny, compnm, compnd := compareTime.Date()
	ny, nm, nd := time.Now().Date()

	return compny == ny && compnm == nm && compnd == nd
}
```
