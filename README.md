# LinkedIn Text Post Automation via Colab

Google Colab notebook to post simple text updates to your LinkedIn profile using the LinkedIn v2 API and OAuth 2.0 Authorization Code Flow.

## Prerequisites

Before using this notebook, you **MUST** set up a LinkedIn Developer Application:

1.  **Create App:** Go to [https://www.linkedin.com/developers/apps/](https://www.linkedin.com/developers/apps/) and create a new application.
2.  **Add Products:** Navigate to the "Products" tab for your App. Add and ensure **Access approved** status for:
    *   `Sign In with LinkedIn using OpenID Connect`
    *   `Share on LinkedIn`
3.  **Configure Redirect URI:** Go to the "Auth" tab. Under "OAuth 2.0 settings", add **EXACTLY** the following URL to the "Authorized redirect URLs" list:
    `https://www.linkedin.com/developers/tools/oauth/redirect`
4.  **Get Credentials:** Still on the "Auth" tab, find and copy your **Client ID** and **Client Secret**. You will need these to run the notebook.

## How to Use

1.  **Open in Colab:** Click the "Open in Colab" badge above (You'll add this later!).
2.  **Run Cell 1 (Setup):** Execute the first cell. It will install necessary libraries and prompt you to enter:
    *   Your LinkedIn App **Client ID**.
    *   Your LinkedIn App **Client Secret** (input will be hidden).
    *   The **Redirect URI** (use the one specified in Prerequisites).
3.  **Run Cell 2 (Generate Auth URL):** Execute the second cell. It generates a unique authorization link.
4.  **Authorize via Browser (Manual Step):**
    *   **Click the URL** printed by Cell 2.
    *   Log in to LinkedIn if required.
    *   Review the permissions and click **"Allow"**.
    *   You'll be redirected (likely to a LinkedIn Developer Tools page). **Copy the ENTIRE URL** from your browser's address bar after this redirect completes.
5.  **Run Cell 3 (Process Redirect):** Execute the third cell. **Paste the full URL** you just copied into the input prompt. It will extract the necessary `code` and `state`.
6.  **Run Cell 4 (Authenticate):** Execute the fourth cell. It uses the code from Cell 3 to get your access token and User URN. It will confirm if authentication was successful.
7.  **Run Cell 5 (Post Update):** **Only if Cell 4 was successful**, run the fifth cell. It will prompt you to enter the text content for your post. After you enter text, it will attempt to post to LinkedIn (Visibility: Connections only). A success message will include a direct link to your new post.

## Re-Authenticating
Your access token will eventually expire. If posting fails with a token error (e.g., 401 Unauthorized), you need to re-authenticate by running **Cell 2** through **Cell 5** again. You typically don't need to re-run Cell 1 unless your credentials change.

## Security Warning
*   **NEVER commit your Client ID or Client Secret directly into the notebook code** if you push it to a public repository like GitHub.
*   This notebook uses `getpass` to hide the Client Secret input during execution, but the secret is still handled within the Colab environment's memory for the session. Be mindful of your environment's security. Consider using Colab Secrets for enhanced security if preferred (requires minor code modification in Cell 1).

## Disclaimer
This notebook interacts with the LinkedIn API. LinkedIn may change its API, policies, or rate limits at any time. Use this tool responsibly and in accordance with LinkedIn's Developer Terms of Use.

## License
[Specify the license you chose, e.g., MIT License]
