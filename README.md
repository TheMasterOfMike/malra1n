# Windows checkra1n potential malware write-up (codename: malra1n)

Hi everyone, as I know some people have been made aware of, I have been looking into the Windows checkra1n garbage over the past day or so. What I am sharing today is a whole look at what I have found over the past day or so.

## Strike 1: Going against checkra1n team's wishes

So, let's start off by going through what checkra1n team wanted:
> Siguza (4/12/2022, 7:12 PM CST): but I did ask for the "checkra1n" name to not be used, to make it clear that this is a 3rd party thing
Very reasonable, correct? Obviously, yes, you wouldn't want a third-party project to be directly associated to the real thing.

So what do these individuals decide to do? Change (mostly) everything internally about checkra1n... but not change a single exterior thing, by this, I mean:
- The executable is named "checkra1n.exe"
- The icon used is still the normal checkra1n icon
- The UI is basically an equivalent clone of the UI used in the official versions of checkra1n

When asked about this, the developer behind this tool said:
> (I am not sharing this devs name) (4/16/2022, 4:56 AM CST): Exe can be renamed not problem, but inside the app there isn’t the name. And no he didn’t ask to not use the icon.

You would think, however, that "making it clear that this is a 3rd party thing" would mean more than just change a couple names in-app, right (even if not directly brought up)?

## Strike 2: A horde of trojan/backdoor detections

While we were in the middle of looking into this, we saw a bunch of reports about Windows Security, among other tools, were detecting trojans and a backdoor.

So I decided to take a look, and while I listed some of them in the original discord message you might have seen from me, Windows Security ended up detecting two more trojans after I sent that message and shared it, these are Bolded in the following messages.

(Note: All messages/threat names come from Windows Security, you may find different names depending on what tools you use to look into this).

**Trojans**:
- **Trojan:Win32/AgentTesla!ml**
- **Trojan:Win32/Tilevn.A**
- Trojan:Win32/Sabisk.FL.B!ml
> This program is dangerous and executes commands from an attacker.

**Backdoor**:
- Backdoor:Win32/Bladabindi!ml
> This program provides remote access to the computer it is installed on.

To not repeat what I said in my original message that (because imo that would take way too long), there are a bunch of reasons why not only is this incredibly strange, but it seems incredibly unlikely that these could just be "Windows being Windows" things.

The dev of this utility proceeded to (after the image spread around a fair bit) bring up why they claim it is being detected by various utilities (Just to note before continuing, VirusTotal finds checkra1n.exe has something in 17/69 cases and finds the entire zip of contents has something in 33/69 cases)

The dev says this is because (responses attached):
- Code Signing Certificate not being present - This is, for the most part, false. This is because that, while yes, some tools will whine about this, this does not cause 'false' Trojan and Backdoor detections.
- As a result of the obfuscation - This is technically true, but I also wouldn't consider it a smoking gun that "oh my god this isn't a malicious program at all" - We have reason to believe that all of them at least have the potential of being tied to obfuscation in some manner... except for Trojan:Win32/Tilevn.A (and even then, the others shouldn't be entirely ruled out, as inherently they were marked as threats because they were tied to actual malicious programs, right?)

## Strike 3: Administrator Privileges stupidity

A couple hours ago, I decided to try looping back into the root of the source of this program in the first place - the bypass utility - in case I forgot something that is of significance.

Around two or so seconds after I open it, I get greeted with a nice UAC prompt... accepting it reopens the utility with administrative privileges... denying it crashes it with some error about checking for updates. Additionally, I also notice the ad at the top of the app does not load until you accept the UAC and let it reopen the utility.

Think I'm lying? Here, have a video https://streamable.com/2ne7o2. This video also shows some stranger behavior where after closing the app, the app will refuse to actually open again for around 15-20 seconds or so.

Even if you ignore the last section of this write-up, and hypothetically assume that everything is related to obfuscation or code signing certificate bullshit, this is extremely questionable and, given the other questionable portions of this, should at least be a huge red flag.

## CONCLUSION:

I personally believe that, even ignoring the stuff about potential Trojans and Backdoors, this is still highly suspicious software (and if you choose not to ignore that stuff, this is basically guaranteed suspicious software. At best, this is god-awfully coded, to the extent where it has so many faults in regards to how it handles everything. At worst, this is a giant puddle of malware that should absolutely be avoided at all costs. (And I'll give you a hint, given the questionable morality of many individuals, including the people behind this utility, I have high reason to believe this is closer to the latter than it is to the former.)
