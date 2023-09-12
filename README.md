# Operation-System-Hardening-Practice
<h1>Description</h1>
In this exercise, I assumed the role of a cybersecurity analyst employed by a company hosting the cooking website, yummyrecipesforme.com. The website's visitors encountered a security issue while loading the main webpage, and my responsibility was to conduct a thorough investigation, identify the problem, document your findings, and propose a solution to rectify the security issue.

During my investigation of this security event, I examined a tcpdump log to uncover the network protocols employed in establishing connections between users and the website. These network protocols serve as the rules and standards governing data transmission among networked devices. Unfortunately, malicious actors can exploit these very protocols to infiltrate and attack private networks. Acquiring the skill to identify commonly used attack protocols is crucial for safeguarding your organization's network against such security incidents.

In successfully completing this assignment, I compiled a detailed account of the events surrounding the security incident and provided a recommendation for implementing a security measure to prevent similar issues from occurring in the future.

<h2>Scenario</h2>
Review the scenario below.

You are a cybersecurity analyst for yummyrecipesforme.com, a website that sells recipes and cookbooks. A disgruntled baker has decided to publish the website’s best-selling recipes for the public to access for free. 

The baker executed a brute force attack to gain access to the web host. They repeatedly entered several known default passwords for the administrative account until they correctly guessed the right one. After they obtained the login credentials, they were able to access the admin panel and change the website’s source code. They embedded a javascript function in the source code that prompted visitors to download and run a file upon visiting the website. After running the downloaded file, the customers are redirected to a fake version of the website where the seller’s recipes are now available for free.

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

A senior analyst confirms that the website was compromised. The analyst checks the source code for the website. They notice that javascript code had been added to prompt website visitors to download an executable file. Analysis of the downloaded file found a script that redirects the visitors’ browsers from yummyrecipesforme.com to greatrecipesforme.com. 

The cybersecurity team reports that the web server was impacted by a brute force attack. The disgruntled baker was able to guess the password easily because the admin password was still set to the default password. Additionally, there were no controls in place to prevent a brute force attack. 

Your job is to document the incident in detail, including identifying the network protocols used to establish the connection between the user and the website.  You should also recommend a security action to take to prevent brute force attacks in the future.



<h3>Part 1: Provide a summary of the problem found in the DNS and ICMP traffic log</h3>
The UDP protocol reveals that the DNS was unreachable; could not retrieve the IP address. This is based on the results of the network analysis, which show that the ICMP echo reply returned the error message: udp port 53 is unreachable. The port noted in the error message is used for DNS service. The most likely issue is that DNS was unable to pick up the service, which led to the error message.
<h3>Part 2: Explain your analysis of the data and provide at least one cause of the incident</h3>
The incident occurred at 1:23 p.m. Customers were trying to access the website but were unable to, so they reported the incident, indicating that an error “destination port unreachable” was the outcome after the loading process. During the investigation, the IT department first tried to access the website and received the same error, then used a network packet analyzer: ICMP which provided details about the incident. There was no service being picked up by the receiving DNS port, as indicated by the ICMP error message “udp port 53 unreachable. The DNS server might be down due to a successful Denial of Service attack or a misconfiguration.
