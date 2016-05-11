# Email

The on-premise Rollbar instance sends emails via standard SMTP.  The
server to use can be configured when running the `configure.sh` program.
This defaults to using the bundled postfix server solution.

We setup your on-premise Rollbar instance to send emails with a from
address patterned like `rollbar@yourdomain.com`.  The username part of
the address is always `rollbar`.  The `yourdomain.com` portion comes
from the FQDN you specify when running configure.sh.  This gives you a
predictable from address that you can add to your spam filters, firewall
whitelists, etc...

## Troubleshooting

Making email work can be a beast.  If you're having trouble with the
bundled postfix server, your best bet is to look in the postfix logs.
This will most likely point you in the right direction.

```sh
./logs.sh -s postfix
```

## Amazon EC2

The bundled postfix service has problems sending email on EC2 instances.
The problem we've seen is that trying to send email to gmail addresses
gets rejected because EC2 IP addresses have terrible reputation.  We
assume this will be a problem as well with other high quality email
providers, so for EC2 we recommend NOT using the built in postfix
service.  There are several ways around this.  If you, the customer,
already have a working SMTP email solution in place (ie. Mailgun, your
own SMTP server, etc...), then you should use that.  If not, then we've
had success using Amazon's SES email service.  That's our recommended
solution when you don't have another one.

When configuring your installation (running configure.sh), be sure to
specify the `--smtp_host`, `--smtp_user`, and `--smtp_password`
options. This will setup your on-premise Rollbar instance to use your
external SMTP provider.

## Amazon SES

If you decide to use SES, then you'll need to go through a few steps to
get it all working right.  I recommend reading the SES documentation to
understand what all is going on there.

http://docs.aws.amazon.com/ses/latest/DeveloperGuide/Welcome.html

If you're in a hurry, though, this seems to be the bare minimum required
to setup the service.

1. enable SES on your account and go to the SES control panel
2. validate your domain using the TXT record method via the "Domains"
   tab
3. validate the individual email addresses you will be sending to via
   the "Email Addresses" tab
4. generate SMTP user credentials
5. plug in the SMTP credentials when running configure.sh
