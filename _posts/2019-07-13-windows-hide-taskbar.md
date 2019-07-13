---
layout: post
title: "the best way to hide taskbar on windows"
category: tools
---

I have searched for many softwares to hide windows taskbar, some of them are too old and not compatiable with windows 10, and some of them meets a problem that when you run windows search the hided taskbar will be showed again.

So I writed a Autohotkey script to test the taskbar status every second and hide taskbar if it is showed, and of course I used a flag to mark if I want to hide it.

```autohotkey
flag = 1
Loop
{
    if (flag == 1){
        if (WinExist("ahk_class Shell_TrayWnd")){
            WinHide ahk_class Shell_TrayWnd
        }
    }else{
        if (!WinExist("ahk_class Shell_TrayWnd")){
            WinShow ahk_class Shell_TrayWnd
        }
    }
    sleep 1
}

^Esc::
    if (flag == 1)
        flag = 0
    else
        flag = 1
return
```