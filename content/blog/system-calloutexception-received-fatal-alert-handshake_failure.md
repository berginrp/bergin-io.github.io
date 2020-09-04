+++
title = "System.CalloutException: Received fatal alert: handshake_failure"
date = "2018-08-16T22:07:53-04:00"
author = "Bergin Panimayam"
type = "post"
permalink = "/2020/08/16/26-revision-v1/"
categories = ["API"]
tags = ["calloutexception", "failure", "handshake", "mutual tls", "two-way ssl"]
+++
At times, a simple configuration can end up showing scary messages like these.

```
System.CalloutException: Received fatal alert: handshake_failure
```

This turns out to be a mutual TLS issue that you may want to look at these configurations first before digging more. For me it also said, contact support with the error ID: xxxxxxxx-xxxxx.

Check your certificate if it’s properly signed, not expired and active.
Check the named credentials to make sure it has the right certificate associated.
if both these are good, then check the target server, if it’s accepting your cert.
A quick check on these things could get things cleared.

Happy coding! 😀