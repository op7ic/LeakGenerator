[![License](https://img.shields.io/:license-gpl3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0.html)
[![python](https://img.shields.io/badge/Python-3.9%20%7C%203.10%20%7C%203.11%20%7C%203.12-blue.svg)](https://www.python.org/downloads/)

**Idea**

This project allows you to generate your own personal email and password leak combo. 

Fancy generating 280 million fake emails with equally fake password? Why not ... (just run 'leakme.py' with appropriate arguments listed below)


**Why?**

For fun. Need more info? read this http://arstechnica.co.uk/security/2016/05/the-massive-password-breach-that-wasnt-google-says-data-is-98-bogus/


**Use**
```
$ python leakme.py

-= LeakGenerator v1.1A by op7ic =-
Discover your own leak with spoofed emails, random passwords and equally random hashes

Supported hash types for '-t' argument:

[+] Main hash alghoritms. Will print "email : password : hash" combo.
md5
sha1
sha256
sha512
ntlm

[+] Hash alghoritms with random salt added. Will print "email : password : hash" combo.
md5_r_salt
sha1_r_salt
sha256_r_salt
sha512_r_salt
ntlm_r_salt

[+] Other type. Will print "email : password" combo.
clear
ad_compromise # special "AD" compromise mode, no usernames just SIDs + hashes

[+] Hash only types that print only hash values and no usernames or emails
md5_hashonly
sha1_hashonly
sha256_hashonly
sha512_hashonly
ntlm_only
md5_r_salt_hashonly
sha1_r_salt_hashonly
sha256_r_salt_hashonly
sha512_r_salt_hashonly
ntlm_r_salt_hashonly

You also need to specify max passwords you want to generate in hex format e.g. 0x00FFFFFF

The final command would look like this:

python leakme.py -t md5_r_salt -m 0x00FFFFFF
```

**Example**

See example.out file for randomly generated 'leak'

**Contributions**

Drop me a pull request

