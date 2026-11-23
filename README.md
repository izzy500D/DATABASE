# Databases: Notes for Cybersecurity & Cloud Beginners

> Part of my Network+ → Security+ → AWS learning journey.
> Source: Professor Messer's Network+ course, plus my own practice.

## 1. What is a database?

A **database** is an organized collection of data that software can store, search, and update quickly.

**Relational database structure**

| Term | Meaning | Example |
|---|---|---|
| Table | One category of data | Customer, Product, Invoice |
| Row | One record | One customer |
| Column | One detail about each record | Firstname, Email |
| Key | An ID that identifies a row and links tables | `Customer_id` |

## 2. SQL (Structured Query Language)

SQL is the standard language for talking to database servers.

```sql
SELECT * FROM Customers WHERE Last_Name='Messer';
```

Meaning: get **all columns** (`*`) from the Customers table where the last name is Messer.

| Command | Purpose |
|---|---|
| `SELECT` | Read data |
| `INSERT` | Add data |
| `UPDATE` | Change data |
| `DELETE` | Remove data |

## 3. Default ports

| DBMS | Protocol / Port |
|---|---|
| **Microsoft SQL Server** | **TCP 1433** |
| MS SQL Browser service | UDP 1434 |
| **MySQL / MariaDB** | **TCP 3306** |
| **PostgreSQL** | **TCP 5432** |
| **Oracle (listener)** | **TCP 1521** |
| MongoDB | TCP 27017 |
| Redis | TCP 6379 |
| Cassandra | TCP 9042 |
| IBM Db2 | TCP 50000 |
| Elasticsearch | TCP 9200 |
| Neo4j (Bolt) | TCP 7687 |
| CouchDB | TCP 5984 |
| Memcached | TCP/UDP 11211 |

Bold = most likely on the Network+ exam. These are *defaults*; admins can change them.

**Memory trick:** MS-SQL **1433**, MySQL **3306**, Postgres **5432**, Oracle **1521**.

## 4. Why databases matter for security

Databases hold passwords, customer records, and payment data, so they are a top target.

**SQL injection:** an attacker enters SQL code into an input field (like a login form) and the app runs it, which can bypass logins or leak/delete data.

**Defenses**
- Validate input
- Use parameterized queries (input is treated as data, never as code)
- Least-privilege database accounts
- Encrypt data at rest and in transit
- Keep databases off the public internet
- Regular backups
- Firewall rules that allow the database port only from the app server

Attackers scan for open database ports (for example with Nmap). Exposed MongoDB and Redis instances have caused many real data leaks.

## 5. Cloud (AWS) connection

- **RDS**: managed relational databases (MySQL, PostgreSQL, Oracle, SQL Server)
- **DynamoDB**: managed non-relational database
- Place databases in a **private subnet**
- Use a **security group** that only allows the app server on the database port
- Access control and network exposure are still the customer's responsibility (shared responsibility model)

## 6. Self-quiz scorecard

| # | Question | Result |
|---|---|---|
| 1 | Default port for Microsoft SQL Server | ✅ TCP 1433 |
| 2 | Default port for MySQL | ✅ TCP 3306 |
| 3 | Which database uses 5432 | ✅ PostgreSQL |
| 4 | Oracle listener port | ✅ TCP 1521 |
| 5 | Which database uses 27017 | ✅ MongoDB |
| 6 | Redis port | ✅ TCP 6379 |
| 7 | Meaning of `*` in `SELECT *` | 📖 Reviewed: all columns |
| 8 | Attack that injects SQL via a form | 📖 Reviewed: SQL injection |
| 9 | Public or private subnet for a database | 📖 Reviewed: private |
| 10 | UDP port for MS SQL Browser | 📖 Reviewed: UDP 1434 |

**Score from memory: 6/6 on the questions I attempted.**
**To retake:** questions 7 to 10 (reviewed, not yet tested from memory).

## 7. Next steps

- [ ] Retake questions 7 to 10 from memory
- [ ] Set up DVWA and practice SQL injection legally
- [ ] Launch a free-tier RDS instance in a private subnet and document the security group rules
- [ ] Scan my own lab VM with Nmap and identify open database ports
