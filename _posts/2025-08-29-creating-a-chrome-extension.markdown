---
title: Creating a Chrome Extension to Query Multiple LLMs
author: kyhle
date: 2025-08-29 12:00:00 +0200
categories: [Technical, Random]
description: Hi all, My name is Kyhle Öhlinger and this blog post forms part of my personal blog. If you enjoy any of the posts, feel free to reach out and let me know :) 
image:
  path: /assets/img/chrome_extensions.jpg
  width: 800
  height: 500
--- 

I've been increasingly bouncing between ChatGPT, Gemini, and Claude depending on the task. LLMs are powerful but I tend to lose track of my open tabs quite frequently. I was thinking about methods that could make it easier to send questions to LLMs from different web pages and came up with the idea of a browser extension. You may say "but Kyhle, don't they have their own implementations which already to this?" and you would be right. Google and OpenAI both have official methods that they promote to solve this very issue. Google has `@gemini` and `@aimode` as shown below:

![img-description](/assets/img/GoogleChrome/20250829135831.png)
_Using @Gemini in the Address Bar_

![img-description](/assets/img/GoogleChrome/20250829140310.png)
_Using @AImode in the Address Bar_

ChatGPT also has their own [Chrome Extension](https://chromewebstore.google.com/detail/chatgpt-search/ejcfepkfckglbgocfkanmcdngdijcgld) which you can use to search directly from the Address bar through the `@` symbol. 

![img-description](/assets/img/GoogleChrome/20250829140846.png)
_Using ChatGPT in the Address Bar_

However, this leads to the same issue as using the platforms individually. Not only do you need to remember the different methods that a single tool can use from the address bar, but you also need to know how to do it for every AI tool which offers similar functionality. This blogpost showcases the very basic Chrome extension that I created to easily pick between the tools, the extension can be found in my [GitHub repo](https://github.com/KyhleOhlinger/scripts/tree/main/Smart%20AI%20Chrome%20Extension). 

# Building the Extension

In essence, this extension provides two sets of functionality:
1. **Popup UI**: type a query, pick an LLM, opens a new tab with your question sent to that LLM.
2. **Google Search Bar Popup**: type a question and select the LLM that you want to send it to straight from the Google search bar. 

#### File Structure & Manifest

First, here’s what the extension's structure looks like:

```
Smart AI Chrome Extension/
├── background.js
├── content.js
├── icons
│   ├── robot_icon-128.png
│   ├── robot_icon-16.png
│   ├── robot_icon-32.png
│   ├── robot_icon-48.png
│   └── robot_icon.png
├── manifest.json
├── popup.html
├── popup.js
├── README.md
└── styles.css
```

If you'd like to learn more about the different file types and their purpose, Google has some documentation on their [developer portal](https://developer.chrome.com/docs/extensions/get-started) which I found useful. 

#### Installing the Chrome Extension

To install the extension in your own browser, you will need to do the following:
1. Navigate to `chrome://extensions`
2. Enable Developer mode
3. Click on "Load Unpacked" and select the extension folder (which you can download from my GitHub Repo)
4. The new extension should appear in the list of installed extensions

![img-description](/assets/img/GoogleChrome/20250828151502.png)
_Installing a New Chrome Extension_

#### Using the Smart AI Chrome Extension

Now that it has been installed, you will be able to make use of the functionality. You can query the LLMs by either selecting the Extension directly, or through the search bar of Google.com. 

![img-description](/assets/img/GoogleChrome/20250828151642.png)
_Available Chrome Extension Functionality_

If you want to use the extension directly, click on the extension icon, type in your question, select the AI platform you want to send the question to, and finally click "Send Question".

![img-description](/assets/img/GoogleChrome/20250828151720.png)
_Using the Chrome Extension Directly_

If you want to use the extension through the Google search bar; type in your question, click on the extension icon, and select the AI platform you want to send the question to. Alternatively, you can use shortcuts on MacOS (cmd+enter) or Windows (alt+enter) to select the LLM:

![img-description](/assets/img/GoogleChrome/20250828151804.png)
_Using the Chrome Extension From the Google Search Bar_


# Challenges
While I was creating this I faced two issues, the first being the [ExtensionInstallBlocklist](https://chromeenterprise.google/policies/?policy=ExtensionInstallBlocklist) from Chrome. My initial iterations of the extension tried to use the `clipboardRead` permission which was blocked by my browser:

![img-description](/assets/img/GoogleChrome/20250828145512.png)
_Google Chrome Extension Settings_

This has since been bypassed by using alternative methods to send the data, but if you're creating your own extension and find that it is blocked, it could be due to the Extension settings. The second challenge (which is still an issue) is that the text data which is pasted into OpenAI's ChatGPT includes the previously pasted data before overwriting it with the new data. I'm not sure why this is happening so if you find a solution to this issue, please let me know! 


# Conclusion

This is definitely not a perfect solution and it will need to be modified for any other LLMs that you are using in this manner, but it was a pretty fun way for me to test out "Vibe coding" with Cursor (as can be seen in the codebase) while also ending up with a solution to a problem that didn't even truly exist.

I hope you found this post useful and if you end up trying out the extension, please let me know how it goes! As always, if you have any questions or comments, please reach out!