---
title: TryHackMe Write Up - Splunk Basics
date: 2025-05-30
tags:
  - blog
  - writeup
  - tryhackme
---

https://tryhackme.com/room/splunk101

For this write up i will skip directly to task 5 since for the tasks before you just need to read the provided text.

Download the attached log file "VPN_logs" and upload this file into the Splunk instance with the right source type.
In case you are using the AttackBox, the file is available in the `/root/Rooms/SplunkBasic/` directory.

1. Upload the data attached to this task and create an index "VPN_Logs". How many events are present in the log file?

It shows in the top left corner of the dashboard
![[Splunk1.png]]
Answer: 2862

2. How many log events by the user **Maleena** are captured?

The navigation bar to the left offers the fields we can use to filter the data. We can find the field name **"UserName"**. When you click on it a window opens with the top values for this field.
![[Splunk2.png]]

Answer: 60

3. What is the name associated with IP 107.14.182.38?

If you click on the field names like in the task before, there is a option so select the field.
![[Splunk3.png]]

If you check yes then you will add this field to the mid section. Since we want to know the user name of a specific IP, I selected the fields **"Source_ip"** & **"UserName"**.

You can change the view type for the mid section to "table" for a cleaner look.
![[Splunk4.png]]

Now you can try to check each entry one by one or you use the search bar and filter your results with the Splunk Search Processing Language.

Use **"Source_ip"** & **"UserName"** and search for the requested values.
![[Splunk5.png]]

Answer: Smith

4. What is the number of events that originated from all countries except France

Utilize the search bar again. But this time we will work with the Keyword *NOT*.

![[Splunk6.png]]

Answer: 2814

5. How many VPN Events were observed by the IP 107.3.206.58?

Same old story. Just do like the other ones.
![[Splunk7.png]]

Answer: 14

Congrats! You now know the basics of Splunk. 

---
