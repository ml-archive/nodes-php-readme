# Setting up a PHP project

We have 4 generations of PHP applications in Nodes

1) PHP 5.5 CakePHP 2x (Lokalbolig, Ironman)
2) PHP 5.5 Laravel 4.2 (Covington, 2BeFound)
3) PHP 5.5 Laravel 5.0 -> 5.1 packages from private github (Issl5, most others have been updated)
4) PHP 7.0 Laravel 5.1 -> 5.4 public packages

### Projects in generation 1-3 needs to run on 
https://github.com/nodes-projects/ndev-php55-vagrant

git clone the project 
use the nodes command to "fix project" which sets up apache config and database

### Projects in generation 4 can run on 
https://laravel.com/docs/5.4/homestead

Follow the guide to homestead

Notes:

VirtualBox 5.1 is preffered

Ex of Homestead.yaml
```
---
ip: "192.168.10.10"
memory: 4096
cpus: 2
provider: virtualbox

authorize: ~/.ssh/id_rsa.pub

keys:
    - ~/.ssh/id_rsa

folders:
    - map: ~/nodes-projects
      to: /var/www

sites:
    - map: pma.local-like.st
      to: /var/www/phpmyadmin

    - map: riide.local-like.st
      to: /var/www/riide/htdocs/public
      php: "7.0"

databases:
    - homestead
```

password for the mysql on homestead is
u: homestead
p: secret

[Link to .env](https://github.com/nodes-projects/readme/blob/master/laravel/homestead-env.md)

Ex of .hosts file
```
192.168.10.10 riide.local-like.st
192.168.10.10 pma.local-like.st
```

Install PMA
```
PMA_VERSION=4.6.6 && cd /var/www && wget https://files.phpmyadmin.net/phpMyAdmin/$PMA_VERSION/phpMyAdmin-$PMA_VERSION-all-languages.zip && unzip phpMyAdmin-*-all-languages.zip && mv phpMyAdmin-*-all-languages phpmyadmin && rm ./phpMyAdmin-*-all-languages.zip
```

Install tig
```
sudo apt-get install tig
```

Install gitflow
```
sudo apt-get install git-flow
```

Install missing php extensions for all versions available

_update apt-get_
```
sudo apt-get update
```

_php5_
```
sudo apt-get install php5.6-mcrypt php5.6-mbstring php5.6-json php5.6-mysql php5.6-opcache php5.6-common php5.6-readline php5.6-curl php5.6-dev php5.6-zip php5.6-soap php5.6-redis -y
```

_php7_
```
sudo apt-get install php7.0 php7.0-mcrypt php7.0-mbstring php7.0-json php7.0-mysql php7.0-opcache php7.0-common php7.0-readline php7.0-curl php7.0-dev php7.0-zip php7.0-soap php7.0-xml -y
```

_php7.1_
```
sudo apt-get install php7.1 php7.1-mcrypt php7.1-mbstring php7.1-json php7.1-mysql php7.1-opcache php7.1-common php7.1-readline php7.1-curl php7.1-dev php7.1-zip php7.1-soap php7.1-xml -y
```

### Setup SSL certificate

 - Create a directory to store certificates in

 `sudo mkdir -p /etc/nodes/ssl/local-like.st`

 - Create file `sudo vim /etc/nodes/ssl/local-like.st/star.local-like.st.pem`

 ```
-----BEGIN CERTIFICATE----- 
MIIFVTCCBD2gAwIBAgIQMQ4pvcJglvoWXOjGWu3V/jANBgkqhkiG9w0BAQsFADCB 
kDELMAkGA1UEBhMCR0IxGzAZBgNVBAgTEkdyZWF0ZXIgTWFuY2hlc3RlcjEQMA4G 
A1UEBxMHU2FsZm9yZDEaMBgGA1UEChMRQ09NT0RPIENBIExpbWl0ZWQxNjA0BgNV 
BAMTLUNPTU9ETyBSU0EgRG9tYWluIFZhbGlkYXRpb24gU2VjdXJlIFNlcnZlciBD 
QTAeFw0xNjEyMDYwMDAwMDBaFw0xNzEyMDYyMzU5NTlaMF0xITAfBgNVBAsTGERv 
bWFpbiBDb250cm9sIFZhbGlkYXRlZDEeMBwGA1UECxMVRXNzZW50aWFsU1NMIFdp 
bGRjYXJkMRgwFgYDVQQDDA8qLmxvY2FsLWxpa2Uuc3QwggEiMA0GCSqGSIb3DQEB 
AQUAA4IBDwAwggEKAoIBAQDcvWj7F2pSwHpJsNz9HCWZF2/HR50J4Zht2b26oD2h 
dyYn1mXbPNhUveIQrE71ymR8FqEBZDjXu7v+ekE8PjsyK/rfZ4zwRHXHJtTJQneb 
QnzsjyNH9x6vNjBQP418mXX2uSmzhfUH7+0MuIgV/dMWKV8avozhs5tsO/bQebyv 
c+PGsDOTgnXAskWwT2kUuboS4e0P70FMgjWG+wNflji5Ig1l9kxMez4iLwHDZBke 
X7UjCyJ4FLzGxkrIfcWmQ1aNwYB8vkcjnDOo6NKs2uncQsSxezWuWlLe7TSy2cff 
fVnP7f7ADaorLzCyRWa/3iRjNCiUWw86Zy4soyAzOfDFAgMBAAGjggHbMIIB1zAf 
BgNVHSMEGDAWgBSQr2o6lFoL2JDqElZz30O0Oija5zAdBgNVHQ4EFgQUx9DRMwTl 
jrj2FT6DrRYEYFaABnQwDgYDVR0PAQH/BAQDAgWgMAwGA1UdEwEB/wQCMAAwHQYD 
VR0lBBYwFAYIKwYBBQUHAwEGCCsGAQUFBwMCME8GA1UdIARIMEYwOgYLKwYBBAGy 
MQECAgcwKzApBggrBgEFBQcCARYdaHR0cHM6Ly9zZWN1cmUuY29tb2RvLmNvbS9D 
UFMwCAYGZ4EMAQIBMFQGA1UdHwRNMEswSaBHoEWGQ2h0dHA6Ly9jcmwuY29tb2Rv 
Y2EuY29tL0NPTU9ET1JTQURvbWFpblZhbGlkYXRpb25TZWN1cmVTZXJ2ZXJDQS5j 
cmwwgYUGCCsGAQUFBwEBBHkwdzBPBggrBgEFBQcwAoZDaHR0cDovL2NydC5jb21v 
ZG9jYS5jb20vQ09NT0RPUlNBRG9tYWluVmFsaWRhdGlvblNlY3VyZVNlcnZlckNB 
LmNydDAkBggrBgEFBQcwAYYYaHR0cDovL29jc3AuY29tb2RvY2EuY29tMCkGA1Ud 
EQQiMCCCDyoubG9jYWwtbGlrZS5zdIINbG9jYWwtbGlrZS5zdDANBgkqhkiG9w0B 
AQsFAAOCAQEAQgY80HDEjTyazR9AyBe770tDcTrgKtVkdXDIpe05oMQEenbV4HWU 
V8QN5SbfJpcXucFmjVvOP/+GXRSLwGr37k4xqn14lfHpVSWUFRqoYsZfNNUuZg37 
kLY9eGcgTwFAnscsHm6vFRDcgbY5a4Ij0k4L+Hh0hjhrAaYb6DVU6tv4LCk2ZC+X 
uagFxW+gixBBEZ+In4S01SaWkjtDpUplaluvxqwMcYBoDb9OTxTrW0gHQaCxBGRH 
Dgw8UGUKCi3LjajlY5zErMMytFlA0RSUPieMn9d1rR9JfmsuzzTz4K9ZLXXhKRyn 
Uf8VxJ5/NOShMdnNs9mTcz/bfI9gM8gt2g== 
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
MIIGCDCCA/CgAwIBAgIQKy5u6tl1NmwUim7bo3yMBzANBgkqhkiG9w0BAQwFADCB
hTELMAkGA1UEBhMCR0IxGzAZBgNVBAgTEkdyZWF0ZXIgTWFuY2hlc3RlcjEQMA4G
A1UEBxMHU2FsZm9yZDEaMBgGA1UEChMRQ09NT0RPIENBIExpbWl0ZWQxKzApBgNV
BAMTIkNPTU9ETyBSU0EgQ2VydGlmaWNhdGlvbiBBdXRob3JpdHkwHhcNMTQwMjEy
MDAwMDAwWhcNMjkwMjExMjM1OTU5WjCBkDELMAkGA1UEBhMCR0IxGzAZBgNVBAgT
EkdyZWF0ZXIgTWFuY2hlc3RlcjEQMA4GA1UEBxMHU2FsZm9yZDEaMBgGA1UEChMR
Q09NT0RPIENBIExpbWl0ZWQxNjA0BgNVBAMTLUNPTU9ETyBSU0EgRG9tYWluIFZh
bGlkYXRpb24gU2VjdXJlIFNlcnZlciBDQTCCASIwDQYJKoZIhvcNAQEBBQADggEP
ADCCAQoCggEBAI7CAhnhoFmk6zg1jSz9AdDTScBkxwtiBUUWOqigwAwCfx3M28Sh
bXcDow+G+eMGnD4LgYqbSRutA776S9uMIO3Vzl5ljj4Nr0zCsLdFXlIvNN5IJGS0
Qa4Al/e+Z96e0HqnU4A7fK31llVvl0cKfIWLIpeNs4TgllfQcBhglo/uLQeTnaG6
ytHNe+nEKpooIZFNb5JPJaXyejXdJtxGpdCsWTWM/06RQ1A/WZMebFEh7lgUq/51
UHg+TLAchhP6a5i84DuUHoVS3AOTJBhuyydRReZw3iVDpA3hSqXttn7IzW3uLh0n
c13cRTCAquOyQQuvvUSH2rnlG51/ruWFgqUCAwEAAaOCAWUwggFhMB8GA1UdIwQY
MBaAFLuvfgI9+qbxPISOre44mOzZMjLUMB0GA1UdDgQWBBSQr2o6lFoL2JDqElZz
30O0Oija5zAOBgNVHQ8BAf8EBAMCAYYwEgYDVR0TAQH/BAgwBgEB/wIBADAdBgNV
HSUEFjAUBggrBgEFBQcDAQYIKwYBBQUHAwIwGwYDVR0gBBQwEjAGBgRVHSAAMAgG
BmeBDAECATBMBgNVHR8ERTBDMEGgP6A9hjtodHRwOi8vY3JsLmNvbW9kb2NhLmNv
bS9DT01PRE9SU0FDZXJ0aWZpY2F0aW9uQXV0aG9yaXR5LmNybDBxBggrBgEFBQcB
AQRlMGMwOwYIKwYBBQUHMAKGL2h0dHA6Ly9jcnQuY29tb2RvY2EuY29tL0NPTU9E
T1JTQUFkZFRydXN0Q0EuY3J0MCQGCCsGAQUFBzABhhhodHRwOi8vb2NzcC5jb21v
ZG9jYS5jb20wDQYJKoZIhvcNAQEMBQADggIBAE4rdk+SHGI2ibp3wScF9BzWRJ2p
mj6q1WZmAT7qSeaiNbz69t2Vjpk1mA42GHWx3d1Qcnyu3HeIzg/3kCDKo2cuH1Z/
e+FE6kKVxF0NAVBGFfKBiVlsit2M8RKhjTpCipj4SzR7JzsItG8kO3KdY3RYPBps
P0/HEZrIqPW1N+8QRcZs2eBelSaz662jue5/DJpmNXMyYE7l3YphLG5SEXdoltMY
dVEVABt0iN3hxzgEQyjpFv3ZBdRdRydg1vs4O2xyopT4Qhrf7W8GjEXCBgCq5Ojc
2bXhc3js9iPc0d1sjhqPpepUfJa3w/5Vjo1JXvxku88+vZbrac2/4EjxYoIQ5QxG
V/Iz2tDIY+3GH5QFlkoakdH368+PUq4NCNk+qKBR6cGHdNXJ93SrLlP7u3r7l+L4
HyaPs9Kg4DdbKDsx5Q5XLVq4rXmsXiBmGqW5prU5wfWYQ//u+aen/e7KJD2AFsQX
j4rBYKEMrltDR5FL1ZoXX/nUh8HCjLfn4g8wGTeGrODcQgPmlKidrv0PJFGUzpII
0fxQ8ANAe4hZ7Q7drNJ3gjTcBpUC2JD5Leo31Rpg0Gcg19hCC0Wvgmje3WYkN5Ap
lBlGGSW4gNfL1IYoakRwJiNiqZ+Gb7+6kHDSVneFeO/qJakXzlByjAA6quPbYzSf
+AZxAeKCINT+b72x
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
MIIFdDCCBFygAwIBAgIQJ2buVutJ846r13Ci/ITeIjANBgkqhkiG9w0BAQwFADBv
MQswCQYDVQQGEwJTRTEUMBIGA1UEChMLQWRkVHJ1c3QgQUIxJjAkBgNVBAsTHUFk
ZFRydXN0IEV4dGVybmFsIFRUUCBOZXR3b3JrMSIwIAYDVQQDExlBZGRUcnVzdCBF
eHRlcm5hbCBDQSBSb290MB4XDTAwMDUzMDEwNDgzOFoXDTIwMDUzMDEwNDgzOFow
gYUxCzAJBgNVBAYTAkdCMRswGQYDVQQIExJHcmVhdGVyIE1hbmNoZXN0ZXIxEDAO
BgNVBAcTB1NhbGZvcmQxGjAYBgNVBAoTEUNPTU9ETyBDQSBMaW1pdGVkMSswKQYD
VQQDEyJDT01PRE8gUlNBIENlcnRpZmljYXRpb24gQXV0aG9yaXR5MIICIjANBgkq
hkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAkehUktIKVrGsDSTdxc9EZ3SZKzejfSNw
AHG8U9/E+ioSj0t/EFa9n3Byt2F/yUsPF6c947AEYe7/EZfH9IY+Cvo+XPmT5jR6
2RRr55yzhaCCenavcZDX7P0N+pxs+t+wgvQUfvm+xKYvT3+Zf7X8Z0NyvQwA1onr
ayzT7Y+YHBSrfuXjbvzYqOSSJNpDa2K4Vf3qwbxstovzDo2a5JtsaZn4eEgwRdWt
4Q08RWD8MpZRJ7xnw8outmvqRsfHIKCxH2XeSAi6pE6p8oNGN4Tr6MyBSENnTnIq
m1y9TBsoilwie7SrmNnu4FGDwwlGTm0+mfqVF9p8M1dBPI1R7Qu2XK8sYxrfV8g/
vOldxJuvRZnio1oktLqpVj3Pb6r/SVi+8Kj/9Lit6Tf7urj0Czr56ENCHonYhMsT
8dm74YlguIwoVqwUHZwK53Hrzw7dPamWoUi9PPevtQ0iTMARgexWO/bTouJbt7IE
IlKVgJNp6I5MZfGRAy1wdALqi2cVKWlSArvX31BqVUa/oKMoYX9w0MOiqiwhqkfO
KJwGRXa/ghgntNWutMtQ5mv0TIZxMOmm3xaG4Nj/QN370EKIf6MzOi5cHkERgWPO
GHFrK+ymircxXDpqR+DDeVnWIBqv8mqYqnK8V0rSS527EPywTEHl7R09XiidnMy/
s1Hap0flhFMCAwEAAaOB9DCB8TAfBgNVHSMEGDAWgBStvZh6NLQm9/rEJlTvA73g
JMtUGjAdBgNVHQ4EFgQUu69+Aj36pvE8hI6t7jiY7NkyMtQwDgYDVR0PAQH/BAQD
AgGGMA8GA1UdEwEB/wQFMAMBAf8wEQYDVR0gBAowCDAGBgRVHSAAMEQGA1UdHwQ9
MDswOaA3oDWGM2h0dHA6Ly9jcmwudXNlcnRydXN0LmNvbS9BZGRUcnVzdEV4dGVy
bmFsQ0FSb290LmNybDA1BggrBgEFBQcBAQQpMCcwJQYIKwYBBQUHMAGGGWh0dHA6
Ly9vY3NwLnVzZXJ0cnVzdC5jb20wDQYJKoZIhvcNAQEMBQADggEBAGS/g/FfmoXQ
zbihKVcN6Fr30ek+8nYEbvFScLsePP9NDXRqzIGCJdPDoCpdTPW6i6FtxFQJdcfj
Jw5dhHk3QBN39bSsHNA7qxcS1u80GH4r6XnTq1dFDK8o+tDb5VCViLvfhVdpfZLY
Uspzgb8c8+a4bmYRBbMelC1/kZWSWfFMzqORcUx8Rww7Cxn2obFshj5cqsQugsv5
B5a6SE2Q8pTIqXOi6wZ7I53eovNNVZ96YUWYGGjHXkBrI/V5eu+MtWuLt29G9Hvx
PUsE2JOAWVrgQSQdso8VYFhH2+9uRv0V9dlfmrPb2LjkQLPNlzmuhbsdjrzch5vR
pu/xO28QOG8=
-----END CERTIFICATE-----
 ```

- Create file `sudo vim /etc/nodes/ssl/local-like.st/star.local-like.st.key`

```
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEA3L1o+xdqUsB6SbDc/RwlmRdvx0edCeGYbdm9uqA9oXcmJ9Zl
2zzYVL3iEKxO9cpkfBahAWQ417u7/npBPD47Miv632eM8ER1xybUyUJ3m0J87I8j
R/cerzYwUD+NfJl19rkps4X1B+/tDLiIFf3TFilfGr6M4bObbDv20Hm8r3PjxrAz
k4J1wLJFsE9pFLm6EuHtD+9BTII1hvsDX5Y4uSINZfZMTHs+Ii8Bw2QZHl+1Iwsi
eBS8xsZKyH3FpkNWjcGAfL5HI5wzqOjSrNrp3ELEsXs1rlpS3u00stnH331Zz+3+
wA2qKy8wskVmv94kYzQolFsPOmcuLKMgMznwxQIDAQABAoIBABNrvr7IspwRPzEY
lHjYbx5nB3ia/mAOLyELFTxEOOfp2buLi26cjdP22Nrqrg/F/M1GGGhM7wtcAxBC
pVativvBDtN1Attoyov5CKOka22HjgIqHcqJHXQA6oNE9CfQQKayZ87ZrFNEcrC5
049Lw7ShczKhLTf2W2hMZky1STqOZ9QBpFKOD102+yvgQio6R186r0Zxrz69zxqI
yVQH9VOI9E0WlszlWf+eGkZtG1tqiz2ItLh08UPzY0ZQvywhkcHoaN1Q0BygI/+U
Lbg1+NWRC4vDoHYrxz1jn4nWZAFTiFGy/g1tzdCxAfAslLjU2N5JBKXDzqaCQyY+
EAcweckCgYEA9XFzou9x1kP4J7G40qOqGG5Wii+cMDMLNNRDiFWZ9cIVYWpmxF3X
acyIVoxSofw+ILBsawu3F7TO7YUPRjQcErVIbmZcUiQhvxwifB36Nic4BqpgNofu
Q9dZMKBJOcUQ9MbywJfhvnCOdSd1naiEaElDJMG3CHOSc074a74yrS8CgYEA5jv0
APWm3r4Q2qYVYxiC6Cs+/7q4kyrSeEqm+HjVwKJqAQw3AYRuxz0MyhfAIzKQGivw
wMi6oIB9IEYBeoXsCvNIMsbV3JqYLKMkwoRp2JQD2wc7IYX01NDuGmJlUXfE2gOY
bGawyzUhXuAIfJMm3iYckpKZLMR7U8A4ractDEsCgYEA4bivnwXUTDgADQlNrzHi
6Ur3/WehnVYkFTas0MHgsHoITambzzV6OQtnyyiLifs/a7K0UpHYlU2sDBYVoPul
YbMkZJtwhf5Cps4KDNlI1eqlhMPFbgD+p5dxp92Q2jcYy/P3JhXH/urmqGlcqlxj
QME3paMdYAFhivfyUKv/UPMCgYARqsYVkMQmUYVvkdEQUqAw+qiR7R0exelyq5/W
b0dPyebCf9J0vlnV1hx2IY5v5QBj0b1evch8an+vi0+vvDkZugNvSgy9KevFeRto
BcstgGYvV4W1E9duwT2ULrrBnqQvapk2sEaewUv3QM/F53DTGS+WG8O/SLCCA70V
rj9pswKBgGLNQ22FrnKgjmbc7nJeM4i3zlFTdUs7XYzqWST4CgNmVeq9IbuYmM1K
xXiC158LvPHVTjS7e6yl0y86cAGlF6Bi50a3+7XhOPO98obRuPuOiyFP3fkWT8i2
q9YP0CrGpjDwXKH0BN6W41MTIZSfZSn3fubTf+nsldbkCyBAQTbJ
-----END RSA PRIVATE KEY-----
```

#### Enable certificate for your site
Homestead checks for certificates on all sites upon provisioning. To avoid Homestead overriding the cerficate configuration for existing sites, replace certificate references for all your sites.

This command should be executed every time a new site is provisioned.

```
sudo find /etc/nginx/sites-available/ -type f -exec sed -i "s/\/etc\/nginx\/ssl\/\(.*\)\.local-like\.st\.crt/\/etc\/nodes\/ssl\/local-like\.st\/star\.local-like\.st\.pem/g" {} \; && sudo find /etc/nginx/sites-available/ -type f -exec sed -i "s/\/etc\/nginx\/ssl\/\(.*\)\.local-like\.st\.key/\/etc\/nodes\/ssl\/local-like\.st\/star\.local-like\.st\.key/g" {} \;
```

**Important** Remember to do this for PhpMyAdmin as well

Restart nginx

`sudo service nginx restart`