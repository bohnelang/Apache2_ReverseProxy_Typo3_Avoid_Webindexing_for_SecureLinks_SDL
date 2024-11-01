# Avoid indexing of SDL files on Typo3 by crawler

## Introduction

On Typo3 you have files that are only temporarely available by this URL. Normally web crawler do index this content and URL. Unfortunately the URL is onley valid for short time 
and thus web crawler should not index this content. Otherwise you will notice in log fles a lot of 404 requests.

## Solution
In http header you could place infoation for web crawler:

```
# Robots should not index URLs that a not capable of deeplink
# https://httpd.apache.org/docs/2.4/expr.html
# https://httpd.apache.org/docs/2.4/mod/mod_headers.html
# "noindex, noarchive, nosnippet" a2enmod headers
#
Header set X-Robots-Tag "noindex, noarchive, nosnippet, nofollow" "expr=%{QUERY_STRING} =~ m#^(.*)tx_nawsecuredl(.*)$#"
Header set X-Robots-Tag "noindex, noarchive, nosnippet, nofollow" "expr=%{Request_URI} =~ m#^/securedl/sdl-(.*)$#"
```

## Result
After enableing this rules the numbers of errors in log reduces nearly up to zero :-)

