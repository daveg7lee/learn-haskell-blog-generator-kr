# 유연한 HTML 콘텐츠 (functions)

우리는 HTML의 반복되는 부분(Ex: html, body 등)을 반복해서 작성하지 않고도 HTML 페이지를 작성할 수 있기를 원합니다. 우리는 함수를 통해 그런 작업을 할 수 있습니다.

함수를 만들고 인수를 넣기 위해서는, 저번에 봤던 것처럼 정의를 만들고 이름과 `=` 표시 사이에 인수의 이름을 적을 수 있습니다.
따라서 함수는 다음과 같은 모양을 가지게 됩니다.

```hs
<name> <arg1> <arg2> ... <argN> = <expression>
```

인수는 등호 오른쪽 범위(`<expression>` 안쪽)에서 사용할 수 있으며 함수의 이름은 `<name>`이 되게 됩니다.

우리는 페이지의 콘텐츠가 될 문자열을 받아 그 문자열을 `html` 과 `body` 태그로 감싸는 함수를 작성할 것입니다.
두 개의 문자열을 합치기 위해 연산자 `<>`을 사용합니다.

```hs
wrapHtml content = "<html><body>" <> content <> "</body></html>"
```

함수 `wrapHtml`은 `content`라는 인수를 받아 앞에 `<html><body>`을 추가하고 뒤에 `</body></html>`을 추가하여 리턴하는 함수입니다. 
> 하스켈에서는 주로 카멜 표기법을 사용한다는 점을 유의하십시오.


이제 이전 장에서 만들었던 `myhtml`의 정의를 다음과 같이 수정할 수 있습니다:

```hs
myhtml = wrapHtml "Hello, world!"
```

다시 말하지만, 하스켈에서는 함수를 호출할 때 괄호가 필요하지 않습니다. 함수 호출의 형식은 다음과 같습니다.

```hs
<name> <arg1> <arg2> ... <argN>
```

그러나, `myhtml`을 사용하지 않고 `main = putStrLn myhtml`에 바로 바인딩하고 싶다면 아래와 같이 괄호로 묶어 식을 나타내야만 합니다.

```hs
main = putStrLn (wrapHtml "Hello, world!")
```

만약 실수로 괄호를 사용하지 않는다면,

```hs
main = putStrLn wrapHtml "Hello, world!"
```

`putStrLn`이 두 개의 인수에 적용되지만 하나만 사용한다는 GHC의 오류가 발생합니다. 이는 위의 형식이 `<name> <arg1> <arg2>` 형식이기 때문입니다. 여기서 앞서 정의한 바와 같이 `<arg1>` 및 `<arg2>`는 `<name>`에 대한 인수입니다.

괄호를 사용하여 올바른 순서로 표현식을 묶을 수 있습니다.

> #### 연산자 우선순위 및 고정성에 대하여
>
> 연산자 (ex: `<>`) 는 양쪽에서 하나씩 두 개의 인수를 취하는 중위 함수입니다.
> 
> 괄호가 없는 동일한 표현식에서 여러 연산자가 있는 경우 *고정성* (왼쪽 혹은 오른쪽)과 *우선순위* (0부터 10사이의 숫자)에 따라 더 밀접하게 결합되는 연산자가 결정됩니다.
>
> 우리의 경우 `<>` 는 *오른쪽* 고정성 가지고 있습니다, 따라서 하스켈은 오른쪽에 보이지 않는 괄호를 추가합니다. 예를 들어:
>
> ```hs
> "<html><body>" <> content <> "</body></html>"
> ```
>
> 하스켈의 관점에서는:
>
> ```hs
> "<html><body>" <> (content <> "</body></html>")
> ```
>
> 우선 순위로 예를 들자면, `1 + 2 * 3` 이라는 식에서 `+` 연산자는 우선 순위 6을 `*` 연산자는 우선 순위 7을 가지므로 `+` 보다 `*`에 우선 순위를 부여합니다. 따라서 하스켈은 이 식을 다음과 같이 보게 될 것입니다.
>
> ```hs
> 1 + (2 * 3)
> ```
> *우선 순위*는 같지만 *고정성*이 다른 연산자를 혼합해 사용할 경우 에러가 발생할 수 있습니다. 이러한 경우에는 명시적으로 괄호를 사용하여 문제를 해결할 수 있습니다

---

연습 문제:

1. `wrapHtml`의 기능을 두 가지 함수로 분리:
   1. 콘텐츠를 `html` 태그로 감싸는 함수
   2. 콘텐츠를 `body` 태그로 감싸는 함수
   
   새로운 함수의 이름은 `html_`과 `body_`가 되야합니다.

2. `myhtml`이 위의 두 함수를 사용하도록 변경하세요.

3. `<head>`와 `<title>` 태그로 비슷한 함수 2개를 만들고 `head_`와 `title_`라는 이름을 붙이세요

4. 두 개의 문자열을 인수로 받아들이는 새로운 함수 `makeHtml`을 작성하세요:
   1. 문자열 하나는 제목이 되고
   2. 다른 하나는 바디 콘텐츠가 되어야합니다.

   그리고 이전 연습에서 구현한 함수를 사용하여 HTML 문자열을 구성합니다.

   함수의 출력은 아래와 같아야 합니다.

   ```hs
   makeHtml "My page title" "My page content"
   ```
   
   ```html
   <html><head><title>My page title</title></head><body>My page content</body></html>
   ```

5. `myhtml`에 `html_`과 `body_`을 직접 사용하는 대신 `makeHtml`을 사용하세요.

---

해답:

<details>
  <summary>연습 문제 1</summary>
  
  ```hs
  html_ content = "<html>" <> content <> "</html>"
     
  body_ content = "<body>" <> content <> "</body>"
  ```

</details>

<details>
  <summary>연습 문제 2</summary>
  
  ```hs
  myhtml = html_ (body_ "Hello, world!")
  ```

</details>

<details>
  <summary>연습문제 3</summary>
  
  ```hs
  head_ content = "<head>" <> content <> "</head>"
  
  title_ content = "<title>" <> content <> "</title>"
  ```

</details>

<details>
  <summary>연습문제 4</summary>
  
  ```hs
  makeHtml title content = html_ (head_ (title_ title) <> body_ content)
  ```

</details>


<details>
  <summary>연습문제 5</summary>
  
  ```hs
  myhtml = makeHtml "Hello title" "Hello, world!"
  ```

</details>


<details>
  <summary>최종 완성본</summary>
  
  ```hs
  -- hello.hs

  main = putStrLn myhtml

  myhtml = makeHtml "Hello title" "Hello, world!"

  makeHtml title content = html_ (head_ (title_ title) <> body_ content)

  html_ content = "<html>" <> content <> "</html>"
     
  body_ content = "<body>" <> content <> "</body>"

  head_ content = "<head>" <> content <> "</head>"
  
  title_ content = "<title>" <> content <> "</title>"
  ```
   이제 hello.hs 프로그램을 실행하고 출력을 파일로 옮겨 브라우저에서 열 수 있습니다.
   
   ```sh
   runghc hello.hs > hello.html
   firefox hello.html
   ```

웹 페이지에 'Hello, world!'가 표시되고 웹 페이지 제목에 'Hello title'이 표시될 것입니다.

</details>


---

## 들여쓰기

아마 당신은 "어떻게 하스켈은 정의가 끝났다는 것을 알 수 있습니까?" 정답은 하스켈은 들여쓰기를 사용해서 항목들이 그룹화되는 것을 결정합니다.

Haskell의 들여쓰기는 약간 까다로울 수 있지만 일반적으로 다른 표현식의 일부로 간주되는 코드는 해당 표현식의 시작 부분보다 더 들여써야 합니다.

두 번째 정의가 첫 번째 정의보다 들여쓰기되지 않기 때문에 두 정의가 별개라는 것을 알 수 있습니다.


### 들여쓰기 팁

1. 들여쓰기를 위한 특정 양의 공백 (2칸, 4칸 등)을 선택하고 변경하지 마세요.
   항상 탭보다는 스페이스를 사용하세요.

2. 한번에 여러번 들여쓰지 마세요.
3. 확실하지 않은 경우 필요에 따라 줄을 삭제하고 한 번 들여쓰기하세요.

여기 몇가지 예시가 있습니다:

```hs
main =
    putStrLn "Hello, world!"
```

또는:

```hs
main =
    putStrLn
        (wrapHtml "Hello, world!")
```

__다음의 스타일을 피하세요__: 둘 이상의 들여쓰기 단계를 사용하거나, 들여쓰기 단계를 완전히 무시하는 스타일

```hs
main = putStrLn
        (wrapHtml "Hello, world!")
```

```hs
main = putStrLn
                (wrapHtml "Hello, world!")
```

