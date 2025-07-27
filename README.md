# Resume Refiner AI Agent

## 📌 Overview
This project is a custom AI-powered Resume Refiner built using n8n. It takes a user's uploaded resume, a job description URL, & their email — then uses OpenAI to analyze the content & send back tailored suggestions to improve the resume for that specific job.

Tech stack:
- Draw.io (map out project)
- n8n (automation platform)
- OpenAI GPT model
- Google Form (trigger)
- Gmail (output)
- Custom JSON parser

---

## 🔁 AI Agent Flow Diagram
# <img width="663" height="414" alt="Screenshot 2025-07-26 at 8 48 07 PM" src="https://github.com/user-attachments/assets/6939d360-18f6-4139-8760-5f781dc268f9" />

---

## 🛠️ Building the Agent

### I. What approach did you take to design your agent?
I broke the workflow into four key parts:
1. **Trigger Node** – Google Form submission collects the resume, job URL, & email.
2. **Job Description Scraper** – Extracts job text from the provided URL using an HTTP Request.
3. **AI Agent Node** – Prompts OpenAI with structured input and requests JSON output.
4. **Email Node** – Sends formatted suggestions back to the user.

The AI agent prompt was written to match my tone & style, focusing on clarity, quantifiable bullet rewrites, & keyword mapping.

### II. What challenges did you face in parsing, formatting, or integrating?
- The job description returned in HTML, so I had to clean the content with a code node.
- Parsing PDF resumes was unreadable at first; the Extract PDF node helped get raw text.
- Getting strict JSON from OpenAI took trial & error — prompt engineering + output schema played a big part.

### III. How did you ensure that the AI returned JSON reliably?
- Enabled `Require Specific Output Format` in the AI Agent node.
- Used a **Structured Output Parser** node to define exactly what JSON keys the response needed.
- Iterated on the prompt until it consistently returned properly formatted JSON.

---

## 🐛 Troubleshooting

### IV. What issues did you encounter & how did you resolve them?
- **Broken JSON from AI:**
  - **Fix:** Rewrote the prompt to clearly request structured output, tested against multiple inputs.

- **Mismatch between resume & job terms:**
  - **Fix:** Added a comparison table output in the JSON showing missing/matched keywords.

- **Bad email formatting:**
  - **Fix:** Switched to corrct AI Agent - was previously using "Send to Message" open AI which wasn't extracting the data correctly or providing the correct output.

---

## 🚀 Optimization

### V. What might you improve or add in future iterations?
- Support for DOCX resume uploads alongside PDFs.
- Integrate LinkedIn scraping for auto-summary suggestions.
- Add a resume score based on keyword overlap & formatting.
- Log form submissions & results in a database for tracking.

---

## 📸 Screenshots

- ✅ Full n8n Agent Workflow view <img width="729" height="270" alt="Screenshot 2025-07-26 at 8 55 18 PM" src="https://github.com/user-attachments/assets/1626c0a3-529f-48ed-9524-e0a2591fc5e0" />

- ✅ AI Agent node configuration <img width="952" height="483" alt="Screenshot 2025-07-26 at 8 57 03 PM" src="https://github.com/user-attachments/assets/6f0d9c17-7c4a-4380-a89d-2a111c5c041d" />

- ✅ Trigger node setup <br><img width="602" height="535" alt="Screenshot 2025-07-26 at 8 57 57 PM" src="https://github.com/user-attachments/assets/701f27f6-3a8c-4d9f-8481-a58d2183cbe8" />

- ✅ Email node configuration <br><img width="515" height="550" alt="Screenshot 2025-07-26 at 8 58 48 PM" src="https://github.com/user-attachments/assets/7d8708a2-fbc1-48bc-b0d9-4add7e68fa4b" />

- ✅ Example form input <br><img width="553" height="563" alt="Screenshot 2025-07-26 at 9 00 06 PM" src="https://github.com/user-attachments/assets/8aa00ba7-6399-41ee-8e10-e34787de825d" />

- ✅ Example email output <img width="918" height="426" alt="Screenshot 2025-07-26 at 9 00 48 PM" src="https://github.com/user-attachments/assets/70039c2e-8e98-4e54-b266-8bc5f1d77bdf" /> 
(This output is from a previous prompt - our class API token ran out so I was not able to test my current prompt)

---

## 📂 Files Included in GitHub
- `resume-refiner-workflow.json` → #exported & uploaded workflow from n8n
- `README.md` → #this file
- `screenshots/` → #added all required screenshots files in this folder
