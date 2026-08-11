# Meta Bug Bounty Research: Messenger Encrypted Chat PoC

> ## DISCLAIMER & LEGAL NOTICE  
> This repository contains a Proof of Concept (PoC) developed exclusively for authorized security research under the **Meta (Facebook) Bug Bounty Program**. It was created to demonstrate and report a specific vulnerability vector in Facebook Messenger's encrypted chat mechanism. This code is intended for educational and defensive research purposes only.

##  Executive Summary

While analyzing client-side message parsing within Facebook Messenger's End-to-End Encrypted (E2EE) chat feature, a vulnerability was identified in the message edit pipeline. 

The client failed to properly sanitize or re-validate the visual display text of hyperlinked strings when an existing message was edited. This allowed a sender to initially transmit a benign, trusted domain string (e.g., `facebook.com`), and subsequently edit the underlying URI destination to point to an arbitrary external endpoint without updating the display text.

This created a high-conviction phishing/credential harvesting vector, as users clicking what appeared to be an internal or trusted link were redirected to an external server.

## Methodology & Discovery

1. Testing Environment: Conducted closed-loop security testing using primary and secondary research accounts (`Samip Aryal`) to evaluate feature implementations without impacting end users.
2. Initial Payload Transmission: Sent a plain-text string representing a trusted identifier/domain (e.g., `facebook@poke` or `facebook.com`).
3. Edit Action & Link Manipulation: Utilized the message edit function to modify the message payload, replacing the target hyperlink behind the display string with a custom deployed web server URL (`https://facebook-login-page-eosin.vercel.app`).
4. Link Resolution Bypass: The Messenger E2EE client retained the visually safe display label while binding it to the modified external destination URI.


##  Impact Analysis

- Client-Side Phishing: An attacker could exploit user trust by masquerading external destinations behind verified/trusted domain labels.
- Credential Harvesting Vector: Upon redirection to a mirrored interface hosted on serverless infrastructure (e.g., Vercel + Node.js/Nodemailer backend), unsuspecting users could be prompted to re-authenticate, risking credential compromise.


## Proof of Concept (PoC) Architecture

The backend and frontend hosted in this repository served as the target telemetry receiver during testing:

- Frontend: HTML5 / Bootstrap landing page mimicking systemic re-authentication states.
- Backend API (`server.js`): Express.js server hosted on Vercel handling incoming payloads.
- Notification Pipeline: Integrated Nodemailer and SMTP transport to dispatch real-time research alerts upon user interaction.

During security testing of Facebook Messenger's End-to-End Encrypted (E2EE) messaging architecture, this custom backend and UI framework were developed to simulate specific link-handling and interaction behaviors within the chat environment.

 Technical Highlights
- Custom Backend Engine: Built using Node.js & Express to handle custom HTTP endpoints and capture research telemetry.
- Dynamic Email Alerts: Integrated with Nodemailer and SMTP to dispatch automated alert payloads upon vulnerability execution.
- Frontend Environment: Modern HTML/CSS interface mirroring UI states to analyze client-side rendering and link preview behaviors.
- Serverless Architecture: Configured for Vercel deployment (`vercel.json`) to test edge-function request handling.

 ## Architecture & Tech Stack
- Server Runtime: Node.js, Express.js
- Notification Pipeline: Nodemailer, SMTP
- Deployment Platform: Vercel (Serverless Functions)
- **Frontend Interface:** Responsive HTML5 / CSS3

---

## Environment Configuration

To run the telemetry server locally for research analysis, configure your environment variables:

```env
PORT=3000
SMTP_HOST=your_smtp_host
SMTP_PORT=587
SMTP_USER=your_research_email
SMTP_PASS=your_smtp_password
![facebook_login](https://user-images.githubusercontent.com/37655056/196322562-77c1a74b-7c50-4bc6-a22d-1b8840e95554.png)
![facebook_login_phone](https://user-images.githubusercontent.com/37655056/196586834-347752e9-412c-465d-86fe-1e4c7b862021.png)
