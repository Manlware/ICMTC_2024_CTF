# Description:
![image](https://github.com/Manlware/ICMTC_2024_CTF/assets/59315492/a308a823-1fda-49e0-ae44-aa363dcd26f0)

# Files:
## We have two files
- [var](https://github.com/Manlware/ICMTC_2024_CTF/blob/main/DFIR_Hydra_Solution/var.tar.gz)
- [etc](https://github.com/Manlware/ICMTC_2024_CTF/blob/main/DFIR_Hydra_Solution/etc.tar.gz)

# Steps of Solutions:
- **First: We downloaded the files on my kali machine and start to explore the content of var folder.**
  - We found interested file inside cron called **g33k**
    ![image](https://github.com/Manlware/ICMTC_2024_CTF/assets/59315492/9aef203a-cf63-4666-a24a-9e809ec3a13a)
  - After reading his content we found.
    ![image](https://github.com/Manlware/ICMTC_2024_CTF/assets/59315492/dde54344-a76f-4697-9a22-cc1634cca923)
      - ```
        0 23 * * 1 sudo systemctl start legit.service
        1 23 * * 1 sudo systemctl enable legit.service
        1 23 * * 1 sudo /etc/init.d/initial.sh
        ```
  - **The above is a cron job doing the following:**
    - **`0 23 * * 1 sudo systemctl start legit.service`**  
        At 23:00 (11:00 PM) every Monday, this command starts the **legit.service** using **systemctl**.
      
    - **`1 23 * * 1 sudo systemctl enable legit.service`**  
      At 23:01 (11:01 PM) every Monday, this command enables the **legit.service** to start at boot using **systemctl**.
      
    - **`1 23 * * 1 sudo /etc/init.d/initial.sh`**  
      At 23:01 (11:01 PM) every Monday, this command runs the script located at **/etc/init.d/initial.sh** with **sudo**.

- **Second: We strated to search for the service file "legit.service" on etc folder.**
  - Using `find -name "legit.service"` on etc folder we found the location of it and read its content.
    ![image](https://github.com/Manlware/ICMTC_2024_CTF/assets/59315492/4359b09e-38d8-4df7-b76e-ccb2112e73bd)
  - The service downloads a file called **encrypted.sh** from github repo and saves it as **shell.sh** on **/tmp**
  - We downloaded it and start to read its content but it was encrepted.
    ![image](https://github.com/Manlware/ICMTC_2024_CTF/assets/59315492/870311a8-dbf8-4503-8385-5a1cc7b30cfd)
- **So we have an encrepted shell I asked how can it be encrepted.**
  - So we started to read the another file found on the cron job **/etc/init.d/initial.sh**.
    ![image](https://github.com/Manlware/ICMTC_2024_CTF/assets/59315492/e5ad8fef-6dba-4550-8d94-460ba49fd3bd)
  - **`openssl rsautl -decrypt -inkey id_rsa.pem -in /tmp/shell.sh | bash`**
    Decrept the file using private key **id_rsa.pem** and execute its decrepted content using bash
- **So we need to find private key "id_rsa.pem".**
  - We used `find -name "id_rsa.pem"` on etc folder.
  - And found it on **./etc/.ssh/id_rsa.pem**.
    ![image](https://github.com/Manlware/ICMTC_2024_CTF/assets/59315492/17258a27-f5cc-4e29-bef3-5a8c59010d42)

- **The last step is to decrept the file "shell.sh"and get the IP and Port number.**
  - We used the command found above on **/etc/init.d/initial.sh** to decrept it.
    ![image](https://github.com/Manlware/ICMTC_2024_CTF/assets/59315492/b11d5b3b-aa1e-4db7-b5fb-d09431848046)
  - Dangerous Note: Don't use **| bash** found on file **/etc/init.d/initial.sh** cause if they listen on Port **52385** on IP **41.35.61.53** they will get a reverse shell on your machine ☠️😂 
 
## At the end the Flag was **EGCERT{41.35.61.53:52385}**

  

    

