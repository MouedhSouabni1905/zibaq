**Tags:** [[Cybersecurity]] [[Networking]]

**IP Filtering Bypass:** to access a network that filters out traffic based on IP address, we can use proxy servers that forward our request through their own IP address which the network recognizes and accepts. The most common private network ranges are 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16, so you usually try to forward the request to one of them, either using `curl -H "X-Forwarded-For: 192.168.0.1" [host]`, or BurpSuite, or using this python script (replacing the ip adresses accordingly):
```
import requests

HEADERS = {
    'Accept-language': 'en-US,en;q=0.9,vi;q=0.8',
    'User-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:92.0)'
                  'Gecko/20100101'
                  'Firefox/92.0',

    'X-Forwarded-For': '192.168.0.1'
}

URL = "[host]"

# send the request
resp = requests.request("GET", URL, headers=HEADERS)

# server response
print(resp.text)
```

**Path traversal:** Use `--path-as-is` to avoid curl's shenanigans of transforming the url. Can also use a custom written web client that sends a request. If the path is stripped, remember that you can start from another folder that the server provides (containing different files for example) and backtrack from there.

**Reflected XSS:** When the input is filtered, or more precisely *sanitized*, there are still way to inject javascript code on a vulnerable website, which include:
- `<body-onload=[JS-INJECTED-SCRIPT]></body>`
- `<img src=[INVALID IMAGE SOURCE] onError=[MALICIOUS SCRIPT]>`

**Stored XSS:** Is injected directly into the website's database (for example, from a submittable form input area). Which means it is *stored* and will run everytime.

**DOM based XSS:** The vulberability exists onn the client side not on the server side (meaning the script should get executed on the user's browser regardless of the server's restrictions). For example, using a hash before the script (in the browser url for example) would make the server ignore the vulnerability but the browser would still execute the code.

**File upload:** Uploading a script or program in an area for file upload instead instead of the specified file format. Sometimes it works by changing the extension or the http header to specify the asked for format.

**XSS Filtering bypass:** https://cheatsheetseries.owasp.org/cheatsheets/XSS_Filter_Evasion_Cheat_Sheet.html

**Remark about sqli:** In oracle database, we do this *'||(QUERY HERE)||'* to inject a query