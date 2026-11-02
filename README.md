# Advanced Internet Programming – Login Project
**Tech stack:** Java Servlets + JSP, MySQL (JDBC), Maven, VS Code

## What it does
- Login page checks username and password against a MySQL table.
- Correct credentials: a **"You are logged in"** popup appears and the **Home page** opens.
- Wrong credentials: an error message is shown on the login page.
- Home page is protected (needs a session). Logout button ends the session.

## Requirements
1. JDK 11 or newer
2. Apache Maven (check with `mvn -v`)
3. MySQL Server
4. VS Code with the **Extension Pack for Java** (suggested automatically on opening the folder)

## Setup steps
### 1. Create the database
Run `database/schema.sql` in MySQL Workbench, or in a terminal:
```
mysql -u root -p < database/schema.sql
```

### 2. Set your MySQL username/password
Edit `src/main/resources/db.properties`:
```
db.user=root
db.password=YOUR_MYSQL_PASSWORD
```

### 3. Run the project
Open the folder in VS Code, open the terminal (Ctrl + `) and run:
```
mvn jetty:run
```
(No Tomcat installation needed. The first run downloads dependencies.)

Open in browser: **http://localhost:8080/**

### 4. Test login
| Username | Password   |
|----------|------------|
| shubham  | shubham123 |
| admin    | admin123   |

Press `Ctrl + C` in the terminal to stop the server.

## Project structure
```
AIP_Login_Project
├── pom.xml
├── database/schema.sql              (table + sample users)
└── src/main
    ├── java/com/aip
    │   ├── servlet/LoginServlet.java    (shows form, checks login)
    │   ├── servlet/HomeServlet.java     (protected home page)
    │   ├── servlet/LogoutServlet.java
    │   ├── dao/UserDAO.java             (database query)
    │   └── util/DBConnection.java, PasswordUtil.java
    ├── resources/db.properties          (DB settings)
    └── webapp
        ├── css/style.css
        ├── index.jsp
        └── WEB-INF
            ├── web.xml
            └── views/login.jsp, home.jsp
```

## Add a new user manually
```sql
INSERT INTO users (username, password_hash, full_name)
VALUES ('newuser', SHA2('newpassword', 256), 'New User');
```

## Common problems
- **"Could not connect to the database"** – MySQL is not running, or the password in `db.properties` is wrong.
- **Port 8080 already in use** – change `<port>8080</port>` in `pom.xml`.
- **Access denied for user** – check the `db.user` / `db.password` values.
