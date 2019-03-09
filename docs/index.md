## **Openemail: It is Free, Open Source, and Dockerized Mail Server**

At [Cybergate](https://cybergate.lk) our effort is to consolidate the best available open source email, collaboration, and email security solutions to provide you highly agile, secure, and enterprise ready world class, Open Source email and collaboration platform that can easily replace any other equivalent commercial alternative.

Our administration **Web UI** is a fork of [Mailcow](https://mailcow.email/) project. We are deeply indebted to their excellent effort in making such a good consolidation of all complex backend  email tools into a single pane of **Web UI** by making it very easy for administrators to manage the system without using complex command line tools and configuration file editing.

Inspired by the concept of [Mailcow](https://mailcow.email/) **all the backend applications of Openemail are running in Docker Containers** by making Openemail a software that is ready to deploy in your private or public cloud infrastructure and utilize the benefit of agility and elasticity of modern day cloud computing.

**Openemail** has been designed to work as a highly scalable and agile software which you can use it to host from few mailboxes to millions of mailboxes which are required by services providers.  

As like any other  open source software  you are  free to use Openemail at your own risk while you can obtained it as a supported and enterprise ready solution which is backed by [Cybergate](https://cybergate.lk) with its world class open source support team.

**Our enterprise support  subscriptions are supporting unlimited mail domains and accounts** while our subscription is an annual SLA which is confined to several levels of support channels and types together with the hardware virtual of physical server profile of the system that you will be using to deploy Openemail. You can have both on premise and hosted solution under these subscription contracts. But all these optional and not required as Openemail is 100% free.


## **Openemail Demo**

You can find a demo at [hasuna.openemail.io](https://hasuna.openemail.io), use the following credentials to login:

- **Administrator**: admin / openemail
- **Domain administrator**: domainadm / openemail
- **Mailbox**: demo@openemaill.io / openemail

## **Get Support**

If you think that you need our support then we are ready to help you. We have several ways of giving you support.

### **Commercial Support**

For commercial support contact [sales@cybergate.lk](mailto:sales@cybergate.lk) or get a support subscription at [Cybergate](https://www.cybergate.lk/solutions).

### **Community Support**

- IRC @ [Freenode, #openemail](irc://irc.freenode.org:6667/openemail)
- GitHub @ [openemail](https://github.com/openemail/openemail)

### **Hosted Openemail**

A fully featured managed **openemaill** is also available. Please contact [Amila](https://www.linkedin.com/in/amila-m-kothalawala-87357152/) on +(94)77 316 545 for more details

### **Service Level Agreement**

You can download our **[Support Level Agreement Here]sla/cybergate-openemail-sla-v1.pdf)** and review it before contacting our sales hot-line **+(94) 766 783 783** for further details

## **Migrate to Openemail at No Cost**

We are happy to announce you that you can easily migrate from Zimbra, Microsoft Exchange  or Office 365 hosted email or any other email service without compromising any of those major email and collaboration features like Addressbook, Calendar, Task and Contact sharing, public folders, resource sharing, Microsoft Outlook and Mobile Sync with native ActiveSync protocol.

## **Openemail is Absolutely Free**

You are well aware that email is by far the most widely used business application of the Internet. From a single owner business to a large enterprise primarily rely on email as their first line of business communication. The intention of this comprehensive free guide is to help you getting **Openemail deployed free** if you have in house systems engineering skills. Openemail is 100% free in terms of software licensing that blocks you from scaling your business.

## **Security is Our Priority**

Openemail thinks that security is a priority. Currently Openemail supports almost all DNS based email security features like SPF,DKIM, DMARC etc,

It is backed by [Rspamd](https://rspamd.com/), a fast, free and open-source spam filtering system where you do not need to make any other investment on spam filtering.

Integrated [Sanesecurity ClamAV signatures](https://sanesecurity.com/improve-the-detection-rate-up-to-90-of-clamav-antivirus-by-adding-sanesecurity-clamav-signatures/) will improve ClamAV detection rate on Macro malware, Javascript malware, Phishing, Spam and other emailed Ransomware upto 90%. This makes your emails free from viruses and malware without an additional financial investment.

**Openemail supports two-factor authentication** for Web UI making it more secure when using web based administration

## **Per User Spam Filtering**

You can fine grain Openemail's spam filtering backend per email box basis by making it is the most flexible in spam managing.

## **Backup and Restore**

Openemail has provided you  all required tools for backing up and restoring by helping administrators to  have goodnight sleep and enjoy their holidays. You can sync your backup to your own FTP server or any other public cloud storage like Amazon S3, Google Bucket or any other.

## **Domain Based Administration with Two-Factor Authentication**

Openemail supports multiple domains in a single installation with domain based administration making the delegation of administration is breezy, easy, and secure.

## **Web UI Feature Overview**

The integrated **openemail UI** allows administrative work on your mail server instance as well as separated domain administrator and mailbox user access:

- DKIM and ARC support
- Black- and whitelists per domain and per user
- Spam score management per-user (reject spam, mark spam, greylist)
- Allow mailbox users to create temporary spam aliases
- Prepend mail tags to subject or move mail to sub folder (per-user)
- Allow mailbox users to toggle incoming and outgoing TLS enforcement
- Allow users to reset SOGo ActiveSync device caches
- imapsync to migrate or pull remote mailboxes regularly
- TFA: Yubi OTP and U2F USB (Google Chrome and derivatives only), TOTP
- Add domains, mailboxes, aliases, domain aliases and SOGo resources
- Add whitelisted hosts to forward mail to mailcow
- Fail2ban-like integration
- Quarantine system
- A lot more...

## **Openemail Containers**

openemail comes with multiple containers linked in one bridged network. Each container represents a single application.

- Dovecot
- ClamAV (optional)
- Solr (optional)
- Memcached
- Redis
- MySQL
- Unbound
- PHP-FPM
- Postfix
- ACME-Client
- Nginx
- Rspamd
- SOGo
- Netfilter
- Watchdog
- Portainer

## **Docker Data Volumes**

The following **Docker volumes** are used to keep dynamic data - take care of them!

- vmail-vol-1
- solr-vol-1
- redis-vol-1
- mysql-vol-1
- rspamd-vol-1
- postfix-vol-1
- crypt-vol-1
