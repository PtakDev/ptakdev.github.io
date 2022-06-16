---
title: Setting up comments on Jekyll site with Chirpy theme
date: 2022-06-16 16:30:00 +0100
categories: [Docs, Chirpy]
tags: [jekyll, comments, giscus, chirpy]     # TAG names should always be lowercase
---

The process of setting up comments on Jekyll site with Chirpy theme is much easier than I could expect. 

## Step 1. Go to [giscus](https://giscus.app/){:target="_blank"} site.

## Step 2. Choose the repository
In the `Configuration` section, choose the website repo that giscus will connect to. As specified, we need to make sure that: 

1. The repository is public, otherwise visitors will not be able to view the discussion.
2. The giscus app is installed, otherwise visitors will not be able to comment and react.
3. The Discussions feature is turned on by enabling it for your repository.


![Repo meets criteria](https://drive.google.com/uc?export=view&id=1FUjNEPxMLtWGZS87k6FRtiHL0rwtG30k){: width="500" height="220" }
_When all criteria are meet, you will see above notification._

We also have to change `Discussion Category`. I have used recommended `Announcments` category.

You can leave the rest of the options as `Default`.

## Step 3. Find section Enable giscus, on the site.

You will find code similar to below.

```xml
<script src="https://giscus.app/client.js"
        data-repo="<GH_USERNAME>/<GH_USERNAME>.github.io"
        data-repo-id="<REPO_ID>"
        data-category="Announcements"
        data-category-id="<ID_CATEGORY>"
        data-mapping="pathname"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="bottom"
        data-theme="dark"
        data-lang="en"
        crossorigin="anonymous"
        async>
</script>
```

## Step 4. Edit **_config.yml** file.

Scroll down to section `comments` in `_config.yml` and in line `active` type `giscus`.
Now go to the `repo` line and type `<GH_USERNAME>/<GH_USERNAME>.github.io` and then in `repo_id` paste the value of `data-repo-id` from the prevoius point. In `category` type value of `data-category` from gisgus site and do same for `category_id` but use value of `data-category-id`. 

```yaml
comments:
  active: giscus         
  disqus:
    shortname:    
  utterances:
    repo:        
    issue_term:
  # Giscus options › https://giscus.app
  giscus:
    repo: <GH_USERNAME>/<GH_USERNAME>.github.io 
    repo_id: <REPO_ID>
    category: Announcements
    category_id: <ID_CATEGORY>
    mapping:          # optional, default to 'pathname'
    input_position:   # optional, default to 'bottom'
    lang:             # optional, default to the value of `site.lang`
```

> You can turn off comments in any post. All you have to do is add `comments: false` to the Front Matter.
{: .prompt-tip }
