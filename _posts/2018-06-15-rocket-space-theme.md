---
layout: post
title:  "Rocket Space Jekyll Theme"
date:   2018-06-15
excerpt: "Rocket space Jekyll theme for you."
project: true
tag:
- jekyll 
- rocket
- space
- blog
- about
- theme
comments: true
---

![Rocket Space Homepage](asd.png)    
    
<center><b>Rocket Space</b> is jekyll theme.</center>
     
 Please give a **star** for motivation and do not hesitate to change this theme. Good Luck!

<iframe src="https://ghbtns.com/github-btn.html?user=gurkanakdeniz&repo=rocket-space&type=star&count=true&size=large" frameborder="0" scrolling="0" width="160px" height="30px"></iframe>    
      
## Installation
* Fork the [Rocket Space repo](https://github.com/gurkanakdeniz/rocket-space/fork)
* Edit `_config.yml` file.
* Remove sample posts from `_posts` folder and add yours.
* Edit `index.md` file in `about` folder.
* Change repo name to `YourUserName.github.io`    
     
That's all.

## Preview

{% capture images %}
	https://raw.githubusercontent.com/gurkanakdeniz/rocket-space/master/assets/img/screenshots/home1.png
https://raw.githubusercontent.com/gurkanakdeniz/rocket-space/master/assets/img/screenshots/home2.png
https://raw.githubusercontent.com/gurkanakdeniz/rocket-space/master/assets/img/screenshots/allpost.png
{% endcapture %}
{% include gallery images=images caption="Screenshots of Rocket Space Theme" cols=3 %}

---

{% capture images %}
https://raw.githubusercontent.com/gurkanakdeniz/rocket-space/master/assets/img/screenshots/post1.png
https://raw.githubusercontent.com/gurkanakdeniz/rocket-space/master/assets/img/screenshots/home2.png
{% endcapture %}
{% include gallery images=images caption="Rocket Space Theme on Small Screen Size" cols=2 %}      
      
See a [live version of RocketSpace](http://gurkanakdeniz.github.io/) hosted on GitHub.      

## Site Setup
A quick checklist of the files you’ll want to edit to get up and running.    

### Site Wide Configuration
`_config.yml` is your friend. Open it up and personalize it. Most variables are self explanatory but here's an explanation of each if needed:

#### title

The title of your site... shocker!

Example `title: My Awesome Site`

#### bio

The description to show on your homepage.

#### description

The description to use for meta tags and navigation menu.

#### url

Used to generate absolute urls in `sitemap.xml`, `feed.xml`, and for generating canonical URLs in `<head>`. When developing locally either comment this out or use something like `http://localhost:4000` so all assets load properly. *Don't include a trailing `/`*.

Examples:

{% highlight yaml %}
url: http://user.github.io
url: http://localhost:4000
url: //cooldude.github.io
url:
{% endhighlight %}

#### reading_time

Set true to show reading time for posts. And set `words_per_minute`, default is 200.

#### logo
Your site's logo. It will show on homepage and navigation menu. Also used for twitter meta tags.

#### background
Image for background. If you don't set it, color will be used as a background.

#### Google Analytics and Webmaster Tools

Google Analytics UA and Webmaster Tool verification tags can be entered in `_config.yml`. For more information on obtaining these meta tags check [Google Webmaster Tools](http://support.google.com/webmasters/bin/answer.py?hl=en&answer=35179) and [Bing Webmaster Tools](https://ssl.bing.com/webmaster/configure/verify/ownership) support.

#### MathJax
It's enabled. But if you don't want to use it. Set it false in  `_config.yml`.

#### Disqus Comments
Set your disqus shortname in `_config.yml` to use comments.

---

### Navigation Links

To set what links appear in the top navigation edit `_data/navigation.yml`. Use the following format to set the URL and title for as many links as you'd like. *External links will open in a new window.*

{% highlight yaml %}
- title: Home
  url: /

- title: Blog
  url: /blog/

- title: Projects
  url: /projects/

- title: About
  url: /about/

- title: Rocket Space
  url: http://user.github.io
{% endhighlight %}

---

## Layouts and Content

Moon Theme use [Jekyll Compress](https://github.com/penibelst/jekyll-compress-html) to compress html output. But it can cause errors if you use "linenos" (line numbers). I suggest don't use line numbers for codes, because it won't look good with this theme, also i didn't give a proper style for them. If you insist to use line numbers, just remove `layout: compress` string from layouts. It will disable compressing.

### Feature Image

You can set feature image per post. Just add `feature: some link` to your post's front matter.

```
feature: /assets/img/some-image.png
or
feaure: http://example.com/some-image.png
```    
 This also will be used for twitter card:

![Rocket Space Twitter Card](asdasd.png)

### Comments
To show disqus comments for your post add `comments: true` to your post's front matter.

---

## Questions?

Found a bug or aren't quite sure how something works? By all means [file a GitHub Issue](https://github.com/gurkanakdeniz/rocket-space/issues/new). And if you make something cool with this theme feel free to let me know.

---

## License

This theme is free and open source software, distributed under the MIT License. So feel free to use this Jekyll theme on your site without linking back to me or including a disclaimer.
