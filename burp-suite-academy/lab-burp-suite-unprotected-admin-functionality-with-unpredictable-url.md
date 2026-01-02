---
description: >-
  https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality-with-unpredictable-url
---

# Lab: Burp Suite - Unprotected admin functionality with unpredictable URL

1. Review the lab home page's source using Burp Suite or your web browser's developer tools.
2. Observe that it contains some JavaScript that discloses the URL of the admin panel.



<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

Admin panel URL: /admin-46g525

3. Load the admin panel and delete `carlos`.



[https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality](https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality)

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
