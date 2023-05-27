<p align="center"><img src="https://user-images.githubusercontent.com/1491536/171987806-e7f290b4-91ed-451c-a7ef-d30f77a24931.svg" width="500"></p>

&nbsp;

<p align="center"><b>CompactGUI transparently compresses your games and programs reducing the space they use without affecting their functionality. It used to use the Windows 10 <code>compact.exe</code> function but now works directly with the Win32 API to be much more efficient.</b></p> 

&nbsp;
&nbsp;

<p align="center"><img src="https://user-images.githubusercontent.com/1491536/172040389-62932137-11ae-49c8-8749-95c0b67f3aab.png" width="250"/><img src="https://user-images.githubusercontent.com/1491536/172040455-6cd06756-6323-44da-b350-daa47f31c5e3.png" width="250"/><img src="https://user-images.githubusercontent.com/1491536/172040456-09c069e3-093a-4c5e-8d69-f52d4dc2f982.png" width="250"/></>



------

**Note - v3.0 Complete rewrite is underway as of June 2022 with the following features:**
 - Rebuilt from scratch in .NET 6 using WPF
 - Smoother, simplified UI
 - Removed dependency on `compact.exe` and directly accesses the Win32 API
 - Background monitoring of compressed folders to keep track of size changes with e.g. Steam updates. 
 - Parallelised and asynchronous programming resulting in over an order of magnitude speed improvement in some cases.
 
    ```yml
    ARK Survival Evolved | 170 GB | 108000 Files
    
    compact.exe:         9m18s   
    CompactGUI v3 a3:    4m42s    49%  faster  # compact.exe yields system resources and checks files which is why this is so much faster
    CompactGUI v3 a2:    8m17s    11%  faster
    CompactGUI v2.6.2:   23m6s    248% slower
        
    Stardew Valley       | 700 MB | 6800 Files

    compact.exe:         17.34s   
    CompactGUI v3 a3:    12.95s   25%  faster
    CompactGUI v3 a2:    17.82s   2.7% slower
    CompactGUI v2.6.2:   81.79s   471% slower
    ```
 - Automatic skipping of files that are smaller than the disk's cluster size, 4kb by default
 - Saving of poorly compressed filetypes per directory to skip on next run

&nbsp;

------
&nbsp;

**What is the Windows 10 compact.exe function?**
It's a commandlet with a collection of new algorithms introduced in Windows 10 that allow you to transparently compress games, programs and other folders with virtually no performance loss.

**Transparently? What does that mean?**
Transparent compression means that files can still be used normally on the computer as if nothing had happened - they don't get repackaged like Zip and Rar files do. 

**How is this different from the built-in compression in older versions of Windows?**
This is similar to the NTFS-LZNT1 compression built-in to Windows (Right click > Properties > Compress to save space) however the newer algorithms introduced in Windows 10+ are far superior, resulting in greater compression ratios with almost no performance impact.Those with older HDDs may even see a decent performance gain in the form of reduced loading times as the smaller files means it takes less time to read programs and games into RAM. [More information can be found here](https://msdn.microsoft.com/en-us/library/windows/desktop/hh920921(v=vs.85).aspx) 




####
 
<p>Download from <a href="[https://github.com/AuronSV/CompactGUI_/releases]"><b>GitHub Releases</b></a></p>

Coming soon: Download from Windows 10/11 Store
  
## Uses
Use this tool to compress folders while still being able to use/run them normally: 
- Reduce the size of games (e.g. ARK-Survival Evolved: 169 GB > 91.2 GB)
- Reduce the size of programs (e.g. Adobe Photoshop: 1.71 GB > 886 MB)
- Compress any other folder on your computer
  
## Extra Features
 - Visual feedback on compression progress and statistics
 - Configurable list of poorly-compressed filetypes that can be skipped.
 - Online integration with community-sourced [database](https://github.com/ImminentFate/CompactGUI/wiki/Community-Compression-Results) to get compression estimates
 - Integration into Windows Explorer context menus for easier use.
 - Analyze the status of existing folders
 - Background monitor to keep track of compressed folders and easily see / recompress them if they've been recently updated (such as Steam games) or decompressed. 
 

<h4 align="center"><b>See the <a href="https://github.com/ImminentFate/CompactGUI/wiki/Community-Compression-Results">Wiki</a> for a list of <a href="https://github.com/ImminentFate/CompactGUI/wiki/Community-Compression-Results"><img src="https://img.shields.io/badge/Games-5085-blue.svg"></a> that have been tested from <a href="https://github.com/ImminentFate/CompactGUI/wiki/Community-Compression-Results"><img src="https://img.shields.io/badge/-34923-lightgrey.svg"></a> submissions</b></h3>
<p>&nbsp;</p>




## Background

Windows 10 includes a little-known but very useful tool called Compact.exe that allows one to compress folders and files on disk, decompressing them at runtime. With any modern CPU (I have tested as old as an i3-370M from 2010 with negligible impact), this added load is hardly noticed, and the space savings are of most use on those with smaller SSDs. 

As program folders and games can be shrunk by up to 60%, this has the added bonus of potentially reducing load times - especially on slower HDDs. 

More information on the inbuilt Windows function can be found [here](https://technet.microsoft.com/en-au/library/bb490884.aspx) and [here](https://msdn.microsoft.com/en-us/library/windows/desktop/hh920921(v=vs.85).aspx) or by typing `compact /q` into the commandline

This tool is intentionally designed to only compress folders and files. Whole drives and entire Windows installations cannot be modified from within CompactGUI - users seeking that functionality should use `compact /compactOS` from the commandline. 

The compression is fully transparent - programs, games and files can still be accessed as normal, and show up in Explorer as they normally would — they'll just be decompressed into RAM at runtime, staying compressed on disk.

## Options
By default, the program runs Compact with the `XPRESS8K` algorithm active. This provides a good balance between compression speed and size reduction. The default that Windows uses is `XPRESS4K` which is faster but compresses less. 
The options available are: 
- XPRESS4K: Fastest, but weakest
- XPRESS8K: Reasonable balance between speed and compression
- XPRESS16K: Slower, but stronger
- LZX: Slowest, but strongest - note it has a higher overhead, so use it on programs/games only if your CPU is reasonably strong or the program/game is older. 

 
 -----
 ### Like this project?
 Please consider leaving a tip on Ko-Fi :) 
 
 <p align="center"><a href='https://ko-fi.com/iridiumio' target='_blank'><img height='42' style='border:0px;height:42px;' src='https://cdn.ko-fi.com/cdn/kofi3.png?v=3' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a></p>
  
