# 이 책에 대하여

> Note: 이 책은 출간한지 얼마 되지 않았습니다. 만약 오류를 발견한다면 [알려주세요](https://github.com/soupi/learn-haskell-blog-generator/issues) (한국어 맞춤법 및 번역 오류는 [여기로](https://github.com/daveg7lee/learn-haskell-blog-generator-kr/pulls))

<!--
<div style="text-align: center">
  <img src="book-logo.png" alt="book logo" style="max-width: 40%">
</div>
-->

이 책에서 저희는 하스켈을 이용하여 저희만의 커스텀 마크업 언어로 작성한 문서를 HTML로 바꿔주는 간단한 정적 블로그 생성기를 만들 것입니다.

저희는:

1. 작은 HTML 출력 라이브러리를 구현
2. 저희만의 커스텀 마크업 언어를 정의하고 파싱
3. 파일을 읽어들이고 여러개의 모듈을 하나로 만들기
4. 터미널에서 인수 구하기
5. 테스트 코드와 문서 작성

챕터별로 우리는 달성하고자 하는 특정한 작업에 집중할 것입니다, 그리고 각 장을 통해 우리는 각 작업을 끝내기에 충분한 양의 하스켈을 배울 것입니다.

## 왜 이 책을 읽어야하나요?

이미 많은 하스켈 튜토리얼, 가이드, 책이 있는데 왜 이 책을 읽어야하나요?

### 장점

분명 더 많은 장점이 있겠지만, 여기 몇 가지 장점들이 있습니다

- 이 책은 **상대적으로 짧습니다** - 많은 하스켈 책들이 몇백 장이 넘어가는 페이지를 가지고 있습니다. 이 책은 (PDF로 출력한다면) 약 150쪽의 페이지를 가지고 있습니다.
- 이 책은 **프로젝트 중심**입니다. 많은 하스켈 책은 기본 개념과 기능들을 깔끔하게 설명하며 하스켈을 가르칩니다. 이 책에서 우리는 프로그램을 만들고, 그 과정에서 하스켈을 배우려고 합니다. 이것은 누군가에게는 장점이 될테지만 누군가에게는 단점이 될 수 있습니다. 여기 또 다른 튜토리얼들이 있습니다. 가장 눈에 띄는 것들은 [Beginning Haskell](https://www.apress.com/gp/book/9781430262510#otherversion=9781430262503)과 [Haskell via Sokoban](https://haskell-via-sokoban.nomeata.de/)이 있습니다.
- 이 책은 디자인 패턴, 테스트 코드, 문서화와 같은 **중요한 주제**에 대해 다룹니다.
- 이 책은 **온라인**이므로 수정이 쉽습니다.
- 이 책은 **공짜**입니다.

### 단점

아마 몇 가지 더 있겠지만, 몇 가지 단점이 있습니다

- It may **lack depth** - many, much longer Haskell tutorials are long because they go
  deeper into the nuts and bolts of each feature.
- It may **not cover as many features or techniques** as other tutorials -
  we try to cover features as they pop up in our implementation, but we will
  probably miss features that aren't as important for our tasks,
  while other resources may try to cover many different use cases.
- It is **very new** and not "battle-tested". Who knows if this is a good approach to
  learning Haskell? Maybe you could help with that!
- It **doesn't have a technical editor**, making the book not as good as it could've been.

### Other learning resources

The [haskell.org/documentation](https://www.haskell.org/documentation/) page lists
many tutorials, books, guides and courses. You can find a few alternatives that I can
recommend [in this list](https://github.com/soupi/haskell-study-plan#about-this-guide).
