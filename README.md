# Go의 문법과 예제

## 목차
- [표준 입출력](#표준-입출력)
- [변수와 상수, 데이터타입](#변수와-상수-데이터타입)
- [연산자](#연산자)
- [조건문](#조건문)

## 표준 입출력
```go
package main

import "fmt" // 표준 입출력 패키지

func main() { // 프로그램 진입점
	fmt.Println("Hello, World!") // 표준 출력
	fmt.Println(fmt.Sprintf("%d", 10)) // string format
	
	// println은 디버깅 목적으로 제공되는 기본 내장 함수이며, 실행 순서가 보장되지 않음.
	println("Hello, World!")
}

```

## 변수와 상수, 데이터타입
```go
package main

import (
	"fmt"
	"reflect" // reflection type 확인용 패키지
)

func main() {

	// 변수 (not used 되는 변수는 에러)
	var strVar string = "Hello, World!"  // 이후 수정 불가 immutable (escape 문자 사용 가능)
	var strVar2 string = `Hello, World!` // Raw String Literal (escape 문자 무시)
	var intVar int = -10                 // int8, int16, int32, int64
	var unsignedVar uint = 10            // uint8, uint16, uint32, uint64, uintptr (양수만 표현)
	var floatVar float64 = 3.14          // float32, float64, complex64, complex128
	var boolVar bool = true
	var byteVar byte = 'a' // byte == uint8
	var runeVar rune = '가' // rune == int32 (유니코드 문자)

	fmt.Println(strVar, strVar2, intVar, unsignedVar, floatVar, boolVar, byteVar, runeVar)

	// 상수 (not used 되더라도 에러가 나지 않음)
	const a int = 10
	const ( // 여러개의 상수를 한번에 선언
		b = 20
		c = 30
		d = 40
	)
	const ( // 0부터 1씩 auto increment 되는 iota
		e = iota // 0
		f        // 1
		g        // 2
	)

	fmt.Println(a, b, c, d, e, f, g)

	// 타입 캐스트
	var iVar int = 100
	var uVar uint = uint(iVar)
	var fVar float32 = float32(iVar)

	// reflection으로 타입 확인
	fmt.Println(reflect.TypeOf(iVar).String(), reflect.TypeOf(uVar).String(), reflect.TypeOf(fVar))

	// string format으로 타입 확인
	fmt.Println(fmt.Sprintf("%T %T %T", iVar, uVar, fVar)) // string format으로 타입 확인

}

```

## 연산자
```go
package main

import "fmt"

func main() {
	const a = 5
	const b = 5

	// 사칙 연산자
	var c = (a+b)/5 - 1*2
	fmt.Println(c) // 0

	// 증감연산자
	c++
	fmt.Println(c) // 1
	c--
	fmt.Println(c) // 0

	// 관계연산자
	fmt.Println(a == b) // true
	fmt.Println(a != b) // false
	fmt.Println(a > c)  // true

	// 논리연산자
	fmt.Println(a == b && a > c) // true
	fmt.Println(a == b || a > c) // true
	fmt.Println(!(a == b))       // false

	// 비트연산자 (Bitwise Operator)
	var d = a & b
	fmt.Println(d) // 5
	d = d << 5
	fmt.Println(d) // 160 왼쪽 시프트 (5 * 2^5)
	d = d >> 5
	fmt.Println(d) // 5 오른쪽 시프트 (160 / 2^5)

	// 할당연산자
	var e = 5
	e += 5         // 덧셈
	fmt.Println(e) // 10
	e -= 5         // 뺄셈
	fmt.Println(e) // 5
	e *= 5         // 곱
	fmt.Println(e) // 25
	e /= 5         // 몫
	fmt.Println(e) // 5
	e %= 3         // 나머지
	fmt.Println(e) // 2

	e = 5                 // 101
	e &= 7                // 111 AND
	fmt.Printf("%b\n", e) // 101
	e = 5
	e |= 7                // OR
	fmt.Printf("%b\n", e) // 111
	e = 5
	e ^= 7                // XOR
	fmt.Printf("%b\n", e) // 010

	e = 5
	e <<= 5
	fmt.Println(e) // 160
	e >>= 5
	fmt.Println(e) // 5

	// 포인터
	var f = 5
	var g = &f
	fmt.Println(f, g) // 5 0xc0000b0008

}

```

## 조건문
package main

import "fmt"

func main() {

	// if

	// 기본 if
	var a = 10
	if a == 1 {
		fmt.Println("One")
	} else if a == 2 {
		fmt.Println("Two")
	} else {
		fmt.Println("Other")
	} // Other

	// optional statement
	if b := a * 2; b >= 20 {
		fmt.Println("Big or Same")
	} else {
		fmt.Println("Small")
	} // Big or Same

	// switch

	// 문자열, 여러 개 동시 비교
	var os = "windows"
	switch os {
	case "":
		fmt.Println("Unknown OS")
	case "windows":
		fmt.Println("Windows")
	case "linux":
		fmt.Println("Linux")
	case "android", "ios":
		fmt.Println("Mobile OS")
	default:
		fmt.Println("Unknown OS")
	} // Windows

	// 조건식 사용
	var score = 80
	switch {
	case score >= 90:
		fmt.Println("A")
	case score >= 80:
		fmt.Println("B")
	default:
		fmt.Println("C")
	} // B

	// 타입 체크
	var val interface{} = 20
	switch val.(type) {
	case int:
		fmt.Println("Integer")
	case string:
		fmt.Println("String")
	default:
		fmt.Println("Unknown")
	} // Integer

	// fallthrough (Go에서는 break가 기본. fallthrough를 사용하면 다음 case로 이동)
	var val2 = 2
	switch val2 {
	case 1:
		fmt.Println("1 이상")
		fallthrough
	case 2:
		fmt.Println("2 이상")
		fallthrough
	case 3:
		fmt.Println("3 이상")
		fallthrough
	default:
		fmt.Println("default")
	} // 2 이상, 3 이상, default

}

