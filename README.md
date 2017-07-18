**Note**: this repo includes lua script for letsencrypt auto-renewal (cf. adhoc repo)


## create aws ec2 instance for load balancer and set routing tables accordingly

> http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_NAT_Instance.html#EIP_Disable_SrcDestCheck

## configure load balancers on aws ec2 instance

> see http://blog.manton.im/2016/07/setting-up-ha-with-haproxy-and.html

## install haproxy

```sh
sudo add-apt-repository ppa:vbernat/haproxy-1.6
sudo apt-get update
sudo apt-get install haproxy
```

## enable auto-start

Edit /etc/default/haproxy to make sure the following line is set as follows:

```sh
# Set ENABLED to 1 if you want the init script to start haproxy.
ENABLED=1
```

## copy config files in /etc/haproxy

(files in this git repo)  
Adapt and rename haproxy.lb01.cfg or haproxy.lb02.cfg to haproxy.cfg according to your set-up and configuration

## automatic sync of certificates across other servers
    
Add the ssh key of a read-only gitlab user authorized on ssl-certificates repo 
    
Copy `sync-ssl-certs.sh` script to `/usr/local/bin`

Use it in a cron job like this for daily runs:

```sh
$ sudo crontab -e
0 4 * * * PATH=$PATH:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin /usr/local/bin/cert-renewal-haproxy.sh
```
