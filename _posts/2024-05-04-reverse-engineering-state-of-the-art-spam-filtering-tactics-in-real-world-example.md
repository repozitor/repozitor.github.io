---
title: "Reverse engineering state-of-the-art spam filtering tactics in real world example"

author: repozitor

tags: [network, span, innovation, email]
categories: [network]

date: 2024-05-03
comments: true
---
# NOTICE
You are ``not allowed`` to use this techniques and tactics for malicious purposes. If you exploit this techniques, you should be responsible for that and writer of this text is not responsible for any consequences. If you are not agree with this, close this page and avoid reading. The purpose of this text is training system administrators and academic purposes by bolding a design flaw in current defense tools against spam filtering. 

# Background - Motivation
Some entities including people and companies are using non-public mail server for their communication. When I talk about the public mail servers, I am mentioning Gmail, Yahoo!, or any other public services. These servers have a nice dataset of spammers and they fight with spammers by having a wide variety of spams per day! However, Other brands are not providing promising service like Gmail. I recently contacted my service provider asking why sometimes my emails are not delivered in inbox. They shared a list of actions to resolve this problem. Unfortunately, I already followed that list without knowing them. Therefore, I always had this question why emails do not deliver in my recipient inbox while spammers can do this to my inbox. Alright, ok. Let's find that out.

## Motivation
Recently, I was receiving regular spam emails from some companies mostly located in china. There was an intersection between all of them:
1. Spams starting with this title: **"Re: ..."**
2. Spams starting with this title: **"Fwd: ..."**
3. Spams starting with this title: **"Fwd: Re: ..."**
4. A mix of **"Re: "** and **"Fwd: "** in the title


# Experiment - An unwanted practice
I always had this question why I am receiving these spams with this patterns. I never knew that. Until I recently applied for a Senior Software Engineering at a company. I've been asked to send back 3 URLs for them. Once I sent my email, I got a rejection notification immediately indeed. I tried again and same thing happened. I was thinking why my emails had been blocked! In no time, I was suspecting on putting URLs in my email. Down the road, I found that, email server disagrees with URLs in email's body. In fact, this is an important feature to mark an email as spam. I used another way to deliver the text that I wanted to. I don't know why, but this idea came to my mind to reply one of the previous emails that this company sent to me. I replied one of those emails with exact same text and URLs (completely legitimate - but innovative). ``BOOOOOM``. My email was accepted! Now, my brain started to collaborating everything in the past to find a reasonable answer for my old question. Why some spams comes with **"Re: ..."** in the title. In fact, spammers use this approach to deliver spam in our inbox. Let's reverse engineer the mail server spam filtering.

# Methodology
## Spam filtering metrics
An incoming email usually must pass certain sort of tests to be delivered in recipient mailbox. Here we can see some of them (not all of them, for sure):
1. Email should be free of any .exe or executable file. For sure, sending .exe and delivering these emails opens attack surface to the victims. In that way, spammer are able to send malicious files to people and use social engineering techniques to encourage them to open it.
2. Email should be free of any URLs. Accepting emails with URLs increase the risk of phishing attacks. Again, URLs are always the initial infection points for phishing attacks. Never ever click on these URLs even if your friend's aunt has passed away and his/her aunt wants to give you free money cause she has nobody left in the universe!
3. ...

## An stateful spam filtering rule
What is stateful filtering? A stateful filtering is a kind of filtering that keeps track and monitors the state of active network connections while analyzing incoming traffic and looking for potential traffic and data risks. Keeping the meaning of stateful in our mind, On top of that, it seems that the algorithm for spam-filtering are working in stateful mode. That means, even if you put .exe or URLs in your email or do a bad behaviors like mentioned, your email can still likely be delivered to your recipient. Why? Because mail servers are not likely want to interrupt communication between two parties. In fact, they might think the communication is already started from either side of points (inside org to out or vice versa) **plus** it passed previous screening spam filtering examination, then this email needs to be delivered. Therefore, MX server allows this email to be delivered.

# Scenario and evaluation
I think a ``design flaw`` now is being **bolded** in mail servers. Let's combine and summarize facts here:
1. Most likely mail servers are using stateful approach for whitelisting emails. If the communication is already established, then all follow up emails should pass the spam screening test no matter of what! That's why appending **"Re: "** can deliver spams in our mailbox.
2. There is a potential fight between filtering and passing rules. It seems that in this case, whitelisting has a higher hand!
3. There is no optimum way (anything less than __O(n)__) to lookup recipient emails if the incoming email replies one of the emails in the past. The reasons are:
   1. Anybody can have a huge list of emails. O(n) scanning and checking existing emails adds a huge overload in big businesses, thus a tremendous amount of delay in delivery/decision. Additionally, This can open a DoS attack too to keep filtering services super busy and stop mail servers responding and accepting new emails.
   2. Email titles may be subject to change! By appending new "Re: " or "Fwd: " or ... This will put title comparison in disadvantage position.
   3. Having no indexed data structure for checking.

In summary, attackers are able to append **"Re: "** and/or **"Fwd: "** to their email's title to bypass spam fighters and deliver the dangerous/harmful content to their victims. Due to the structure of mail storage, we have no effective way for detecting false or true established stateful communication. Using **"Re: "** is an easy option for mail servers while they open attack surface to users. **Avoiding interrupting the email communication is very important. However, we need a robust approach to detect good/bad stateful communication rather than relying on email title**. Before scientists come up with a nice solution, the easiest way for system administrators but not best, is to prioritize filtering higher than whitelisting while we may receive complaints from users! :(
