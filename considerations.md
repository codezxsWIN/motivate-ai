
# Considerations for Using Motivational AI Assistant

Before using or contributing to this project, please review the following considerations to ensure proper setup and usage. This project, **motivate-ai**, relies on external APIs and requires careful configuration to function correctly.

---

## 1. API Keys and Webhook Configuration

- **Secure API Keys:**
  The `index.html` file contains placeholders for sensitive information:
  - `YOUR_ELEVENLABS_API_KEY`: Placeholder for the ElevenLabs API key used for text-to-speech functionality.
  - `YOUR_WEBHOOK_URL`: Placeholder for the webhook URL used to process user input and return motivational responses.

- **Do Not Hardcode Keys:**
  Never replace these placeholders directly in `index.html` with actual API keys or webhook URLs, as this exposes sensitive data in client-side code, especially in a public repository.

- **Set Up a Backend:**
  To securely manage API keys and webhook URLs:
  - Create a backend (e.g., using Node.js with Express) to handle API requests.
  - Store sensitive data in a `.env` file (e.g., `ELEVENLABS_API_KEY=your_key`, `WEBHOOK_URL=your_url`).
  - Ensure `.env` is listed in `.gitignore` to prevent accidental commits.
  - Update `index.html` to call your backend endpoints (e.g., `/api/elevenlabs` instead of the ElevenLabs API directly).

### Example backend setup (Node.js + Express):

```javascript
// server.js
const express = require('express');
const app = express();
require('dotenv').config();

app.use(express.json());

app.post('/api/elevenlabs', async (req, res) => {
    try {
        const response = await fetch(`https://api.elevenlabs.io/v1/text-to-speech/${process.env.ELEVENLABS_VOICE_ID}`, {
            method: 'POST',
            headers: {
                'Accept': 'audio/mpeg',
                'Content-Type': 'application/json',
                'xi-api-key': process.env.ELEVENLABS_API_KEY
            },
            body: JSON.stringify(req.body)
        });
        res.set('Content-Type', 'audio/mpeg');
        res.send(await response.blob());
    } catch (error) {
        res.status(500).send('Error processing audio');
    }
});

app.listen(3000, () => console.log('Server running on port 3000'));

```

-   **Obtain API Keys:**\
    If you don't have an ElevenLabs API key, sign up at [ElevenLabs](https://elevenlabs.io/) to obtain one. The webhook URL should be provided by your service (e.g., Make.com or another webhook provider).

* * * * *

2\. Backend Requirement
-----------------------

This project requires a backend to function fully due to the use of external APIs (ElevenLabs for text-to-speech) and a webhook for processing user input.

Without a backend, the placeholders (`YOUR_ELEVENLABS_API_KEY`, `YOUR_WEBHOOK_URL`) will cause the application to fail when attempting to fetch audio or send data to the webhook.

Follow the setup instructions in the `README.md` to create and configure a backend.

* * * * *

3\. Testing and Deployment
--------------------------

-   **Local Testing:**\
    Before deploying, test the application locally:

    -   Set up a backend as described above.

    -   Serve the HTML file using a local server (e.g., `npx http-server`).

    -   Open [http://localhost:8080](http://localhost:8080/) in your browser to verify functionality.

-   **GitHub Pages:**

    -   GitHub Pages is static and cannot run a backend.

    -   The UI will render, but backend-dependent features (text-to-speech, webhook responses) will **not** work unless the backend is hosted elsewhere (e.g., Heroku, Vercel).

-   **Full Deployment:**

    -   Host the backend on a platform like Heroku, Vercel, or Render.

    -   Update `index.html` to point to your backend's URL (e.g., `https://your-backend.com/api/elevenlabs`).

* * * * *

4\. Attribution and Licensing
-----------------------------

-   This project includes a dynamically loaded GitHub attribution section linking to `codezxsWIN`.

-   **Do Not Remove Attribution:** The attribution is protected by a basic integrity check. Removing or modifying it violates the project's license (see `LICENSE` file).

-   **License Compliance:** This project is licensed under the MIT License (see `LICENSE`). You may use, modify, and distribute the code, but you must retain the copyright notice and attribution to `codezxsWIN`.

* * * * *

5\. Security Best Practices
---------------------------

-   **Do Not Commit Sensitive Data:**\
    Double-check that no API keys, webhook URLs, or other sensitive data are committed to the repository. Use `.gitignore` to exclude files like `.env`.

-   **Obfuscate JavaScript (Optional):**\
    To make the client-side code harder to modify, consider obfuscating the JavaScript in `index.html`:

    ```
    npm install -g javascript-obfuscator
    javascript-obfuscator index.html --output index.min.html

    ```

-   **Monitor Usage:**\
    If using the ElevenLabs API, monitor your usage to avoid exceeding rate limits or incurring unexpected costs.

* * * * *

6\. Dependencies
----------------

This project relies on external libraries:

-   [SweetAlert2](https://cdn.jsdelivr.net/npm/sweetalert2@11)

-   [dotLottie Player](https://unpkg.com/@dotlottie/player-component@2.7.12)

Ensure these URLs are accessible and not blocked by your network or browser settings.

If hosting on a custom domain, verify that CORS policies allow these external resources.

* * * * *

7\. Contributions
-----------------

If contributing to this project:

-   Follow the setup instructions in `README.md`.

-   Do **not** include sensitive data in pull requests.

-   Respect the attribution and licensing terms.

-   Test changes locally with a backend before submitting.

* * * * *

8\. Contact
-----------

For questions or issues, please open an issue in this repository or contact the project owner at `codezxsWIN`.
