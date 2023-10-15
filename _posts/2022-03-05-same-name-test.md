---
published: true
title:  "[error.log] 다른 날짜 같은 파일명&카테고리 오류"

categories:
  - error.log
tags:
  - [Blog, jekyll, Github, error.log]

toc: true
toc_sticky: true
 
date: 2022-03-05 15:03:00
last_modified_at: 2022-03-05 15:03:00
---

## 블로그 포스팅 파일명(같은 카테고리)

깃헙 블로그에 글을 쓰다 보면(=포스팅) 파일명을 어떻게 할지 고민하게 된다.  
기본적으로 **'yyyy-mm-dd-포스트이름.md'** 양식으로 적게 될 텐데, 그러다 보면 같은 포스트이름이 생길 수도 있다.  
하지만 블로그의 링크 주소는 **'깃헙주소/카테고리/포스트이름'**이 되다 보니 날짜가 달라도 그 뒤의 '포스트이름'이 같다면, 거기에 카테고리까지 같다면 문제가 되지 않을까?  
그래서 직접 테스트 해 보았다!!  
<br>

## 다른 날짜, 같은 파일명으로 저장해서 돌리면?
`bundle exec jekyll serve` 명령어는 현재 마련한 블로그 구조 파일들이 잘 돌아가는지 로컬에서 확인할 때 쓴다.  
난 기존에 [[JavaScript] 순열 Permutation](https://mialee-luvcat.github.io/algorithm/study-permutation/){:target="_blank"} 글을 쓴 적이 있는데, 날짜만 다르고 똑같은 파일명을 만들어 보았다.  

기존 순열 글 파일명 = 2022-03-01-study-permutation.md  
새로운 글 파일명 = 2022-03-05-study-permutation.md  
카테고리 = 둘 다 같게 함.  

기존 글의 **excerpt**는 '원래 글'이라고 하고, 새로운 글의 **excerpt**에는 '테스트!'라고 적어뒀다.  

### 기존 글
<center><img width="706" alt="스크린샷 2022-03-05 오후 3 17 27" src="https://user-images.githubusercontent.com/87490361/156871023-cde1a5bf-3979-4c67-a8f8-69a9a82e3f75.png"></center>


### 새로운 글
<center><img width="706" alt="스크린샷 2022-03-05 오후 3 16 02" src="https://user-images.githubusercontent.com/87490361/156870974-1f615689-59eb-45f7-ba45-90b4d991e6d2.png"></center>
<br/>

## 결과
`bundle exec jekyll serve` 명령어를 돌려서 확인해보았다.  
그랬더니 평소엔 보지 못했던 충돌(conflict) 문장이 보였다.  

```shell
// siri-syl은 내 깃헙 계정이다
// l_siri는 내 맥북 컴퓨터 이름이다.

 ~/mialee-luvcat.github.io   main  bundle exec jekyll serve             
Configuration file: /Users/l_siri/mialee-luvcat.github.io/_config.yml
            Source: /Users/l_siri/mialee-luvcat.github.io
       Destination: /Users/l_siri/mialee-luvcat.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
       Jekyll Feed: Generating feed for posts
          Conflict: The following destination is shared by multiple files.
                    The written file may end up with unexpected contents.
                    /Users/l_siri/mialee-luvcat.github.io/_site/algorithm/study-permutation/index.html
                     - /Users/l_siri/mialee-luvcat.github.io/_posts/2022-03-01-study-permutation.md
                     - /Users/l_siri/mialee-luvcat.github.io/_posts/2022-03-05-study-permutation.md
                    
                    done in 3.592 seconds.
 Auto-regeneration: enabled for '/Users/l_siri/mialee-luvcat.github.io'
    Server address: http://127.0.0.1:4000
  Server running... press ctrl-c to stop.
```  
<br>

**이미지의 경우**
<center><img width="1010" alt="스크린샷 2022-03-05 오후 3 20 38" src="https://user-images.githubusercontent.com/87490361/156871116-8b1fc2b3-cf28-4300-82d0-b2748fb3b440.png"></center>  

그래도 테스트가 돌아가긴 해서 로컬에서 어떻게 보이는지 확인해 봤다.  

## 블로그 포스팅 상태
<center><img width="879" alt="스크린샷 2022-03-05 오후 3 25 55" src="https://user-images.githubusercontent.com/87490361/156871323-e32080eb-159d-4919-9cb3-e7fbb813ae54.png"></center>  

**???**  
보기엔 무사히 작성된 것 같다!  
**그러나...**  
각 타이틀을 눌러보면 문제라는 걸 알 수 있었다.  

### 기존 글 = 새로운 글
<center><img width="879" alt="스크린샷 2022-03-05 오후 3 32 09" src="https://user-images.githubusercontent.com/87490361/156871752-02e1e315-2314-40eb-b799-ac066252a5b8.png"></center>  

링크가 아예 같으니, 새로 작성된 글 기준으로만 내용이 보인다는 것을 알 수 있었다...  
즉, 날짜 외에 카테고리와 파일 이름이 같을 경우 마지막 글을 기준으로만 보인다!  

## 해결 방법

같은 이름으로 포스트 파일을 만들지 말자...!  
만약 비슷한 이름이 필요하다면 1 2 3 같은 숫자를 붙이자!  
또한 `bundle exec jekyll serve`로 로컬 테스트를 꼭 실행해보자! 터미널에서 친절하게 충돌되는 걸 알려준다 ^^!  

<br>  
<br>  
