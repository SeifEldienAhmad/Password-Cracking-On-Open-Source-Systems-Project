# 🔑 Password Cracking Project – Write-up

## 📌 Project Overview  
This project focused on password cracking techniques using **John the Ripper** and **Hashcat** against the intentionally vulnerable **Metasploitable 2** system.  
The purpose was to understand how attackers exploit weak password storage and to highlight the importance of strong authentication practices.

---

## ⚙️ Tools Used  
- **John the Ripper** – dictionary & brute force cracking  
- **Hashcat** – GPU-based password cracking  
- **Metasploitable 2** – vulnerable target system  
- **DVWA (Damn Vulnerable Web Application)** – for practical web login brute forcing  
- **Wordlists** – e.g. `rockyou.txt`

---

## 📝 Steps Performed  

### 1. Setup & Recon  
- Launched **Metasploitable 2** VM as the target system.  
- Accessed **DVWA** for web-based authentication testing.  
- Identified weak password-protected services and login pages.  

---

### 2. John the Ripper (Metasploitable 2 & DVWA)  
- Extracted password hashes from `/etc/shadow` in Metasploitable 2.  
- Ran **John the Ripper** with the `rockyou.txt` wordlist:  
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt shadow.hashes
```
- Successfully cracked several weak user passwords.  

- Against **DVWA** login, used John to simulate brute force with a wordlist, proving how default/weak credentials can be quickly compromised.

---

### 3. Hashcat (Metasploitable 2)  
- Exported hashes from the target.  
- Used **Hashcat** with GPU acceleration to speed up cracking. Example command:  
```bash
hashcat -m 500 shadow.hashes /usr/share/wordlists/rockyou.txt
```
- Verified cracked passwords matched the vulnerable accounts on Metasploitable 2.  
- Documented progress and results across different platforms (LinkedIn, Medium, Dev.to, Twitter).

---

## 🚨 Findings  
- Many accounts in Metasploitable 2 used **default credentials** or **weak dictionary words**.  
- DVWA allowed brute force without effective lockout controls.  
- Password hashes were stored using weak algorithms (e.g., unsalted MD5).  

---

## 🛡️ Mitigation & Security Best Practices  
- Use **modern hashing algorithms** (e.g., bcrypt, scrypt, Argon2) with proper salting.  
- Enforce **complex, long, and unique passwords**.  
- Apply **rate limiting and account lockout policies** in web applications.  
- Replace weak services with secure alternatives.  
- Educate users on **password hygiene** and implement **MFA (Multi-Factor Authentication)**.  

---

## 🎯 Learning Outcome  
Through this project, we gained hands-on experience in:  
- Cracking password hashes with **John the Ripper** and **Hashcat**.  
- Understanding weaknesses in legacy systems like Metasploitable 2 and DVWA.  
- Mapping offensive techniques to defensive strategies.  
