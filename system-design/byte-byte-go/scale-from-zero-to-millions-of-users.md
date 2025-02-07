# Scale from Zero to Millions of Users

Reference : https://bytebytego.com/courses/system-design-interview/scale-from-zero-to-millions-of-users

## 1. Single Server Setup

1. User makes a request to DNS(Domain Name System) to resolve the domain name to an IP address.
2. DNS returns the IP(Internet Protocol) address to the user's browser. (DNS is usually a paid 3rd party service and not hosted on our server)
3. Using the IP address, the browser makes a HTTP(Hypertext Transfer Protocol) request to our web server.
4. The web server processes the request and returns the response to the browser.
5. The browser renders the response and displays the website.

## 2. Single Server Setup with Caching

1. User makes a request to DNS(Domain Name System) to resolve the domain name to an IP address.
2. DNS returns the IP(Internet Protocol) address to the user's browser. (DNS is usually a paid 3rd party service and not hosted on our server)
3. The browser makes a request to the web server using the IP address.
4. The web server processes the request and returns the response to the browser. It usually contains HTML pages(HTML, CSS, JavaScript) or JSON data.
5. The browser renders the response and displays the website. (How browser renders the response? For now take a look at https://blog.logrocket.com/how-browser-rendering-works-behind-scenes/)

## 3. Database

Usually we need another server to host the database.
It sounds too much common nowadays to separate the database and the web server, but the benefit of it is that we can scale the database independently from the web server.

### Different types of databases

- Relational Database(SQL)

- NoSQL Database(Non-relational)

Usually Relational Database is the go-to for most of the developers, but in the cases below Non-relational DB can be a better choice.

- When application requires super high latency.
- Data is not structured and don't have relationships.
- Need to store massive amount of data.
