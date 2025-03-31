# Repudiation

The example demonstrates a vulnerability that can lead to repudiation by malicious users attempting to access the services provided by a server.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Run the server __insecure.ts__.

3. Pretend to be a malicious user and interact with the services by sending requests from the browser.

4. Do you think your actions can be repudiated?

## For you to do

1. Briefly explain the vulnerability.
   * insecure.ts does not contain any logging functionality. This is considered a vulnerability since we cannot track a user's actions inside our application, meaning we cannot hold a user accountable for any malicious activity they perform. 
2. Briefly explain why the vulnerability is addressed in __secure.ts__.
   * secure.ts addresses this by integrating logging for all user actions, allowing us to hold users accountable for any malicious actions they may take
3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?
   * A centralized design pattern is used in secure.ts with the implementation of the logging mechanism. A centralized logstream is established, to which all aspects of the server write to, including GETs, POSTs, middleware, errors, etc.