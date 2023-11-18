# DOM XSS
The third and final type of XSS is another `Non-Persistent` type called `DOM-based XSS`. While reflected XSS sends the input data to the back-end server through HTTP requests, `DOM XSS` is completely processed on the `client-side through JavaScript`. DOM XSS occurs when JavaScript is used to change the page source through the `Document Object Model (DOM)`.

In DOM based XSS user input will not reach to backend server that's why it is not stored nor persistence.

# Source & Sink
To further understand the nature of the DOM-based XSS vulnerability, we must understand the concept of the `Source and Sink` of the object displayed on the page. The `Source` is the JavaScript object that takes the user input, and it can be any input parameter like a URL parameter or an input field, as we saw above.

On the other hand, the Sink is the function that writes the user input to a DOM Object on the page. If the Sink function does not properly sanitize the user input, it would be vulnerable to an XSS attack. Some of the commonly used JavaScript functions to write to DOM objects are:

1) document.write()
2) DOM.innerHTML
3) DOM.outerHTML

Furthermore, some of the `jQuery` library functions that write to DOM objects are:
1) add()
2) after()
3) append()

# DOM Attacks

If we try the XSS payload we have been using previously, we will see that it will not execute. This is because the `innerHTML` function does not allow the use of the `<script>` tags within it as a security feature. 
However we can use:
```bash
<img src="" onerror=alert(window.origin)>
```

The above line creates a new HTML image object, which has a onerror attribute that can execute JavaScript code when the image is not found. So, as we provided an empty image link (""), our code should always get executed without having to use <script> tags:
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/78e80a6f-2e24-4836-81c7-f1a294bbdf66)


https://github.com/offensivecyber03/htbacademy/assets/71892943/0d704d25-cfd8-42b1-a45f-07f9249d9b64


