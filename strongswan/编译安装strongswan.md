```
./configure --sysconfdir=/etc  --enable-openssl --enable-nat-transport --disable-mysql --disable-ldap  \
--enable-static --enable-md4 --enable-eap-mschapv2 --enable-eap-aka --enable-eap-aka-3gpp2  \
--enable-eap-gtc --enable-eap-identity --enable-eap-md5 --enable-eap-peap --enable-eap-radius --enable-eap-sim \
--enable-eap-sim-file --enable-eap-simaka-pseudonym --enable-eap-simaka-reauth --enable-eap-simaka-sql \
--enable-eap-tls --enable-eap-tnc --enable-eap-ttls --enable-vici --enable-swanctl --enable-eap-radius --enable-pki
make install
```

从git版本开始编译
```
sudo apt-get install automake autoconf libtool pkg-config gettext perl python flex bison gperf
```
