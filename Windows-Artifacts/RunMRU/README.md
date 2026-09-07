# Windows RunMRU Analysis

## Objective

To examine commands recorded in the Windows RunMRU Registry key and identify their relative order using the MRUList value.

## Scenario

Three commands were entered through the Windows Run dialog in the following order:

1. `notepad`
2. `calc`
3. `mspaint`

The RunMRU Registry key was then examined using Registry Editor to identify the recorded entries and their relative order.

## Artifact Location

The RunMRU key was examined at the following Registry path:

```text
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU
```

## Tool Used

**Windows Registry Editor (regedit)** was used to inspect the RunMRU key, its stored command entries, and the MRUList value.

## Findings

| Registry Value | Stored Data | Order Among the Three Commands |
|---|---|---|
| k | mspaint\1 | Most recent |
| j | calc\1 | Second most recent |
| i | notepad\1 | Oldest |

The MRUList value was `kjihgfedcba`. Its first three characters, `kji`, corresponded to `mspaint`, `calc`, and `notepad`, from most recent to oldest.


## Interpretation

The recorded entries show commands submitted through the Windows Run dialog. MRUList indicates their relative order, but does not provide an execution timestamp for each command.

These entries alone do not prove successful execution. Additional evidence, such as Prefetch and relevant Event Logs, should be examined to support that conclusion.
