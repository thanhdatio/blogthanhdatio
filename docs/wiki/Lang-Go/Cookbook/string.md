---
tags:
  - golang
---

# Strings and Text

## 1. Changing a character in a string

```go
str := "hello"
c := []rune(str)
c[0] = 'c'
s2 := string(c) // s2 == "cello"
```

## 2. Looping over a string with `for` or `for-range`

```go
// gives only the bytes:
for i:=0; i < len(str); i++ {
  ... = str[i]
}
// gives the Unicode characters:
for ix, ch := range str {
  ...
}
```

## 3. Number of characters in string

The fastest way is:

```go
utf8.RuneCountInString(str)
```

An equivalent way is:

```go
len([]int(str))
```

## 4. Concatenating strings

The fastest way is:

```go
// with a bytes.Buffer
var buffer bytes.Buffer
var s string
buffer.WriteString(s)
fmt.Print(buffer.String(), "\n")
```

Other ways are:

```go
s := []string{"foo", "bar", "baz"}
fmt.Println(strings.Join(s, ", ")) // foo, bar, baz

str1 += str2 // using += operator
```

## 5. Reverse a String

```go
package main

import "fmt"

func reverse(s string) string {
	runes := []rune(s)
	n := len(runes)
	mid := n / 2

	for i := 0; i < mid; i++ {
		runes[i], runes[n-1-i] = runes[n-1-i], runes[i]
	}

	return string(runes)
}

func main() {
	// reverse a string:
	str := "the quick brown 狐 jumped over the lazy 犬"

	fmt.Printf("The reversed string using variant is: `%s`\n", reverse(str))
}
```

??? example "Output"
    The reversed string using variant is: `犬 yzal eht revo depmuj 狐 nworb kciuq eht`

## 6. Generate random string of fixed length

??? info "References"

    - SO: [How to generate a random string of a fixed length in Go?](https://stackoverflow.com/questions/22892120/how-to-generate-a-random-string-of-a-fixed-length-in-go)
    - Calhoun.io: [Creating Random Strings in Go](https://www.calhoun.io/creating-random-strings-in-go/)

```go
package main

import (
	"fmt"
	"math/rand"
)

const letters = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ"

func randSeq(n int) string {
	b := make([]byte, n)
	for i := range b {
		b[i] = letters[rand.Intn(len(letters))]
	}
	return string(b)
}

func main() {
	fmt.Println(randSeq(10)) // e.g. irIXkcjdon
}
```