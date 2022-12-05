---
title: "Generating CPU Load with PowerShell"
date: 2021-10-07T15:46:43+02:00
draft: false
toc: true
images:
tags: [blog,cpu,testing]
---

# Placing CPU under stress with PowerShell

So I have changed a few things in one of my lab servers and needed to make sure I would not "burn" the CPU down while I am sleeping if some process gets stuck at 100%...
You never know what the gremlins on your apps are going to do while you're at sleep, so I thought "Better be safe than sorry" and although a ThreadRipper 2 is... somehow hard to overload, I decided to give it a go and load it up.

## Why PowerShell?

Well, I had to go with PowerShell as my hosts are Core versions of Windows Server and hence, no graphical display support for most of the test / load CPU apps.
Strangely enough this did the trick quite well. Although initially it was only charging the CPU at 50%... at a certain moment it just went ballistic and loaded the whole 48 threads to 100%.

## The script...

In the search on the interwebs I found a script that actually does the whole trick and kudos to the guy that shared it [here](https://www.robvit.com/windows_server/generate-cpu-load-with-powershell/ 'Generate CPU Load with Powershell') and decided to copy it here in case... you know... his blog goes away for some reason.

### The code
```PowerShell
$NumberOfLogicalProcessors = Get-WmiObject win32_processor | Select-Object -ExpandProperty NumberOfLogicalProcessors

ForEach ($core in 1..$NumberOfLogicalProcessors){ 

start-job -ScriptBlock{

    $result = 1;
    foreach ($loopnumber in 1..2147483647){
        $result=1;
        
        foreach ($loopnumber1 in 1..2147483647){
        $result=1;
            
            foreach($number in 1..2147483647){
                $result = $result * $number
            }
        }

            $result
        }
    }
}

Read-Host "Press any key to exit..."
Stop-Job * 
```

And that's all you need :)

Let it rip for a few minutes and you'll see how your CPU runs!