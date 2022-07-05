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

> #### An aside about operator precedence and fixity
>
> operators (like `<>`) are infix functions which take two arguments - one from each side.
>
> When there are multiple operators in the same expression without parenthesis, the operator
> *fixity* (left or right) and *precedence* (a number between 0 and 10) determine which
> operator binds more tightly.
>
> In our case `<>` has *right* fixity, so Haskell adds invisible parenthesis on the right side
> of `<>`. So for example:
>
> ```hs
> "<html><body>" <> content <> "</body></html>"
> ```
>
> is viewed by Haskell as:
>
> ```hs
> "<html><body>" <> (content <> "</body></html>")
> ```
>
> For an example of precedence, in the expression `1 + 2 * 3`,
> the operator `+` has precedence 6, and the operator `*` has precedence 7,
> so we give precedence to `*` over `+`. Haskell will view this expression as:
>
> ```hs
> 1 + (2 * 3)
> ```
>
> You might run into errors when mixing different operators with the *same precedence*
> but *different fixity*, because Haskell won't understand how to group these expressions.
> In that case we can solve the problem by adding parenthesis explicitly.

---

Exercises:

1. Separate the functionality of `wrapHtml` to two functions:
   1. One that wraps content in `html` tag
   2. one that wraps content in a `body` tag

   Name the new functions `html_` and `body_`.
2. Change `myhtml` to use these two functions.
3. Add another two similar functions for the tags `<head>` and `<title>`
   and name them `head_` and `title_`.
4. Create a new function, `makeHtml`, which takes two strings as input:
   1. One string for the title
   2. One string for the body content
   
   And construct an HTML string using the functions implemented in the previous exercises.
   
   The output for:
   
   ```hs
   makeHtml "My page title" "My page content"
   ```
   
   should be:
   
   ```html
   <html><head><title>My page title</title></head><body>My page content</body></html>
   ```
5. Use `makeHtml` in `myhtml` instead of using `html_` and `body_` directly

---

Solutions:

<details>
  <summary>Solution for exercise #1</summary>
  
  ```hs
  html_ content = "<html>" <> content <> "</html>"
     
  body_ content = "<body>" <> content <> "</body>"
  ```

</details>

<details>
  <summary>Solution for exercise #2</summary>
  
  ```hs
  myhtml = html_ (body_ "Hello, world!")
  ```

</details>

<details>
  <summary>Solution for exercise #3</summary>
  
  ```hs
  head_ content = "<head>" <> content <> "</head>"
  
  title_ content = "<title>" <> content <> "</title>"
  ```

</details>

<details>
  <summary>Solution for exercise #4</summary>
  
  ```hs
  makeHtml title content = html_ (head_ (title_ title) <> body_ content)
  ```

</details>


<details>
  <summary>Solution for exercise #5</summary>
  
  ```hs
  myhtml = makeHtml "Hello title" "Hello, world!"
  ```

</details>


<details>
  <summary>Our final program</summary>
  
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

   We can now run our `hello.hs` program, pipeline the output into a file,
   and open it in our browser:
   
   ```sh
   runghc hello.hs > hello.html
   firefox hello.html
   ```

It should display `Hello, world!` on the page and `Hello title` on the page's title.

</details>


---

## Indentation

You might ask how does Haskell know a definition is complete?
The answer is: Haskell uses indentation to know when things should be grouped together.

Indentation in Haskell can be a bit tricky, but in general: code which is supposed to be
part of another expression should be indented further than the beginning of that expression.

We know two definitions are separate because the second one is not indented further than the first one.


### Indentation tips

1. Choose a specific amount of spaces for indentation (2 spaces, 4 spaces, etc) and stick to it.
   Always use spaces over tabs.
2. Do not indent more than once in any given time.
3. When in doubt, drop line as needed and indent once.

Here are a few examples:

```hs
main =
    putStrLn "Hello, world!"
```

or:

```hs
main =
    putStrLn
        (wrapHtml "Hello, world!")
```

__Avoid the following styles__, which use more than one indentation steps, or completely disregard
indentation steps:

```hs
main = putStrLn
        (wrapHtml "Hello, world!")
```

```hs
main = putStrLn
                (wrapHtml "Hello, world!")
```

