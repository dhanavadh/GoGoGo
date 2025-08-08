# Fundamental Golang
![Golang logo](https://pkg.go.dev/static/shared/logo/go-blue.svg)

Personal docs for learning Golang. This will contain everything you need to know from scratch to advance (maybe). Also, please note that this note is made by me and for me. Reference notes will be displayed below.

## Fundamental Commands

To run go lang, you can use `go run main.go`

Compile golang to binary code by using `go build main.go`

nodemon also available in Golang. you can type 

`nodemon --exec go run main.go --signal SIGTERM`

`go mod tidy` >>scan จาก code ของเราว่าใช้งาน package อะไรบ้าง จากนั้นจะทำการ download และแก้ไขไฟล์ go.mod เสมอ เมื่อมีการเปลี่ยนแปลง ทั้งการเพิ่มและลบสิ่งที่ไม่ได้ใช้งานใน code ออกไป

`go mod download` >> to make it easy to remember >> comparable to `pnpm i`

## Go Module
Go module is somekind like node_module and package.json.

we can init the module by typing `go mod init github.com/**/go-example`
then we will get go.mod file. For example it will look like this.

```go
module github.com/dhanavadh/gogogo

go 1.24.5

require (
	github.com/google/uuid v1.6.0 // indirect
)
```

## Go Packages

we can use command like `go get github.com/google/uuid` to install package. Then we will get `go.sum` file.

`go.sum` is a file to show package version.

`go.mod` is a file to show library list.

The project structure will look like this

```bash
├── go.mod --> package.json
├── go.sum --> checksum library version
└── main.go --> file project
```

Use `go list -m all` to check the existing package.

## Package Declaration
Reference from mikelopster, we can create package seperately from main.go

```bash
├── go.mod
├── go.sum
├── main.go
└── mike
  ├── mikelopster.go
  └── test.go
```

you can see that the new package (mikelopster) will be inside the mike folder.

in `mikelopster.go` file
```go
package mikelopster

import "fmt"

func SayMikelopster() {
	fmt.Println("Hello mikelopster")
}
```
in `test.go` file
```go
package mikelopster

import "fmt"

func SayTest() {
	fmt.Println("Hello Test")
}

```

Then, in main function.

```go
package main

import (
  "github.com/mikelopster/go-example/mike"
)

func main() {
  mikelopster.SayMikelopster()
  mikelopster.SayTest()
}
```

## Private/Public Function
- function **ที่ขึ้นต้นด้วยตัวพิมพ์เล็ก** = private function (ที่เรียกใช้จากภายใน package เดียวกันได้เท่านั้น)
- function **ที่ขึ้นต้นด้วยตัวพิมพ์ใหญ่** = public function (ที่เรียกใช้จากภายในหรือภายนอกก็ได้)

### Example

```go
package mikelopster

import "fmt"

func SayMikelopster() {
	fmt.Println("Hello mikelopster")
	sayTest()
}
```
The `sayTest` function still can be used in the mikelopster package. but it cannot be used in public.

### Internal function
What if we want to use function in lopster.go?

```bash
├── go.mod
├── go.sum
├── main.go
└── mike
  ├── internal
  │   └── lopster
  │       └── lopster.go
  ├── mikelopster.go
  └── test.go
```

The answer is it cannot be used in other package except the lopster itself.
That's because the `internal` folder will be a controller to make the package itself to be private.