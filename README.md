# Windows-10-PowerShell-MIDI

Folks on the Mac use MIDI controllers and the built-in scripting language to control things like app switching, or to send commands to specific apps. I first heard about this when watching a Sonic State podcast and learning that Nick uses (or used at the time) a little Korg Nano control to switch between people on Skype and/or change which input was active on the podcasting program. 

I've been totally jealous of that for some time. With the release of Windows 10 and our new, modern, multi-client MIDI API, I thought it was time to build out something like this for Windows users. We don't have MIDI routing in Windows yet, but we do have PowerShell, which lets you do a fair bit of automation and other system-level hacking.

![Input Events](/doc/powershell_midi.png)

## What is PowerShell?

PowerShell is the advanced command prompt/shell built into Windows. It first found favor with network/system administrators, but has since expanded to include client and IoT developers, as well as web folks, among the users. It does require some programming savvy, so it's not something you can use to drag and drop components to build out a script.

PowerShell can be extended through cmdlets (command-lets) written typically in C# or Visual Basic. Folks also make script libraries available for others to use both for free and for sale.

PowerShell version 5 comes with Windows 10.

Some PowerShell sites:
[PowerShell Scripting Center](https://technet.microsoft.com/en-us/scriptcenter/dd742419.aspx)
[10 Cool things you can do with Windows PowerShell](http://www.techrepublic.com/blog/10-things/10-cool-things-you-can-do-with-windows-powershell/)
[Scripting with Windows PowerShell](https://technet.microsoft.com/en-us/library/bb978526.aspx)
[Upcoming PowerShell Book on Amazon](http://www.amazon.com/Windows-PowerShell-Step-3rd/dp/0735675112/ref=sr_1_1?s=books&ie=UTF8&qid=1439375829&sr=1-1&keywords=windows+powershell)

## What is this?

This library enables you to use Windows 10 MIDI APIs from PowerShell. If you can automate it from PowerShell, you'll now be able to have it either send information to a MIDI device (sounds, lighting, etc.), or be triggered from a MIDI controller (like programmable touch pads and other controllers).

## What does it include?

The code here includes MIDI send, and basic MIDI receive (note on/off, plus continuous controller messages, and program change). The samples were written using a Novation LaunchPad, but are generic enough (with the exception of the text banner scrolling) to work on anything.

## How do I use it?

To use the MIDI API from PowerShell, copy the compiled C# DLL (PeteBrown.PowerShell.Midi.dll) from the /bin/debug folder to the folder where your script resides (or some other convenient location) and update the import path in the script to point to it. Then follow the examples in the scripts for how to send and receive events. The rest is just PowerShell.

Requires Windows 10 and .NET (installed with Windows 10), plus a little imagination.

You'll want to get the ID of the MIDI device you plan to use. There's a script made just for that.

![List MIDI devices](/doc/powershell_list_midi_devices.png)

You'll then use that ID when getting an input or output device. See the individual scripts for specific examples.

## What's it not for?

This isn't meant to be a high-performance MIDI scripting library. PowerShell, by its nature, is command-line focused and is not like sending MIDI messages straight from compiled C code. For example, this would likely not be a good choice to use to read information off the network, and translate OSC messages to MIDI. Similarly, this would probably make a horrible MIDI clock source. :)

If there are common requests that you believe should be packaged up into higher performance code and made its own PowerShell cmdlet, however, I'm happy to entertain that. See Requests below.

## Requests?

If you have ideas for scripts you want to see as examples, please let me know. Also, if you have some functionality you'd like to see exposed, or something made easier, I'm happy to work on this to make it as useful and fun as possible.

## System Requirements

This was built using Visual Studio 2015 Community, RTM. It also uses this VS 2015 add-in for editing PowerShell scripts. Required only if you want to load the psproj in Visual Studio and mess around with the source
https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597
