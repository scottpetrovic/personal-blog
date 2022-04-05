---
title: "Mobile version of Wordpress in 3 steps"
date: "2009-06-19"
categories: 
  - "computer"
  - "interaction-design"
  - "web-design"
tags: 
  - "mobile-design"
  - "wordpress-plugins"
---

I just spent 15 minutes getting a mobile version of the blog to work. It was dead easy.

**Step 1:** [Download the plugin](http://wordpress.org/extend/plugins/wordpress-mobile-edition/) (don't use the auto-installer if you have 2.8)

**Step 2:** Drag the files in the respective folders (screenshot using FileZilla FTP Client)

<table border="1" cellspacing="0" cellpadding="0"><tbody><tr><td><a href="http://blog.scottpetrovic.com/wp-content/uploads/2009/06/mobile_plugin.gif"><img class="alignleft size-full wp-image-660" title="mobile_plugin" src="images/mobile_plugin.gif" alt="mobile_plugin" width="290" height="372"></a><a href="http://blog.scottpetrovic.com/wp-content/uploads/2009/06/mobile_theme.gif"><img class="alignleft size-full wp-image-661" title="mobile_theme" src="images/mobile_theme.gif" alt="mobile_theme" width="247" height="348"></a></td></tr></tbody></table>

**Step 3:** Activate Plugin. That is it!

### Testing to see if it works if you don't have a mobile device

[![final_mobile](/images/final_mobile.gif "final_mobile")](http://blog.scottpetrovic.com/wp-content/uploads/2009/06/final_mobile.gif)

If you don't have a good way to test it, run Firefox and get the extension [User Agent Switcher addon](https://addons.mozilla.org/en-US/firefox/addon/59). This will allow Firefox to trick websites to thinking you are running anything from IE4 to iPhone 3.0 .  The default list doesn't have many agents, so [download this bigger list](http://blog.scottpetrovic.com/wp-content/uploads/2009/06/switcher.xml) I found in the forum and import it.

Now just change your user agent to something like iPhone and go to your website. You should see your website mobified. Since the mobile version has its own theme, it can be customized just like any other theme. I really like how the theme uses the [one-window drill down design pattern](http://designinginterfaces.com/One-Window_Drilldown) for navigating. Good way to mesh mobile design into existing web design usage.

I will probably spend a little more time in the code seeing how it recognized the user agent and swaps the theme.
