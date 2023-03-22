---
title: Setting Up Utterances as Commenting System
description: How I selected utterences for the comment system of this blog and
  how easy was it to setup.
author: syncster
date: 2023-03-22T06:05:18.770Z
tags:
  - comment system
---

Hello, and welcome back to my C programming journey blog. I'm excited to share my second article with you today, and in this post, I'm going to be talking about how I set up a commenting system on this blog using a service called Utterances.

Instead of just me talking,I wanted to add some dynamic content to my blog, and one of the things I thought would be a commenting system so that I can get the insights from readers. However, I didn't want to use a service like Disqus, which stores the comment data on their servers. Instead, I decided to go with Utterances, which stores the comment data in issues on GitHub.

## What is Utterances?

Utterances is a commenting system that uses GitHub issues as the backend. When someone leaves a comment on your blog post, Utterances creates a new issue in your GitHub repository with the comment data. You can then manage your comments and reply to them directly in the GitHub issue tracker.

The great thing about Utterances is that it's completely free and open-source, and it's very easy to set up on your blog.

## How I Set Up Utterances

I found setting up Utterances very straightforward, here’s what I did:

1. First, head over to the Utterances website and click on the "Get started" button.
2. Next, you'll need to authorize Utterances to access your GitHub account. Click on the "Authorize GitHub" button and follow the prompts to give Utterances access.
3. Once you’ve authorized Utterances, choose the repository of your static site where the comments will be stored.
4. After you've chosen your repository, you'll need to configure Utterances by adding a script to your blog's HTML code. The Utterances website provides detailed instructions on how to do this based on the static site generator you're using. Here is what worked for me:

```
 <script src="https://utteranc.es/client.js"
  repo="{username/repo_title}"
  issue-term="pathname"
  theme="github-light"
  crossorigin="anonymous"
  async>
 </script>
```

Just change the `{username/repo_title}` to your username and repository. Place the code below each article of your blog and see the result!

5. Finally, you can customize the look and feel of your Utterances comments by editing the CSS on your blog or change the theme in the JS code you inserted.
   And that's it! Once you've completed these steps, your blog should have a fully-functional commenting system powered by Utterances.

## Conclusion

Adding a commenting system to my blog has been a great way to engage with my readers and get feedback on my C programming journey. I chose to use Utterances because it stores the comment data on my own GitHub repository, which gives me more control over my data.

Setting up Utterances was a straightforward process, and I'm really happy with the results. If you're thinking about adding a commenting system to your blog, I highly recommend giving Utterances a try.

Thanks for reading, and I hope you found this post helpful. Stay tuned for more updates on my C programming journey!
