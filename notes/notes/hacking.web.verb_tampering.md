---
id: 71u25fapz36zbeg3pk2kfkh
title: Verb Tampering
desc: ""
updated: 1678040981029
created: 1678037729930
---

# HTTP Verb Tampering

The Http methods are :

**POST**: use to post data to the server in the body

**GET**: used to send or retrieve data, the parameters are sent via the URL

**HEAD**: same as get but it returns only the headers

**OPTIONS**: To list out the methods available for a URL

**TRACE** echos back the client request

**PUT**: used to send a full payload update to the server

**PATCH**: used to send a partial payload update to the server

**DELETE**: used to delete a resource.

### Detecting Available methods in a URL

There are multiple ways to know which methods are available in a given URL

1. Using _curl_: we can use curl with the combination of the option method to get the methods available in the URL , that is of course if the OPTIONS method it self is allowed we will get results otherwise we will get a _Method not allowed_ result

```bash
curl -X OPTIONS http://target -v
```

we have to use the -v flag to show the results otherwise options will returns nothing. This is because the options method does not return neither the headers nor the body of the response.

2. **Using NMAP**:
   we can use the _http-methods_ script in NMAP to do the same test however we need to specify the IP without the http or https prefix

   ```bash
   nmap --script http-methods 192.165.22.14
   ```

   To specify other URL path we can use the **http-methods.url-path** option like so

   ```bash
    nmap --script http-methods --script-args http-methods.url-path='/website' 192.168.22.14
   ```

3. **Metasploit**:
   we can use the _auxiliary/scanner/http/options_ module to achieve the same result.
