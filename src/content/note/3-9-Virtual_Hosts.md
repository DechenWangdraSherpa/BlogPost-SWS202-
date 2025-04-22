---
title: 3-9-Virtual Hosts
seriesId: 3-Web-Information-Gathering
publishDate: "2025-04-22T15:30:00Z"
---

# Virtual Hosts

Once the DNS directs traffic to the correct server, the web server configuration becomes crucial in determining how the incoming requests are handled. Web servers like Apache, Nginx, or IIS are designed to host multiple websites or applications on a single server. They achieve this through virtual hosting, which allows them to differentiate between domains, subdomains, or even separate websites with distinct content.

## How Virtual Hosts Work: Understanding VHosts and Subdomains

At the core of virtual hosting is the ability of web servers to distinguish between multiple websites or applications sharing the same IP address. This is achieved by leveraging the HTTP Host header, a piece of information included in every HTTP request sent by a web browser.

The key difference between VHosts and subdomains is their relationship to the Domain Name System (DNS) and the web server's configuration.

- **Subdomains**: These are extensions of a main domain name (e.g., blog.example.com is a subdomain of example.com). Subdomains typically have their own DNS records, pointing to either the same IP address as the main domain or a different one. They can be used to organize different sections or services of a website.
  
- **Virtual Hosts (VHosts)**: Virtual hosts are configurations within a web server that allow multiple websites or applications to be hosted on a single server. They can be associated with top-level domains (e.g., example.com) or subdomains (e.g., dev.example.com). Each virtual host can have its own separate configuration, enabling precise control over how requests are handled.

If a virtual host does not have a DNS record, you can still access it by modifying the hosts file on your local machine. The hosts file allows you to map a domain name to an IP address manually, bypassing DNS resolution.

Websites often have subdomains that are not public and won't appear in DNS records. These subdomains are only accessible internally or through specific configurations. VHost fuzzing is a technique to discover public and non-public subdomains and VHosts by testing various hostnames against a known IP address.

![Image Placeholder]  <!-- Space for the image -->

## Server VHost Lookup

The following illustrates the process of how a web server determines the correct content to serve based on the Host header:

1. **Browser Requests a Website**: When you enter a domain name (e.g., www.inlanefreight.com) into your browser, it initiates an HTTP request to the web server associated with that domain's IP address.
2. **Host Header Reveals the Domain**: The browser includes the domain name in the request's Host header, which acts as a label to inform the web server which website is being requested.
3. **Web Server Determines the Virtual Host**: The web server receives the request, examines the Host header, and consults its virtual host configuration to find a matching entry for the requested domain name.
4. **Serving the Right Content**: Upon identifying the correct virtual host configuration, the web server retrieves the corresponding files and resources associated with that website from its document root and sends them back to the browser as the HTTP response.

In essence, the Host header functions as a switch, enabling the web server to dynamically determine which website to serve based on the domain name requested by the browser.

## Types of Virtual Hosting

There are three primary types of virtual hosting, each with its advantages and drawbacks:

1. **Name-Based Virtual Hosting**: This method relies solely on the HTTP Host header to distinguish between websites. It is the most common and flexible method, as it doesn't require multiple IP addresses. It’s cost-effective, easy to set up, and supports most modern web servers. However, it requires the web server to support name-based virtual hosting and can have limitations with certain protocols like SSL/TLS.
2. **IP-Based Virtual Hosting**: This type of hosting assigns a unique IP address to each website hosted on the server. The server determines which website to serve based on the IP address to which the request was sent. It doesn't rely on the Host header, can be used with any protocol, and offers better isolation between websites. Still, it requires multiple IP addresses, which can be expensive and less scalable.
3. **Port-Based Virtual Hosting**: Different websites are associated with different ports on the same IP address. For example, one website might be accessible on port 80, while another is on port 8080. Port-based virtual hosting can be used when IP addresses are limited, but it’s not as common or user-friendly as name-based virtual hosting and might require users to specify the port number in the URL.

## Virtual Host Discovery Tools

While manual analysis of HTTP headers and reverse DNS lookups can be effective, specialized virtual host discovery tools automate and streamline the process, making it more efficient and comprehensive. These tools employ various techniques to probe the target server and uncover potential virtual hosts.

Several tools are available to aid in the discovery of virtual hosts:

| Tool        | Description                           | Features                                              |
|-------------|---------------------------------------|-------------------------------------------------------|
| gobuster    | A multi-purpose tool often used for directory/file brute-forcing, but also effective for virtual host discovery. | Fast, supports multiple HTTP methods, can use custom wordlists. |
| Feroxbuster | Similar to Gobuster, but with a Rust-based implementation, known for its speed and flexibility. | Supports recursion, wildcard discovery, and various filters. |
| ffuf        | Another fast web fuzzer that can be used for virtual host discovery by fuzzing the Host header. | Customizable wordlist input and filtering options. |

### Gobuster

Gobuster is a versatile tool commonly used for directory and file brute-forcing, but it also excels at virtual host discovery. It systematically sends HTTP requests with different Host headers to a target IP address and then analyzes the responses to identify valid virtual hosts.

To brute force Host headers, you need to prepare the following:
1. **Target Identification**: First, identify the target web server's IP address. This can be done through DNS lookups or other reconnaissance techniques.
2. **Wordlist Preparation**: Prepare a wordlist containing potential virtual host names. You can use a pre-compiled wordlist, such as SecLists, or create a custom one based on your target's industry, naming conventions, or other relevant information.
