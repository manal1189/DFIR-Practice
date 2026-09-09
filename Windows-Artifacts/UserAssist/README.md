# Windows UserAssist Artifact Analysis

## Overview

UserAssist is a Windows Registry artifact that can provide information about applications accessed through the Windows graphical interface.

For this practice, I searched for and opened Windows Character Map, then examined the UserAssist Registry artifact to find the trace left by this activity.

---

## Test Activity

I launched **Character Map** through the Windows Start menu.

The application executable is:

```text
charmap.exe
```
![Character Map launched](<Screenshot 2026-09-09 015359.png>)

---

## Artifact Location

UserAssist is stored inside the user's `NTUSER.DAT` Registry hive at:

```text
Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist
```

The executable entry was found under the following `Count` subkey:

```text
Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{CEBFF5CD-ACE2-4F4F-9178-9926F41749EA}\Count
```
![Searching for the encoded UserAssist entry](<Screenshot 2026-09-09 020006.png>)

---

## ROT13-Encoded Entry

UserAssist stores program names using ROT13.

Instead of appearing as:

```text
charmap.exe
```

the program appeared in Registry Editor as:

```text
puneznc.rkr
```

The complete Registry value was:

```text
{1NP14R77-02R7-4R5Q-O744-2RO1NR5198O7}\puneznc.rkr
```

The value type was `REG_BINARY`, which means the related activity information was stored as binary data.

![Raw UserAssist Registry entry](<Screenshot 2026-09-09 020829.png>)

---

## Parsing the Artifact

I used **Registry Explorer** to examine the UserAssist artifact.

The tool decoded the ROT13 value and displayed the execution and focus information in a readable format.

![UserAssist key in Registry Explorer](<Screenshot 2026-09-09 030012.png>)

## Results

| Field         | Recovered Value        |
| ------------- | ---------------------- |
| Program Name  | `{System}\charmap.exe` |
| Run Counter   | `4`                    |
| Focus Count   | `1`                    |
| Focus Time    | `20 seconds`           |
| Last Executed | `2026-09-08 22:54:04`  |

### Result Explanation

* **Program Name:** Character Map was identified inside the Windows System directory.
* **Run Counter:** The record showed a run counter of four.
* **Focus Count:** The application received one recorded focus event.
* **Focus Time:** The application remained in focus for approximately 20 seconds.
* **Last Executed:** The tool displayed the last recorded execution time as `2026-09-08 22:54:04`.

The run counter may include earlier activity from the same user profile, so it does not necessarily represent only the actions performed during this test.

The timestamp should also be interpreted using the correct timezone for the examined system.

![Parsed UserAssist result](<Screenshot 2026-09-09 032906.png>)

---


## Forensic Value

UserAssist can help investigators:

* Identify applications accessed through the Windows GUI.
* Review recorded run and focus information.
* Find the last recorded execution time.
* Associate application activity with a Windows user profile.
* Add supporting information to an investigation timeline.

---

## Limitations

UserAssist should not be used as the only source of evidence.

It does not provide the complete command line, and the presence of an application does not prove that its activity was malicious.

The findings should be correlated with other Windows artifacts, such as:

* Prefetch
* Amcache
* LNK files
* Jump Lists
* Windows Event Logs

---

## Tools Used

* Windows Character Map
* Registry Editor
* Registry Explorer

---

## Key Takeaway

Launching Character Map left a trace inside the Windows UserAssist Registry artifact.

The program name was stored using ROT13, while Registry Explorer decoded the entry and displayed the recorded run count, focus information, and last execution time.

This practice showed how UserAssist can support the reconstruction of application activity on a Windows system.
