# 🔄 SavepointSync - MySQL Rollback Service with Express

This Node.js project automatically rolls back a MySQL database to the latest savepoint every second by calling an external API. It's designed to help maintain data integrity and consistency in distributed or high-frequency transactional systems.

---

## 🚀 Features

- Connects to a MySQL database using `mysql2/promise`
- Calls a REST API to fetch the latest savepoint hash
- Periodically (every 1 second) rolls back the database using a stored procedure
- Error-handled and logs status in real-time
- Lightweight and suitable for microservice architectures

---

## 🛠️ Technologies Used

- Node.js
- Express.js
- MySQL
- Axios

---

## 🧠 Project Structure

```
rollback-service/
├── index.js         # Main service logic
├── package.json     # Dependencies
└── README.md        # Documentation
```

---

## ⚙️ Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/rollback-service.git
cd rollback-service
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Database Connection

Edit the `dbConfig` in `index.js` to match your MySQL credentials:

```js
const dbConfig = {
  host: 'localhost',
  user: 'root',
  password: '',
  database: 'project1'
};
```

### 4. Configure API Endpoint

Ensure the API (`http://localhost:3001/savepoint`) returns the latest savepoint in this format:

```json
{
  "hash_code": "abc123"
}
```

### 5. Create Stored Procedure in MySQL

Make sure you have a stored procedure in MySQL like this:

```sql
DELIMITER //
CREATE PROCEDURE rollback_to_savepoint(IN savepoint_hash VARCHAR(255))
BEGIN
  -- Your rollback logic here
END //
DELIMITER ;
```

### 6. Run the Service

```bash
node index.js
```

---

## 🔄 How it Works

Every second:

1. The service fetches the latest savepoint hash from the API.
2. If a savepoint is found, it calls the `rollback_to_savepoint(savepoint_hash)` stored procedure.
3. Logs the rollback activity to the console.

---

## 🧪 Example Log Output

```bash
Server is running on http://localhost:3000
Rolling back to savepoint: abc123
Rolling back to savepoint: abc123
No savepoint found. Skipping rollback.
```

---

## 📬 API Endpoint Example

The service expects the API at `/savepoint` to respond with:

```json
{
  "hash_code": "abc123"
}
```

---

## 🛡️ Error Handling

- Catches database or API errors
- Gracefully logs and continues operation

---

## 📄 License

MIT License

---

## 👨‍💻 Author

Hari PT  
