# [Go] 一种简化处理 HTTP Error 的技术
### [Go] A Technique Simplifies the Verbosity of HTTP Error Handling

*This note is based on [Kevin Gillette's 'Effective Go Error Handling Talk"](https://go-talks.appspot.com/github.com/xtblog/gotalks/error-handling.slide)*

在 Go 语言中，处理 HTTP Error 的标准做法是：

```go
func MyHandle(w http.ResponseWriter, r *http.Request) {
  // do some stuff
  // Retrieve data from DB
  record, err := db.Get("key")
  if err != nil {
    http.Error(w, err.Error(), StatusInternalServerError)  // Database error translated to HTTP internal error
    return
  }
  
  // Render web page
  if err := RenderTemplate('template'); err == ErrTemplateNotFound {
    http.Error(w, err.Error(), http.StatusNotFound)
    return
  }
}
```
http.Error() 的缺省行为也无非是将错误信息写入到 w 中，从而得以在浏览器中显示。可是设定的 Status code 有啥用呢？










