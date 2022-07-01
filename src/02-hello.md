# Hello, world!

이 장에서는 간단한 HTML "hello world" 프로그램을 만들고 하스켈 툴체인을 사용해 프로그램을 컴파일하고 실행시켜 볼 것입니다.

> 만약 하스켈 툴체인을 설치하지 않았다면, [haskell.org/downloads](https://haskell.org/downloads)을 방문하여 하스켈 툴체인을 다운로드 받으세요

## 하스켈 소스 파일

하스켈 소스 파일은 정의들로 구성됩니다.

가장 일반적인 정의 유형은 다음과 같은 형식을 가지고 있습니다:

```hs
<name> = <expression>
```

🚨 주의:

1. expression은 이름에 바인딩하지 않고는 사용할 수 없습니다.
2. 이름은 무조건 소문자로 시작해야만 합니다.
3. 하나의 파일 안에서 같은 이름은 사용할 수 없습니다.

`main` 이라는 이름의 정의를 가지고 있는 소스 파일은 실행 파일로 취급됩니다, 그리고 `main` 은 프로그램의 진입점으로 바인딩 됩니다.

`hello.hs` 라는 하스켈 소스 파일을 하나 생성하고, 아래 내용을 작성해봅시다:

```hs
main = putStrLn "<html><body>Hello, world!</body></html>"
```

여기서 우리는 `main` 이라는 새로운 이름을 정의했습니다, 그리고 이것을 `putStrLn "<html><body>Hello, world!</body></html>"` 이라는 expression에 바인딩 했습니다.

여기서 `main`은 `putStrLn` 이라는 함수를 `"<html><body>Hello, world!</body></html>"` 이라는 문자열을 인수로 호출하고 있습니다. `putStrLn` 은 문자열 하나를 입력으로 받아 그 문자열을 터미널에 출력해주는 함수입니다.

__주의__: 하스켈에서는 함수에 인수를 전달하기 위한 괄호가 필요하지 않습니다.

위 프로그램을 실행하면 다음과 같은 문자가 출력되는 것을 확인할 수 있습니다:

```
<html><body>Hello, world!</body></html>
```

## 프로그램 컴파일하기

이 작은 프로그램을 실행하기 위해서는, 우리는 `ghc` 라는 커멘트 라인 프로그램을 사용해서 컴파일할 수 있습니다:

```sh
> ghc hello.hs
[1 of 1] Compiling Main             ( hello.hs, hello.o )
Linking hello ...
```

`hello.hs` 파일로 `ghc` 를 호출하면 다음과 같은 아티팩트 파일들이 생성됩니다:

1. `hello.o` - 오브젝트 파일
2. `hello.hi` - 하스켈 인터페이스 파일
3. `hello` - 네이티브 실행 파일

컴파일이 끝난 후에는, 다음과 같이 `hello` 파일을 실행할 수 있습니다

```sh
> ./hello
<html><body>Hello, world!</body></html>
```

## 프로그램 인터프리팅하기

위와 같이 파일을 컴파일하는 방법도 있지만, 아티팩트 파일의 컴파일 단계를 건너뛰고, 아래와 같이 커맨드 라인 프로그램 `runghc`을 사용해 소스 파일을 직접 실행할 수도 있습니다.

```sh
> runghc hello.hs
<html><body>Hello, world!</body></html>
```

또한, 프로그램의 출력을 파일로 만들어 파이어폭스에서 확인해 볼 수도 있습니다.

```sh
> runghc hello.hs > hello.html
> firefox hello.html
```

위의 커맨드는 파이어폭스를 열고 `Hello, world!`라고 적혀있는 웹 페이지를 보여줄 것입니다.

이 튜토리얼을 진핸하는 동안에는 `runghc` 를 사용하기를 추천합니다. 컴파일을 할 경우 훨씬 빠른 프로그램이 나오지만, 인터프리터는 잦은 수정이 일어나는 동안에 빠른 피드백을 제공합니다.

> 만약 core Haskell tools에 대해 더 알고 싶다면 [이 포스트](https://gilmi.me/blog/post/2021/08/14/hs-core-tools)를 읽어볼 수 있습니다, 하지만 위에 적혀있는 내용으로도 앞으로의 과정을 충분히 진행할 수 있습니다.

## 더 많은 바인딩

우리는 `putStrLn`에 바로 HTML 문자열을 보내는 것이 아닌 새로운 이름으로 전달할 수 있습니다. 아래와 같이 `hello.hs`의 내용을 바꿔보세요.

```hs
main = putStrLn myhtml

myhtml = "<html><body>Hello, world!</body></html>"
```

__주의__: 바인딩을 선언하는 순서는 중요하지 않습니다.

