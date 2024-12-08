## Who are you?
### HTTP requests
1. Initiating the Request
When you enter a URL (e.g., https://example.com) in your browser, your browser sends an HTTPS request to the server that hosts the website.
2. Establishing a Secure Connection
HTTPS uses TLS (Transport Layer Security) to encrypt the communication. Here's how it ensures security:

a. Handshake:
The browser contacts the server and requests a secure connection.
The server sends a digital certificate (proof of its identity).
The browser verifies the certificate using a Certificate Authority (CA). If the certificate is valid, the browser trusts the server.

b. Key Exchange:
The browser and server generate session keys (unique for this session) to encrypt the data exchanged.

3. Sending the Request
Once the secure connection is established:
The browser sends the actual HTTP request to the server, such as:
```
Copy code
GET /index.html HTTP/1.1
Host: example.com
```
This request is encrypted, so anyone intercepting it cannot read the contents.

4. Server Processes the Request
The server decrypts the request, processes it, and sends a response (e.g., the website content) back to the browser.
The response is also encrypted before being sent.

6. Receiving the Response
The browser decrypts the server’s response using the session keys.
It displays the content (e.g., a webpage) to you.

GET method - used to request data from a specified resource. 
POST method - used to send data to a server to update a resource.

Suppose we have this request:
```
GET / HTTP/1.1
Host: mercury.picoctf.net:38322
Cache-Control: max-age=0
Accept-Language: en-US,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.6778.86 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- RFCs(Request For Comments) governs the structure and behavior of the request.
- `GET / HTTP/1.1` -> follows _HTTP Request/response Protocol_ (if it was a response the former won't be there)
- `Host:`, `User-Agent:` and all are headers, which are key-value pairs which provide data about requests and responses.
- There are different RFCs specifying the format for each header. 

## SOAP
The given XML snippet is related to XXE (XML External Entity) injection, and here's an explanation of each part:

<!DOCTYPE foo [ ... ]>
This line defines a Document Type Definition (DTD) inside the XML document. DTD is used to define the structure and rules of an XML document. The foo part here is just a placeholder name for the document type.

<!DOCTYPE foo: Declares the document type as foo (it can be anything, this is just a name).
[ ... ]: Everything inside the square brackets is the internal DTD for this XML document.
<!ENTITY xxe SYSTEM "file:///etc/passwd">
This line defines an entity called xxe.

<!ENTITY: Begins the entity definition.
xxe: The name of the entity. This is how you will reference the entity later in the XML document (in this case, &xxe;).
SYSTEM: This specifies that the entity is an external entity, which means it can point to a file or resource outside the XML document.
"file:///etc/passwd": The value of the xxe entity. It's pointing to the local system file /etc/passwd, which contains user information on Unix-based systems.
When this entity is referenced later in the XML, the XML parser will attempt to access the file:///etc/passwd file from the server. If the server allows external entity processing (XXE), it will try to read the contents of the file and insert it into the document.

]>
This ends the DTD and closes the DOCTYPE declaration.
