apache-tools
===========

Scripts Apache

#balancer-manager.py

 Allow you to manage Worker/BalancerMember defined in your apache2 mod_proxy conf : 

```bash
    <Proxy balancer://tomcatservers>
        BalancerMember ajp://10.152.45.1:8001 route=web1 retry=60
        BalancerMember ajp://10.152.45.2:8001 route=web2 retry=60
    </Proxy>
```

You have to allow /balancer-manager
Like :
```bash
 #RewriteCond %{REQUEST_URI} !=/balancer-manager
 ProxyPass /balancer-manager !
 <Location /balancer-manager>
   SetHandler balancer-manager
   Order Deny,Allow
   Deny from all
   Allow from 127.0.0.1
 </Location>
```

If necessary, fix in the script :
```bash
#host header
headers = {"Host": '127.0.0.1' }
#ip to reach apache
url="http://127.0.0.1/balancer-manager"
```


##Dependency
```bash
   apt-get install python-argparse
```

##Usages

Help :
```bash
balancer-manage.py 
usage: balancer-manage.py [-h] [-l] [-a ACTION] [-w WORKER]

optional arguments:
  -h, --help            show this help message and exit
  -l, --list            List Worker member and status
  -a ACTION, --action ACTION
                        "enable" or "disable" the specified Worker
  -w WORKER, --worker WORKER
                        Worker name : example ajp://127.0.0.1:8001
```

Exemple :
```bash
  ./balancer-manager.py -l
  ./balancer-manager.py -w ajp://10.152.45.1:8001 -a enable
```
