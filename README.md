# Investigation-of-vulnerabilities-in-implementation-of-crypto-library.
The goal of this problem statement is to identify unknown vulnerabilities in the implementation of crypto libraries used by OpenVPN for Internet Protocol Security (IPsec), IPV6 deployment.
SIH 2023 PROJECT: PS ID- SIH1453 [BITHEADS]
By scrutinizing OpenVPN's crypto libraries, our team is actively identifying and resolving
vulnerabilities through a meticulous process of static and dynamic analyses complemented
by ethical exploitation for comprehensive improvements.
GOALS
Goal 1: Understand the basic concept of OpenVPN
Goal 2: Find all the vulnerability tools in the implementation of crypto libraries in OpenVPN
(IPSEC) in IPv6
Goal 3: Perform static and dynamic analysis of relevant code to discover any unknown bug
Goal 4: Identification of known and unknown vulnerabilities of crypto libraries in OpenVPN
(IPSEC) in IPv6
Goal5: Investigate and report vulnerabilities configure leading to
- Exploitation vector
- Compromise of data confidentiality
SOLUTION APPROACH
Understanding the basic workings of OpenVPN
Tools and Resources Used
● Findings of Synk.io:
Path Traversal (12 instances): Allows unauthorized file access.
Potential Buffer Overflow (11 instances): Caused by unsafe strcpy function usage.
Insecure Password Hashing (7 instances): Use of weak EVP_md5_sha1 hash.
Double Free (5 instances): Attempt to free the same memory block twice.
Improper Null Termination (5 instances): Risk of information disclosure or buffer
overflows.
Use After Free (4 instances): Incorrect dynamic memory management.
Dereference of NULL Pointer (3 instances): Accessing invalid memory addresses.
Server-Side Request Forgery (SSRF) (2 instances): Potential for unauthorized server
requests.
Python 2 Source Code (2 instances): Use of outdated and unsupported Python 2.
Memory Allocation of String Length (1 instance): Potential for memory-related
issues.
Authentication Bypass by Spoofing (1 instance): Weakness in identity verification.
Integer Overflow (1 instance): Vulnerability due to numerical calculation errors.
● Findings of CPP Checker:
The focus area of CPP Checker was identifying cryptographic vulnerabilities,
memory management issues, input validation errors, incorrect usage of cryptographic
functions, insecure configuration options and compliance with coding standards.
The outcomes it gave were some basic warnings and errors e.g., missing return
statements, lack of initialization, etc.
CPP Checker
● Findings of Truffle Hog:
Gave the information about public, and private keys and other credentials present in
the GitHub repository.
Truffle Hog
● Findings of Boofuz:
Boofuz
● Findings of Valgrind:
Valgrind
● Findings of Nessus:
Nessus
● Findings of OpenVAS:
OpenVAS
● Findings of CVE List:
CVE list gave the known vulnerabilities along with the patched and unpatched
vulnerabilities.
CLIENT AND SERVER SETUP
● Server:
● Client:
● Wireshark analysis on OpenVPN client and server connection:
Wireshark
INNOVATION
After following this approach, the vulnerabilities that we narrowed down are:
1. Dereference of a NULL Pointer in file ssl_mbedtls.c
https://github.com/Atharvakarekar/openvpn/blob/ca84ea53679f97b2957f3cc65ce6041
a7fc3a99f/src/openvpn/ssl_mbedtls.c#L702
Exploitation:
This includes simulations for potential scenarios where hash might be NULL, or
hashlen could be invalid (too large or too small). Additionally, it includes a simulation
of allocation failure for to_sign. These scenarios are detected and handled within the
sign_data function, simulating potential issues in the code flow.
2. Buffer Overflow in file win32.c
https://github.com/Atharvakarekar/openvpn/blob/8656b85c7324fc9ae7f10a9f37227a5
8766aae33/src/openvpn/win32.c#L975
Exploitation:
Modify arg Length: Provide an argument longer than maxlen + 1 character.
Observe Behavior: The code might crash or behave unexpectedly due to overwritten
memory.
Both these vulnerabilities are currently unpatched in the latest OpenVPN version i.e., version
2.6.8,
