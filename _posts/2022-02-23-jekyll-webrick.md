---
published: true
title:  "[error.log] jekyll serve - webrick file 오류 "

categories:
  - Trouble Shooting
tags:
  - [Blog, jekyll, Github, webrick, error.log]

toc: true
toc_sticky: true
 
date: 2022-02-22 02:04:00
last_modified_at: 2022-02-28 03:04:30
---

## jekyll 테마를 설치하다가 마주한 webrick 오류

깃헙 블로그에 jekyll 테마를 설치하다 보면 수많은 종류의 오류들과 마주하게 된다.
그중 하나인 **cannot load such file -- webrick (LoadError)** 에 대해 다뤄보고자 한다.

<br>

### 어떻게 마주하게 되는가?
`bundle exec jekyll serve`이 명령어는 `bundle install`을 진행한 후 로컬에서 잘 됐는지 확인할 때 쓴다.
하지만 이 `bundle exec jekyll serve`를 사용했을 때 간혹 이런 오류를 접하게 된다.
<br/>

```bash
// siri-syl은 내 깃헙 계정이다
// l_siri는 내 맥북 컴퓨터 이름이다.

✘  ~/siri-syl.github.io   master ±  bundle exec jekyll serve
Configuration file: /Users/l_siri/siri-syl.github.io/_config.yml
            Source: /Users/l_siri/siri-syl.github.io
       Destination: /Users/l_siri/siri-syl.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
       Jekyll Feed: Generating feed for posts
     Build Warning: Layout 'page' requested in about.markdown does not exist.
          Conflict: The following destination is shared by multiple files.
                    The written file may end up with unexpected contents.
                    /Users/l_siri/siri-syl.github.io/_site/index.html
                     - index.html
                     - index.markdown
                    
                    done in 1.531 seconds.
 Auto-regeneration: enabled for '/Users/l_siri/siri-syl.github.io'
                    ------------------------------------------------
      Jekyll 4.2.1   Please append `--trace` to the `serve` command 
                     for any additional information or backtrace. 
                    ------------------------------------------------
/Users/l_siri/.rbenv/versions/3.0.2/lib/ruby/gems/3.0.0/gems/jekyll-4.2.1/lib/jekyll/commands/serve/servlet.rb:3:in `require': cannot load such file -- webrick (LoadError)

```
<br>

**이미지의 경우**

<center><img width="735" alt="스크린샷 2022-02-27 오후 10 40 45" src="https://user-images.githubusercontent.com/87490361/155889000-8c206744-59d6-4069-8b22-5bee2123c2f4.png"></center>

이런 경우 빨갛게 되어 있는 문장은 뒤로 하고 볼드체로 되어 있는
**cannot load such file -- webrick (LoadError)**
를 주목하면 된다.
한마디로 webrick가 없어서 불러올 수 없다는 것이 되니, webrick를 추가하면 된다!
<br>

### 해결 방법

터미널에 `bundle add webrick`을 쳐서 webrick를 추가하면 된다!

<br>