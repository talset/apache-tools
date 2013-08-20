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

Fix if necessary :
```bash
#vhostname
headers = {"Host": '127.0.0.1' }
#ip to reach apache
url="http://127.0.0.1/balancer-manager"
```


##Dependency
```bash
   apt-get install python-argparse
```

##Example of use:

```bash
  ./balancer-manager.py -l
  ./balancer-manager.py -w ajp://10.152.45.1:8001 -a enable
```
