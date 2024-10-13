# The Big Three

## Languages of the Web

- Server-side:
  - Many more...
  - Ruby.
  - PHP.
  - .NET.
  - Server-side JavaScript (e.g. Node).
  - Python.
  - Java.
  - Perl.
  - Go.
- Communication:
  - JSON.
  - Raw.
  - XML.
- Client-side:
  - JavaScript.
  - CSS: Stylesheets.
  - WebAssembly (Wasm).

## On-Going Communications

- AJAX Polling:
  - Short: Make requests to the server on a timer.
  - Long: Server waits for something to happen.
- Simple AJAX/XHR (XMLHttpRequest): Open a connection to the server, send a message, get a response closing the connection.
- WebRTC:
  - Allows for real-time and peer-to-peer communication.
  - Typically used for high bandwidth applications where reliability isn't key, e.g. Video/audio streaming.
- WebSockets: Bidirectional communication over a TCP socket to the server. Now the best option.

## The Biggest Web Application Security Threats

- Cross-site Scripting: Injecting client-side code to manipulate a page.
- SQL Injection: Injecting data into a database to manipulate a DB query.
- HTML and Parameter Manipulation:
  - Manipulating what the client sends to the server.
  - Sending the unexpected.

## Cross-Site Scripting

- The normal process:
  - This is controlled by the application.
  - This HTML is then rendered and displayed by the browser.
  - Normally it is the server and applications job to generate HTML.
- How cross-site scripting breaks this:
  - Users are able to inject new HTML code (thus scripts) into pages in a way that can be executed by other users.
- Two major types:
  - Stored: Where a user input is written or stored and later displayed back as the result of a query.
  - Reflected: Where a user input to a page can be populated with XSS and gets output as a result when that page displays.
- Examples:
  - Server Form.
  - Example 1:
    - Server:
    ![Example 1](https://remnote-user-data.s3.amazonaws.com/8pLrO19Y63pEdlh5eY38bCSmdqP4eCbFYkqTh8IvyVAcuL_ifsQYA6F9MHB6kiNKXhHsoS_IkUAiwyJptI5WHq_zTcsjrqifm1OBRc5TOirLkvuxn2BvkvNlqeAkS0ho.png)
    - Client: My username is `<strong>Oli< /strong>`
  - Example 2:
    - Client: My username is `<script>alert(1); < /script>`
    - Server:
    ![Example 2](https://remnote-user-data.s3.amazonaws.com/fMe0fydjo0UsiwO1PQkrtfTzsbGAduElQ6EUu-NReKOXqVOiWdYoy5yMlBbfm4lfN7vx85F7GcVgOdEcLtW_diUw5zmSuPU921XxMdbqWfMzXJPOXO1efLaMEqh5jKfq.png)
    - Now we have found a vulnerability.
    ![Vulnerability](https://remnote-user-data.s3.amazonaws.com/h8M56DRuCog467S8wOkhiyuHAka18uxfXPNnU3j8f3Qahpqu92VKrRvY7Glvuau81H5t30yk-cRO_glNsVkfBfv3b22EscAeZlYfYfa8IBa4YfBs-F5xo6ZaXsKoPr7J.png)
- Can be found using the XSS locator (polyglot).

## Once a vulnerability has been found

- You can include external javascript:
  - Botnet control.
  - Bitcoin mining.
  - Malware or compromise.
- You can run any javascript:
  - Control or manipulate the page in any way.
  - Control or manipulate the user's browser.
  - Get the current content of the authentication cookie.
  - Make requests as if we were the user's browser:
    - As if logged in.
  - Make outgoing requests.

## SQL Injection

- Manipulating the query sent between the server and the database (using SQL).
- Insert something into the query to change it.
- Example:
  - Input: `Bob"; DROP TABLE users; ‒`
  - Query: `SELECT * FROM users WHERE username="Bob"; DROP TABLE users; ‒"`
- Example 2:
  - Input:
    - Username: Oli
    - Password: `something' OR '1='1`
  - Query: `SELECT * FROM users WHERE username='Oli' AND password='something' OR '1'='1'`
- Example 3:
  - Input:
    - Password: something
    - Username: `Oli' ‒`
  - Query: `SELECT * FROM users WHERE username='Oli' ‒ AND password='something'`

## HTML and Parameter Manipulation

- Manipulating the inputs that the client sends to the server.
- Using:
  - The URL itself and its parameters.
  - Forms and their parameters.
  - JavaScript server requests & API calls.
  - Communication.
- How to do parameter manipulation:
  - Using the browser:
    - Inspect and modify using the developer tools.
  - Using client-side scripting:
    - Execute code in the console.
  - Downloading and modifying:
    - Download the source code, make local changes.
  - Using extensions:
    - Web developer toolbar.
  - Using scripts.
  - Using tools.
