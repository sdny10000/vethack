# Money Moves — Kit 02 demo

Money Moves is a Kit 02 demo for veterans to explore a money question, see a plain-language answer and next step, and review monthly income and expenses. The question picker, free-form questions, and savings follow-ups all use the same backend Q&A.

## Run locally

1. Install Node.js 22 or newer and the Azure CLI.
2. Copy `.env.example` to `.env`. The Azure OpenAI endpoint is prefilled; set `AZURE_OPENAI_MODEL` to the name of your deployed Azure OpenAI model.
3. Sign in with an Azure identity that has permission to use the Azure OpenAI deployment:

   ```powershell
   az login
   ```

4. Install dependencies and start the app:

   ```powershell
   npm install
   npm start
   ```

5. Open `http://localhost:3000`.

The backend uses Microsoft Entra ID via `DefaultAzureCredential` and requests a token for `https://cognitiveservices.azure.com/.default`. For Azure hosting, assign the app a managed identity and grant it access to the Azure OpenAI resource. No API key is needed or should be placed in the browser or repository.

## Page 8 challenge

The challenge is to help a veteran understand one confusing money moment—such as a first civilian paycheck or collections letter—in plain, non-judgmental language, then offer one small step they can take this week and a real-person resource for anything bigger.

The home page starts with a pick-list of common money questions for Chris and other veterans: pay changes, monthly budget, collection letters, VA benefits, health coverage, retirement accounts, savings, credit, or where to start. Selecting “Why did my paycheck change after service?” opens a visual comparison of Chris’s Army and civilian take-home pay, explains the different pay structures and deductions, and lets the user choose a typical two-check month or annual monthly average before adding it to the budget. Choosing “How much money comes in and goes out?” opens a guided monthly cash-flow walkthrough with editable amounts and a live savings what-if. In the sample budget, saving $150 instead of $100 per month leaves about $595 after listed bills and reaches a $3,000 goal from $1,100 in about 13 instead of 19 months. These guided calculations run in the browser; they do not require the AI service. Other questions use the AI answer flow; veterans can also paste redacted document text or describe a concern. Broader transition topics and reminders are secondary.

For a no-case-data version of the paycheck question, open `http://localhost:3000/paycheck-change-workflow.html` after starting the server. It is an interactive workflow where the user can skip amounts or compare their own pay periods and optionally enter statement-level earnings and deduction details. Its free-form note and currently entered comparison details go to the Azure OpenAI deployment only when the user explicitly selects “Explain my note with Money Moves.” The military/civilian document controls only select and display filenames locally; this app does not read or upload document contents. This workflow does not contain Chris’s figures. The existing main demo remains at `http://localhost:3000/`.

## Privacy and prototype limits

Questions, recent chat history, and the editable monthly money snapshot from the main demo are sent to the configured Azure OpenAI deployment to generate answers. In the paycheck workflow, the note and entered comparison details are sent only after the user explicitly selects the explain button. The backend requests `store: false`; do not paste real personal, account, or government ID information. Uploaded file contents are not read or transmitted. Names, amounts, dates, and local organizations in the Chris case are fictional hackathon materials.

This is financial education, not legal, tax, investment, credit, insurance, or benefits advice. Verify referrals and deadlines and consult a qualified person for individual decisions. A production service also needs privacy review, validated referrals and sources, and qualified human oversight.
