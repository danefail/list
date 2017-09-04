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
