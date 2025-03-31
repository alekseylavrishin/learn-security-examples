# Denial-of-Service (DoS)

This example demonstrates DoS vulnerabilities and how they can be exploited.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Ignore if you have already done this once. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?id[$ne]=
    ```

4. Do you see the server crashing?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts** that can lead to a DoS attack.
   * insecure.ts does not contain any functionality to limit the amount of requests a server can handle at any given time.
   * Additionally, insecure.ts does not implement a try/catch block when querying the database in the GET '/userinfo' route. 
     * If an invalid uid is passed, the entire server will crash
2. Briefly explain how a malicious attacker can exploit them.
   * Given there is no rate limiting functionality, a malicious attacker can overload the server with requests until it crashes
   * Or the attacker can pass an invalid uid to crash the server when it goes to query the noSQL database.
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the DoS vulnerability?
   * secure.ts implements a rate limiter to restrict the amount of requests a given IP address can send at a time, reducing the chance of the server becoming overloaded by multiple concurrent requests.
   * Additionally, secure.ts implements a try/catch block when querying the DB in the GET '/userinfo' route, eliminating a potential crash when an invalid uid is provided.