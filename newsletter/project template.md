**This is temporary here, should be converted to a proper project template**

- Don't use shortened links (slack join, or youtube videos) because it causes emails to go to spam. Use long versions instead. For instance, this is our full Slack join- join.slack.com/t/winglang/shared_invite/zt-23emj8uue-ZF4ijRNtdDOLO5F7iIz~NA
- Use markdown code blocks instead of pictures of code
- View our blog in light mode
- Create a new empty email, or clone the previous newsletter
- Copy the html of the blog from our website into the email (click in the mail and then click "advanced" in the toolbar that is added - copy the div with the markdown class
- Remove the first blockquotes html element
- Remove visual artifacts (look in the visual editor, not the html, there will probably be squares there you can delete)
- Add a prefix to all the links in the start so that they are full links to the different sections in the blog on our website
- Use the same settings of the previous newsletter in terms of lists, from address, etc. - this will already happen automatically if you cloned the previous newsletter
- Change the subject to be relevant to this newsletter. You can use A/B test for it
- Test the email in Husbpot with different devices and clients
- Send the email to private email inboxes and see that it arrives OK, not in the Spam or Promotions folder and that when looking at the email source it passes all tests (DKIM, SPF, etc..)
- Make sure that there are no warning from Hubspot before sending and fix whatever you see, except for the ones about the lack of personalization tokens. If you see a warning about shortened links then look in youtube links that they are not youtu.be, also in the slack join link - these are the most common offenders
