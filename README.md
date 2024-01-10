# Wing is Going To Market

## GTM Ownership

Ownership                             | Owner                             | Runbook
--------------------------------------|-----------------------------------|---------------------------
Commercial track lead                 | @staycoolcall911                  |
Open-source track lead                | @revitalbarletz                   | [Project template](https://github.com/orgs/winglang/projects/28/views/1)
Visual design                         | @amielpb                          |
TikTok, Instagram                     | @amielpb                          |
Copywriting and messaging             | @Chriscbr                         |
Landing pages                         | @NathanTarbert (with Nevo)        |
Video                                 | @NathanTarbert                    |
Social (twitter, linkedin)            | @NathanTarbert                    |
Product Hunt                          | @NathanTarbert (with Nevo)        | 
Influencers                           | @NathanTarbert (with Nevo)        |
Thought Leaders                       | @NathanTarbert (with Nevo)        |
Newsletter                            | @NathanTarbert, @MarkMcCulloh     |
Wingly                                | @NathanTarbert                    |
Analytics                             | @ainvoner                                 |
Content                               | @ShaiBer (via HitSubscribe, Asher, Nathan)|
SEO                                   | @ShaiBer (via HitSubscribe)               |
Case studies                          | @ShaiBer (via Adam PR)            |
Public relations                      | @ShaiBer (via Adam PR)            |
Open-source community                 | @revitalbarletz                   |
CFPs                                  | @revitalbarletz (via Sharone CFP) |
Conferences                           | @revitalbarletz                   |
Hackathons                            | @revitalbarletz (via Nevo)        |
Sales collaterals                     | @staycoolcall911                  |
Websites (winglang/wing.cloud)        | @amielpb                          |
Workshops, tutorials                  | TBD (squad)                       |
Documentation squad                   | TBD (squad)                       |
Communities (reddit, slack, discord)  | @NathanTarbert + TBD (squad)      |


---


## Newsletter structure

These are the sections that should be in each, any additional section is always welcome.
- First make sure the title of the newsletter
- Latest Wingly changelog topics with links to each item
- Next Wingnuts events
  - This may contain the Wingly update
  - Any future workshop or meetup
- Next Community events/office hour/meeting
  
## Newsletter sending instructions

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
