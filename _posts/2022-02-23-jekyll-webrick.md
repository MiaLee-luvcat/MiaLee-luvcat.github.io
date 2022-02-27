---
published: true
title:  "[error.log] jekyll serve - webrick file 오류 "

categories:
  - Trouble Shooting
tags:
  - [Blog, jekyll, Github, Git]

toc: true
toc_sticky: true
 
date: 2022-02-25 03:04:30
last_modified_at: 2022-02-25 03:04:30
---


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