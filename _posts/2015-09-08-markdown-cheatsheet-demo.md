---
title: 마크다운 공부 겸 첫글.
updated: 2015-09-08 20:00
---

> This is Markdown Cheatsheet Demo for **The Plain**, this Jekyll theme. Please check the raw content of this file for the markdown usage.

> 위에것이 원본이고 이를 따라서 마크다운에 대해 **공부**해 볼것입니다. 해석은 철저히 내 기준으로 할 것이니, **절대** 신뢰하지마세요. 사실 해석을 안할수도잇음...


## Typography Elements in One
## #개수에 따라서 글자 크기가 작아집니다. 

1~6개까지 갯수가 많아질수록 글자가 작아집니다.

Let's start with a informative paragraph. **This text is bolded.** But not this one! _How about italic text?_ Cool right? Ok, let's **_combine_** them together. 
Yeah, that's right! I have code to highlight, so `ThisIsMyCode()`. What a nice! Good people will hyperlink away, so [here we go](#) or [http://www.example.com](http://www.example.com).
   
<br>
**\*을 두개 써서 감싸면** 굵어지네요.  
_\_로 감싸면_ 기울임이구요.   
**_혼합도 됩니다!_**   
`코드를 강조하려면` `  기호를 쓰면 됩니다.  
[여기](#) 처럼 하이퍼링크를 걸고 싶으면 \[여기\]\(#\) 요렇게.
 
<div class="divider"></div>

## Footnote 각주

Let's say you have text that you want to refer with a footnote, you can do that too! This is an example for the footnote number one [^1]. You can even add more footnotes, with link! [^2]   
각주를 달려면 [^3]. 각주 안에서도 기존의 마크다운이 사용가능합니다.

<div class="divider"></div>

## Blockquote 인용

> > \> 로 시작하면 됩니다. 인용안에 인용도 가능

> Start by doing what's necessary; then do what's possible; and suddenly you are doing the impossible. --Francis of Assisi     

**NOTE:** This theme does NOT support nested blockquotes.   

> 두려워하지 말라 내가 너와 함께 함이라 놀라지 말라 나는 네 하나님이 됨이라 내가 너를 굳세게 하리라 참으로 너를 도와 주리라 참으로 나의 의로운 오른손으로 너를 붙들리라두려워하지 말라 내가 너와 함께 함이라 놀라지 말라 나는 네 하나님이 됨이라 내가 너를 굳세게 하리라 참으로 너를 도와 주리라 참으로 나의 의로운 오른손으로 너를 붙들리라 --이사야 41장 10절    

**NOTE:** 제가 이 블로그를 만드는데 사용한 테마는 인용안에 인용을 지원하지 않기  
  는 **개뿔 잘됨.**


<div class="divider"></div>

## List Items 리스트

1. First order list item
2. 그냥 1.하면 됩니다.

* Unordered list can use asterisks
- Or minuses
+ Or pluses
* \*이나 \+ \- 에 의해서도 리스트가 됩니다.

<div class="divider"></div>

## Code Blocks 코드 블럭

```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```

```python
s = "Python syntax highlighting"
print s
```

```
   ```을 이용하여 코드의 시작과 끝에 줄을 바꿔 쓰면 코드블럭이 됩니다. 
   ```javascript 같이 언어의 이름을 스면 그에 맞게 하이라이팅을 합니다.

```

<div class="divider"></div>

## Table 표

아래 보이는 그대로 치면됩니다...

### Table 1: With Alignment 정렬

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

```
| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |
```

### Table 2: With Typography Elements 요소

Markdown | Less      | Pretty
---      | ---       | ---
*Still*  | `renders` | **nicely**
1        | 2         | 3

```
Markdown | Less      | Pretty
---      | ---       | ---
*Still*  | `renders` | **nicely**
1        | 2         | 3
```

<div class="divider"></div>

## Horizontal Line 가로줄

The HTML `<hr>` element is for creating a "thematic break" between paragraph-level elements. In markdown, you can create a `<hr>` with any of the following:

* `___`: three consecutive underscores
* `---`: three consecutive dashes
* `***`: three consecutive asterisks
* 위에거 세개씩 치면 다 줄이됨. 차이점이 잘안보임..   
<br>
renders to:
  
___

---

***

<div class="divider"></div>

## Media 미디어

### YouTube Embedded Iframe 유튜브를 포함한 Iframe

<iframe width="560" height="315" src="https://www.youtube.com/embed/xxkUwF3XFdI" frameborder="0" allowfullscreen></iframe>

유튜브의 동영상에서 **소스 코드**를 누르면 코드가 나옴. <br>

```
<iframe width="560" height="315" 
src="https://www.youtube.com/embed/xxkUwF3XFdI" 
frameborder="0" allowfullscreen></iframe>
```

### Image

![Minion](http://octodex.github.com/images/minion.png)

아래의 코드와 같이 처리하면 됨.
```
![Minion](http://octodex.github.com/images/minion.png)

```

## 마무리
> 첫 글을 어떤 글을 올릴까 생각해 보다가 그냥 있던 예제 자체를 마크업 공부도 할겸 한글화 해보자는 생각이 들어 시도해 보았다.   
생각보다 재미있는 경험이었다.   
사실 조금 더 의미있는 첫글이길 바랬지만, 간단히 올려보았다.   
(사실 지울지도 모름.)

[^1]: Footnote number one yeah baby!
[^2]: A footnote you can link to - [click here!](#)
[^3]: \[^3\]의 형식으로 달면됩니다.

