
# Pickle Rick - Try Hack Me - Writeup

First of all, I look at the website source code, I found 2 things:

- There is a comment is source code: 
```
<!--
    Note to self, remember username!
    Username: R1ckRul3s
-->
```

- There is a ```assets``` directory contains many stuffs

![assets-image](https://github.com/hung-qt/tryhackme-writeups/blob/main/PickleRick/assets-image.png)

Using ```curl``` command to get the content of ```robots.txt``` file:

``` curl http://10.10.216.172/robots.txt ```

Get the content: ```Wubbalubbadubdub```

So I guess this is the password for the account named ```R1ckRul3s```, I tried them for SSH authentication but it is not true. So they might be for another login authentication. 

Looing again at the ```assets``` directory, I see that there are two images, two gifs and some CSS, JS code.

The image ```rickandmorty.jpeg``` is used at the main page at ```http://10.10.216.172```, so other image and gifs should belonged to hidden websites.

First try with ```http://10.10.216.172/portal``` give me no luck, the second with ```http://10.10.216.172/portal.php``` give me a login page.

![login-page](https://github.com/hung-qt/tryhackme-writeups/blob/main/PickleRick/login-page-image.png)

With the username: ```R1ckRul3s``` and password: ```Wubbalubbadubdub```, I successfully logged into that site.

From here, I saw that the ```Commands``` section is interesting, other sections seems not working.

Try runnung some basic commands like ```ls, pwd, cd, ...```, all of them works except for ```cat``` command.

The result of ```ls``` command (by inputting the word "ls" and press enter):
```
Sup3rS3cretPickl3Ingred.txt
assets
clue.txt
denied.php
index.html
login.php
portal.php
robots.txt
```

Entering ```http://10.10.216.172/Sup3rS3cretPickl3Ingred.txt```, the website return us first ingredient that Rick needs:

```mr. meeseek hair``` - answer for first question

Next, I checked for the root privilege by running this command ```sudo -l```, the result:

```
Matching Defaults entries for www-data on ip-10-10-216-172:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www-data may run the following commands on ip-10-10-216-172:
    (ALL) NOPASSWD: ALL
```

This means that we can run ```sudo``` without password.

With my experience, I guess the second and third ingredients will locate in the ```home``` folder and ```root``` folder.

Running ```ls``` on both directories, it strengthens my judgment.

Excuting both commands to get the second and the third:

```less "/home/rick/second ingredients"``` - ```1 jerry tear```

```sudo less "/root/3rd.txt"``` - ```fleeb juice```
