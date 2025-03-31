# Tampering

This example demonstrates tampering through script injection.

## Steps to reproduce

1. Install all dependencies

    `npm install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. In the browser, type a potentially malicious script in the name field of the form

    ```
        <script> document.body.innerHTML = "<a href='https://google.com'> Gotcha </a>"</script>
    ```

4. Do you see the potentially malicious hyperlink being injected into the form?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
   * In insecure.ts, the input is not being sanitized on line 58. The server is implicitly trusting that a user will only enter an alphanumeric string.
   * An attacker could submit a string with a malicious payload, such as malicious code in the case of an XSS attack.
2. Briefly explain how a malicious attacker can exploit them.
   * An attacker could submit malicious code through the name field, that when ran, could execute a payload performing unauthorized actions on the recipient's machine.
3. Briefly explain why **secure.ts** does not have the same vulnerabilities?
   * secure.ts sanitizes the user's input, removing any harmful HTML code, before the form is submitted. 