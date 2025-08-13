# BB-TOTP
A TOTP 2FA Authenticator and store for the BlackBerry Web Browser.

Leveraging a BlackBerry device in 2025 is made more difficult because of the lack of having a 2FA TOTP Authenticator. Building new applications in 2025 for the BlackBerry is almost impossible because of the takedown of BlackBerry services so this implementation works in the web browser.

Modern QR code scanning in web apps typically relies on APIs like getUserMedia to access the camera, but legacy browsers (like that on the Blackberry Passport) do not support these APIs. Without native camera support, you can't scan QR codes directly so this implementation relies upon  users manually typing in the secret code that they would otherwise get from scanning a QR code.

We use the browers localStorage to store the Authenticator codes. Storing sensitive information in localStorage is not as secure as using a dedicated authentication app but its a necessary tradeoff to be able to provide an authenticator application on a BlackBerry in 2025. The page does have an optional password lock that once set requires a password each time the page is loaded. It’s meant as a deterrentnot strong cryptography but it’s better than providing un-gated access to the page.

A global setting (timeOffset) is used to adjust the current time (in seconds) for TOTP generation. A simple input/button is provided so users can experiment with different offset values if your device’s clock isn’t exactly in sync with Google Authenticator (TOTP works entirely off the device’s clock, so if different devices have different clock errors, each device will generate a slightly different code relative to “real time.” In other words, if one device’s clock is 18 seconds ahead of the actual time and another’s is correct (or lags behind), then the codes won’t match unless each clock is synchronized.)

A “Clear All Accounts” link is available below the Add Account block. Clicking it will remove all saved accounts (i.e. clear the related localStorage entry).

Each account row includes a small “Delete” link (shown to the right of the account name) so users can remove that account without clearing all data.

A  built-in HMAC-SHA1 (byte-accurate, RFC-style) is used to calculate the code from a shared secret (ie. no web API calls are needed, everything is entirely offline).

To use this, simply download the page to your BlackBerry and launch it from the local file store using your BlackBerry built-in web browser.


