# Project Structure
An overview of the project directory structure is shown below

    /
    ├── main.js: Main application start code
    ├── config.js: Module to load configuration files
    ├── package.json: Details of application package
    ├── /build: Files needed to build application
    ├── /app
    |   ├── app.html: Main app web contents. Embeds a webview inside of itself to actually embed the application
    |   ├── app-nosplash.html: Same as app.html but with no splash screen
    |   ├── live.html: Live view html
    |   ├── /fonts: App fonts
    |   ├── /css: App CSS
    |   └── /js: App renderer js
    └── /config
        ├── Deployment Specific Images
        └── config.json: Deployment specific config

## Application Flow
 1. main.js is run by electron. This creates a new window of app.html.
 2. main.js then sends the required configuration data and url to this new window.
 3. That page is loaded and the user can navigate the app like they were in a web browser.
 4. The web application detects that this is the desktop app