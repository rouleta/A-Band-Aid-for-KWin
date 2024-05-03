# A-Band-Aid-for-KWin
The design of key files to overcome KWin problems on Fedora38KDE
 KWin revival of x11 Fedora 38 KDE,   by Zano

Subject:

As is the case with many Linux distributions, on Fedora38KDE
KWin doesn't work well on x11 because during init process it is
unable to make the two main (text)files with which it can perform
all its functions. While by contrast the other needed files are
well produced by ksmserver.

The present hack consists to design manually all the files required
by the KWin session manager, keeping in mind the example of
Fedora36KDE, which works perfectly.

To start KWin in a perfect manner use the set of successive
manipulations. And to simplify the explanations, a true example
of files produced by KWin for 4xVirtual Desktops is selected in:

~/.config/session

where  ~ means /home/usrName

konsole_1020b17a1a5175000170972253100000014850009_1709723475_359340
konsole_1020b17a1a5175000170972253100000014850009_1709737722_999027
konsole_1020b17a1a5175000170972254400000014850010_1709723475_359369
konsole_1020b17a1a5175000170972254400000014850010_1709737722_999258
konsole_1020b17a1a5175000170972255700000014850011_1709723475_358724
konsole_1020b17a1a5175000170972255700000014850011_1709737722_999371
konsole_1020b17a1a5175000170972257100000014850012_1709723475_359387
konsole_1020b17a1a5175000170972257100000014850012_1709737722_999412

where the odd files size is 936, the even one 961. The odd files
are produced by KWin when the option (2) has been selected. The even
family appears when we select the /KWin option (1):

"System Settings" > "Startupand Shutdown" > "Session Management" >
"Restore previous logout"

and reboot the PC. The even files are obtained when we select the
option (2):

"System Settings" > "Startup and Shutdown" > "Session Management" >
"Session manually saved by user"

See the standard manner to operate KWin during its init setting phase.
In addition to the above family files, KWin writes two extra files
in ~/.config/session :

``kwin_saved at previous logout_''
``kwin_saved by user_''

and a specific server to govern after a login the re-reading step 
of screen data:

~/.config/ksmserverrc

which works both for options (1) and (2). The two parts of this file
should be changed, the original being:

# [General]
loginMode=restorePreviousLogout

# [LegacySession: saved at previous logout]
count=0

# [LegacySession: saved by user]
count=0

# [Session: saved at previous logout]
clientId1=1020b17a1a5175000170973739400000014680004
clientId2=1020b17a1a5175000170972244200000014760007
clientId3=1020b17a1a5175000170972253100000014850009
clientId4=1020b17a1a5175000170972254400000014850010
clientId5=1020b17a1a5175000170972255700000014850011
clientId6=1020b17a1a5175000170972257100000014850012
count=6
discardCommand3[$e]=rm,$HOME/.config/session/konsole_10
20b17a1a5175000170972253100000014850009_1709737722_999027
discardCommand4[$e]=rm,$HOME/.config/session/konsole_10
20b17a1a5175000170972254400000014850010_1709737722_999258
discardCommand5[$e]=rm,$HOME/.config/session/konsole_10
20b17a1a5175000170972255700000014850011_1709737722_999371
discardCommand6[$e]=rm,$HOME/.config/session/konsole_10
20b17a1a5175000170972257100000014850012_1709737722_999412
program1=/usr/libexec/DiscoverNotifier
program2=/usr/bin/kalendarac
program3=/usr/bin/konsole
program4=/usr/bin/konsole
program5=/usr/bin/konsole
program6=/usr/bin/konsole
restartCommand1=/usr/libexec/DiscoverNotifier,-session,1020b17a1a
5175000170973739400000014680004_1709737722_998719
restartCommand2=/usr/bin/kalendarac,-session,1020b17a1a5175000170
972244200000014760007_1709737722_999037
restartCommand3=/usr/bin/konsole,-session,1020b17a1a5175000170972
253100000014850009_1709737722_999027
restartCommand4=/usr/bin/konsole,-session,1020b17a1a5175000170972
254400000014850010_1709737722_999258
restartCommand5=/usr/bin/konsole,-session,1020b17a1a5175000170972
255700000014850011_1709737722_999371
restartCommand6=/usr/bin/konsole,-session,1020b17a1a5175000170972
257100000014850012_1709737722_999412
restartStyleHint1=0
restartStyleHint2=0
restartStyleHint3=0
restartStyleHint4=0
restartStyleHint5=0
restartStyleHint6=0
userId1=usrName
userId2=usrName
userId3=usrName
userId4=usrName
userId5=usrName
userId6=usrName

[Session: saved by user]
clientId1=1020b17a1a5175000170972297000000033400005
clientId2=1020b17a1a5175000170972244200000014760007
clientId3=1020b17a1a5175000170972253100000014850009
clientId4=1020b17a1a5175000170972254400000014850010
clientId5=1020b17a1a5175000170972255700000014850011
clientId6=1020b17a1a5175000170972257100000014850012
count=6
discardCommand3[$e]=rm,$HOME/.config/session/konsole_1020b17a1a5175
000170972253100000014850009_1709723475_359340
discardCommand4[$e]=rm,$HOME/.config/session/konsole_1020b17a1a5175
000170972254400000014850010_1709723475_359369
discardCommand5[$e]=rm,$HOME/.config/session/konsole_1020b17a1a5175
000170972255700000014850011_1709723475_358724
discardCommand6[$e]=rm,$HOME/.config/session/konsole_1020b17a1a5175
000170972257100000014850012_1709723475_359387
program1=/usr/libexec/DiscoverNotifier
program2=/usr/bin/kalendarac
program3=/usr/bin/konsole
program4=/usr/bin/konsole
program5=/usr/bin/konsole
program6=/usr/bin/konsole
restartCommand1=/usr/libexec/DiscoverNotifier,-session,1020b17a1a5175
000170972297000000033400005_1709723475_358445
restartCommand2=/usr/bin/kalendarac,-session,1020b17a1a51750001709722
44200000014760007_1709723475_358699
restartCommand3=/usr/bin/konsole,-session,1020b17a1a51750001709722531
00000014850009_1709723475_359340
restartCommand4=/usr/bin/konsole,-session,1020b17a1a51750001709722544
00000014850010_1709723475_359369
restartCommand5=/usr/bin/konsole,-session,1020b17a1a51750001709722557
00000014850011_1709723475_358724
restartCommand6=/usr/bin/konsole,-session,1020b17a1a51750001709722571
00000014850012_1709723475_359387
restartStyleHint1=0
restartStyleHint2=0
restartStyleHint3=0
restartStyleHint4=0
restartStyleHint5=0
restartStyleHint6=0
userId1=usrName
userId2=usrName
userId3=usrName
userId4=usrName
userId5=usrName
userId6=usrName

With the help of an editor, the ksmserverrc file should be reduced to

[General]
loginMode=restorePreviousLogout

[LegacySession: saved at previous logout]
count=0

[LegacySession: saved by user]
count=0

[Session: saved at previous logout]
clientId1=1020b17a1a5175000170973739400000014680004
clientId2=1020b17a1a5175000170972244200000014760007
clientId3=1020b17a1a5175000170972253100000014850009
count=3
discardCommand3[$e]=rm,$HOME/.config/session/konsole_1020b17a1a5175
000170972253100000014850009_1709737722_999027
program1=/usr/libexec/DiscoverNotifier
program2=/usr/bin/kalendarac
program3=/usr/bin/konsole
restartCommand1=/usr/libexec/DiscoverNotifier,-session,1020b17a1a5175
000170973739400000014680004_1709737722_998719
restartCommand2=/usr/bin/kalendarac,-session,1020b17a1a5175000170972
244200000014760007_1709737722_999037
restartCommand3=/usr/bin/konsole,-session,1020b17a1a5175000170972253
100000014850009_1709737722_999027
restartStyleHint1=0
restartStyleHint2=0
restartStyleHint3=0
userId1=usrName
userId2=usrName
userId3=usrName

[Session: saved by user]
clientId1=1020b17a1a5175000170972297000000033400005
clientId2=1020b17a1a5175000170972244200000014760007
clientId3=1020b17a1a5175000170972253100000014850009
count=3
discardCommand3[$e]=rm,$HOME/.config/session/konsole_1020b17a1a5175
000170972253100000014850009_1709723475_359340
program1=/usr/libexec/DiscoverNotifier
program2=/usr/bin/kalendarac
program3=/usr/bin/konsole
restartCommand1=/usr/libexec/DiscoverNotifier,-session,1020b17a1a5175
000170972297000000033400005_1709723475_358445
restartCommand2=/usr/bin/kalendarac,-session,1020b17a1a51750001709722
44200000014760007_1709723475_358699
restartCommand3=/usr/bin/konsole,-session,1020b17a1a51750001709722531
00000014850009_1709723475_359340
restartStyleHint1=0
restartStyleHint2=0
restartStyleHint3=0
userId1=usrName
userId2=usrName
userId3=usrName

Note that this KWin flexibility is a powerful means to modify the setting
``kwin_saved by user_'' which usually needs to reboot the PC.

In the same manner, the file ``kwin_saved at previous logout_'' produced
by KWin during the init process is

[Session]
active=1
activities1=ab93c009-71d4-4bd4-bda9-4496987eaa14
activities2=ab93c009-71d4-4bd4-bda9-4496987eaa14
activities3=ab93c009-71d4-4bd4-bda9-4496987eaa14
activities4=
activities5=ab93c009-71d4-4bd4-bda9-4496987eaa14
activities6=
count=6
desktop=1
desktop1=1
desktop2=2
desktop3=3
desktop4=-1
desktop5=4
desktop6=-1
fsrestore1=0,0,0,0
fsrestore2=0,0,0,0
fsrestore3=0,0,0,0
fsrestore4=0,0,0,0
fsrestore5=0,0,0,0
fsrestore6=0,0,0,0
fullscreen1=0
fullscreen2=0
fullscreen3=0
fullscreen4=0
fullscreen5=0
fullscreen6=0
geometry1=915,28,1004,994
geometry2=916,28,1004,994
geometry3=916,28,1004,994
geometry4=0,0,1920,1080
geometry5=916,28,1004,994
geometry6=0,1022,1920,58
iconified1=false
iconified2=false
iconified3=false
iconified4=false
iconified5=false
iconified6=false
keepBelow1=false
keepBelow2=false
keepBelow3=false
keepBelow4=true
keepBelow5=false
keepBelow6=false
maximize1=1
maximize2=1
maximize3=1
maximize4=0
maximize5=1
maximize6=0
opacity1=1
opacity2=1
opacity3=1
opacity4=1
opacity5=1
opacity6=1
resourceClass1=konsole
resourceClass2=konsole
resourceClass3=konsole
resourceClass4=plasmashell
resourceClass5=konsole
resourceClass6=plasmashell
resourceName1=konsole
resourceName2=konsole
resourceName3=konsole
resourceName4=plasmashell
resourceName5=konsole
resourceName6=plasmashell
restore1=915,0,1004,1022
restore2=916,0,1004,1022
restore3=916,0,1004,1022
restore4=0,0,1920,1080
restore5=916,0,1004,1022
restore6=0,1022,1920,58
sessionId1=1020b17a1a5175000170972253100000014850009
sessionId2=1020b17a1a5175000170972254400000014850010
sessionId3=1020b17a1a5175000170972255700000014850011
sessionId4=1020b17a1a5175000170973739400000014680005
sessionId5=1020b17a1a5175000170972257100000014850012
sessionId6=1020b17a1a5175000170973739400000014680005
shaded1=false
shaded2=false
shaded3=false
shaded4=false
shaded5=false
shaded6=false
shortcut1=
shortcut2=
shortcut3=
shortcut4=
shortcut5=
shortcut6=
skipPager1=false
skipPager2=false
skipPager3=false
skipPager4=false
skipPager5=false
skipPager6=false
skipSwitcher1=false
skipSwitcher2=false
skipSwitcher3=false
skipSwitcher4=false
skipSwitcher5=false
skipSwitcher6=false
skipTaskbar1=false
skipTaskbar2=false
skipTaskbar3=false
skipTaskbar4=false
skipTaskbar5=false
skipTaskbar6=false
stackingOrder1=4
stackingOrder2=1
stackingOrder3=2
stackingOrder4=0
stackingOrder5=3
stackingOrder6=5
staysOnTop1=false
staysOnTop2=false
staysOnTop3=false
staysOnTop4=false
staysOnTop5=false
staysOnTop6=false
sticky1=false
sticky2=false
sticky3=false
sticky4=true
sticky5=false
sticky6=true
userNoBorder1=false
userNoBorder2=false
userNoBorder3=false
userNoBorder4=true
userNoBorder5=false
userNoBorder6=true
windowRole1=MainWindow#1
windowRole2=MainWindow#1
windowRole3=MainWindow#1
windowRole4=
windowRole5=MainWindow#1
windowRole6=
windowType1=Normal
windowType2=Normal
windowType3=Normal
windowType4=Desktop
windowType5=Normal
windowType6=Dock
wmCommand1=
wmCommand2=
wmCommand3=
wmCommand4=
wmCommand5=
wmCommand6=

It should be used to replace the text found in ``kwin_saved by user_'' so that
the two kwin_* files becomes identical... leading to get the same screen
organisation of virtual desktops.

Now two new konsole files should be designed by using the above konsoles_*.
Their names could be (for exple)

konsole_1020b17a1a5175000170972253100000014850009_1709723475_359341
konsole_1020b17a1a5175000170972253100000014850009_1709737722_999028

whose contents is taken from konsoles_* family. The first file is
based on the contents of odd konsoles files, the other one the even
konsoles files. But here again, some little changes are needed.
Note that the same process should be used to write the two above
files to get for the first one the following structure:

[1]
Active=0
Tabs=[{"Orientation":"Horizontal","Widgets":[{"SessionRestoreId":1}]}]

[Number]
NumberOfSessions=1
NumberOfWindows=1

[Session1]
Encoding=UTF-8
LocalTab=%d : %n
Profile[$e]=$HOME/.local/share/konsole/Prof1.profile
RemoteTab=(%u) %H
SessionGuid={ed6211af-c02d-4b0b-a598-6b860fc1e59b}
TabColor=
WorkingDir[$e]=$HOME

[WindowProperties1]
1920x1080 screen: Height=994
1920x1080 screen: Width=1004
1920x1080 screen: XPosition=915
1920x1080 screen: YPosition=28
ClassName=Konsole::MainWindow
ObjectName=MainWindow#1
RestorePositionForNextInstance=false
State=AAAA/wAAAAD9AAAAAQAAAAAAAAAAAAAAAPwCAAAAAvsAAAAiAFEAdQBpAGMAawBDAG8AbQBtAGEAbgBkAHMARABvAGMAawAAAAAA/////wAAAXwBAAAD+wAAABwAUwBTAEgATQBhAG4AYQBnAGUAcgBEAG8AYwBrAAAAAAD/////AAABFQEAAAMAAAPsAAADlgAAAAQAAAAEAAAACAAAAAj8AAAAAQAAAAIAAAACAAAAFgBtAGEAaQBuAFQAbwBvAGwAQgBhAHIBAAAAAP////8AAAAAAAAAAAAAABwAcwBlAHMAcwBpAG8AbgBUAG8AbwBsAGIAYQByAQAAASP/////AAAAAAAAAAA=
VGA-1=VGA-1

[1]
Active=0
Tabs=[{"Orientation":"Horizontal","Widgets":[{"SessionRestoreId":1}]}]

[Number]
NumberOfSessions=1
NumberOfWindows=1

[Session1]
Encoding=UTF-8
LocalTab=%d : %n
Profile[$e]=$HOME/.local/share/konsole/Prof2.profile
RemoteTab=(%u) %H
SessionGuid={81286739-830b-4d17-a1d8-71bd3eab4746}
TabColor=
WorkingDir[$e]=$HOME

[WindowProperties1]
1920x1080 screen: Height=994
1920x1080 screen: Width=1004
1920x1080 screen: XPosition=916
1920x1080 screen: YPosition=28
ClassName=Konsole::MainWindow
ObjectName=MainWindow#1
RestorePositionForNextInstance=false
State=AAAA/wAAAAD9AAAAAQAAAAAAAAAAAAAAAPwCAAAAAvsAAAAiAFEAdQBpAGMAawBDAG8AbQBtAGEAbgBkAHMARABvAGMAawAAAAAA/////wAAAXwBAAAD+wAAABwAUwBTAEgATQBhAG4AYQBnAGUAcgBEAG8AYwBrAAAAAAD/////AAABFQEAAAMAAAPsAAADlgAAAAQAAAAEAAAACAAAAAj8AAAAAQAAAAIAAAACAAAAFgBtAGEAaQBuAFQAbwBvAGwAQgBhAHIBAAAAAP////8AAAAAAAAAAAAAABwAcwBlAHMAcwBpAG8AbgBUAG8AbwBsAGIAYQByAQAAASP/////AAAAAAAAAAA=
VGA-1=VGA-1

and so on for the two last odd  konsole_*. But the followin changes must be introduced
to get

[1]
Active=0
Tabs=[{"Orientation":"Horizontal","Widgets":[{"SessionRestoreId":1}]}]

[2]
Active=0
Tabs=[{"Orientation":"Horizontal","Widgets":[{"SessionRestoreId":2}]}]
...

[Number]
NumberOfSessions=4
NumberOfWindows=4

[Session1]
Encoding=UTF-8
LocalTab=%d : %n
Profile[$e]=$HOME/.local/share/konsole/Prof1.profile
RemoteTab=(%u) %H
SessionGuid={ed6211af-c02d-4b0b-a598-6b860fc1e59b}
TabColor=
WorkingDir[$e]=$HOME

[Session2]
Encoding=UTF-8
LocalTab=%d : %n
Profile[$e]=$HOME/.local/share/konsole/Prof2.profile
RemoteTab=(%u) %H
SessionGuid={81286739-830b-4d17-a1d8-71bd3eab4746}
TabColor=
WorkingDir[$e]=$HOME
...

[WindowProperties1]
1920x1080 screen: Height=994
1920x1080 screen: Width=1004
1920x1080 screen: XPosition=915
1920x1080 screen: YPosition=28
ClassName=Konsole::MainWindow
ObjectName=MainWindow#1
RestorePositionForNextInstance=false
State=AAAA/wAAAAD9AAAAAQAAAAAAAAAAAAAAAPwCAAAAAvsAAAAiAFEAdQBpAGMAawBDAG8AbQBtAGEAbgBkAHMARABvAGMAawAAAAAA/////wAAAXwBAAAD+wAAABwAUwBTAEgATQBhAG4AYQBnAGUAcgBEAG8AYwBrAAAAAAD/////AAABFQEAAAMAAAPsAAADlgAAAAQAAAAEAAAACAAAAAj8AAAAAQAAAAIAAAACAAAAFgBtAGEAaQBuAFQAbwBvAGwAQgBhAHIBAAAAAP////8AAAAAAAAAAAAAABwAcwBlAHMAcwBpAG8AbgBUAG8AbwBsAGIAYQByAQAAASP/////AAAAAAAAAAA=
VGA-1=VGA-1

[WindowProperties2]
1920x1080 screen: Height=994
1920x1080 screen: Width=1004
1920x1080 screen: XPosition=916
1920x1080 screen: YPosition=28
ClassName=Konsole::MainWindow
ObjectName=MainWindow#2
RestorePositionForNextInstance=false
State=AAAA/wAAAAD9AAAAAQAAAAAAAAAAAAAAAPwCAAAAAvsAAAAiAFEAdQBpAGMAawBDAG8AbQBtAGEAbgBkAHMARABvAGMAawAAAAAA/////wAAAXwBAAAD+wAAABwAUwBTAEgATQBhAG4AYQBnAGUAcgBEAG8AYwBrAAAAAAD/////AAABFQEAAAMAAAPsAAADlgAAAAQAAAAEAAAACAAAAAj8AAAAAQAAAAIAAAACAAAAFgBtAGEAaQBuAFQAbwBvAGwAQgBhAHIBAAAAAP////8AAAAAAAAAAAAAABwAcwBlAHMAcwBpAG8AbgBUAG8AbwBsAGIAYQByAQAAASP/////AAAAAAAAAAA=
VGA-1=VGA-1

...

and do the same for the new even file:

[1]
Active=0
Tabs=[{"Orientation":"Horizontal","Widgets":[{"SessionRestoreId":1}]}]

[2]
Active=0
Tabs=[{"Orientation":"Horizontal","Widgets":[{"SessionRestoreId":2}]}]

...

[Number]
NumberOfSessions=4
NumberOfWindows=4

[Session1]
Encoding=UTF-8
LocalTab=%d : %n
Profile[$e]=$HOME/.local/share/konsole/Prof1.profile
RemoteTab=(%u) %H
SessionGuid={ed6211af-c02d-4b0b-a598-6b860fc1e59b}
TabColor=
WorkingDir[$e]=$HOME

[Session2]
Encoding=UTF-8
LocalTab=%d : %n
Profile[$e]=$HOME/.local/share/konsole/Prof2.profile
RemoteTab=(%u) %H
SessionGuid={81286739-830b-4d17-a1d8-71bd3eab4746}
TabColor=
WorkingDir[$e]=$HOME
...

[WindowProperties1]
1920x1080 screen: Height=994
1920x1080 screen: Width=1004
1920x1080 screen: XPosition=915
1920x1080 screen: YPosition=28
ClassName=Konsole::MainWindow
ObjectName=MainWindow#1
RestorePositionForNextInstance=false
State=AAAA/wAAAAD9AAAAAQAAAAAAAAAAAAAAAPwCAAAAAvsAAAAiAFEAdQBpAGMAawBDAG8AbQBtAGEAbgBkAHMARABvAGMAawAAAAAA/////wAAAXwBAAAD+wAAABwAUwBTAEgATQBhAG4AYQBnAGUAcgBEAG8AYwBrAAAAAAD/////AAABFQEAAAMAAAPsAAADlgAAAAQAAAAEAAAACAAAAAj8AAAAAQAAAAIAAAACAAAAFgBtAGEAaQBuAFQAbwBvAGwAQgBhAHIBAAAAAP////8AAAAAAAAAAAAAABwAcwBlAHMAcwBpAG8AbgBUAG8AbwBsAGIAYQByAQAAASP/////AAAAAAAAAAA=
ToolBarsMovable=Disabled
VGA-1=VGA-1

[WindowProperties2]
1920x1080 screen: Height=994
1920x1080 screen: Width=1004
1920x1080 screen: XPosition=916
1920x1080 screen: YPosition=28
ClassName=Konsole::MainWindow
ObjectName=MainWindow#2
RestorePositionForNextInstance=false
State=AAAA/wAAAAD9AAAAAQAAAAAAAAAAAAAAAPwCAAAAAvsAAAAiAFEAdQBpAGMAawBDAG8AbQBtAGEAbgBkAHMARABvAGMAawAAAAAA/////wAAAXwBAAAD+wAAABwAUwBTAEgATQBhAG4AYQBnAGUAcgBEAG8AYwBrAAAAAAD/////AAABFQEAAAMAAAPsAAADlgAAAAQAAAAEAAAACAAAAAj8AAAAAQAAAAIAAAACAAAAFgBtAGEAaQBuAFQAbwBvAGwAQgBhAHIBAAAAAP////8AAAAAAAAAAAAAABwAcwBlAHMAcwBpAG8AbgBUAG8AbwBsAGIAYQByAQAAASP/////AAAAAAAAAAA=
ToolBarsMovable=Disabled
VGA-1=VGA-1
...

Note that the ``ToolBarsMovable=Disabled'' has been added. To terminate the init
process, the name of these two new konsole files must be exchanged in the original
form of ksmserverrc and appear in place of :

konsole_1020b17a1a5175000170972253100000014850009_1709723475_359340
konsole_1020b17a1a5175000170972253100000014850009_1709737722_999027

one must use :

konsole_1020b17a1a5175000170972253100000014850009_1709723475_359341
konsole_1020b17a1a5175000170972253100000014850009_1709737722_999028

and 

1020b17a1a5175000170972253100000014850009_1709723475_359341
1020b17a1a5175000170972253100000014850009_1709737722_999028

Putting these two new files in ~/.config/session, they will be adopted by KWin
during the next reboot, so that the 8 konsoles files, even and odd, will become 
useless. To check the success of these operations it will be sufficient to observe 
if or not the KWin screen manager works without the 8 initial konsole family. Then,
before logout, choose the next starting option (1). After login you should recover
the intial screen arrangement, equipped with 4 virtual konsoles. 
