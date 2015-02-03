```
ssh -o 'ProxyCommand ncat --proxy 10.1.1.5:20002 %h %p' root@10.1.1.6
```