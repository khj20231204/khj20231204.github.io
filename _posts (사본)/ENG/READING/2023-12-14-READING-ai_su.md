---
layout: single
title: su와 sudo차이
categories: READING
tag: 
---

The option -i with ‘sudo -i’ is used to launch a new shell with the environment variables set to those of the target user. It is commonly used to gain a root shell or switch to another user’s shell session with elevated privileges.   

The main difference between ‘su’ and ‘sudo -i’ lies in the way they handle user authentication and execute subsequent commands.   
    1. ‘su’ (substitute user): It allows you to switch to another user account, typically the root account, by entering the target user’s password. Once you have switched to that user, you have full access to their privileges and environment variables. However, it requires knowing the target user’s password.   
    2. ‘sudo -i’ (superuser do with interactive shell): It enables you to execute a command with root privileges by using your own password. The ‘-i’ option launches a new shell with the environment variables of the target user (usually root). This means that you can execute subsequent commands as the target user without needing to know their password. It provides a more controlled and auditable way to perform administrative tasks.
In summary, ‘su’ allows you to directly become another user with their privileges, while ‘sudo -i’ grants temporary root access without needing to know the target user’s password.   