**Idea**

This project allows you to generate your own personal email and password leak combo. 

Fancy generating 280 milion fake emails with equally fake password? Why not ... (just run 'leakme.py')

If you **really** need to create more emails/passwords just edit the file and change 'min' and 'max' variable.

**Why?**

For fun. Need more info? read this http://arstechnica.co.uk/security/2016/05/the-massive-password-breach-that-wasnt-google-says-data-is-98-bogus/


**Use**

To generate clear text passwords only

python leakme.py clear

To generate sha512 passwords only:

python leakme.py sha512

To generate sha256 passwords only:

`python leakme.py sha256`

To generate sha1 passwords only:

`python leakme.py sha1`

To generate md5 passwords only:

`python leakme.py md5`

To generate sha512 + random salt:

`python leakme.py sha512_r_salt`

To generate sha256 + random salt:

`python leakme.py sha256_r_salt`

To generate sha1 + random salt:

`python leakme.py sha1_r_salt`

To generate md5 + random salt:

`python leakme.py md5_r_salt`

**Example**

See example.out file for randomly generated 'leak'

**Contributions**

Drop me a pull request

