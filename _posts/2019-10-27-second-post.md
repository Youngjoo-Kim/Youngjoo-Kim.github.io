---
title: "Markdown using method"
date: 2019-10-27 22:30:28 -0400
categories: Markdown Study
---

# 마크다운 사용법
## 1. Markdown 이란?

### 1.1. 마크다운의 정의
Markdown은 텍스트 기반의 마크업언어로 2004년 존그루버에 의해 만들어졌으며 쉽게 쓰고 읽을 수 있으며 HTML로 변환이 가능하다. 특수기호와 문자를 이용한 매우 간단한 구조의 문법을 사용하여 웹에서도 보다 빠르게 컨텐츠를 작성하고 보다 직관적으로 인식할 수 있다. 마크다운이 최근 각광받기 시작한 이유는 깃헙(https://github.com) 덕분이다. 깃헙의 저장소Repository에 관한 정보를 기록하는 README.md는 깃헙을 사용하는 사람이라면 누구나 가장 먼저 접하게 되는 마크다운 문서였다. 마크다운을 통해서 설치방법, 소스코드 설명, 이슈 등을 간단하게 기록하고 가독성을 높일 수 있다는 강점이 부각되면서 점점 여러 곳으로 퍼져가게 된다.

### 1.2. 마크다운의 장-단점

#### 1.2.1. 장점
```
	1. 간결하다.
	2. 별도의 도구없이 작성가능하다.
	3. 다양한 형태로 변환이 가능하다.
	3. 텍스트(Text)로 저장되기 때문에 용량이 적어 보관이 용이하다.
	4. 텍스트파일이기 때문에 버전관리시스템을 이용하여 변경이력을 관리할 수 있다.
	5. 지원하는 프로그램과 플랫폼이 다양하다.
```
#### 1.2.2. 단점
```
1. 표준이 없다.
2. 표준이 없기 때문에 도구에 따라서 변환방식이나 생성물이 다르다.
3. 모든 HTML 마크업을 대신하지 못한다.
```

## 2. 문법
### 2.1. Headers
Header 사용법은 다음과 같다.
- 	큰 제목: 문서 제목

	```
    This is an Header1
	==================
    ```

	This is an Header1
    ==================
- 	작은 제목: 문서 부제목

	```
	This is an Header2
	------------------
	```
	This is an Header2
    ------------------
- 	글 머리: 1~6까지만 지원

	```
	# This is a H1
	## This is a H2
	### This is a H3
    #### This is a H4
	##### This is a H5
	###### This is a H6
	```

	# This is a H1
	## This is a H2
	### This is a H3
	#### This is a H4
	##### This is a H5
	###### This is a H6
    ####### This is a H7	(7부터는 지원이 안되는 것을 확인할 수 있음)

## 2.2. BlockQuote
이메일에서 사용하는 > 블럭인용문자를 이용한다.
	`> This is a blockqute.`
> This is a first blockqute.
>> This is a second blockqute.
>>> This is a third blockqute.

이 안에서는 다른 마크다운 요소를 포함할 수 있다.
>### This is a H3
>> - List
>>> `code`

## 2.3. 목록
목록에는 순서있는 목록과 순서없는 목록 두 가지로 분류되어 있다.
##### - 	순서있는 목록(번호)
순서있는 목록은 숫자와 점을 사용한다.
```
1. 첫번째
2. 두번째
3. 세번째
```

현재까지는 어떤 번호를 입력해도 순서는 내림차순으로 정의된다.
```
1. 첫번째
3. 세번째
2. 두번째
```
1. 첫번째
3. 세번째
2. 두번째

딱히 개선될 것 같지는 않다. 존 그루버님께서 문제삼지 않고 계시기 때문에

##### - 	순서없 목록(글머리 기호)
```
* 빨강
  * 녹색
    * 파랑

+ 빨강
  + 녹색
    + 파랑

- 빨강
  - 녹색
    - 파랑
```
* 빨강
  * 녹색
    * 파랑

+ 빨강
  + 녹색
    + 파랑

- 빨강
  - 녹색
    - 파랑

혼합해서 사용하는 것도 가능하다.
```
* 1단계
    - 2단계
    	+ 3단계
            = 4단계
```
* 1단계
    - 2단계
    	+ 3단계
            = 4단계

## 2.4. 코드` <pre><code></code></pre>`
4개의 공백 또는 하나의 탭으로 들여쓰기를 만나면 변환되기 시작하여 들여쓰지 않은 행을 만날때까지 변환이 계속된다.
> 한줄 띄어쓰면 인식이 제대로 안되는 문제가 발생하곤 합니다.

```
This is a normal paragraph:

    This is a code block.
end code block.
```

``` This is a normal paragraph: This is a code block. end code block. ```

**실제로 적용해보면, 다음과 같이 출력된다.**

This is a normal paragraph:

    This is a code block.
end code block.

## 2.5. 수평선 `<hr/>`
아래 줄은 모두 수평선을 만든다. 마크다운 문서를 미리보기로 출력할 때 페이지 나누기 용도로 많이 사용한다.

```
* * *

***

*****

- - -

---------------------------------------
```

* * *

***

*****

- - -

---------------------------------------

## 2.6. 링크
링크에 대한 설명은 다음과 같다.
**- 참조 링크**

```
[link keyword][id]
[id]: URL "Optional Title here"

Link: [Google][googlelink]
[googlelink]: https://google.com "Go google"
```

Link: [Google][googlelink] [googlelink]: https://google.com "Go google"

**- 인라인 링크**
```
syntax: [Title](link)
```
Link: [Google](link)

**- 자동 연결**
```
<http://example.com/>
<address@example.com>
```
<http://example.com/>
<address@example.com>

## 2.7. 강조

```
*single asterisks*
_single underscores_
**double asterisks**
__double underscores__
++underline++
~~cancelline~~
```

*single asterisks*
_single underscores_
**double asterisks**
__double underscores__
++underline++
~~cancelline~~



## 3. 정리
Markdown은 일반 텍스트 편집기에서도 손쉽게 작성이 가능한 마크업 언어이다. 단, 기본 문법을 익히기 위한 듀토리얼 정도만 해본다면 적응하는데 효과적일 것이다. 본인은 "Haroopad"를 활용하여 문서를 편집하고 있지만, 이외에도 다양한 도구와 플랫폼이 존재하고 있어 이용하는데 어렵지 않다. 마크다운과 Haroopad를 활용하여 GitHub pages를 보다 빠르고 쉽게 업로드 할 수 있게 되었다.
* 이외에도 더 많은 문법이 궁금하다면, 다음의 링크를 참조하면 좋을 것이다.
<https://daringfireball.net/projects/markdown/syntax>