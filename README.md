publicdns2cname
===============

#### What is this?

Automatically add EC2 Public DNS as a CNAME of any domain on Route53 when the instance starts.  
Your hostname will be persistent, like an Elastic IP!

#### Why?

When an EC2 instance starts from stop state (= not reboot), global IP address and public DNS will be randomly changed unless you enabled Elastic IP on that instance.

But normally EIP is allowed to have 5 per account, so assigning them to each instance is not a best practice. This script make it easy to access specific instance with any hostname you choose, using EC2 instance tags.

#### Example?

Let's say you put "web1" to "sub-domain" tag on your instance, and you choose base domain as "ec2.example.com". With this script, you can access to the instance by "web1.ec2.example.com" all the time. No matter how many times the instance does stop/start.

I suggest having it as a hostname. Like EC2 public DNS, internal name resolving inside VPC will be local IP, while external name resolving will stay global IP.

#### Requiremnents

- Runs only on Amazon Linux (I guess it works on CentOS with awscli installed).
- Use of AWS Route53
- [awscli must be configured](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html) with route53 and ec2 privileges.
- Your EC2 instance should have "sub-domain" tag.

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

#### Credit

This is bash script + awscli re-implementation of [hostname_to_route53.rb](http://lab.tricorn.co.jp/y-kimura/4634), thank you for inspiration.
