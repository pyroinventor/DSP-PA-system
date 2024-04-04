# DSP-PA-system

I had been playing bass in a band with three of my friends for about a year when we decided to start trying to get some gigs. One crucial peice of equipment we lacked was a PA system. A powered pair of PA speakers or passive PA + amp combo was going to cost anywhere from $500 to $1000+. This was out of range for our non existent budget, so I decided to put some of my speaker design experience to use and build a system from scratch. I was able to buy the speaker drivers, amps, and misc. parts like terminal cups and top hat mounts for around $200. Add some tripod stands, DIY power supply from server PSUs, and an aliexpress DSP board that runs SigmaDSP and you have a fully DSP controllable 700w PA system for less than $300.
![bandPA](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/95359b90-6752-4ae7-a7f2-790735bbb98a)
Here it is at our first paid gig :)

## Description

The speakers are 2-way, and I wanted to make them DSP controllable and actively crossed to allow as much flexibility as possible in tuning the setup to different environments. There are 3 amplifier boards: a 2x300W class D amp for the woofers, and two mono 50W class D amps, one for each tweeter. This allows me to send a seperate input to each speaker driver from the DSP. The amps and DSP are housed in a small plastic storage bin. To power the amps, there is a DC input jack to be used with a modest 24V 70W laptop style power supply, or an XT60 connector to hook up to the 24V 920W supply made from two server PSUs in series. I considered adding a subwoofer, but decided that for our gigs the bass amp would cut it. 

## Build Process

I already had the woofers as they were scrapped from another project (see my DIY PA V1 repo), so I began by designing an enclosure to fit their TS parameters as well as possible without being too big or inconveniently shaped. I settled on a fairly traditional 6-sided shape that could be mounted on a tripod or rested on one of its 45 deg angles to tilt up. After calculating the volume, taking into account the woofer, tweeter, and internal bracing displacement, I cut the pieces out of some plywood and floorboards I had laying around. Maybe not the best isotropic Hi-Fi material, but it got the job done. Here are the shells:

![paBoxes](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/c94d6b6d-0c6c-4e34-9675-9b442dcaffa3)
Wood filler in the screw holes / brad nail dents
![primerPA](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/9e03f837-f4b1-4e63-a27a-18f809befa2b)
First coat of primer

I put the enclosures together and ran some acoustic tests with my calibrated mic and REW, and the frequency response lined up pretty close to what I was anticipating. I also decided to add some carpeting to make them look a little more professional. To test the DSP, I set the speakers up in my basement and took some frequency response measurements. 

![basementPA](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/8faae4c6-4e4d-4515-91f8-6844d1a214c0)
This is from later, but you get the idea

I was then able to export the FR from REW and import it into SigmaStudio before inverting it. After some smoothing and tweaks to avoid crazy sub frequency amplification, I uploaded the EQ profile to the DSP and took another FR measurement to test if it worked. After a lot of troubleshooting, it did! To keep things simple, in addition to the EQ profile I integrated simple high / low pass crossovers to seperate the bass from the treble frequencies and keep the drivers happy.   

![Screenshot 2024-04-04 171249](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/f6e9ae30-e842-4d70-8349-78c048d0b5a2)
Here is an old version of the SigmaStudio setup

## Usage

To set up in a new location, I simply mount the speakers on their tripods or set them up on the floor, take some frequency response measurements with REW, transfer the results into SigmaDSP and upload the customized profile onto the DSP board. I'll usually take another FR measurement to make sure everything looks hunky dory, then I can move on to setting up rest of music gear. Depending on the venue, I'll use either the laptop PSU or the beefy server supply. Usually the laptop supply is fine for vocals in a small venue.

![livingroomPA](https://github.com/pyroinventor/DSP-PA-system/assets/77114423/9cf5e4dd-11a6-4f17-bcbf-5930c1889df7)
This is the setup I used for a little acoustic set in my livingroom. \
Maybe not the most replicable setup, but hopefully it serves as inspiration for anyone who wants to build something similar. Thanks for reading!


