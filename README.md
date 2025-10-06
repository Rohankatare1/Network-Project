[README.md](https://github.com/user-attachments/files/22729263/README.md)
# 🔐 CNT 5008 Project — Web Server Port Knocking (Rohan Katare)

**Course:** CNT 5008 — Computer Networks  
**Student:** Rohan Katare  

---

## 📘 Project Overview
This project implements a **port-knocking mechanism** that controls access to a lightweight web server.  
By default, the web server’s TCP port (8080) remains closed. Only after a specific sequence of UDP packets (“knocks”) is received will the web server open and begin serving requests.

The implementation modifies the original `weblite.c` program, resulting in a secure, access-controlled version named **`weblite_knock.c`**.  
This approach demonstrates how **UDP-based port knocking** can be used to add a layer of security by requiring a hidden authentication sequence before allowing access.

---

## 🧩 How It Works
1. **Initial State:**  
   TCP port **8080** is closed; the web server is inactive.
2. **Knocking Sequence:**  
   The server listens for UDP packets sent to ports: 1100 → 1200 → 1300

- Each knock must occur within **5 seconds** of the previous one.  
- After each successful knock, that UDP port is **closed** before the next is opened.
3. **Server Activation:**  
When the correct sequence is received in order and within the time limit,  
TCP port 8080 is opened, and the web server begins accepting HTTP connections.
4. **Extra Credit (Optional):**  
A knock to **UDP port 1400** will close port 8080 and reset the server to the initial state.

---

## 🧠 Components
| File | Description |
|------|--------------|
| `weblite_knock.c` | Modified lightweight web server that implements the UDP port-knocking logic. |
| `udp_send.c` | Simple UDP client used to send knock messages. Takes IP address, port number, and message as command-line arguments. |
| `Makefile` | (Optional) Used for easy compilation of both programs. |
| `RohanKatareProject.zip` | Contains all source files and binaries submitted for grading. |

---

## ⚙️ Compilation & Execution

### 1️⃣ Build the Programs
```bash
gcc -o weblite_knock weblite_knock.c
gcc -o udp_send udp_send.c

