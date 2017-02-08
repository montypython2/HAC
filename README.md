```
=== Index ===
./Backdoor_Busting
./v12
./v13
./v13_2016
./v13_2016_FINAL

Help credits:
Willox    - Helping cheaters lose their marbles since '14
RyanJGray - Helping with testing & ideas. Best of luck with your own AC
```

## Don't use this. It will not work and will break your server!##
## This code is only for historic reasons / learning from ##
## If you plan on using this despite the warning read bellow##

-=[UH]=- General HeX.


"A good attempt at something impossible".

Those words mean a lot. As far as I know, no-one has ever beaten it, but more on that later.

I first began this project as "NoBB" (No BaconBot) in 2009 as my first real Lua project, just after I started hosting a Deathmatch server. Before this, my only experience with Lua was in editing Life Support devices for SpaceBuild in 2008.

NoBB and early versions of HAC were simply blacklists of commands, which reported to the server via a concommand. This quickly became useless as more and more cheats were being written.

HeX's AntiCheat began to take shape in early 2010. At first I just added filename keyword checking no NoBB, and later a hook blacklist, global function blacklist, and always expanding the ever increasing concommand blacklist. Eventually this got too big and was crashing GMod when it loaded (I found out GMod has a file limit of 255KB per .lua file), so I started work on a whitelist-based system instead of blacklisting everything possible...

Around March 2011 I wrote a lua file reader to get a private cheat from a player who I was chatting to at the time. This worked perfectly so I integrated this (StreamHKS) into HAC, to check every player who joins. This has worked very well ever since, and has collected a huge amount of private hacks.

HAC has got better and better over time, and as of this post is the best GMod AntiCheat as far as I know. This was all before GMod 13, version HAC106, which I released along with all previous versions on my SVN.

I've also helped a few server admins with AntiCheat systems over the years, especially during the Sethhack days. The biggest being Twoscore and Mindblast. Almost all other servers that use a Lua AntiCheat have stolen code and/or detection methods from HAC.

=== Everything below is from the private GMod 13 version ===

After the GMod 13 switchover, everything was broken as Garry doesn't understand the words "backwards compatibility". I was left with a broken server and a crappy "new" game. I almost quit GMod hosting then, but me and a friend spent about 4 weeks getting it all working again.

I also rewrote a lot of it to make it more efficient during this time. The file reader was the most difficult as Garry changed all the file functions and removed DataStream without replacing its functionality, because he hates everyone.

I finally wrote a replacement for DataStream, NetBurst (sh_HACBurst), which allows unlimited length strings to be sent both ways over net, Garry's new system, using a buffer so as not to overflow the channel, and got the file reader working again (no arbitrary Garry'd 64KB size limit). Although over the years HAC has been running, I've hardly ever changed the serverside code until 2013 (there are still bits of NoBB code in there from 2009...)

Recently, I've been rewriting the whole serverside to make it much easier to add new checks in; a lot of things are now in their own table/namespace. HAC.Speed.Check etc. But it still relies on the 5 year old HAC.DoBan function. The most recent improvement is a system to send checks dynamically, BurstCode I've called it as it uses NetBurst.

It sends one, and then waits for the response before sending another. If any checks fail (hacks were detected), or it times out, it doesn't send more. This means if people are trying to intercept the checks & steal the code, they only get one before being banned.

Some interesting things HAC can do that no other AntiCheat in GMod can, as far as I know:

Console key logger, all keys pressed are logged.
Detection of ANY unknown cvars/concommands, even if not added through Lua.
100% serverside speedhack/angle/anti-aim/sv_cheats/sv_allowcslua detection.
Speedhackers end up in a bin!
Several methods to attempt thwart skiddie file stealers (see sv_FixEnum/sv_BurstCode).
Two different methods of screenshot logging
Checking of bound keys.
Re-binding of keys.
Very large amounts of self-checking to prevent bypasses.
Steam group checking.
Advanced keyword checking of client's Lua files.
Detection of overrides to GMod's default files.
Protection against serverside backdoors/takeover/RCON stealing.
Total blockage of SendFile/RequestFile. Bans anyone uploading/download non-sprays.
Name validation, refuses connection for skiddie/troll names, newlines, invisible spaces, certain UTF chars etc (see sv_PWAuth/sv_UTF)
Total RCON protection. Whitelisted to in-game admin's IP and SteamID.
HIIIIGHWAY TO HELL!
=== Usefulness of HAC vs. C++ cheats ===

HAC works against 100% of all Lua cheats and modules (for real!), but it has real trouble detecting pure C++ cheats. Only by the traces they leave in the engine (CVars etc), and serverside detections (like SMAC) can these be detected.

So now I'm at a point where I have a perfect Lua AntiCheat, but less and less people are using Lua to cheat. There will always be copy+pasted Lua cheats in GMod, it is after all a Lua-based game, but C++ cheats are becoming more of a problem.

Part of the reason I'm releasing all this is

Because engine-based C++ cheats like in CSS are more common for GMod now, it's only a matter of time before increasing numbers of cheaters use them. All it takes is a C++-based Sethhack-like cheat, and it'll be 2012 all over again.
Due to Garry's server browser, my server has been empty more times than it's had players. See http://unitedhosts.org/bar/end for more information.
It's going to cost another £480 to renew a server that no-one plays on.
Even when the server was running, people would rather play on cheater-infested DarkRP hosted by 12yo kids who pay to be admin.
GMod isn't the fun sandbox game it used to be back in 2007.
This CoderHire crap is ruining GMod. It used to be about free & open user-made content, now it's about selling the latest shitty addons for DarkRP.
However I will *not\* be leaving quietly. I've spent far too long trying to protect GMod, to keep a fair and clean game for everyone, and look where I am now. Closing down my server due to hacks and a total lack of players.

Therefore I'm releasing an absolutely MASSIVE collection of hacks that have been logged over the years from over 500 cheaters.

These many thousands of folders contain a very large amount of private code (or copy+pasted rubbish) and will no doubt piss off a lot of people. Rough guide as to what is included:

All the HAC ban & report logs (tons of goodies in here)
Lots of private GMod module DLLs. (some with source)
A few C++ hack sources, including an lua injector and file stealers.
Screenshots sent to me from cheaters bragging about their code.
My own notes & ideas file, containing interesting notes/detection ideas/future plans.
A whole load of R&D, random code snippets, test scripts, raw resources such as sound files etc.
=== HAC Bypass methods ===

Pure Lua = No chance. Pure C = Will avoid most of the checks, but may set off usercmd/angle detections. Lua/C = May still set off the above, but this is where the real danger lies. If you know what you're doing, you may be able to be stealthy and avoid 99% of the checks.

=== How to avoid the loss of your marbles ===

Don't even bother detouring anything. Or if you do, do it from C. Beware of bc_XDCheck/bc_FuncThis.
Do not load before HAC. garbage and _R will get you.
Do not load after HAC. You'll get the detoured functions and end up bursting your bagpipes.
A direct attack on HAC or its reporting system, excluding blocking it from loading, may work, but watch out for the hundreds of self-checks.
Screenshots will still get you. Try returning false data.
Don't ever store any hack-related files in the first garrysmod/ folder or above. Yes Lua can read here.
Don't use key binds.
=== HAC's files & modules ===

HAC uses many C++ binary modules on the serverside. These are critical to the functionality of many of the checks and it won't start without them.

The modules were built with Visual Studio 2010 on an XP 32bit platform, and designed to run on Win2003 x86. They probably function fine under an NT6-based OS (win7 etc), but I've not tried. The source & project files are there if you want to compile them for your OS/platform.

. gmsv_hac_win32.dll -- Main HAC module. Contains file I/O, unrestricted concommand etc.
. gmsv_dns_win32.dll -- DNS Lookup, see sv_RCON
. gmsv_vfft_win32.dll -- Old, IsValidFileForTransfer hook. Replaced with gmsv_slog2_win32.dll
. gmsv_slog2_win32.dll -- Command logging, can hook ALL concommands run by clients. Also contains INetChannel hooks for SendFile/ReceiveFile
. gmsv_cvar3_win32.dll -- CVar3 by Blackops, compiled without the sigscan.
. gmsv_hideip_win32.dll -- overrides the player_connect event's IP address.
. gmsv_farcon_win32.dll -- Fixed gmsv_rcon by Fangli.
. gmsv_usercmd_win32.dll --  CUserCmd functions, see sv_UCmd
. gmsv_longmath_win32.dll -- 64bit addition/subtraction.
. gmsv_askconnect_win32.dll -- See sv_EatKeys
. gmsv_clientcommand_win32.dll -- Run some commands on players that are blocked by RCC
. gmsv_sourcenetinfo_win32.dll -- INetChannel functions. See hac_base
. pl_cvquery.dll -- BlueKirby's CVar query module, see sv_CVQuery
--- Main ---
lua/en_hac.lua --CL, HAC's main clientside section. This is loaded by lua/includes/init.lua (patched by sv_FixEnum)
lua/en_streamhks.lua --CL section of sv_StreamHKS, the hack stealer. Included by en_hac
lua/hac_base.lua --SV, base functions and utils for serverside code
lua/hac_base_post.lua --SV, base loaded after hac_base
lua/hac_modules.lua --SV, Loads all the DLLs used on the serverside
lua/hac_nosend.lua --SV, list of PERMABANNED cheaters. BurstCodes are never sent to these people
lua/autorun/client/cl_hac.lua --Decoy loader
lua/autorun/client/nuke_config_client.lua --Real loader, loads the HAC/*.lua plugins
lua/autorun/server/sv_hac.lua --Main serverside section
lua/includes/extensions/datasteam.lua --Fake script to tell if init.lua was messed with. Intentional mis-spelling.

--- BurstCodes ---
lua/burst/bc_CapCheck.lua --Check the output of render.Capture is actually jpeg data
lua/burst/bc_CVL.lua --"cvarlist", see sv_CVL
lua/burst/bc_DLX.lua --Checks for download/data/ulx_logs, clients stealing them
lua/burst/bc_Dump.lua --string.dump's hook.Call/Run and compares against known value
lua/burst/bc_EatKeys.lua --Uses cvar3 or other modules if installed to rebind keys
lua/burst/bc_EatKeysAll.lua --Rebinds keys anyway
lua/burst/bc_EatShit.lua --Old check, for Oubhack, but may still work on others
lua/burst/bc_FuckOub.lua --Another one for Oubhack, pcall's functions with bad args, catch error, check path
lua/burst/bc_Garbage.lua --Checks on collectgarbage()
lua/burst/bc_GCall.lua --Checks for correct functioning of a _G metatable
lua/burst/bc_HasMT.lua --Checks for bad metatables
lua/burst/bc_Hooker.lua --Check CRC of stack calling a hook
lua/burst/bc_Hooker2.lua --Various hook.Call override checks
lua/burst/bc_KLog.lua --Keylogger
lua/burst/bc_LPT.lua --Checks call stack of self
lua/burst/bc_NukeData.lua --Wipe a client's /data folder
lua/burst/bc_ShitList.lua --Searches down the dir tree for known cheat files. Even works on root of drive.
lua/burst/bc_Spectate.lua --Admin spectate script
lua/burst/bc_XDCheck.lua --Detour checks

--- Really, I'm surprised no one else has hidden checks in ents before ---
lua/entities/auto_removed/cl_init.lua --Emergency en_streamhks loader if en_hac was blocked.
lua/entities/hac_monitor/cl_init.lua --Ensure certain HAC parts loaded properly.
lua/entities/hac_monitor/init.lua --Serverside section of the above
lua/entities/hac_rocket/cl_init.lua --Report the client's modules, nuke Lua if not en_hac loaded


--- Plugins ---
HAC stores most checks in plugins. These are not true plugins as they can't be removed, they inter-depend on each other, but it does help separate the code into more manageable pieces.

Lua/HAC/sv_TimeOut.lua --Check if players are timing out
lua/HAC/cl_BindBuff.lua --Get config.cfg, see sv_BindBuff
lua/HAC/cl_BSoD.lua --Fake bluescreen, example: http://unitedhosts.org/bar/tmp/BSoD.html
lua/HAC/cl_Message.lua --Messages, notifications, sounds. sv_GPath also has code here
lua/HAC/cl_RSX.lua --Pointless rubbish / decoy
lua/HAC/cl_SpinMeRound.lua --CL section of sv_SpinMeRound, used for color overlay
lua/HAC/cl_TakeSC.lua --Capture screenshots
lua/HAC/cl_Whoops.lua --Attempt to RunStringEx as system files, if skiddie file stealer, will overwrite their files. And another en_hac load check
lua/HAC/sh_Binds.lua --Prevent gm_spawn / say binds
lua/HAC/sh_DownloadFilter.lua --Send list of downloaded content to server
lua/HAC/sh_HACBurst.lua --For sending large strings between client<->server
lua/HAC/sh_PEX.lua --Serverside LocalPlayer():ConCommand()
lua/HAC/sv_Speed.lua --Speedhack detection & mitigation, freeze client if to many ucmd's are sent
lua/HAC/sv_ANC.lua --Anti-Noclip. If sbox_noclip == 0 and noclip, explode.
lua/HAC/sv_BadMapEnts.lua --Remove lua_run / point_servercommand from map.
lua/HAC/sv_BallOfSteel.lua --Gives previous cheaters the Balls of Steel. Needs FSA for ranks
lua/HAC/sv_BannedCmds.lua --Add FCVAR_CHEAT flag to bad commands.
lua/HAC/sv_BindBuff.lua --Bind checking, propkill, aimbot etc
lua/HAC/sv_Binds.lua --HAC_AllowSay if eatkeys binds, plus fruit.
lua/HAC/sv_Boom.lua --Explosion functions. The famous HAAAAAAX.
lua/HAC/sv_BSoD.lua --Bluescreen trigger
lua/HAC/sv_BurstCode.lua --Sends checks to clients dynamically, if any fail/time out, doesn't send more
lua/HAC/sv_CMod.lua --Module check, mainly old GM12 code. Also has DLC, the DLL stealer
lua/HAC/sv_ConCon.lua --Commands-over-net system to prevent aliasing of concommands
lua/HAC/sv_Crash.lua --For stupid people
lua/HAC/sv_CVCheck.lua --Serverside convar checker. Does not use any clientside code
lua/HAC/sv_CVL.lua --Cvarlist, processes and handles the return from bc_CVL
lua/HAC/sv_Detections.lua --Extra punishments for certain things, also handles Permaban
lua/HAC/sv_Dev.lua --Code counter and various testing functions
lua/HAC/sv_DownloadFilter.lua --Kicks for failing to download the content (sounds etc)
lua/HAC/sv_EatKeys.lua --Handles breaking & re-binding of client's keys
lua/HAC/sv_FixEnum.lua --Patches default GMod files with custom load/detection/self-defence/override code
lua/HAC/sv_Fixer.lua --What Garry should have done all along. CLAMP THE FUCKING CLIENT VARS!
lua/HAC/sv_GPath.lua --Logs client's game paths, to tell if they're on Windows and for the BSoD
lua/HAC/sv_Group.lua --Kick for being in certain troll/cheating groups
lua/HAC/sv_HACBurstEx.lua --Utils for HACBurst, mostly the "on complete" function
lua/HAC/sv_HideIP.lua --Probably not needed now, but blocks client IPs from player_connect game event
lua/HAC/sv_HSP.lua --HeX's Server Plugins integration, mainly so the HSP ChatFilter doesn't eat words
lua/HAC/sv_InfAng.lua --Infinite angle guard
lua/HAC/sv_KickID.lua --Alternative kickid command
lua/HAC/sv_KLog.lua --Client keylogger, serverside for bc_KLog
lua/HAC/sv_KWC.lua --KeyWordCheck, scans all HKS file for keywords, and if default overridden, kick
lua/HAC/sv_LPT.lua --Serverside of bc_LPT and en_hac's LPT
lua/HAC/sv_NameHack.lua --Kicks for changing name while in-game
lua/HAC/sv_NoRS.lua --Serverside protection against backdoor'd addons
lua/HAC/sv_NukeData.lua --Serverside to bc_NukeData, wipe a client's /data folder
lua/HAC/sv_PropBlock.lua --Block spawning of props with "../"
lua/HAC/sv_PRS.lua --PlayerReallySpawn, calls this hook when a client actually moves
lua/HAC/sv_PWAuth.lua --Handle server connection/bans/neversend, blocks certain names
lua/HAC/sv_RCON.lua --RCON protection, whitelisted to my IP
lua/HAC/sv_RSX.lua --Load of rubbish
lua/HAC/sv_SelfExists.lua --Handles init checks & non-ban kicking
lua/HAC/sv_Serious.lua --EIGHT if they have sv_cheats 1
lua/HAC/sv_SkidCheck.lua --Cheater warning notification. Handles adding/message
lua/HAC/sv_SLOG.lua --Command logger, catches ANY unknown concommand run on clients, including lua_run_cl
lua/HAC/sv_SpinMeRound.lua --Used in sv_UCmd to spin client right round like a record
lua/HAC/sv_SteamAPI.lua --Steam web API, handles shared account kicking, VAC bans etc
lua/HAC/sv_StreamHKS.lua --Hack stealer and keyword filename banner. Calls KWC
lua/HAC/sv_TakeSC.lua --Screenshot handler, saves to specified folder as well as player's h_ folder
lua/HAC/sv_TwoScore.lua --Add any cheaters from the TwoScore banlist
lua/HAC/sv_UCmd.lua --UserCmd seed/random detector.
lua/HAC/sv_UTF.lua --Block connect of clients with certain Unicode chars in their name
lua/HAC/sv_VFFT.lua --Block SendFile/ReceiveFile of any non-spray file
lua/HAC/sv_XDetector.lua --Old metatable check left over from GM12, but still works


--- Lists ---
lua/lists/cl_B_HAC.lua --Main clientside blacklist
lua/lists/cl_W_HAC.lua --Main clientside whitelist
lua/lists/sh_W_GSafe.lua --Whitelist of all globals
lua/lists/sh_W_HKS.lua --Files from HKS that are not cheats
lua/lists/sh_W_HKS_Old.lua --2nd list when the first got too big
lua/lists/sv_AdvDupe.lua --Old list of good/bad entities that can be duped. Not in use, never bothered to fix it.
lua/lists/sv_Buff.lua --Good/bad binds
lua/lists/sv_Cmds.lua --Bad commands, see sv_BannedCmds
lua/lists/sv_CMod.lua --Keywords for .DLL checks
lua/lists/sv_CVList.lua --See sv_CVL
lua/lists/sv_ECheck.lua --Main keyword list for filenames. Bad/Good/False positive
lua/lists/sv_EyeAngles.lua --Paths that can use SetEyeAngles/SetViewAngles. See en_hac
lua/lists/sv_FalsePos.lua --False positive list, skip these
lua/lists/sv_SkidList.lua --All the cheaters, lots!
lua/lists/sv_SLOG.lua --See sv_SLOG, good/bad.

--- Resources ---
--- Materials ---
materials/hac/hac.vmt --Used to mark the ban position on certain maps, see sv_Boom
materials/hac/spray.vmt
materials/hac/spray.vtf

materials/vgui/notices/oldcleanup.vmt --Used for HAC.GAN messages
materials/vgui/notices/olderror.vmt
materials/vgui/notices/oldgeneric.vmt
materials/vgui/notices/oldhint.vmt
materials/vgui/notices/oldundo.vmt
materials/vgui/notices/oldcleanup.vtf
materials/vgui/notices/olderror.vtf
materials/vgui/notices/oldgeneric.vtf
materials/vgui/notices/oldhint.vtf
materials/vgui/notices/oldundo.vtf

--- Sounds ---
sound/hac/big_explosion_new.mp3 --Just as they get banned
sound/hac/computer_crash.mp3 --sv_Crash
sound/hac/csi_2.mp3 --Old, replaced with highway_to_hell
sound/hac/highway_to_hell.mp3 --Plays on everyone else when a player gets banned: https://www.youtube.com/watch?v=P96uAcTuGVc
sound/hac/horns_new.mp3 --sv_BSoD
sound/hac/no_no_no.mp3 --sv_HAC
sound/hac/really_cheat.mp3 --sv_HAC/bc_EatKEysAll
sound/hac/right_round_baby.mp3 --sv_SpinMeRound
sound/hac/serious_loud.mp3 --sv_Serious
sound/hac/sorry_exploding.mp3 --sv_SkidCheck
sound/hac/still_not_working.mp3 --sv_HAC
sound/hac/test_is_now_over.mp3 --sv_SeldExists
sound/hac/tsp_bomb_fail.mp3 --sv_SkidCheck
sound/hac/tsp_run_around.mp3 --sv_EatKeys
sound/hac/whats_in_here.mp3 --sv_StreamHKS
sound/hac/you_are_a_horrible_person.mp3 --sv_HAC
sound/hac/balls_of_steel.wav --sv_BallOfSteel
sound/hac/extra_ball.wav --sv_BallOfSteel
sound/hac/play_balls1.wav --sv_BallOfSteel
sound/hac/play_balls2.wav --sv_BallOfSteel
sound/hac/eight.wav --sv_Serious/bc_EatKEysAll

=== Stats ===

] hac_lines

::::     :::: :::::::::: ::::::::  ::: ::::    :::  ::::::::  
+:+:+: :+:+:+ :+:       :+:    :+:     :+:+:   :+: :+:    :+: 
+:+ +:+:+ +:+ +:+       +:+        +:+ :+:+:+  +:+ +:+        
+#+  +:+  +#+ :#::+::#  +#++:++#++ +#+ +#+ +:+ +#+ +#+        
+#+       +#+ +#+              +#+ +#+ +#+  +#+#+# +#+        
#+#       #+# #+#       #+#    #+# #+# #+#   #+#+# #+#    #+# 
###       ### ###        ########  ### ###    ####  ########  

=== Total counts for all 111 files in 7 catagories ===
    Bytes                 - 1.75 MB
    Tables                - 4,910
    Files                 - 112
    CComment              - 379
    FixMe                 - 33
    Locals                - 2,024
    Lines                 - 58,036
    Lines no Lists        - 30,543
    Functions             - 971
    Blank                 - 6,248
    Comment               - 1,607
    Plugins               - 67
    Modules               - 12
    Hooks                 - 75
    Permabans - IP        - 77
    Permabans - SteamID   - 248
    Total skiddies        - 6,692
    Total unique bans     - 311
    Bans since GMod 13    - 852
    Failure messages      - 171
    Size of hac_log.txt   - 14.48 MB
    Size of hac_init.txt  - 3.14 MB
=== End ===


Main CL
    Bytes     - 48.32 KB
    Tables    - 65
    Files     - 1
    CComment  - 15
    Blank     - 255
    Locals    - 347
    Comment   - 6
    Functions - 104
    Lines     - 1,856
    FixMe     - 0


Code
    Bytes     - 51.8 KB
    Tables    - 54
    Files     - 19
    CComment  - 5
    Blank     - 612
    Locals    - 220
    Comment   - 8
    Functions - 79
    Lines     - 2,368
    FixMe     - 0


Load CL
    Bytes     - 5.16 KB
    Tables    - 1
    Files     - 2
    CComment  - 0
    Blank     - 45
    Locals    - 24
    Comment   - 1
    Functions - 8
    Lines     - 202
    FixMe     - 0


Base
    Bytes     - 131.33 KB
    Tables    - 491
    Files     - 7
    CComment  - 56
    Blank     - 737
    Locals    - 378
    Comment   - 211
    Functions - 175
    Lines     - 5,226
    FixMe     - 3


Main SV
    Bytes     - 44.32 KB
    Tables    - 54
    Files     - 1
    CComment  - 53
    Blank     - 360
    Locals    - 54
    Comment   - 213
    Functions - 37
    Lines     - 1,611
    FixMe     - 8


Lists
    Bytes     - 1.11 MB
    Tables    - 3,889
    Files     - 15
    CComment  - 18
    Blank     - 538
    Locals    - 23
    Comment   - 56
    Functions - 10
    Lines     - 30,543
    FixMe     - 1


Plugins
    Bytes     - 373.65 KB
    Tables    - 356
    Files     - 67
    CComment  - 232
    Blank     - 3,701
    Locals    - 978
    Comment   - 1,112
    Functions - 558
    Lines     - 16,230
    FixMe     - 21
=== The end ===

I that hope someone finds all this information useful.

A lot of it certainly isn't public, and the people who do know about what you'll soon read keep it to themselves for obvious reasons. You should now download HAC's source code and begin. I'd start with sv_HAC & en_HAC, then the plugins/DLLs. A find-in-files feature is essential here.

Thanks go to:

Willox (STEAM_0:0:19321794) -- Advice/code/testing/ideas, and without whom, hundreds of cheaters would still have their marbles.

Fangli (STEAM_0:0:19962914) -- For the oubhack takedown, sharing his banlist/code ideas/testing.

Sykranos (see hac_nosend.lua) -- For years of leaking me hundreds of private cheats & modules, destroying Tyler's reputation, and being a double agent in many cases to obtain private code.

G-Force (STEAM_0:1:19084184) -- For leaking Sethhack's "cloud scripts" to me, and helping with the SH problem in 2012.

Discord (STEAM_0:1:24101589) -- For helping understand upvalues and the stack in 2011.

C0BRA (STEAM_0:0:32164051) -- For failing to bypass HAC many times in 2010, inspiring me to create sv_SelfExists.

TGiFallen (STEAM_0:0:26495621) -- For ideas and advice.

Lutis -- For making sure that I didn't accidentally ban all the Mac users!

Fucks go to:

JamieH (STEAM_0:0:25687098, STEAM_0:0:37652268, STEAM_0:1:86271998) -- For stealing and leaking HAC's clientside code on Facepunch (TWICE), for copy+pasting a C++ hack & Lua file stealer, for buying & using Sethhack in 2012, for buying the UnitedHosts.org domain before I could complete the checkout and then trying to sell it back to me in 2012, and for being a cheating scumbag who knows nothing but how to piss people off and cause drama. Fuck off you absolute asshole.

ZeroTheFallen (STEAM_0:1:38717786) -- For being a cheating minge, writing backdoor'd addons, profiting from the cheating problem, stealing and leaking HAC's clientside files on Hackforums, and using hacks on my server then claiming that he didn't.

niller303 (STEAM_0:1:64607538) -- For stealing and leaking HAC's clientside files on Hackforums, skidding a C++ hack & file stealer from meep's/oubhack's code.

Nanocat (STEAM_0:1:42964759, STEAM_0:0:57521974) -- for writing a C++ hack, stealing HAC's clientside files.

"key event coder" (see hac_nosend.lua, too many alts to list) -- for copy+pasting and then selling a C++ GMod cheat, claiming that it bypasses HAC (it does not), then DDoSing my server.

Oub (STEAM_0:1:34029133, STEAM_0:1:24452164) -- For trying to sell hacks and steal clientside files. No you don't.

MeepDarknessMeep (see hac_nosend.lua) - for stealing and leaking HAC's clientside files to friends, which ended up on Hackforums, writing and giving away/selling C++ cheats, and trying to cheat on my server with 8 alt accounts in the same fucking night.

Tyguy (see hac_nosend.lua) -- For being a 12 year old skiddie that copy+pastes code and gets given cheats by people who should know better.

Grey Helios/LordOfGears (see hac_nosend.lua) -- Stealing HAC's clientside files, writing/giving away a C++ hack, helping skids.

Deus3xitium (STEAM_0:0:52004216, STEAM_0:0:68148834) -- For constant bullshitting, and having access to code and hacks that he doesn't want to share to help development of HAC.

Snowboi/Kasper (STEAM_0:1:69145936, STEAM_0:0:40291467) -- For selling a copy+pasted piece of crap called gDaap (get their database in the Booty).

DigitalInsanity/Spirit (STEAM_0:1:23097032, STEAM_0:1:19522344) -- For having access to Nanocat's hack source but refusing to help. Fuck off.

Lenny (STEAM_0:0:30422103, STEAM_0:1:68284745) -- For stealing HAC's clientside files, giving skids code, posting stuff he shouldn't, and trying to prove his pack of cheat scripts aren't cheats.

Leystryku (see hac_nosend.lua) -- For writing a file stealer, writing C++ hacks, giving hacks to tyler, profiting from the cheating problem.

nerve (STEAM_0:1:76354629, STEAM_0:0:4268975, STEAM_0:0:12356551, and probably more) -- Skidding a file stealer from oubhack.

And above all, to Garry -- For constantly breaking things, changing stuff without telling people, not documenting all changes in his "updates", not listening to improvements/bug fixes/complaints or even fucking common sense, having zero care for anyone in the anti-cheating community, and for writing the best sandbox game of all time.

Anyone who I've forgotten, you're probably in the booty archive.

See hac_nosend.lua for the worst of the worst (permaban these people from any server that you own), and sv_SkidList for everyone else.

If you run a server and would like to prevent all these assholes from joining, check out my SkidCheck addon here on GitHub.

And so this ends GMod hosting for me. I'll probably still be playing this game, as there's amusement to be found in the thousands of badly-run RP servers. But it'll never be the same as running my server. I still feel mixed about shutting down, having been with this game & community for so long.

Goodbye, and Garry, if you ever read this, listen to the community for a change instead of "my game my responsibility" in regards to the cheating problem that still exists and that you're currently doing nothing about. I'd start by talking to Willox and me.

=== HAC setup instructions ===

Must have write access to C:/hac_totalbans.txt
"HeX's AntiCheat" goes in addons/, the modules go in lua/bin.
Open sv_HAC.lua and edit HAC.Conf to match your environment. Add your own Steam API key and set the file paths.
Don't bother if the gamemode isn't Sandbox. You'll have to rewrite it all yourself if it isn't.
Do not use ULX, or remove its stupid metatable on _G if you do.
READ ALL THE CODE before you even attempt to start it up. Understand how it works.
Remove the noob blocker
Remove the contents of sh_W_HKS, BUT KEEP AT LEAST ONE LINE.
Remove the contents of sh_W_GSafe.lua, this needs to be re-generated.
Remove only the volatile tables in cl_W_HAC, these also need to be re-generated.
Start the server, it will patch a few files and restart the map. You may need to exit the SRCDS process for it to work properly due to the last GMod update's latest fuckup breaking timers on map change.
Fix any serverside errors.
Changing the line count or even shuffling functions around in en_hac will result in a ban. Make sure to update sv_LPT/sv_HAC if you do this.
Do hac_silent 1 and join, wait for the few thousand ban reports. This will take some time. You may have to edit out the removing of globals from en_hac if the game crashes on spawn/everything is nil.
Whitelist all the reports:
ff_* files go in sh_W_HKS
_G* files go in sh_W_GSafe
Most of the others go in cl_W_HAC, work it out.
Restart the server and rejoin. This time edit the RCount/GCount/GCICount/GCBCount in sv_HAC.
Mac users have different fonts. Make sure to test on Mac OS - OR IT WILL BAN ALL MAC USERS!
=== Critical notes & daily maintenance ===

You'll have to keep up to date with the following:

Review and empty the SCFolder every 45MB (~600 screenshots or so).
A lot of players will create an H_* folder in /data. Add any ff_* files to a folder called "data/ff" and run "ff" on SRCDS, then add the data from "data/hks.txt" to sh_W_HKS, delete ff and hks.txt and restart the server.
cc_*/cv_* files go in sv_CVList.
If someone gets banned, their H_* folder will have an IS_BANNED.txt file. See their ban_* file for what caused it. Also add their ff_* files etc as usual.
Add any sk_* file entries to sv_SkidList.
If you notice new cheats by the kwc_* file, add their filename keywords to sv_ECheck to trigger a detection. Careful of "wooden_shack" etc having "hack" in the name. See sv_ECheck.
You can contact me on Steam for any advice/questions about HAC or how any of it works if you want, but I *ABSOLUTELY WILL NOT* help kids and/or people who can't code set it up.

-=[UH]=- General HeX.

