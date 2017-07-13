Chain INPUT (policy ACCEPT)
target     prot opt source               destination
DROP       all  --  51.255.65.0/24       anywhere
DROP       all  --  31.179.146.0/24      anywhere
DROP       all  --  46.161.9.0/24        anywhere
DROP       all  --  5.143.231.0/24       anywhere
DROP       all  --  216.244.66.0/24      anywhere

Add new things to this list, e.g.,:

$ sudo iptables -A INPUT -s 216.244.66.0/24 -j DROP

Find out which IPs might be candidates to drop:

cd to DSpace logs dir, e.g., /dspace-ext/logs/

$ cat localhost_access_log.2017-07-13.txt |cut -d ' ' -f1 |sort -nr|uniq -c|sort -nr|head
