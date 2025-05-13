### 🔵 Starting Point: A User Wants to Access `www.foobar.com`

1. The user opens a browser and types: `www.foobar.com`.
2. The browser contacts the **DNS system** to resolve this domain name into an IP address.

### 🔵 DNS Role

- **Domain Name**: `foobar.com` is a human-readable name used to access the server.
- The **"www"** in `www.foobar.com` is a **DNS "A" record** (Address record) that points to the IP **8.8.8.8**, which is the IP address of the server hosting the website.

### 🔵 Inside the Server (IP: 8.8.8.8)

The server contains all the components needed to run the website:

- **Web Server (Nginx)**  
  Nginx receives HTTP requests from the user and acts as the first point of contact. It routes requests to the application server.

- **Application Server (PHP-FPM)**  
  Processes the server-side logic written in PHP. For example, when a user logs in or fills a form, the application server handles that logic.

- **Application Files (Codebase)**  
  This is your website's source code (PHP, HTML, CSS, JavaScript). It contains the logic and content served to the users.

- **Database (MySQL)**  
  Stores all the structured data for your application — user accounts, posts, comments, etc. The application server communicates with the database to retrieve or store data.

### 🔵 Communication with the User

- The server uses the **HTTP or HTTPS protocol** to send web content (HTML, CSS, etc.) back to the user's browser.

---

## ✅ Key Terms Recap

| Component               | Role                                                                 |
|------------------------|----------------------------------------------------------------------|
| **Server**             | A physical or virtual machine that runs software to serve content or data |
| **Domain name**        | Human-friendly address pointing to the server’s IP                   |
| **"www" DNS Record**   | A DNS **A record** mapping `www.foobar.com` to `8.8.8.8`             |
| **Web Server**         | Handles HTTP requests and serves static files or forwards dynamic requests |
| **Application Server** | Processes business logic and connects to the database                |
| **Database**           | Stores and retrieves structured data                                 |
| **HTTP/HTTPS**         | Protocol used to transfer data between client and server            |

---

## ❗ Issues With This Infrastructure

1. **SPOF (Single Point of Failure)**  
   If the single server crashes, the whole website goes offline.

2. **Downtime for Maintenance**  
   Updating the application, restarting the web server, or making configuration changes can temporarily make the website unavailable.

3. **No Scalability**  
   As traffic increases, this single server can become overwhelmed. There's no way to distribute the load to other servers, leading to slowdowns or crashes.
