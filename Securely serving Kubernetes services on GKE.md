---
created: 2020-04-15T00:56:55-04:00
modified: 2020-04-15T01:10:03-04:00
title: Securely serving Kubernetes services on GKE
---

Deploying software services with Kubernetes on Google Kubernetes Platform is a very straightforward experience. The challenge becomes how to serve public internet requests in a secure manner. This post will describe a method for exposing Kubernetes Https services to public requests that will use Google managed certificates.

# Reserve an address

While a static address is not required, it will simply future changes. When an Ingress object is deleted, so is the public ip address lease. If you do not reserve an address for the Ingress, a new one will be issued if the object is deleted. Which is fine if you are managing DNS updates along with Ingress changes. I'm not, so let's reserve one.

```
gcloud compute address reservation --global
```

Now get the address