# Connect your org

Salesforce Studio connects to an org in one click with the sign-in you already have. If your org does not allow that, connect with your own OAuth app instead.

## 1. Install the extension

1. Download `salesforce-studio-<version>.zip` from the [latest release](https://github.com/fcopensource/salesforce-studio-releases/releases/latest) and unzip it.
2. Open `chrome://extensions` (or `edge://extensions` in Microsoft Edge) and turn on **Developer mode**.
3. Click **Load unpacked** and choose the unzipped folder.
4. Pin **Salesforce Studio** from the Extensions menu.

Keep the folder where it is: the browser loads the extension from it. To update, unzip the new release over the same folder and click **Reload** on the extension.

## 2. Connect with your Salesforce sign-in

1. Sign in to your org in Chrome or Edge as you normally do.
2. With any Salesforce tab open (Lightning, Setup, Classic or Visualforce), click the **Salesforce Studio** icon.
3. Studio opens connected to that org and loads its components.

Not on a Salesforce tab? Open Studio from the toolbar: the home screen lists every org you are signed in to, each with a **Connect** button.

Studio never stores your Salesforce password or session. Signing out of Salesforce disconnects Studio.

## 3. Check your user's access

Your Salesforce user needs:

- **API Enabled**
- **Modify Metadata Through Metadata API Functions** (or **Modify All Data**)
- **Author Apex**, to save Apex classes and triggers
- **View Setup and Configuration**

A System Administrator has all of these. Ask your admin if any are missing.

## 4. If your org blocks browser sign-in: connect with an OAuth app

Some orgs restrict API access from browser sessions, for example with API Access Control. Studio then says your sign-in does not allow API access. Connect with an OAuth app instead:

1. In Studio, open **Settings** and copy the **callback URL** shown under *Connect with your own OAuth app*. It looks like `https://<id>.chromiumapp.org/`.
2. In Salesforce Setup, open **External Client App Manager** (or **App Manager → New Connected App** in older orgs) and create an app.
3. Enable OAuth and set the **Callback URL** to the URL you copied, including the trailing slash.
4. Add the scope **Manage user data via APIs (api)**.
5. Turn on **Require Proof Key for Code Exchange (PKCE)** and turn off **Require Secret for Web Server Flow**.
6. Save, then copy the app's **Consumer Key**. Never paste a Consumer Secret into Studio.
7. Back in Studio **Settings**, paste the Consumer Key. Tick **Sandbox** for a sandbox, or enter your **My Domain** URL if your org requires it, then click **Connect**.

A new app can take a few minutes to become active. Create the app in the same org you connect to.

## 5. Save your first change

1. Open a component from the explorer and make a small change.
2. Press <kbd>Ctrl</kbd> + <kbd>S</kbd> (<kbd>⌘</kbd> + <kbd>S</kbd> on a Mac). The change is saved to the org, and the console confirms it.
3. If Salesforce rejects the change, the console shows the error in red and your edit stays in the editor. Fix it and save again.

Saving an Apex class or trigger in production runs your org's Apex tests, as Salesforce requires. Lightning web components, Aura and Visualforce never run tests.

To see a diff first, validate without saving, or deploy several components together, use **Review changes** from the **•••** menu.

## Troubleshooting

| What you see | What to do |
| --- | --- |
| "Your sign-in does not allow API access" | Your org blocks browser sessions for the API. Connect with an OAuth app (step 4). |
| "Not signed in" | Sign in to that org in a browser tab, then connect again. |
| invalid client or app not found | Check the Consumer Key, that the app is in this org, and wait a few minutes after creating it. |
| Callback mismatch | Copy the callback URL from Studio's Settings again, including the trailing slash. |
| Insufficient access | Your user is missing a permission from step 3. |
| An empty folder | The org has none of that component type outside managed packages. |
| "Org source changed since it was loaded" (Review changes) | Someone changed the component in the org. Reload it from the explorer, then reapply your edit. |
| A deployment is still running | Use **Resume status** in the console. Closing Studio does not cancel a deployment. |

Need help? Visit [veyraeditor.com](https://veyraeditor.com/salesforce-studio).
