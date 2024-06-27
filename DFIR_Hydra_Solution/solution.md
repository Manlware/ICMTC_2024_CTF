# Description:
![image](https://github.com/Manlware/ICMTC_2024_CTF/assets/59315492/a308a823-1fda-49e0-ae44-aa363dcd26f0)

# Files:
## We have two files
- [var](https://github.com/Manlware/ICMTC_2024_CTF/blob/main/DFIR_Hydra_Solution/var.tar.gz)
- [etc](https://github.com/Manlware/ICMTC_2024_CTF/blob/main/DFIR_Hydra_Solution/etc.tar.gz)

# Steps of Solutions:
- **First: I downloaded the files on my kali machine and start to explore the content of var folder.**
  - I found interested file inside cron called **g33k**
    ![image](https://github.com/Manlware/ICMTC_2024_CTF/assets/59315492/9aef203a-cf63-4666-a24a-9e809ec3a13a)
  - After reading his content we found.
    ![image](https://github.com/Manlware/ICMTC_2024_CTF/assets/59315492/dde54344-a76f-4697-9a22-cc1634cca923)
      - ```
        0 23 * * 1 sudo systemctl start legit.service
        1 23 * * 1 sudo systemctl enable legit.service
        1 23 * * 1 sudo /etc/init.d/initial.sh
        ```
  - The above is a cron job doing the following:
    - **`0 23 * * 1 sudo systemctl start legit.service`**  
        At 23:00 (11:00 PM) every Monday, this command starts the **legit.service** using **systemctl**.
      
    - **`1 23 * * 1 sudo systemctl enable legit.service`**  
      At 23:01 (11:01 PM) every Monday, this command enables the **legit.service** to start at boot using **systemctl**.
      
    - **`1 23 * * 1 sudo /etc/init.d/initial.sh`**  
      At 23:01 (11:01 PM) every Monday, this command runs the script located at **/etc/init.d/initial.sh** with **sudo**.

- **Second: I Strated to search for the service file "legit.service" on etc folder.**
  - Using `find -name "legit.service"` on etc folder we found the location of it and read its content.
  - 
    

