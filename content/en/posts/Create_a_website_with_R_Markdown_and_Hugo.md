+++
title = "Create a website with R Markdown and Hugo"
date = "2019-12-03T17:56:58-05:00"
lastmod = "2021-01-26T18:12:58-05:00"
categories = ["Website"]
tags = ["Hugo","R markdown"]
slug = "Create_a_website_with_R_Markdown_and_Hugo"
toc = true
draft = false
+++
<!-- TOC -->
<!-- /TOC -->

In this tutorial I will show you how to create your own website with R package `blogdown`, Hugo, Github, and Netlify in 1h without any background.

# Program setting
Before creating the website, we have to install several softwares.

[R](https://www.r-project.org/) is a open source programming language and environment for statistical computing and graphics.

[R studio](https://rstudio.com/) is an integrated development environment for R.

[Blogdown](https://github.com/rstudio/blogdown) is an R package to generate static websites and blogs based on R Markdown and Hugo

[Hugo](https://gohugo.io/) is a popular open-source static site generator.

[Netlify](https://www.netlify.com/) is a platform for hosting and serveless backend service for static websites

[Github](https://www.github.com/) is a softwared development platform offering distributed version control and source code management.

[Git](https://git-scm.com/download/) is a distributed version-control system for tracking changes in source code during software development.

# Preliminary preparations

## Software installation

Before creating your website, make sure you install [R](https://cran.r-project.org/mirrors.html) and [R studio](https://rstudio.com/products/rstudio/download/#download).

## Create a Github repository

Ater registering a Github account, you should create a new repository for the website. It’s better to use your domain name as the repository name. Check to initialize with a **README** and **add .gitignore:R**

![Create a new repository in Github](https://res.cloudinary.com/azuretimes/image/upload/v1575387770/website/git_respository.png)

After clicking **Create repository**, you will go back to the main page of the new repository. Clike the green **Clone or download button**, click on the clipboard icon to copy the clone URL with HTTPs for your new repository. You’ll paste this text into R studio in the next section.

![Clone with HTTPS](https://res.cloudinary.com/azuretimes/image/upload/v1575389544/website/respository_URL.png)

## Custom domain Registration [optional]

A domain name to a website is similar to a street address to a house. Although you can use free subdomain names provided by Github or Netlify, I highly recommend you to regsiter your own domain with a minimal cost(~$10/per year).

Popular domain name registrars includes [Namecheap](https://www.namecheap.com/), [Cloudflare](https://www.cloudflare.com/) and [GoDaddy](https://www.godaddy.com/).
## Create a website in R studio

### R studio setting

`RStudio -> Preferences -> Sweave >- Weave Rnw files using: knitr`

`RStudio -> Preferences -> Sweave >- Typeset LaTex into PDF using: XeLaTeX`

### Blogdown Installation

Install `blogdown` package in R studio.

```
#Install blogdown package from CRAN
install.packages("blogdown")

#Install static site generator Hugo
blogdown::install_hugo()

#Check hugo version
blogdown::hugo_version()

#Update hugo the latest version
blogdown::update_hugo()
```

### Version control via Git
`File -> New project -> New Project >- Version Control >- Git`

Paste repository URL with HTTPS in previous Github step into **Repository URL** and choose a directory to store your website.

![clone_github](https://res.cloudinary.com/azuretimes/image/upload/v1575390048/website/Clone_github.png)

### Setting gitignore

Now you are “in” the R studio project. To avoid submitting specific files or dictinoaires, you should edit `.gitignore` file in the file viewer panel in Rstudio. More details can be found here. Edit the file as below:

```
public  #If using netlify
.DS_store #For mac user; if wondow user, Thumbs.db instead
blogdown
.Rproj.user
.Rhistory
.RData
.Ruserdata
static/figures
```

The files or dictionaries above will not be submitted to Git.

### Initializing Blogdown

There are multiple [Hugo themes](https://themes.gohugo.io/). Use [hugo-coder](https://themes.gohugo.io/hugo-coder/) theme as an example, click the **Homepage** button in the Coder theme website to enter the corresponding github page (See snapshot below). you can see in the top left corner of the page, the repository for this `hugo-coder` theme is maintained by `luizdepra` in the folder `hugo-coder`. So copy the repository as `luizdepra/hugo-coder` for future theme choice. 

![hugo-coder_theme](https://res.cloudinary.com/azuretimes/image/upload/v1575397130/website/theme.png)

Create a new project in R studio: 

`File -> New project -> New Project -> New Directory >- Website using blogdown`

In the next window, specify the directory name of the blog (I suggest using your **domain name**) and the subdirectory to place blogs and theme. The default hugo theme is [yihui/hugo-lithium](https://github.com/yihui/hugo-lithium). You can replace the Hugo theme with the repository name of your favorite theme, e.g. `luizdepra/hugo-coder` for hugo-coder theme. Then click **Create Project**.

![Choose_blowdown_theme](https://res.cloudinary.com/azuretimes/image/upload/v1575397090/website/blogdowntheme.png)

**You are done with the website!**

You can view the website locally by clicking the menu to find Addins button in the top-right: `Addins >- Serve Site` to view your website in the **Viewer window** in R studio.

![addins](https://res.cloudinary.com/azuretimes/image/upload/v1575398708/website/Addins.png)

### Customize the theme

The configuration file `config.toml` contains all the parameters to for your site.

- Change the `baseurl` to your domain name with `https://`(In my case is `baseurl = https://ziweipan.me/`). **Attention:The URL should always end with a / trailing slash** At this point, you haven’t deployed your site yet (we will talk about it later), so we can view it locally you can use `Addins -> Serve Site`, or run `blogdown::serve_site` function.

- You can also change `title`, `description` etc.

- To add comments to the blog, add your your disqus shortname (disqusShortname = “"). Here is a tutorial for installing disqus on Hugo: https://notes.peter-baumgartner.net/tutorial/how-to-install-disqus-on-hugo/.

- For multilingual mode in `hugo-coder` theme, check [Multilingual Mode](https://github.com/luizdepra/hugo-coder/wiki/Multilingual-Mode) for more details.

- More custom layouts options can be found in [Yihui’s Markdown tutorial](https://bookdown.org/yihui/blogdown/custom-layouts.html)

# Write blogs in R studio

## Add a new blog

Since our website is ready, we can write our blogs in the website: `Addins >- New Post`

![Write new post](https://res.cloudinary.com/azuretimes/image/upload/v1575399487/website/newpost.png)

**Filename** will be automatically generated after filling **Title**. All the new posts go into the `content/post` folder since `post` folder is the defalut subdirectory. You can add your **categories** and **Tags**.

## Global options setting
In startup profile file, you can set up global options to avoid typing options every time you start a new R session: 
```
file.edit("~/.Rprofile")
```

Default options can be found [here](https://bookdown.org/yihui/blogdown/global-options.html). You can make some changes on your preference. For example, if you prefer writing Rmd posts (instead of the default *.md), and want the author of new posts to be “John Doe” by default. You can set these options in the profile file:
```
options(blogdown.ext = ".Rmd", blogdown.author = "John Doe")
```
In this case, when you write a post, the fields “Author” and “Format” will be automatically populated.

# Host your website in Netlify

Now you have your local website with post. You can ultilize Netlify to build, test, and deploy websites.

## Connect with Github repository
You can [sign up Netlify](https://app.netlify.com/signup) with your Github account. In your home page of Netlify, click `New site from Git >- Continuous Deployment: GitHub`, then select your existing repository of the website.

![Create_site_on_Netlify](https://res.cloudinary.com/azuretimes/image/upload/v1575406659/website/Netlify.png)

In the next page, You can either use default Hugo version explained in [Netlify](https://docs.netlify.com/configure-builds/common-configurations/#hugo), or assign specific hugo version:`Show advanced >- New variable`, then change build setting in the environment(See snapshot above): fill `Key` with `HUGO_VERSION` and fill `Value` with specific hugo version. PS: to check the hugo version installed in R, use  `blogdown::hugo_version()`.

Then click **Deploy site** to be guided to the deploy homepage.

## Connect domain and domain name registrars

In your site homepage on Netlify, click **Settings**. You can see setting menu in the bottom left corner of the page, click `Domain management -> Domains -> ... -> Edit domain`, then add your own domain name.

![Domain_management](https://res.cloudinary.com/azuretimes/image/upload/v1575408039/website/domain_management.png)

Then click `Go to DNS panel` to go to Domain name system (DNS) settings. In `DNS settings >- nameservers`, copy the custom nameservers generated by Netlify.

![Nameservers_Netlify](https://res.cloudinary.com/azuretimes/image/upload/v1575408494/website/Nameservers_Netlify.png)

## Point your domain’s nameservers to Netlify

Go back to your domain provider website. Take [Namecheap](https://www.namecheap.com/) for example, log in your account, go to `Dashboard -> Domain list -> Manage -> Nameservers -> Custom DNS`, paste the custom nameservers(See the snapshot above) in Netlify.

![Assigning_Nameservers_in_Namecheap](https://res.cloudinary.com/azuretimes/image/upload/v1575408929/website/Nameservers_namecheap.png)

All the settings are done and now we can focused on writing the blogs in R studio.

# Keep blogs updated online from blogdown via Github to Netlify

In previous introduction we introduce how to write new blogs but all the files or changes are done locally. so we have to update the posts online to Netlify via Github.

Go back to R studio.

**Commit changes**: Clicking the top right menu `Git -> Commit`. Select all changed files and write a commit message to confirm these changes.

![Commit_to_Github](https://res.cloudinary.com/azuretimes/image/upload/v1575418334/website/Commit.png)

**Push changes**: Click on the **push** button on top right menu to transfer all your committed changes to GitHub. A window will open, and you can see if the changed files are transferred successfully.You can also check github repository to check the status of your commited changes.

![Push_to_Github](https://res.cloudinary.com/azuretimes/image/upload/v1575418487/website/push.png)

Meanwhile, you can log in Netlify to monitor deploy status since Netlify automatically builds deploy previews for all pull requests. In Netlify, Click `Preview deploy` to go to the URL of your new website, or directly open your website with your domain name.

![Preview_deploy](https://res.cloudinary.com/azuretimes/image/upload/v1575419521/website/previewdeploy.png)

# Website is online!(finally)

**Congratulations! Your website is online now!**

You can enter your custom domain to check your website.


# Reference: 

[Yihui Xie - Blogdown: Creating Websites with R Markdown](https://bookdown.org/yihui/blogdown/)

[Peter Baumgartner - Blogdown Tutorial](https://notes.peter-baumgartner.net/tutorial/blogdown-tutorial-part-1/)

[Alison Hill - Up & Running with blogdown](https://alison.rbind.io/post/2017-06-12-up-and-running-with-blogdown/)

[Setting up our blog with RStudio and blogdown I: Creating the blog](http://estebanmoro.org/post/2019-02-02-setting-up-your-blog-with-rstudio-and-blogdown-i-creating-the-blog/)

[钟浩光 - 用 R 语言的 blogdown+hugo+netlify+github 建博客](https://cosx.org/2018/01/build-blog-with-blogdown-hugo-netlify-github/)