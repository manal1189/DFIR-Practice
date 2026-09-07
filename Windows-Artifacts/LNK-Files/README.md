# Windows LNK File Analysis

## Objective

To examine a Windows shortcut file and identify forensic information about the original file, including its path and timestamps.

## Scenario

A text file named `Forensic_Test.txt` was created and opened on a Windows system. The generated LNK file was then examined to recover information about the original file.

![Forensic test text file](43b727a1-0f24-45f3-879f-b65a33c7de10.png)

## Evidence

- Artifact: `Forensic_Test.lnk`
- Artifact type: Windows Shortcut File
- Location: `%APPDATA%\Microsoft\Windows\Recent`

## Tool Used

**LECmd** by Eric Zimmerman was used to parse and examine the LNK file.

![Opening the Windows Recent folder](7f9c834e-661a-4faf-a420-d44a2f9629ee.png)

![LNK file in the Recent folder](79eb4993-f911-4fac-b5b5-1ed56829a607.png)

![LNK file properties](180fb517-4495-42b9-b980-e25a24667f81.png)

## Command Used

```cmd
LECmd.exe -f "%APPDATA%\Microsoft\Windows\Recent\Forensic_Test.lnk" --nid --neb
```

## Analysis Process

1. Located the LNK file in the Windows Recent folder.
2. Parsed the artifact using LECmd.
3. Reviewed the source and target timestamps.
4. Compared the shortcut metadata with the original file information.


## Findings

| Item | Created | Modified | Accessed |
|---|---|---|---|
| LNK Source | 2026-09-01 22:43:00 | 2026-09-01 22:47:28 | 2026-09-01 23:21:53 |
| Target File | 2026-09-01 22:43:00 | 2026-09-01 22:43:00 | 2026-09-01 22:43:34 |

![LECmd output showing source and target timestamps](29d40b33-7885-4b21-96dc-9b222c949060.png)

