## Find out what filters are in place

`$ sudo iptables -L`

    Chain INPUT (policy ACCEPT)
    target     prot opt source               destination
    DROP       all  --  51.255.65.0/24       anywhere
    DROP       all  --  31.179.146.0/24      anywhere
    DROP       all  --  46.161.9.0/24        anywhere
    DROP       all  --  5.143.231.0/24       anywhere
    DROP       all  --  216.244.66.0/24      anywhere

## Add new things to this list
e.g.:

`$ sudo iptables -A INPUT -s 216.244.66.0/24 -j DROP`

## Find out which IPs might be candidates to drop

cd to DSpace logs dir, e.g., /dspace-ext/logs/

`$ cat localhost_access_log.2017-07-13.txt |cut -d ' ' -f1 |sort -nr|uniq -c|sort -nr|head`

    468084 127.0.0.1
      4523 66.249.66.64
      3382 5.143.231.44
      3239 216.244.66.242
      2896 157.55.39.216
      1926 40.77.167.121
      1924 68.180.231.57
      1796 216.244.66.250
      1631 40.77.167.36
      1302 66.249.66.66

Ignore 127.0.0.1, since that's all coming from the local server. The others you can run through IP Lookup tools to locate the owner. If it's a cloud computing company, drop it per the above command.
