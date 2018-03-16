# Communication
The YACRS web application communicates with the electron web app using
IPC. This is a method electron uses to communicate over different processes.
Functions in `app/js/webview-preload.js` are callable by the web application.

These functions mostly send a further IPC message main.js. This is how
the live view is displayed.