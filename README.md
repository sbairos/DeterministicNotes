# DeterministicNotes
Different ways to hash a phrase, so I can remember


Bash

<pre><code>set +o history</code></pre>
<pre><code>echo -n 'user:phrase:0:example-site' | openssl dgst -sha256 -binary | openssl base64 | sed -e 's/[^0-9A-Za-z]//g' | egrep -o '.{3}' | head -5 | paste -sd'-' -</code></pre>
<pre><code>set -o history</code></pre>


Python

<pre><code>import base64, hashlib, re
h = hashlib.sha256(); h.update(b'user:phrase:0:example-site');  '-'.join([re.sub(r'[^0-9A-Za-z]', '', base64.b64encode(h.digest()) .decode())[i:i+4] for i in range(0, 12, 3)])</code></pre>

My rules
user includes @whatever.com
site does not include .com
