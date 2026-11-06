# Phishing Analysis 

## 📖 Overview

**Author:** Mohit Patil  
**Platform:** Blue Team Labs Online (BTLO)  
**Challenge:** Phishing Analysis  
**Category:** Security Operations (SO)  
**Difficulty:** Easy  
**Completed:** Nov 6, 2026

## 🎯 Scenario
As a SOC Analyst, I was tasked with investigating a suspicious email reported by a user. The objective of this lab is to perform static analysis on the provided email (.eml) file to extract key Indicators of Compromise (IOCs), understand the attacker's methodology, and identify the malicious payload or destination.

## 🛠️ Tools Used
*   Text Editor (for raw email header analysis)
*   Email Client (for rendering the .eml file)
*   OSINT Tools (URL2PNG, whois.domaintools.com)

---

## 🕵️‍♂️ Investigation & Walkthrough

### 1. Who is the primary recipient of this email?
By analyzing the email headers, specifically the `To:` field, we can identify the intended target of this phishing attempt.
*   **Answer:** `kinnar1975@yahoo.co.uk`
*   Reference:

    <img width="843" height="133" alt="Screenshot 2026-11-06 100047" src="https://github.com/user-attachments/assets/b246b262-a307-4bae-ab05-eeb8757d9c35" />

### 2. What is the subject of this email?
Reviewing the `Subject:` header reveals how the attacker attempted to trick the user into opening the email by making it look like an administrative bounce-back message.
*   **Answer:** `Undeliverable: Website contact form submission`
*   Reference: 

    <img width="770" height="73" alt="Screenshot 2026-11-06 100102" src="https://github.com/user-attachments/assets/b67b65c8-06cd-42d5-a48a-179a9b181ef4" />


### 3. What is the date and time the email was sent?
Checking the `Sent:` header gives us the exact timestamp of the attack, which is crucial for timeline reconstruction in an incident response scenario.
*   **Answer:** `18 March 2021 04:14`
*   Reference: 

    <img width="830" height="85" alt="Screenshot 2026-11-06 100142" src="https://github.com/user-attachments/assets/3dd5fc38-5c8c-43dd-8b87-065c91fa46c8" />


### 4. What is the Originating IP?
By tracing back through the `Received:` headers from bottom to top, we can find the IP address of the server that originally sent the email. 
*   **Answer:** `103.9.171.10`
*   Reference: 

    <img width="1460" height="195" alt="Screenshot 2026-11-06 100658" src="https://github.com/user-attachments/assets/49fed12f-6dd8-437d-93b0-f5aaec9ea262" />


### 5. Perform reverse DNS on this IP address, what is the resolved host?
Using `whois.domaintools.com` (or simply looking at the adjacent information in the `Received` header where the IP is enclosed in brackets), we can resolve the originating IP to its hostname.
*   **Answer:** `c5s2-1e-syd.hosting-services.net.au`
*   Reference: 

    <img width="1032" height="525" alt="Screenshot 2026-11-06 235559" src="https://github.com/user-attachments/assets/08862b4c-762f-495f-a856-153d07dd9c07" />


### 6. What is the name of the attached file?
Opening the email in a client or reviewing the MIME boundaries in the raw text reveals an attached file meant to be opened by the victim.
*   **Answer:** `Website contact form submission.eml`
*   Reference: 

    <img width="833" height="281" alt="Screenshot 2026-11-06 102349" src="https://github.com/user-attachments/assets/40961284-dae8-4679-a9d8-702b7bdf8e97" />
  

### 7. What is the URL found inside the attachment?
By inspecting the source code/HTML of the attached `.eml` file, we find an embedded hyperlink designed to direct the user to a malicious site promising "Good earnings".
*   **Answer:** `https://35000usdperwwekpodf.blogspot.sg` 
*   Reference: 

    <img width="1077" height="173" alt="Screenshot 2026-11-06 101555" src="https://github.com/user-attachments/assets/3654abcf-e2f7-4088-b468-8a52906faab5" />

  
### 8. What service is this webpage hosted on?
Looking at the domain name of the extracted URL, we can identify the hosting provider abused by the attacker.
*   **Answer:** `blogspot` (or Blogger)
*   Reference:
  
    <img width="1180" height="170" alt="Screenshot 2026-11-06 103729" src="https://github.com/user-attachments/assets/2dc3457a-ebef-49ea-b663-4a6fb752c634" />

### 9. Using URL2PNG, what is the heading text on this page?
Since navigating to potentially malicious infrastructure is dangerous (and the site might be taken down), utilizing a service like URL2PNG allows us to safely view what the site looked like. 
*   **Answer:** `Blog has been removed`
*   Reference: 

    <img width="602" height="352" alt="Screenshot 2026-11-06 104226" src="https://github.com/user-attachments/assets/3016808c-d41a-4895-8f2c-d86863118e4d" />


---

## 💡 Conclusion & Key Takeaways
This challenge effectively demonstrated the core fundamentals of phishing email analysis. Key takeaways include:
*   The importance of carefully dissecting email headers (`To`, `From`, `Subject`, `Date`, `Received`) to establish the baseline facts of the communication.
*   How attackers utilize nested or attached `.eml` files to bypass basic spam filters and hide malicious URLs.
*   The value of using safe, out-of-band OSINT tools (like URL2PNG) to investigate suspicious links without risking direct exposure to malicious infrastructure.

<img width="1137" height="852" alt="Screenshot 2026-11-06 132328" src="https://github.com/user-attachments/assets/c8e58919-431c-4ce5-97ac-767343362fca" />
