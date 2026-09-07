# Windows Prefetch Analysis

## Objective

To analyze Windows Prefetch files and examine recorded program execution details, including run counts and execution timestamps.

## Example

The PECmd output shown below was examined to identify the executable name, recorded run count, and last run timestamp associated with a Tor Browser installer.

## Artifact Location

Windows Prefetch files are typically stored in:

```text
C:\Windows\Prefetch
```

## Tool Used

**PECmd** by Eric Zimmerman was used to parse the Prefetch file and display its recorded execution details.


## Example Command

```powershell
.\PECmd.exe -d "C:\DFIR\Prefetch" --csv "C:\DFIR\Output" --csvf "Prefetch_Results.csv"
```

The paths above are examples and should be adjusted to match the evidence and output folders.

## Findings

| Field | Recorded Value |
|---|---|
| Executable Name | TORBROWSER-INSTALL-WIN64-10.0 |
| Run Count | 1 |
| Last Run | 2021-04-29 18:22:32 |

The timestamp is reproduced as displayed in the PECmd output.

## Interpretation

The Prefetch output records one execution of the Tor Browser installer. This does not, by itself, prove that installation completed or that the browser was subsequently opened.
