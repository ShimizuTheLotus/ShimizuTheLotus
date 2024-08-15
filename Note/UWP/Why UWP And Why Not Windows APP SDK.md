# UWP is abandoned by Microsoft, why still UWP?
UWP is a new kind of program started from Windows 10. It was designed to run on "Universal Windows Platform".
UWP Apps have limited authorities. Behaviors such as reaching all files can be limited by users. However, the failure of Windows Phone directedly resulted to the deserting of UWP. Now Microsoft is trying to develop Windows APP SDK.

**However, I have these reasons to consider using UWP in a higher priority.**

## Natural limited accessory to sensitive information could get more trust from users.
**Windows APP SDK can easily do things some companies like: scan all your files in your disks, and the App is just for Instant Messaging.** Using UWP, natural limited authorities could let users trust you more.

## More friendly to your disk space, this is UWP.
Project files of Windows APP SDK are strangely **HUGE**. I have a Windows APP SDK project and its file size is **5GiB**. Why *strangely*? I copied its codes to a new Windows APP SDK project, and it just have 400MiB, much lighter than the previous one. Same things, diverse space. And most importantly, they're **HUGE**.

*In addition, if you use C++/CX to write a UWP app, it will also be huge.*

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
| Mica Alt [^LimitsComparisonOfUWPAndWindowsAPPSDKRefer1] | X | O |
| C# Version | Up to 7.0 | Higher |
| Apps On Windows Phone [^LimitsComparisonOfUWPAndWindowsAPPSDKRefer2] | O[^LimitsComparisonOfUWPAndWindowsAPPSDKRefer3] | X |

[^LimitsComparisonOfUWPAndWindowsAPPSDKRefer1]: Mica Alt is different with Mica, the color of destop background will be more obvious than Mica.
[^LimitsComparisonOfUWPAndWindowsAPPSDKRefer2]: Windows Phone is a kind of Wnidows device. "Windows Phone" Here refers to Windows Phone with Windows 10 Mobile. **All "Windows Phone" in this documents refer to Windows Phone with Windows 10 Mobile.**
[^LimitsComparisonOfUWPAndWindowsAPPSDKRefer3]: Windows Phone can only install UWP apps. Plus, The maximum Windows version of Windows Phone is Windows 10 1607. So your UWP target version shouldn't higher than that. This means you'll have a huge limit of using visual effects. Almost no one use Windows Phone. But if you're a lover, **do it!**
