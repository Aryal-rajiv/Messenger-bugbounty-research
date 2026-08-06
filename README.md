# Meta Bug Bounty Research: Messenger Encrypted Chat PoC

> ⚠️ **DISCLAIMER & LEGAL NOTICE**  
> This repository contains a Proof of Concept (PoC) developed exclusively for authorized security research under the **Meta (Facebook) Bug Bounty Program**. It was created to demonstrate and report a specific vector of vulnerability within Facebook Messenger's encrypted chat mechanism. This code is intended for educational and defensive research purposes only.

---

## 🔍 Research Overview

During security testing of Facebook Messenger's End-to-End Encrypted (E2EE) messaging architecture, this custom backend and UI framework were developed to simulate specific link-handling and interaction behaviors within the chat environment.

### Technical Highlights
- **Custom Backend Engine:** Built using Node.js & Express to handle custom HTTP endpoints and capture research telemetry.
- **Dynamic Email Alerts:** Integrated with Nodemailer and SMTP to dispatch automated alert payloads upon vulnerability execution.
- **Frontend Environment:** Modern HTML/CSS interface mirroring UI states to analyze client-side rendering and link preview behaviors.
- **Serverless Architecture:** Configured for Vercel deployment (`vercel.json`) to test edge-function request handling.

---

## 🛠️ Architecture & Tech Stack

- **Server Runtime:** Node.js, Express.js
- **Notification Pipeline:** Nodemailer, SMTP
- **Deployment Platform:** Vercel (Serverless Functions)
- **Frontend Interface:** Responsive HTML5 / CSS3

---

## ⚙️ Environment Configuration

To run the telemetry server locally for research analysis, configure your environment variables:

```env
PORT=3000
SMTP_HOST=your_smtp_host
SMTP_PORT=587
SMTP_USER=your_research_email
SMTP_PASS=your_smtp_password
![facebook_login](https://user-images.githubusercontent.com/37655056/196322562-77c1a74b-7c50-4bc6-a22d-1b8840e95554.png)
![facebook_login_phone](https://user-images.githubusercontent.com/37655056/196586834-347752e9-412c-465d-86fe-1e4c7b862021.png)
