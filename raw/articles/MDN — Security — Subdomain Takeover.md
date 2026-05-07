# Subdomain Takeover

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/Subdomain_takeover

A subdomain takeover occurs when an attacker gains control over a subdomain of a target domain. Typically, this happens when the subdomain has a canonical name (CNAME) in the DNS, but no host is providing content for it. This can happen because either a virtual host hasn't been published yet or a virtual host has been removed. An attacker can take over that subdomain by providing their own virtual host and then hosting their own content for it.

If an attacker can do this, they can potentially read cookies set from the main domain, perform cross-site scripting, or circumvent content security policies.

## How do they happen?

### During provisioning

An attacker sets up a virtual host for a subdomain name before you get to do it.

Suppose you control the domain example.com. You want to add a blog at blog.example.com, and you decide to use a hosting provider who maintains a blogging platform. The process you go through might look like this:

1. You register the name "blog.example.com" with a domain registrar.
2. You set up DNS records to direct browsers to the virtual host.
3. You create a virtual host at the hosting provider.

Unless the hosting provider verifies that the entity who sets up the virtual host actually is the owner of the subdomain name, an attacker who is quicker than you could create a virtual host with the same hosting provider, using your subdomain name.

### During deprovisioning

You take down your virtual host, but an attacker sets up a new virtual host using the same name and hosting provider.

You decide that you no longer want to maintain a blog, so you remove the virtual host from the hosting provider. However, if you don't remove the DNS entry that points to the hosting provider, an attacker can now create their own virtual host with that provider, claim your subdomain, and host their own content under that subdomain.

## Defenses against Subdomain Takeover

- **Define standard processes for provisioning and deprovisioning hosts.**
  - Start provisioning by claiming the virtual host; create DNS records _last_.
  - Start deprovisioning by removing DNS records _first_.

- **Create an inventory of all of your organization's domains and their hosting providers,** and update it as things change, to ensure that nothing is left dangling.

- **Put pressure on hosting vendors to close gaps;** ask how they verify that someone claiming a virtual host actually has a legitimate claim to the domain name.
