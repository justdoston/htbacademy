# Types of XSS

1) Stored (Persistent) XSS
The most critical type of XSS, which occurs when user input is stored on the back-end database and then displayed upon retrieval (e.g., posts or comments)
<br>
2) Reflected (Non-Persistent) XSS	Occurs when user input is displayed on the page after being processed by the backend server, but without being stored (e.g., search result or error message)
<br>
3) DOM-based XSS	Another Non-Persistent XSS type that occurs when user input is directly shown in the browser and is completely processed on the client-side, without reaching the back-end server (e.g., through client-side HTTP parameters or anchor tags)
