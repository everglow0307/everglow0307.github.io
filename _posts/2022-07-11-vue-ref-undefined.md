---
title:  "Vue Ref Undefined 오류 해결"
excerpt: "ref 인식안되는 에러"

categories: 
  - vue
tags:
  - [vue, ref]

toc: true
toc_sticky: true
 
date: 2022-07-11
---

## Ref undefined 오류 뜨는 경우


 :page_with_curl: 일단, vue에서 ref는 부모컴포넌트에서 하위의 컴포넌트에 접근해서 특정 메소드를 수행할 경우와 같이 <u style="color:skyblue;">**<span style="color:skyblue;">하위 컴포넌트에 접근하기 위한 속성</span>**</u>이다.


이러한 ref속성을 이용해 하위 컴포넌트의 메소드를 수행하려고 했는데, ref를 인식하지 못하는 undefined 에러가 떴다.


![image](https://user-images.githubusercontent.com/71758210/178224461-c4e36cbf-8050-46b2-9518-191875b6e51c.png)


코드를 보니 렌더링 문제였다.



## :heavy_check_mark:해결 

v-if로 해당 컴포넌트가 조건이 적용안돼서 렌더링이 안 된상태에서 ref속성으로 부르니 undefined가 뜬 거다.

<span style="color:red;">v-if 대신 v-show로 수정하니 에러없이 해당 ref속성을 사용할 수 있었음.</span>







