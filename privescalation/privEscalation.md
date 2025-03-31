# Privilege Escalation

The example demonstrates a privilege escalation vulnerability and how to exploit it.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, send a GET request

    ```
        http://localhost:3000/send-form
    ```

4. Try different UserIds and see which one gives you authorized access to change the role of that user.

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
   * The POST '/update-role' route allows anybody to update a role so long as they provide a valid uid containing the role of 'Admin'
2. Briefly explain how a malicious attacker can exploit them.
   * A malicious attacker will have the ability to upgrade any user's privileges as long as they have a valid uid belonging to an Admin account. 
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?
   * secure.ts gets the uid and role of the currently logged-in user from the session, as opposed to being provided by the user. If the currently logged-in user's role is 'Admin', then they have the ability to change a role. If not, then they are forbidden from updating roles.
   * This ensures that only properly authenticated users, who contain Admin rights, can update user roles, preventing malicious attackers or unauthorized individuals from doing so.