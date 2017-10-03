# The DANE fail list

DANE is a standard that allows TLS certificates to be bound to DNS names using DNSSEC.
As of today (2017), one of its most prominent uses is for email; bringing transport
encryption to SMTP. A few major MTAs (such as Postfix, Cloudmark and Halon) supports
it, and a growing number of domains are being signed.

If domain is DNSSEC-signed, but its DNS server fail to give proper answers in response
to TLSA queries, email delivery to this domain will fail for senders using DANE. The
most common problem is servers responding with SERVFAIL.

This is a verified list of DNSSEC-signed domains, which doesn't give proper TLSA
responses, and therefore needs to be excluded from DANE verification, in order to
have email delivered to them.

See https://danefail.org/ for more information, or create a pull request for suggested
updates.

## Reach out before adding
Before adding a domain to the list, contact the domain in question (info@ etc, as well as postmaster@ and hostmaster@) and if possible the DNS service provider, possibly by using the email template below:

> Hi,
>
> The domain XXX [hosted at YYY] ZZZ which prevents encrypted email delivery to this domain from email systems using DANE. We urge you to fix this (or disable DNSSEC), but in the meantime we like to add you to a list of domains that should be bypassed, so that email delivery doesn’t fail to your domain: https://danefail.org
>
> We’re sending this email to make sure that you don’t use DANE email encryption. Even if you’re added to the list, you’ll be automatically removed, should the DNS server be fixed.
>
> [unbound-host example]
>
>Thanks,

where XXX is the domain, YYY is the DNS and/or email provider, ZZZ is the problem (such as "have broken DNSSEC" or "doesn't respond to TLSA queries") and the example could be something like:

```
$ unbound-host -f /etc/unbound/root.key -v -t TLSA _25._tcp.mx-of-XXX
Host _25._tcp.mx-of-XXX not found: 3(NXDOMAIN) (BOGUS (security failure))
```
