### Introduction to Phishing 
---

**Starting my Investigation**
![Dashboard](SOCsimulator/first.png)
The first thing we notice after sometimes are the **5 alerts** in total (4 medium phishing and one higher-severity firewall alert)

> While we should start with the higher severity alert, we will start from the phishing alert,

---

*** First Alert-8814 Inbound Email Containing Suspicious External Link***

See the content and the description of the problem first ,
![1st Alert](SOCsimulator/hr1.png)
Now after revewing the description of the alert, we will take the owenrship of the alert
![owenrship of the alert](SOCsimulator/hr2.png)

Now we will investigate the domain and the URL as the alert was triggered bacause the email contained the external URL link,
We will see domain at SIEM, Search  `j.garcia@thetrydaily.thm` at SIEM we will get 4 events which if we see carefully the interaction bettwen emails and the link was not clicked by the recipeint; inorder to conform our guess let's search the domain and URL at online sandboxes like **VirusTotal** & **AnyRun**
![j.garcia@thetrydaily.thm](SOCsimualtor/hr3.img)


The domain and the URL looks fine so this must be false positive
![Report of 1st](SOCsimulator/hr4.png)

---

*** Second Alert-8816 – Access to Blacklisted External URL Blocked by Firewall***

This was triggerd when the user attempted to acces the external link which is listed in organization's balcklist, we will investigate further as we will see first did the firewall blocked or denied 

![2nd alert](SOCsimulator/firewall1.png) 

Now, let's see if the link was blocked or accesed ny firewall

![search the link at SIEM](SOCsimulator/firewall2.png)

As we can see the requested was blocked by the firewall

So this is **true postive** even though the firewall blocked it the user tried to acces the malicous URl which is balcklisted by organization

![2nd Report](SOCsimulator/firewall3.png)

Lately this does't require further escalation, as firewall successfully prevenetd any compromise.

---

*** Third Alert-8817 – Inbound Email Containing Suspicious External Link**

As we read through the description we can tell the sender domain is sketcy and with the external URL link in the email

![3rd alert](SOCsimulator/microsoft1.png)

There is a high chance this is a phishing email trying to impersonate as a microsoft judt looking at a domain and tying to create false felling of urgency, NOw we will see first at splunk if the recipient had clicked the link ot not

![no-reply@m1crosoftsupport.co](SOCsimulator/micosoft2.png)

The log  show's that the recipient has not clicked the link yet this is a good sign becasue this means he and the system has not been compromised 

So, this alert is **true positive** the user has not clciked the lick so it may or may not require further escalation 

![3rd Report](SOCsimulator/microsoft3.png)

The recommendation would be a change in the user credentaial and user traning along with the blocking if the domain via firewall and informing the recipient about the phishing email

---

*** Forth Alert-8815 – Inbound Email Containing Suspicious External Link***

Firstly,the name of the sender domain (urgents@amazon.biz) is not a legitimate one.Secondly,it creates urgency(“package will be returned within 48 hours”), and lastly uses a shortened link (bit.ly) to mask the real destination.

![4th alert](SOCsimulator/amz1.png)

Let's search in our SIEM if recipient has chlicked the link or not 

![urgents@amazon.biz](SOCsimulator/amz2.png)

We can see in the log of splunk that the user has not clicked the link meaning the system hasn't been compromised 

So this is true postive that needs further escalation or not casue the user has not clicked the link and the system is not compromised .We should block the suspicious domain and URL and inform the recipient to not click any links from this sender.

![4th report](SOCsimulator/amz3.png)

### We are safe…(until the next alert)

![complete](SOCsimulator/last.png)

---
***Alish***  
