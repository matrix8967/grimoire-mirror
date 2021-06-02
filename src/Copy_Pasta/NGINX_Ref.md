```sh
#!/usr/bin/env bash
set -eE

RED='\033[0;31m'
GREEN='\033[0;32m'
NC='\033[0m' # No Color

# Def needs a lot of adjustments -- pretty trashy and nowhere near universal.
# Requires non-default package `ccze` for log readability.

#Variable for Current Date.
c_date=$(date -u +"%d/%b/%Y")

# Number of 444 Disconnects:

echo -e "-----"
echo -e "Number of 444 Disconnects:"
grep "$c_date" /var/log/nginx/goaccess.log |grep "\" 444 " |wc -l

# Number of 404s:
echo -e "-----"
echo -e "404's today:"
grep "\" 404 " /var/log/nginx/access.log |grep $c_date |wc -l

# Request returning 404s:
echo -e "-----"
echo -e "Request returning 404s"
grep "\" 404 " /var/log/nginx/access.log |grep "$c_date" |cut -d \" -f 2 |sort |uniq -c |sort -rh |ccze -A

# Total # of http requests
echo -e "-----"
echo -e "Total http reqs:"
grep "$c_date" /var/log/nginx/access.log |wc -l

# Total # of http requests that generated a 200 response code:
echo -e "-----"
echo -e "Total http 200 return code:"
grep "$c_date" /var/log/nginx/access.log |grep "\" 200 " |wc -l

# Total # of unique IPs:
echo -e "-----"
echo -e "Total # of Unique IPs:"
grep "$c_date" /var/log/nginx/access.log |awk '{print $1}' |sort -u |wc -l

# Unique IPs today sorted by # of requests
echo -e "-----"
echo -e "Unique IPs sorted by # of requests:"
grep "$c_date" /var/log/nginx/access.log |awk '{print $1}' |sort |uniq -c |sort -rh

# Top 20 referrer urls for today:
echo -e "-----"
echo -e "Top 20 referrer URLs:"
grep $c_date /var/log/nginx/access.log |cut -d \" -f 4 |sort |uniq -c |sort -rh |head -20

# Top 20 webserver requests for today:
echo -e "-----"
echo -e "Top 20 webserver requests today:"
grep "$c_date" /var/log/nginx/access.log |cut -d \" -f 2 |sort |uniq -c |sort -rh |head -20
```
