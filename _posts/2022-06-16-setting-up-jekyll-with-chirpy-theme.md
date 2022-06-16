---
title: Setting up Jekyll site with Chirpy theme
date: 2022-06-16 10:00:00 +0100
categories: [Docs, Jekyll]
tags: [jekyll,ubuntu 20.04,chirpy]     # TAG names should always be lowercase
---

> I have followerd TechnoTim [`YouTube video`](https://youtu.be/F8iOU1ci19Q){:target="_blank"} to set up this website and host it on a GitHub site.
{: .prompt-info }

>I am running Jekyll on local enviroment on Ubuntu 20.04 Virtual Machine and I am using VS Code on my local Windows machine, with the Remote - SSH extension to edit files locatet in VM. 
{: .prompt-info }

##### Requirements: 

`GitHub`, [`Bundler`](https://bundler.io/){:target="_blank"}, `Ubuntu VM`


# Setting up Local enviroment

#### Step 1. Copy Chirpy repository
Create new repository from the [Chirpy Starter](https://github.com/cotes2020/chirpy-starter/generate){:taget="_blank"}, and name it <GH_USERNAME>.github.io, where GH_USERNAME represents your GitHub username.

### Step 2. Clone repo to local
```shell
git clone git@github.com:<GH_USERNAME>/<GH_USERNAME>.github.io.git
```

#### Step 3. Install Dependencies
Before running for the first time, go to the root directory of your site, and install dependencies as follows:
```shell
bundle
```

>To install Bundler, I had to edit a `/etc/gai.conf`{: .filepath} file as I had some probles with IPv6 setup. I added `precedence  2a04:4e42::0/32  5` to it. You can read more in [this](https://stackoverflow.com/questions/49800432/gem-cannot-access-rubygems-org){:target="_blank"} Stackoverflow post.
{: .prompt-warning }

#### Step 4. Run site local
Run the following command in the root directory of the site:
```shell
bundle exec jekyll s
```
>I had to install ruby-dev package in order to meke everything work.
{: .prompt-warning }

# Creating your first post

### Step 1. Edit _config.yml file.
Locate the `_config.yml` file and open it. We need to change few settings.

```yaml
# Change to your timezone › http://www.timezoneconverter.com/cgi-bin/findzone/findzone
timezone: Europe/Madrid

title: Site Title                       # the main title

tagline: Site Sub-Title                 # it will display as the sub-title

description: >-                         # used by seo meta and the atom feed
  Website description.

# fill in the protocol & hostname for your site, e.g., 'https://username.github.io'
url: 'https://<GH_USERNAME>.github.io'

github:
  username: <GH_USERNAME>               # change to your github username

twitter:
  username: <TW_USERNAME>               # change to your twitter username
```
> These are just some of the basic settings examples. You adjust the options accoringly to your needs. 
{: .prompt-tip   }

### Step 2. Create markdown file
In VS Code, locate a floder `_post`{: .filepath} and create new `.md` file. 
You can copy and paste below for tests.

```markdown
---
title: My first post
date: 2021-06-15 12:45:00 +0100
categories: [Docs]
tags: [tag]     # TAG names should always be lowercase
---
### This is H3 Title 
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse vestibulum tellus tristique nibh imperdiet pellentesque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed a ipsum a massa pulvinar eleifend. Pellentesque sodales feugiat eros non mattis. In et augue non urna porttitor vestibulum ornare sit amet ligula.

```

### Step 3. Save the file and refresh your website.

You should be able to see your post on the home page. 

# Hosting the site on GiHub

### Step 1. Make sure your repo is public on GitHub. 
### Step 2. Commit yout code to GitHub. 

```shell
git add .
git commit -m "First post: My fist post"
git push
```

After you pushed your code to GitHub, you should be able to see in GitHub, in tab Actions of your repo, workflow running. When it's finished, go to Step 3.

### Step 3. Change GitHub Pages source
Go to the setting of your repository and on the left site panel choose `Pages`. Next you need to find Source seection and change the branch to `gh-pages` and press `Save`.

### Step 4. Go to your website!

##### References: 

[`Chirpy`](https://github.com/cotes2020/jekyll-theme-chirpy){:target="_blank"}
[`Bundler`](https://bundler.io/){:target="_blank"}
[`Meet Jekyll - The Static Site Generator`](https://youtu.be/F8iOU1ci19Q){:target="_blank"}


