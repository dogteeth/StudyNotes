#### note:
For every user downloading your app, Apple creates a receipt containing some meta-information (which app version the user downloaded, when, and so on).

When your app offers in-app purchases, those are also saved in the receipt. Since this receipt is automatically synced with all devices of the user, it is the right choice to check what a user bought and unlock the content on all of his devices correspondingly.

See here for an article from Apple about receipt validation techniques. If you choose the local (on-device) receipt validation, I recommend you to use the TPInAppReceipt library to encode the receipt. That saves a lot of headaches.

#### Setup In-App Purchase

- Go to  "Certificates, Identifiers & Profiles
- Registering an App ID, use Bundle ID(must be the same in xcode project), and check In-App Purchase Box is checked.
- Select In-App Purchase, add a new in app purchase account.
- Must Know Content
  - Reference Name: Name for your In-App Purchase.
  - Product ID: use "Bundle ID", plus "Reference Name".
