# DeterministicNotes
Different ways to hash a phrase, so I can remember


### Bash

Plain:
<pre><code>echo -n "user:phrase:0:example-site" | openssl dgst -sha256 -binary | openssl base64 | sed -e 's/[^0-9A-Za-z]//g' | egrep -o '.{3}' | head -5 | paste -sd'-' -</code></pre>

With prompt:
```
read -s PHRASE && echo -n "user:$PHRASE:0:example-site" | openssl dgst -sha256 -binary | openssl base64 | sed -e 's/[^0-9A-Za-z]//g' | egrep -o '.{3}' | head -5 | paste -sd'-' -
```

Disable history
```
set +o history
set -o history
```


### Python

<pre><code>import base64, hashlib, re
h = hashlib.sha256(); h.update(b'user:phrase:0:example-site');  '-'.join([re.sub(r'[^0-9A-Za-z]', '', base64.b64encode(h.digest()) .decode())[i:i+4] for i in range(0, 12, 3)])</code></pre>

### My rules
user includes @whatever.com
site does not include .com
