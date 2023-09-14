# Operation-System-Hardening-Practice
<h1>Description</h1>
In this exercise, I assumed the role of a cybersecurity analyst employed by a company hosting the cooking website, yummyrecipesforme.com. The website's visitors encountered a security issue while loading the main webpage, and my responsibility was to conduct a thorough investigation, identify the problem, document your findings, and propose a solution to rectify the security issue.

During my investigation of this security event, I examined a tcpdump log to uncover the network protocols employed in establishing connections between users and the website. These network protocols serve as the rules and standards governing data transmission among networked devices. Unfortunately, malicious actors can exploit these very protocols to infiltrate and attack private networks. Acquiring the skill to identify commonly used attack protocols is crucial for safeguarding your organization's network against such security incidents.

In successfully completing this assignment, I compiled a detailed account of the events surrounding the security incident and provided a recommendation for implementing a security measure to prevent similar issues from occurring in the future.

<h2>Scenario</h2>
Review the scenario below.

You are a cybersecurity analyst for yummyrecipesforme.com, a website that sells recipes and cookbooks. A disgruntled baker has decided to publish the website’s best-selling recipes for the public to access for free.

The baker executed a brute force attack to gain access to the web host. They repeatedly entered several known default passwords for the administrative account until they correctly guessed the right one. After they obtained the login credentials, they were able to access the admin panel and change the website’s source code. They embedded a Javascript function in the source code that prompted visitors to download and run a file upon visiting the website. After running the downloaded file, the customers are redirected to a fake version of the website where the seller’s recipes are now available for free.

Several hours after the attack, multiple customers emailed yummyrecipesforme’s helpdesk. They complained that the company’s website had prompted them to download a file to update their browsers. The customers claimed that, after running the file, the address of the website changed and their personal computers began running more slowly.

In response to this incident, the website owner tries to log in to the admin panel but is unable to, so they reach out to the website hosting provider. You and other cybersecurity analysts are tasked with investigating this security event.

To address the incident, you create a sandbox environment to observe the suspicious website behavior. You run the network protocol analyzer tcpdump, then type in the URL for the website, yummyrecipesforme.com. As soon as the website loads, you are prompted to download an executable file to update your browser. You accept the download and allow the file to run. You then observe that your browser redirects you to a different URL, greatrecipesforme.com, which is designed to look like the original site. However, the recipes your company sells are now posted for free on the new website.


- <a> The logs show the following process: </a>
    -  The browser requests a DNS resolution of the yummyrecipesforme.com URL.
    -  The DNS replies with the correct IP address.
    -  The browser initiates an HTTP request for the webpage.
    -  The browser initiates the download of the malware.
    -  The browser requests another DNS resolution for greatrecipesforme.com.
    -  The DNS server responds with the new IP address.
    -  The browser initiates an HTTP request to the new IP address.

A senior analyst confirms that the website was compromised. The analyst checks the source code for the website. They notice that Javascript code has been added to prompt website visitors to download an executable file. Analysis of the downloaded file found a script that redirects the visitors’ browsers from yummyrecipesforme.com to greatrecipesforme.com.

The cybersecurity team reports that the web server was impacted by a brute force attack. The disgruntled baker was able to guess the password easily because the admin password was still set to the default password. Additionally, there were no controls in place to prevent a brute-force attack.

Your job is to document the incident in detail, including identifying the network protocols used to establish the connection between the user and the website.  You should also recommend a security action to take to prevent brute-force attacks in the future.



<h3>Part 1: Security incident Report </h3>
The incident involved the disruption of the Hypertext Transfer Protocol (HTTP). To ascertain the issue, a combination of running tcpdump and accessing the website yummyrecipesforme.com was employed to detect the problem and capture protocol and traffic data in a DNS & HTTP traffic log file. This evidence led to the conclusion that the malevolent file was transmitted to users' computers via the HTTP protocol at the application layer.

A hacker carried out a brute force attack to infiltrate the web host using a dictionary attack method. They injected a JavaScript function into the source code, which, upon visitors accessing the website after gaining admin panel access, prompted them to download and execute a file. Subsequently, customers who ran the downloaded file were redirected to a counterfeit version of the website where the seller's recipes were available for free. Multiple customers reached out to yummyrecipesforme's helpdesk for assistance, and the admin entrusted my team with investigating the incident. We created a sandbox environment to monitor suspicious activity. I conducted network protocol analysis using tcpdump, which yielded log details.

The cybersecurity analyst scrutinized the tcpdump log and observed the browser's initial request for the IP address of the yummyrecipesforme.com website. Once the connection was established via the HTTP protocol, the analyst recalled the file download and execution. The logs exhibited a significant shift in network traffic as the browser sought a new IP resolution for the greatrecipesforme.com URL. Subsequently, the network traffic was rerouted to the new IP address associated with the greatrecipesforme.com website. In summary, the website was compromised through a brute-force attack.

Based on the incident report detailing how the attack transpired, I highly recommend that everyone change their passwords and implement Multi-Factor Authentication (MFA). The MFA plan should include an additional step where users must confirm their identity by verifying a one-time password (OTP) sent to their email or phone. After confirming their identity via login credentials and the OTP, they will gain access to the system. This additional layer of authorization will likely deter malicious actors attempting brute force attacks from gaining access to the system.
