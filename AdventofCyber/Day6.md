# Day 6
Step 1:
In this day, learnt about what YARA rules are and how they are used to determine what the malware is doing.
So to get started firstly I had to run the following commands which gave me the following output:
~~~
PS C:\Users\A
dministrator > C:\Tools\.\JingleBells.ps1
Get-WinEvent : No events were found that match the specified selection criteria.
At C:\Tools\JingleBells.ps1:124 char:18
+     $lastEvent = Get-WinEvent -LogName $logName -MaxEvents 1
+                  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (:) [Get-WinEvent], Exception
    + FullyQualifiedErrorId : NoMatchingEventsFound,Microsoft.PowerShell.Commands.GetWinEventCommand

No events found in Sysmon log.
Monitoring Sysmon events... Press Ctrl+C to exit.
Get-WinEvent : No events were found that match the specified selection criteria.
At C:\Tools\JingleBells.ps1:144 char:22
+         $newEvents = Get-WinEvent -LogName $logName | Where-Object {  ...
+                      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (:) [Get-WinEvent], Exception
    + FullyQualifiedErrorId : NoMatchingEventsFound,Microsoft.PowerShell.Commands.GetWinEventCommand

No new events found.
~~~
So what was happening here a C script was uploaded in the file Jingle Bells which were so that they checked the Sysmon Log for any new events, here events mean any changes undergone in the system like any new files added or any programs run without permission etc.
But as we can see there were no new events because the malware hadnt been executed yet.

Step 2:
For execution of the malware, I went to the tools folder and executed the file merrychristmas.exe file, which gave me a popup which included the flag for q1.
This specific message popped up because I had ran the above script in the terminal without exiting.

![image](https://github.com/user-attachments/assets/d50a7d33-a9b8-4ae2-bdda-d2aca57b373e)


Step 3:
I used a tool Floss and run the following command:
~~~
floss.exe C:\Tools\Malware\MerryChristmas.exe |Out-file C:\tools\malstrings.txt
>> Get-WinEvent : No events were found that match the specified selection criteria.       ...
>> At C:\Tools\JingleBells.ps1:124 char:18
>> +     $lastEvent = Get-WinEvent -LogName $logName -MaxEvents 1tmas.exe |Out-file C:\tools\malstrings.tx
>> +                  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
>>     + CategoryInfo          : ObjectNotFound: (:) [Get-WinEvent], Exception
>>     + FullyQualifiedErrorId : NoMatchingEventsFound,Microsoft.PowerShell.Commands.GetWinEventCommand
>> O: floss.stackstrings: extracting stackstrings from 87 functions
>> No events found in Sysmon log.███████████████████████████████| 87/87 [00:01<00:00, 72.29 functions/s]
>> Monitoring Sysmon events... Press Ctrl+C to exit.om 14 functions...
>> Get-WinEvent : No events were found that match the specified selection criteria.
>> At C:\Tools\JingleBells.ps1:144 char:220007530: 100%|████████| 14/14 [00:00<00:00, 18.25 functions/s]
>> +         $newEvents = Get-WinEvent -LogName $logName | Where-Object {  ...
>> +                      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~████████| 24/24 [00:27<00:00,  1.16s/ functions]
>>     + CategoryInfo          : ObjectNotFound: (:) [Get-WinEvent], Exception
>>     + FullyQualifiedErrorId : NoMatchingEventsFound,Microsoft.PowerShell.Commands.GetWinEventCommand
>> RE-VM 12/12/2024 16:10:16
~~~
which gave me the following output. Now what floss was doing here is that the malware can be easily made more stealthy by hardcoding the variables or endcoding them in base64.
this makes it harder for the aforesaid script to detect the malware(makes it easier for the malware to bypass YARA rules).

Now when the above script was run it piped the encoded variables into a file named malstrings.txt and that was where the new flag was stored.

![image](https://github.com/user-attachments/assets/8405a003-90db-4ac5-b132-573cd0f5d369)


Learnings:
1) Learnt about YARA rules and what they signify and how they are used to detect malwares.
2) Learnt about the Floss tool and its use.
3) Learnt what a sandbox is and how it is different from a normal device.



