# UWP is abandoned by Microsoft, why still UWP?
UWP is a new kind of program started from Windows 10. It was designed to run on "Universal Windows Platform".
UWP Apps have limited authorities. Behaviors such as reaching all files can be limited by users. However, the fail of Windows Phone directedly resulted to the deserting of UWP. Now Microsoft is trying to develop Windows APP SDK.

**However, I have these reasons to consider using UWP in a higher priority.**

## Natural limited accessory to sensitive informations could get more trust from users.
**Windows APP SDK can easily do things some company like: scan all your files in your disks, and the App is just for Instant Messaging.** Using UWP, natural limited authorities could let users trust you more.

## More friendly to your disk space, this is UWP.
Project files of Windows APP SDK are strangely **HUGE**. I have a Windows APP SDK project and its files is **5GiB**. Why *strangely*? I copied its codes to a new Windows APP SDK project, and it just have 400MiB, much lighter than the previous one. Same things, diverse space. And most importantly, they're **HUGE**.

*What about UWP?* Until now, my whole local repository of Tagme_, sizes 23.3MiB. And for It's project files, 18.8MiB only!! Plus, I added much codes in Tagme_.

## UWP is lighter, faster
Until now(Feb. 17, 2024, 3:15, GMT+0), UWP still has better performance than Windows APP SDK.
>## Performance considerations
>Today in version 1.4 of the Windows App SDK, launch speeds, RAM usage, and installation size of WinUI 3 apps are larger/slower than seen in UWP. We're actively working to improve this.

Source: https://learn.microsoft.com/en-us/windows/apps/windows-app-sdk/migrate-to-windows-app-sdk/what-is-supported#performance-considerations

## Limits Comparison of UWP and Windows APP SDK
**Some features are not available in UWP. Like what I said: "*consider using UWP in a higher priority.*", not "Only UWP"**

To help you consider what time you should not use UWP, I made this table:
| Feature | UWP | Windows APP SDK |
|---|:---:|:---:|
| Mica | O | O |
| Mica Alt [LimitsComparisonOfUWPAndWindowsAPPSDKRefer1] | X [t] | O |
| C# Version | Up to 7.0 | Higher |
| Apps On Windows Phone [Limits Comparison of UWP and Windows APP SDK Refer 2] | O | X |

[LimitsComparisonOfUWPAndWindowsAPPSDKRefer1]: Mica Alt is different with Mica, the color of destop background will be more obvious than Mica.
[Limits Comparison of UWP and Windows APP SDK Refer 2]: Windows Phone is a kind of Wnidows devices. "Windows Phone" Here refers to Windows Phone with Windows 10 Mobile.
[t]: test
