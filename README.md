# Shutdown Timer

<img width="800" height="600" alt="Неоновый циферблат в сумерках" src="https://github.com/user-attachments/assets/86af6d84-ae8d-43bf-8d87-9a66bd82495e" />

A tiny, lightweight Windows app that shuts down, restarts or puts your computer to sleep after a time you choose. Enter hours, minutes and/or seconds, click one button, and Windows will do the rest when the countdown ends.

No installer. No setup. Download the zip, extract it, open the .exe file, and it's ready to use.

If you like the app, you can support the author here: https://www.donationalerts.com/r/gl1tch19

## What is it for?

Shutdown Timer is useful whenever you want your PC to turn itself off, restart or go to sleep later, without you being there:

- Falling asleep while watching a movie, a series or YouTube
- Leaving a large download, game update or file copy running overnight
- Waiting for a long video render, export or backup to finish
- Restarting your PC after updates finish installing
- Limiting your own screen time or your kids' computer time
- Any situation where you think "I'll turn it off in 40 minutes" and know you'll forget

Under the hood, the app uses the built-in Windows commands `shutdown /s /t <seconds>` for shutdown and `shutdown /r /t <seconds>` for restart, and the standard Windows sleep function for sleep. It just gives you a friendly window instead of making you calculate seconds and type commands by hand.

## Quick start

1. Download the zip file from the Releases page (or from the files in this repository).
2. Extract the zip. Inside you will find 3 files: ShutdownTimer.exe, ShutdownTimer.cs and Build.bat.
3. Open ShutdownTimer.exe. This is the only file you need. The other two are only for building from source.
4. Confirm the Windows UAC prompt (administrator rights are needed to schedule a shutdown or restart).
5. Enter the time and click Sleep, Restart or Shut down.

That's it. There is nothing to install, no installer to run, and nothing is added to your system. You can keep the folder anywhere (Desktop, Downloads, a USB drive) and delete it whenever you want.

## Features

- Portable and installer-free. Just open the .exe file and use it.
- Three power actions. Sleep, Restart and Shut down, all in one small window.
- Separate fields for hours, minutes and seconds. No need to convert everything into minutes or seconds yourself.
- Fill in only what you need. Empty fields count as zero. For example, typing 40 into the minutes field alone means "in 40 minutes".
- Flexible input. Each field accepts up to 4 digits, so 90 minutes or 120 minutes work just as well as 1 hour 30 minutes.
- Digits only. The fields ignore any other characters, so you can't enter invalid values by accident.
- One-click scheduling. Click the button of the action you want and the timer starts immediately.
- Live countdown. After you start the timer, the window shows exactly how much time is left, in HH:MM:SS format, and which action will happen, for example "The computer will go to sleep in 00:39:58".
- Smart bottom-right button. Before the timer is started, the button reads Close and closes the app. While the timer is running, the same button reads Cancel and cancels the timer. The app stays open, so you can immediately set a new time or close it.
- Replaces old timers safely. Any previously scheduled shutdown or restart is cleared before the new action is set, so you never get a "shutdown already in progress" error.
- Input validation. The app warns you if you enter zero time or a value above the Windows maximum (10 years).
- Locked fields and buttons while running. Once the timer starts, the time fields become read-only and the action buttons are disabled, so the countdown can't be changed by accident.
- Safety warning for Sleep. If you try to close the window while a sleep timer is running, the app warns you that the computer will not go to sleep.
- Automatic administrator rights. The app asks for elevation by itself (a standard Windows UAC prompt) and restarts with administrator privileges. You don't need to right-click and choose "Run as administrator".
- Clean dark interface. A simple, modern dark window with large, easy-to-read time fields and fully readable buttons.
- Keyboard friendly. Press Enter to start the Shut down timer and Esc to trigger the bottom-right button (Close or Cancel). Clicking a field selects its contents so you can type a new value right away.
- Very low resource usage. A small native Windows Forms app with no heavy runtime and no background activity apart from a one-second timer for the countdown.
- No dependencies. It uses only components that are already built into Windows 10 and Windows 11.

## Screens and controls

| Element | Description |
| --- | --- |
| Hours / Minutes / Seconds | Three input fields for the delay. Empty = 0. |
| Status line | Shows hints, errors, and the live countdown. |
| Sleep button | Puts the computer to sleep after the entered delay. |
| Restart button | Restarts the computer after the entered delay. |
| Shut down button | Shuts the computer down after the entered delay. |
| Close button | Shown when no timer is running. Closes the app. |
| Cancel button | Shown while the timer is running. Cancels the timer and keeps the app open. |

## Requirements

- Windows 10 or Windows 11 (64-bit or 32-bit)
- .NET Framework 4.x (already included in Windows 10 and 11, nothing to install)
- Administrator rights (the app requests them automatically)

## Usage

1. Open ShutdownTimer.exe and confirm the UAC prompt.
2. Enter the delay, for example 40 in the minutes field.
3. Click Sleep, Restart or Shut down.
4. Watch the countdown. For Restart and Shut down you can also just walk away. For Sleep, keep the app open (you can minimize it).
5. Changed your mind? Click Cancel to stop the timer. Then enter a new time, or click Close to exit.

### Examples

| Hours | Minutes | Seconds | Result |
| --- | --- | --- | --- |
| 0 | 40 | 0 | Action in 40 minutes |
| 1 | 30 | 0 | Action in 1 hour 30 minutes |
| 0 | 0 | 45 | Action in 45 seconds |
| 2 | 0 | 0 | Action in 2 hours |

## Important notes

- Unsaved work will be lost. When Windows shuts down or restarts on a timer, running applications are closed without further prompts (this is how `shutdown /s /t <seconds>` and `shutdown /r /t <seconds>` work). Save your work before the timer ends.
- Sleep needs the app to stay open. Shutdown and restart are scheduled by Windows itself, but the sleep countdown is run by the app. If you close the window, the computer will not go to sleep. The app warns you before closing in this case.
- Closing the window with the X button does not cancel a scheduled shutdown or restart. They stay scheduled in Windows. Use the Cancel button to abort them.
- Cancelling manually. If you closed the app but want to abort a scheduled shutdown or restart, open Command Prompt and run: `shutdown /a`
- Restart and Shut down do not need the app to stay open. You can safely close the window after starting the timer.

## Troubleshooting

### Windows SmartScreen shows "Windows protected your PC"

The app is not code-signed, so Windows may show a warning for any newly downloaded .exe. Click More info, then Run anyway. If you prefer not to trust a prebuilt file, you can build it yourself from the source code (see below).

### My antivirus blocks or deletes the file

Small unsigned programs are sometimes flagged by mistake. You can add the file to your antivirus exceptions, or build it yourself from the source code to be sure of what you are running.

### The UAC prompt appears every time

This is expected. Administrator rights are required to schedule a shutdown or restart, and Windows always asks for confirmation.

### The app closes immediately after the UAC prompt

This happens if you click "No" in the UAC window. Start the app again and choose "Yes".

### The .exe does not open from inside the zip

Extract the zip to a normal folder first (right-click the zip, then Extract All), and then open ShutdownTimer.exe from that folder.

### The computer did not go to sleep

Make sure the app was still open when the countdown ended. Closing the window cancels the sleep timer.

## How it works

- On startup, the app checks whether it has administrator rights. If not, it restarts itself with the standard runas elevation.
- When you click Shut down or Restart, the app converts hours, minutes and seconds into total seconds, clears any old timer with `shutdown /a`, and schedules the action with `shutdown /s /t <seconds>` or `shutdown /r /t <seconds>`.
- When you click Sleep, the app counts down by itself and puts the computer to sleep with the standard Windows sleep function when the time is up.
- A one-second timer updates the countdown in the window.
- Cancel stops the countdown, cancels the scheduled shutdown or restart if there is one, and unlocks the fields and buttons. Close simply exits the app.

## Building from source (optional)

You only need this if you want to compile the app yourself instead of using the ready-made .exe. No Visual Studio or SDK is required, because the project is compiled with the C# compiler that ships with Windows.

1. Extract the zip to a normal folder.
2. Make sure Build.bat and ShutdownTimer.cs are in the same folder.
3. Double-click Build.bat.
4. After a few seconds, a fresh ShutdownTimer.exe appears in the same folder.

## Project structure

The zip contains 3 files:

- ShutdownTimer.exe: ready-to-use app (just open it)
- ShutdownTimer.cs: source code (C#, Windows Forms)
- Build.bat: one-click build script using the built-in Windows C# compiler

## Support the project

Shutdown Timer is free and will stay free. If it saved you some time or made your evenings a bit more comfortable, you can support the author with a donation:

https://www.donationalerts.com/r/gl1tch19

Every donation helps to keep improving the app and make new useful tools. Thank you!

## License

This project is licensed under the MIT License. See the LICENSE file for details.
