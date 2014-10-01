publicdns2cname
===============

#### What is this?

Automatically add EC2 Public DNS as a CNAME on Route53 when the instance starts.  
Your hostname will be persistent, like an Elastic IP!

#### Example?

Let's say you put "web1" to "sub-domain" tag on your instance, and you choose base domain as "ec2.example.com". Then you can access to the instance with "web1.ec2.example.com" forever, no matter how many times the global IP changes. If you make it as a hostname (by editing /etc/sysconfig/network), internal connection between EC2 instances will be local IP, while external connection will stay global IP.

#### Requiremnents

Runs only on Amazon Linux. Use Route53. [awscli must be configured](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html) with route53 and ec2 privileges. Your EC2 instance need to have "sub-domain" tag.

#### Install

```bash
cd /etc/init.d/
curl -kOL https://raw.githubusercontent.com/lowply/publicdns2cname/master/publicdns2cname
vim publicdns2cname
# Modify HOSTED_ZONE_ID and DOMAIN_NAME
chown root:root publicdns2cname
chmod 755 publicdns2cname
chkconfig publicdns2cname on
```

This is bash + awscli re-implementation of [hostname_to_route53.rb](http://lab.tricorn.co.jp/y-kimura/4634), thank you for inspiration.
