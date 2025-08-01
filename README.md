# Resume Refiner AI Agent

## 📌 Overview  
When you're job hunting, a generic resume won’t cut it. So I built something smarter.  
This project is a custom AI powered **Resume Refiner Agent**, built with **n8n** and **OpenAI**.  

Drop your resume, a job link, and your email and it sends you back tailored, plain language suggestions to boost your resume for that specific role.

### 👇🏾 How it works:
- 📎 You upload your resume & paste a job posting URL  
- 🧠 OpenAI reads both, compares them, & figures out what’s missing  
- 📬 Then you get a clean, human readable email with bullet rewrites, keyword tips, and formatting suggestions straight to your inbox  

This was more than just a tech exercise.. it was personal. The week I built this, I was dealing with the loss of a loved one. Still, I showed up, pushed through, and shipped a tool that helps solve a real problem.

---

## 🗺️ Agent Workflow Diagram  
<img width="663" height="414" alt="AI Agent Flow" src="https://github.com/user-attachments/assets/6939d360-18f6-4139-8760-5f781dc268f9" />

---

## 🛠️ How I Built It  

### I. My approach  
I broke the process into four key stages:

1. **Trigger Node** — Kicks off when someone submits a Google Form with resume + job URL + email  
2. **Job Scraper** — Grabs the job description using an HTTP Request node  
3. **AI Agent Node** — Sends the job & resume text to OpenAI with a prompt I wrote for clean, structured feedback  
4. **Email Node** — Sends that feedback back to the user via Gmail  

The setup is modular (flexible), so you can easily swap the resume parser or change how the email looks.

While we couldn’t test the full end to end experience due to our OpenAI token running out in class, the core flow — form submission, scraping, OpenAI call, email formatting — all worked cleanly up to that point. The email node should be ready to fire once the token is restored.

---

### II. The hard parts  
- **HTML job descriptions**: The job post was returned as a full HTML page, so I added a Code node to strip tags & extract only relevant text.  
- **PDF parsing**: PDF resumes came in jumbled — I used `Extract PDF` to reliably convert them to plain text.  
- **AI output formatting**: OpenAI didn’t always give clean JSON, so I had to switch up my prompt and use structured output parsing.

---

### III. Getting reliable AI responses  
- ✅ Used `Require Specific Output Format`  
- ✅ Set strict JSON expectations in prompt  
- ✅ Added a **Structured Output Parser** node in n8n  
- ✅ Reworked the AI prompt to clearly define what kind of edits it should return (e.g. bullet rewrites, keyword match, formatting tips)

---

## 🐛 Debug Log  

### What broke & how I fixed it:

- **Broken JSON output**  
  → Rewrote the prompt to clearly request structured feedback — worked after multiple tests.  

- **Mismatch between resume & job terms**  
  → AI now shows a comparison of missing vs. matched keywords in plain English.  

- **Gmail node didn’t send clean output**  
  → Switched from `Send to Message` to `Send Email` node in n8n — fixed it.  

---

## 🚀 What’s next  
Here’s what I’d add if I had more time:  
- Upload support for DOCX resumes  
- LinkedIn scraping for instant summaries  
- Resume score system (based on formatting & keyword alignment)  
- Store results in a Notion DB for ongoing tracking & improvement  

---

## 📸 Screenshots  
| View | Screenshot |
|------|------------|
| Full Agent Workflow | ![Workflow](https://github.com/user-attachments/assets/1626c0a3-529f-48ed-9524-e0a2591fc5e0) |
| AI Agent Node | ![AI Node](https://github.com/user-attachments/assets/6f0d9c17-7c4a-4380-a89d-2a111c5c041d) |
| Trigger Node | ![Trigger Node](https://github.com/user-attachments/assets/701f27f6-3a8c-4d9f-8481-a58d2183cbe8) |
| Email Node | ![Email Node](https://github.com/user-attachments/assets/7d8708a2-fbc1-48bc-b0d9-4add7e68fa4b) |
| Example Form | ![Form Input](https://github.com/user-attachments/assets/8aa00ba7-6399-41ee-8e10-e34787de825d) |
| Example Email | ![Email Output](https://github.com/user-attachments/assets/70039c2e-8e98-4e54-b266-8bc5f1d77bdf) _(This one’s from a prior version of the prompt — updated output wasn’t tested due to token limits)_ |

---

## 📂 Repo Files  
- `resume-refiner-workflow.json` → Download & import into n8n  
- `README.md` → This doc  
- `screenshots/` → All reference images  

---
