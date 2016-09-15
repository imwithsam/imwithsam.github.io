---
layout: post
title: Email Delivery Best Practices
---

There are several things you can and should do to set your transactional and
marketing emails up for maximal delivery rates. In this post, I am going to
highlight three important ones:

1. SPF
2. DKIM
3. DMARC

### SPF

SPF stands for Sender Policy Framework. You basically tell your domain's name
server that the mail server you're sending from is approved. Depending on how
the receiver's email server is configured, it takes this approval into account
when it decides whether or not to deliver your email to the recipient.

To do this, you'll have to create or update the SPF TXT entry on your DNS. The
TXT entry will look something like:

```
v=spf1 a mx include:spf.mtasv.net include:_spf.createsend.com ~all
```
Breaking this down, the `v=spf1 a mx` part at the beginning identifies the SPF
version and what to match on. This is followed by an `include:` for each mail
server you want to register as approved, in this case `spf.mtasv.net` and
`_spf.createsend.com`. Finally, there is one `~all` soft fail mechanism at the
end. Your SPF TXT entry will probably look similar to this one, but your mail
service will provide you with the exact values needed. Refer to [SPF Record
Syntax](http://www.openspf.org/SPF_Record_Syntax) for more information on these
values.

One limitation of SPF is it does not take the `From` domain into account. It
only checks the `Return-Path` domain. This is where DKIM comes in.


### DKIM

DKIM stands for Domainkeys Identified Mail. DKIM is similar to SSL. It sends a
signature generated with a private key along with each of your emails. Your
public key is stored in a DKIM entry on your DNS. The receiving mail server uses
this public key to determine if your signed email was altered from its original
state.

### DMARC

DMARC stands for Domain-based Message Authentication, Reporting & Conformance.
It provides recipient mail servers with your recommended policy for handling
potentially phony emails with your domain name. Each recipient's mail service is
reponsible for how it handles questionable emails, but with a DMARC record in
place you can help them make better decisions. Furthermore, your DMARC record
can specify that reports of these potentially spoofed emails be sent to you.
These are all important in helping you to keep the trust factor of your domain
as high as possible and maximize the chances that the emails you actually send
are not filtered out before reaching your intended recipients.
