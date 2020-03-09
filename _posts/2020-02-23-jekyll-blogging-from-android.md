---
layout: post
title: Jekyll Blogging From Android
date: 2020-02-23 18:53
category: 
author: Prasanth kanna
tags: [Jekyll, Git]
summary: Jekyll Blogging directly from Android
image: jekyll-blogging-from-android/img.jpg
---

You have successfully published a blog via github-pages using Jekyll. You can edit or add a new post to that blog while on the go, from your mobile, instead of sitting in front of PC. Let's see how.

[SETUP](#setup)

[EDITING BLOG](#editing-blog)

## SETUP

* On your Android Device, Install: [Spck Code Editor](https://play.google.com/store/apps/details?id=io.spck&hl=en_IN){:target="_blank"}
* Get yourself a [Github Personal Access Token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line#creating-a-token){:target="_blank"}. Follow upto step 9 and store the copied token somewhere, because you can only see it once.
* Set your Username, Token and Email
* In `Spck App`, Go to Projects Tab. Click on the little Github Source Control Icon

![]({{site.baseurl}}/img/jekyll-blogging-from-android/spck_git.jpg)

* Click on `Git Credentials` and set your Username, Token and Email
* Click on `Clone Repo` and paste your Jekyll Blog Repo URL
* If your Git Credentials match, your repo will be cloned and will be available on the app to be modified. Else if you are getting any errors, check your credentials esp., Token

## EDITING BLOG

* If you have successfully cloned the Jekyll Blog Repo, Go to your `_posts` folder and modify any of your existing posts for testing this setup
* Click on the button highlighted in the following image:

![]({{site.baseurl}}/img/jekyll-blogging-from-android/spck_git_commit_push1.jpg)

* Click `Commit All` -> Enter Commit Message -> Press Enter
  
![]({{site.baseurl}}/img/jekyll-blogging-from-android/spck_git_commit_push2.jpg)

* After Committing is done, Click `Push` -> Press OK
* That's it!!! You have successfully modified your post from mobile.
* You can also add new posts and modify the blog as you want and commit and push to git to publish your updates.
* If you have already changed the blog from PC and want to get the latest copy on mobile, Just press `Pull`
