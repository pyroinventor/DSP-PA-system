# DSP-PA-system

I had been playing bass in a band with three of my friends for about a year when we decided to start trying to get some gigs. One crucial peice of equipment we lacked was a PA system. A powered pair of PA speakers or passive PA + amp combo was going to cost anywhere from $500 to $1000+. This was out of range for our non existent budget, so I decided to put some of my speaker design experience to use and build a system from scratch. I was able to buy the speaker drivers, amps, and misc. parts like terminal cups and top hat mounts for around $200. Add some tripod stands, DIY power supply from server PSUs, and an aliexpress DSP board that runs SigmaDSP and you have a fully DSP controllable 700w PA system for less than $300.
![bandPA](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/95359b90-6752-4ae7-a7f2-790735bbb98a)
Here it is at our first paid gig :)

## Description

The speakers are 2-way, and I wanted to make them DSP controllable and actively crossed to allow as much flexibility as possible in tuning the setup to different environments. There are 3 amplifier boards: a 2x300W class D amp for the woofers, and two mono 50W class D amps, one for each tweeter. This allows me to send a seperate input to each speaker driver from the DSP. The amps and DSP are housed in a small plastic storage bin. To power the amps, there is a DC input jack to be used with a modest 24V 70W laptop style power supply, or an XT60 connector to hook up to the 24V 920W supply made from two server PSUs in series. I considered adding a subwoofer, but decided that for our gigs the bass amp would cut it. 

## Build Process

I already had the woofers as they were scrapped from another project (see my DIY PA V1 repo), so I began by designing an enclosure to fit their TS parameters as well as possible without being too big or inconveniently shaped. I settled on a fairly traditional 6-sided shape that could be mounted on a tripod or rested on one of its 45 deg angles to tilt up. I calculated the woofer chamber volume with WinISD:

![Screenshot 2024-04-05 094736](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/cadf97f6-ecdd-4658-a278-f7e953e539f4)


After taking into account the woofer, tweeter, and internal bracing displacement, I cut the pieces out of some plywood and floorboards I had laying around. Maybe not the best isotropic Hi-Fi material, but it got the job done. Here are the shells:

![paBoxes](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/c94d6b6d-0c6c-4e34-9675-9b442dcaffa3)
Wood filler in the screw holes / brad nail dents

## Frequency Response and DSP

After the drivers were installed, I ran some acoustic tests with my calibrated mic and REW:

![Screenshot 2024-04-05 095857](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/2019a751-6236-406b-a4bf-2d01d3579bfc) \
Impedance response captured with soundcard and custom measurement rig
![Screenshot 2024-04-05 095915](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/ce914d01-4f56-4f3c-ab88-3f6066af6818) \
Woofer frequency response captured with calibrated mic

I then imported the frequency response and impedance curve tests into VituixCAD to test some different active, passive, and digital crossover ideas: 

![Screenshot 2024-04-05 095515](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/b671aa50-3bb1-4981-bebb-90facc50d117) \
Uploading FR and Z curve files
![Screenshot 2024-04-05 095418](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/59a52e2e-6f6b-4907-a90a-1b53cb538e3e) \
Analog crossover with discrete components
![Screenshot 2024-04-05 095430](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/701e2087-d0bf-46e0-bc5d-05e1c73903d7) \
Op amp based active crossover
![Screenshot 2024-04-05 095446](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/a0bfd59d-5f82-41c0-a746-458ff4c00d69) \
Digital crossover to simulate DSP

Using this insight, I put together a simple high pass RC filter for the piezo horn loaded tweeter: 
![Screenshot 2024-04-05 105150](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/a6fff3a2-81a1-4f82-b88f-b3e4f7d78eee)
(not strictly required but it can reduce some "piezo-y" sound artifacts) \ 
That peak at 5kHz proved difficult, so I put together this notch filter:
![Screenshot 2024-04-05 104936](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/220b681e-26cf-4ffa-bd32-ae5d674a484f)
But ended up going with the simple high pass and leaving the notch filtering to the DSP.

Here is one revision of the SigmaStudio DSP crossover setup
![Screenshot 2024-04-04 171249](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/f6e9ae30-e842-4d70-8349-78c048d0b5a2)

And here is the response I got before tuning in the DSP settings:
![Screenshot 2024-04-05 095927](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/ca4832f8-3ac3-46cd-95c7-37310ea7d953)

## Usage

To set up in a new location, I simply mount the speakers on their tripods or set them up on the floor, take some frequency response measurements with REW, transfer the results into SigmaDSP and upload the customized profile onto the DSP board. I'll usually take another FR measurement to make sure everything looks hunky dory, then I can move on to setting up rest of music gear. Depending on the venue, I'll use either the laptop PSU or the beefy server supply. Usually the laptop supply is fine for vocals in a small venue.

![livingroomPA](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/9cf5e4dd-11a6-4f17-bcbf-5930c1889df7)
Here is the system being used for a little acoustic set in my livingroom. \
Maybe not the most replicable setup, but hopefully it serves as inspiration for anyone who wants to build something similar. Thanks for reading!


