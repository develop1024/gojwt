#### 安装
`go get github.com/develop1024/gojwt`

#### 使用示例
```go
package main

import (
	"fmt"
	"github.com/develop1024/gojwt"
	"time"
)

func main() {
	// 生成token
	secret := []byte("hello secret")
	token, err := gojwt.GenerateToken(secret, map[string]interface{}{
		"iss": "wang",
		"exp": time.Now().Add(time.Second * 1).Unix(),
		"foo": "bar",
	})

	if err != nil {
		panic(err)
	}

	fmt.Println("token: ", token)

	// 解析token
	claims, err := gojwt.ParseToken(token, secret)
	if err != nil {
		fmt.Println(err)
	} else {
		fmt.Println(claims)
		fmt.Println(claims["exp"])
		fmt.Println(claims["iss"])
	}
}
```