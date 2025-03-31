# Tampering

This example demonstrates information disclosure by injecting malicious query objects to a NoSQL database.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?username[$ne]=
    ```

4. Do you see user information being displayed despite the malicious request not having a valid username in the request?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
   * In insecure.ts, the username is being blindly passed into the database without being sanitized or checked for an invalid format/invalid characters.
2. Briefly explain how a malicious attacker can exploit them.
   * A malicious attacker could exploit this using noSQL injection by directly querying the database to return the details of any saved user.
   * The attacker could then use the compromised user's details to gain access to the application via their account.
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the information disclosure vulnerability?
   * secure.ts sanitizes the user-provided input by removing any characters that are not alphanumeric, removing the ability for an attacker to inject noSQL queries.