# ElevateLabs-internship-task2

## Objective:
Identify phishing characteristics in a suspicious email sample
---

## Step 1: Acquire a Phishing Email
I sourced a real phishing email in `.eml` format named `sample-10.eml` from the repository 'https://github.com/rf-peixoto/phishing_pot/blob/main/email/sample-10.eml'. It impersonates Microsoft and alerts the user about an "unusual sign-in activity" in an attempt to trigger panic and gain user interaction.

## The Email
The email seems like a normal email that from "Microsoft account team" stating that some individual from Moscow,Russia has signed-in into target user's microsoft account. This creates a sense of urgency in the target, leading them to take all actions specified in the email(common phishing tatic).
The email did not have any sign of threatning language, it only creates a sense of urgency amongst individual.

---


## Step 2: Header Analysis
I extracted the header from the `.eml` file and analyzed it using [MxToolbox Email Header Analyzer](https://mxtoolbox.com/EmailHeaders.aspx).

 Here's a full analysis of the email:  
https://mxtoolbox.com/Public/Tools/EmailHeaders.aspx?huid=53a8823d-4c86-4a01-bf9f-c40edcb11839

### Key Findings:
- **SPF:** fail  
  The sending IP `89.144.44.2` is not authorized to send on behalf of `access-accsecurity.com`.

- **DKIM:** none  
  No digital signature present. Likely a phish.

- **DMARC:** permerror  
  The domain does not have a valid DMARC(Domain-based Message Authentication, Reporting, and Conformance) policy.   Indicates that it is most likely a phishing email.
  
- **Return-Path:** `bounce@thcultarfdes.co.uk`  
  Does not match the `From` address (`no-reply@access-accsecurity.com`), indicating spoofing.

- **Reply-To:** `sotrecognizd@gmail.com`  
  Replies go to a personal Gmail account instead of Microsoft — a major red flag. Now we know that it a phishing    email.

---
Upon analysing this, I realised these were the indicators of a phishing email, which was constructed professionally. 

## Step 3: Analyze Email Content (Body)

### Email Summary:
- **From:** `no-reply@access-accsecurity.com`
- **Subject:** `Microsoft account unusual sign-in activity`
- **Fake IP mentioned:** `103.225.77.255 (Russia)`
- **Button/link:** `mailto:sotrecognizd@gmail.com`

### Phishing Traits Identified:
 Trait                    Description 

1. Spoofed Domain          : Domain mimics Microsoft but is unrelated. 
2. Suspicious Reply-To     : Gmail address to receive responses. 
3. No Authentication       : SPF, DKIM, and DMARC failed or misconfigured. 
4. Urgent Language         : Mentions "unusual sign-in" to provoke panic. 
5. Fake Button             :“Report The User” opens a mail client instead of a secure portal. This enables 
                             attacker to gain the victim email address, giving them a light that the victim would                              fall for a phishing email.
6. Image Tracker           : Loads a tracking pixel from `thebandalisty.com`. Malicious.

---

### Suspicious contents
**The fake button:-**
"Reports the user" this will open a mail client instead of portal where we wanted to report the suspicious user from Russia, that tried to log into our account. This mail client, will send my email to the attacker, indicating that I clicked on the button and giving them the light that I might fall for this email again.
**The Image Tracker:-**
This email has a tracker that will load a tracking pixel from `thebandalisty.com`. This will give the attacker my IP address and my email client, to further launch cyberattacks on me.

---
## Tools that I used
- MxToolbox Header Analyzer
- Sublime Text for `.eml` review
---

## Included Files

 File Name               Description                            

1. `sample-10.eml`         : The phishing email sample              
2. `email_header.txt`      :Extracted raw header (manually saved)  
3. `header_analysis_link.txt`:Link to full MxToolbox header results  
4. `README.md`             :This full report                        

---

## Conclusion
This phishing message shows typical spoofing methods: headers mismatch, unauthenticated sources, and a deceptive reply-to mechanism. This analysis made me more aware of header-based detection and red flag indicators for phishing attempts.
