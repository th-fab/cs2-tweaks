# General Gameplay Tweaks

General Tweaks sorted by Issue

___WORK IN PROGRESS!___

TOC:

- [General Gameplay Tweaks](#general-gameplay-tweaks)
  - [Stuttering](#stuttering)
    - [Reflex and LLM, uncap FPS ingame](#reflex-and-llm-uncap-fps-ingame)
    - [High Polling rate causing stuttering/fps drops](#high-polling-rate-causing-stutteringfps-drops)
    - [Disable fTPM (AMD)](#disable-ftpm-amd)
  - [Mouse Issues](#mouse-issues)
    - [Note](#note)
    - [MarkC Mouse Fix](#markc-mouse-fix)
    - [Force disable raw input](#force-disable-raw-input)
    - [SmoothMouseXCurve / SmoothMouseYCurve](#smoothmousexcurve--smoothmouseycurve)
    - [Disable MouseSpeed and MouseAccel](#disable-mousespeed-and-mouseaccel)
  - [Network](#network)
    - [interp ratio](#interp-ratio)


## Stuttering

### Reflex and LLM, uncap FPS ingame
1. Disable Reflex in ingame Settings
2. Set `fps_max 0` 
3. Use Launch Option `-noreflex`
4. Enable Low Latency Mode (LLM) in NVCP (`LOW` or `ULTRA`)
5. Limit FPS in NVCP/RTSS to a sustainable number (e.g. `288` if your PC manages)

[Relevant reddit thread](https://www.reddit.com/r/GlobalOffensive/comments/1gu9h7l/godtier_setting_for_best_frames_dont_use_reflex/)

### High Polling rate causing stuttering/fps drops
A high polling rate of your mouse can cause high CPU load and therefore stuttering in CS2. This seems to be fixed in Windows 11 V22H2 [Relevant BlurBusters Thread](https://forums.blurbusters.com/viewtopic.php?t=12157).

If you're still on an older version of Windows, you might need to lower the polling rate of your mouse. 

### Disable fTPM (AMD)
[Reddit Thread](https://www.reddit.com/r/cs2/comments/1gdbh86/finally_i_fixed_the_stuttering_issue_on_my_system/)

Basically says to disable fTPM in BIOS. Not tested.

## Mouse Issues

### Note
Most mouse issues are caused by high variance in frame-time (to fix see [Stuttering](#stuttering))

### MarkC Mouse Fix
__WARNING: Since CS2 uses raw-input by default, this can be seen as placebo as it basically does nothing!__

[Website of the MarkC Mousefix](https://donewmouseaccel.blogspot.com/2010/03/markc-windows-7-mouse-acceleration-fix.html)

### Force disable raw input
[Relevant reddit thread](https://www.reddit.com/r/GlobalOffensive/comments/1icvaqk/hidden_launch_options_for_rawinput_enabledisable/)

Use the following launch option (replace `-novid +fps_max xxx` with your current launch options):

`cmd /c set SDL_MOUSE_RELATIVE_MODE_WARP=1 & %command% -novid +fps_max xxx`

(In Steam or CS2? Not tested yet!)

### SmoothMouseXCurve / SmoothMouseYCurve
[Relevant BlurBusters Comment](https://forums.blurbusters.com/viewtopic.php?f=10&t=13397&start=10#p103968)

In the Registry editor navigate to ` HKEY_CURRENT_USER\Control Panel\Mouse` and replace the Values of the Keys `SmoothMouseXCruve` and `SmoothMouseYCruve` with the Value `0`.

Note: This is similar to what [MarkC Fix](#markc-mouse-fix) does, so might as well be placebo / irrelevant for games with hardcoded raw input.

### Disable MouseSpeed and MouseAccel
[Relevant BlurBusters Thread]()

In the registry editor navigate to `HKEY_CURRENT_USER\Control Panel\Mouse`. Create the Key `MouseAccel` (string value) if it is not present and set its value to `0`.

In the same folder set the value of the `MouseSpeed` Key to `-`. 

## Network

### interp ratio

It is apparently possible to change the convar `cl_interp_ratio` in CS2 again. It seems to work differently to _Buffer to smooth over packet loss_

Apparently it can be set to values from `0-5`, with lower values being smaller delays (5 not recommended). Try setting it to values from `0-2` and play around with it for best results. In theory `cl_interp_ratio 0` should work best, but this changes according to your own and your opponents ping (Higher ping => higher value).