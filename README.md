# Shutdown Timer

<img width="800" height="600" alt="Неоновый циферблат в сумерках" src="https://github.com/user-attachments/assets/86af6d84-ae8d-43bf-8d87-9a66bd82495e" />

A tiny, lightweight Windows app that shuts your computer down after a time you choose. Enter hours, minutes and/or seconds, click one button, and Windows will power off when the countdown ends.

No installer. No setup. Download the zip, extract it, open the .exe file, and it's ready to use.

If you like the app, you can support the author here: https://www.donationalerts.com/r/gl1tch19

## What is it for?

Shutdown Timer is useful whenever you want your PC to turn itself off later, without you being there:

- Falling asleep while watching a movie, a series or YouTube
- Leaving a large download, game update or file copy running overnight
- Waiting for a long video render, export or backup to finish
- Limiting your own screen time or your kids' computer time
- Any situation where you think "I'll turn it off in 40 minutes" and know you'll forget

Under the hood, the app simply runs the built-in Windows command shutdown /s /t <seconds> for you. It just gives you a friendly window instead of making you calculate seconds and type commands by hand.

## Quick start

1. Download the zip file from the Releases page (or from the files in this repository).
2. Extract the zip. Inside you will find 3 files: ShutdownTimer.exe, ShutdownTimer.cs and Build.bat.
3. Open ShutdownTimer.exe. This is the only file you need. The other two are only for building from source.
4. Confirm the Windows UAC prompt (administrator rights are needed to schedule a shutdown).
5. Enter the time and click Shut down.

That's it. There is nothing to install, no installer to run, and nothing is added to your system. You can keep the folder anywhere (Desktop, Downloads, a USB drive) and delete it whenever you want.

## Features

- Portable and installer-free. Just open the .exe file and use it.
- Separate fields for hours, minutes and seconds. No need to convert everything into minutes or seconds yourself.
- Fill in only what you need. Empty fields count as zero. For example, typing 40 into the minutes field alone means "shut down in 40 minutes".
- Flexible input. Each field accepts up to 4 digits, so 90 minutes or 120 minutes work just as well as 1 hour 30 minutes.
- Digits only. The fields ignore any other characters, so you can't enter invalid values by accident.
- One-click scheduling. The Shut down button (bottom right) schedules the shutdown immediately.
- Live countdown. After you start the timer, the window shows exactly how much time is left, in HH:MM:SS format.
- Smart bottom-right button. Before the timer is started, the button reads Close and closes the app. While the timer is running, the same button reads Cancel and cancels the scheduled shutdown. The app stays open, so you can immediately set a new time or close it.
- Replaces old timers safely. Any previously scheduled shutdown is cleared before the new one is set, so you never get a "shutdown already in progress" error.
- Input validation. The app warns you if you enter zero time or a value above the Windows maximum (10 years).
- Locked fields while running. Once the timer starts, the time fields become read-only so the countdown can't be changed by accident.
- Automatic administrator rights. The app asks for elevation by itself (a standard Windows UAC prompt) and restarts with administrator privileges. You don't need to right-click and choose "Run as administrator".
- Clean dark interface. A simple, modern dark window with large, easy-to-read time fields.
- Keyboard friendly. Press Enter to start the timer and Esc to trigger the bottom-right button (Close or Cancel). Clicking a field selects its contents so you can type a new value right away.
- Very low resource usage. A small native Windows Forms app with no heavy runtime and no background activity apart from a one-second timer for the countdown.
- No dependencies. It uses only components that are already built into Windows 10 and Windows 11.

## Screens and controls

| Element | Description |
| --- | --- |
| Hours / Minutes / Seconds | Three input fields for the delay before shutdown. Empty = 0. |
| Status line | Shows hints, errors, and the live countdown. |
| Shut down button | Schedules the shutdown with the entered delay. |
| Close button | Shown when no timer is running. Closes the app. |
| Cancel button | Shown while the timer is running. Cancels the scheduled shutdown and keeps the app open. |

## Requirements

- Windows 10 or Windows 11 (64-bit or 32-bit)
- .NET Framework 4.x (already included in Windows 10 and 11, nothing to install)
- Administrator rights (the app requests them automatically)

## Usage

1. Open ShutdownTimer.exe and confirm the UAC prompt.
2. Enter the delay, for example 40 in the minutes field.
3. Click Shut down.
4. Watch the countdown, or just walk away. Your PC will turn off when the time is up.
5. Changed your mind? Click Cancel to abort the shutdown. Then enter a new time, or click Close to exit.

### Examples

| Hours | Minutes | Seconds | Result |
| --- | --- | --- | --- |
| 0 | 40 | 0 | Shutdown in 40 minutes |
| 1 | 30 | 0 | Shutdown in 1 hour 30 minutes |
| 0 | 0 | 45 | Shutdown in 45 seconds |
| 2 | 0 | 0 | Shutdown in 2 hours |

## Important notes

- Unsaved work will be lost. When Windows shuts down on a timer, running applications are closed without further prompts (this is how shutdown /s /t <seconds> works). Save your work before the timer ends.
- Closing the window with the X button does not cancel the timer. The shutdown stays scheduled in Windows. Use the Cancel button to abort it.
- Cancelling manually. If you closed the app but want to abort the shutdown, open Command Prompt and run: shutdown /a
- The app does not need to stay open. It only schedules the shutdown through Windows, so you can safely close the window after starting the timer.

## Troubleshooting

### Windows SmartScreen shows "Windows protected your PC"

The app is not code-signed, so Windows may show a warning for any newly downloaded .exe. Click More info, then Run anyway. If you prefer not to trust a prebuilt file, you can build it yourself from the source code (see below).

### My antivirus blocks or deletes the file

Small unsigned programs are sometimes flagged by mistake. You can add the file to your antivirus exceptions, or build it yourself from the source code to be sure of what you are running.

### The UAC prompt appears every time

This is expected. Administrator rights are required to schedule the shutdown, and Windows always asks for confirmation.

### The app closes immediately after the UAC prompt

This happens if you click "No" in the UAC window. Start the app again and choose "Yes".

### The .exe does not open from inside the zip

Extract the zip to a normal folder first (right-click the zip, then Extract All), and then open ShutdownTimer.exe from that folder.

## How it works

- On startup, the app checks whether it has administrator rights. If not, it restarts itself with the standard runas elevation.
- When you click Shut down, it converts hours, minutes and seconds into total seconds, clears any old timer with shutdown /a, and schedules a new one with shutdown /s /t <seconds>.
- A one-second timer updates the countdown in the window.
- Cancel runs shutdown /a, stops the countdown and unlocks the fields. Close simply exits the app.

## Building from source (optional)

You only need this if you want to compile the app yourself instead of using the ready-made .exe. No Visual Studio or SDK is required, because the project is compiled with the C# compiler that ships with Windows.

1. Extract the zip to a normal folder.
2. Make sure Build.bat and ShutdownTimer.cs are in the same folder.
3. Double-click Build.bat.
4. After a few seconds, a fresh ShutdownTimer.exe appears in the same folder.

## Project structure

The zip contains 3 files:
ShutdownTimer.exe Ready-to-use app (just open it)
ShutdownTimer.cs Source code (C#, Windows Forms)
Build.bat One-click build script using the built-in Windows C# compiler

## Support the project

Shutdown Timer is free and will stay free. If it saved you some time or made your evenings a bit more comfortable, you can support the author with a donation:

https://www.donationalerts.com/r/gl1tch19

Every donation helps to keep improving the app and make new useful tools. Thank you!

## License

This project is licensed under the MIT License. See the LICENSE file for details.
