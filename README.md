# ISC353-Spring2026-Phishing-Awareness-Project

## Project Description
This project is a cybersecurity awareness simulation developed for ISC353 Information Systems Security. The project demonstrates how phishing campaigns can be created, delivered, and analyzed in a controlled educational environment using GoPhish.

The main goal is to understand phishing attack techniques, test user awareness, and show how organizations can improve security training and reduce phishing risks.

## Team Members
- Student 1: Hajer Mubarak Alajmi / 2191118722
- Student 2: Hajar Thamer Alsahaib / 2191115194

## Tools and Technologies
- GoPhish
- Kali Linux
- Ngrok
- Gmail SMTP
- HTML
- CSS
- GitHub

## Project Structure
```text
Phishing-Awareness-Project/
│
├── README.md
├── requirements.txt
├── LICENSE
├── .gitignore
│
├── email-templates/
│   └── sample-email.html
│
├── landing-pages/
│   └── login-page.html
│
├── screenshots/
│   └── results-evidence.png
│
└── report/
    └── final-report.pdf

System Architecture

The project uses GoPhish to create and manage phishing awareness campaigns. Gmail SMTP is used to send the simulation emails, while ngrok exposes the local landing page through a public URL. GoPhish records user actions such as email opens, link clicks, and submitted form data.

Setup Instructions
Install and run GoPhish on Kali Linux.
Log in to the GoPhish admin panel.
Create a sending profile using Gmail SMTP.
Create an email template using GoPhish variables such as {{.URL}} and {{.Tracker}}.
Create a landing page with a simple HTML form.
Run ngrok to expose the local phishing server.
Create a GoPhish campaign and launch it in a controlled environment.
Review campaign results and screenshots.
Usage Example

This project can be used to demonstrate:

How phishing emails are structured.
How fake login or survey pages are created for awareness training.
How GoPhish tracks opens, clicks, and submissions.
How users can learn to recognize suspicious messages.
Ethical Notice

This project is for educational and awareness purposes only. It must only be used in a controlled environment with permission. It must not be used to attack, trick, or harm real users.


Final project submission for ISC353 Spring 2026.
