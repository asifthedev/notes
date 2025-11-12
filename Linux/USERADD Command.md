# USERADD Command

```bash
sudo adduser username
```

### Notes:

- This creates:
  
  - A new user account
  
  - A home directory at `/home/username`
  
  - Default shell `/bin/bash`

- It will prompt you for:
  
  - Password
  
  - User info (you can skip with Enter)

## Give the User Administrative (sudo) Rights

```bash
sudo usermod -aG sudo username
```

### Notes:

- Adds the user to the **sudo** group (which allows running admin commands using `sudo`).

- You can confirm with:
  
  ```bash
  groups username
  ```
  
  It should show `sudo` in the list.

## Switch to Another User

```bash
su - username
```

### Notes:

- The `-` loads the user’s environment (like PATH, home, etc.)

- To go back to your original user:
  
  ```bash
  exit
  ```



## **4. List All Users**

### Command:

```bash
cut -d: -f1 /etc/passwd
```

### Notes:

- Shows every username in the system.

---

## **5. Check User Details**

### Command:

```bash
id username
```

### Output includes:

- UID (User ID)

- GID (Group ID)

- Groups the user belongs to

---

## **6. Create a User Without Prompt (Non-Interactive)**

```bash
sudo adduser --disabled-password --gecos "" username
```

### Notes:

- Useful for scripts or automated setups.

- You can set a password later with:
  
  ```bash
  sudo passwd username
  ```

---

## **7. Change User Password**

```bash
sudo passwd username
```

---

## **8. Delete a User**

### Remove the user but keep their files:

```bash
sudo deluser username
```

### Remove the user **and their home directory**:

```bash
sudo deluser --remove-home username
```

---

## **9. Add User to Other Groups**

```bash
sudo usermod -aG groupname username
```

### Example:

Add user to Docker group:

```bash
sudo usermod -aG docker username
```

---

## **10. Check Group Memberships**

```bash
groups
# or
groups username
```

---

## **11. Lock and Unlock a User Account**

### Lock:

```bash
sudo passwd -l username
```

### Unlock:

```bash
sudo passwd -u username
```

---

## **12. Disable Interactive Login (for system/service accounts)**

```bash
sudo usermod -s /usr/sbin/nologin username
```

---

## **13. SSH Setup for a New User**

1. Switch to the user:
   
   ```bash
   su - username
   ```

2. Create `.ssh` directory:
   
   ```bash
   mkdir -p ~/.ssh && chmod 700 ~/.ssh
   ```

3. Add public key:
   
   ```bash
   nano ~/.ssh/authorized_keys
   ```
   
   Paste your SSH public key.

4. Set permissions:
   
   ```bash
   chmod 600 ~/.ssh/authorized_keys
   ```

---

## **14. System File Locations**

| File           | Description                   |
| -------------- | ----------------------------- |
| `/etc/passwd`  | Basic user account info       |
| `/etc/shadow`  | Encrypted passwords           |
| `/etc/group`   | Groups info                   |
| `/etc/sudoers` | Sudo privileges configuration |

---

## **15. Safety Notes**

- **Never edit `/etc/passwd` or `/etc/shadow` manually** unless you know what you’re doing.

- Always use `adduser`, `usermod`, and `deluser` for safety.

- Avoid using `root` account directly — use `sudo` instead.

---

Would you like me to add **a summary cheat sheet** (like a compact one-page version) that you can save or print for quick reference?
