---
title: Using NVIDIA Optimus switchable graphics with GTX 860M on Ubuntu 15.04
slug: using-nvidia-optimus-switchable-graphics-with-gtx-860m-on-ubuntu-15-04
date_published: 2015-11-30T00:00:00.000Z
date_updated: 2015-11-30T00:00:00.000Z
---

|

| A long running older project  | A relatively newer project |

| Needs command-line invocation | Is a GUI solution (CLI method available too) |

| A per-process implementation  | A session-wide implementation |

| Focus on power saving  | Focus on high performance from discrete GPU |

| Have to explicitly run each process
with bb to benefit from NVIDIA GPU | All processes in current session 
run either on NVIDIA or all on Intel |

**NOTE**: Before installing any kernel level drivers (either prime or bumblebee), always make sure you have updated `linux-headers-generic`

### [Using NVIDIA Prime (nvidia-prime)](Using NVIDIA Prime (nvidia-prime))

So I set off on  path to use NVIDIA Prime.

Using **nvidia-340-updates** driver from the xorg-edgers ppa, as of 30th Nov, 2015,

this works perfectly. So let's go through the steps to make it work.
**UPDATE**: The latest drivers for 860M is 352.63, and you can hence use ***nvidia-352-updates*** instead of ***nvidia-340-updates***

First let's do away with bumblebee if you've installed it

    sudo apt-get remove --purge bumblebee* primus nvidia*
    

Perform a reboot here, so your system safely configures itself to run on Intel/mesa.

Let's add edgers' repo and install nvidia-340.

    sudo add-apt-repository ppa:xorg-edgers/ppa
    sudo apt-get update
    sudo apt-get install nvidia-340-updates
    

Again, it is safe to perform a reboot here.

Let's get the prime and settings packages now.

    sudo apt-get install nvidia-settings nvidia-prime
    

Now before we reboot, we need to make sure of one thing,

that is nvidia is loaded before bbswitch always.

For that, edit `/etc/modules` and add these two lines

    nvidia-304-updates
    bbswitch
    

Now reboot your system. If all has gone right, you can switch between NVIDIA and Intel using the `nvidia-settings` configuration utility. **You have to logout and login every time you switch graphics cards. Also unlike optirun/primusrun, when you have enabled NVIDIA, everything in your current sessoin works with NVIDIA and similarly for Intel. To switch graphics, you have to open the *nvidia-settings* panel and switch graphics card, and logout and login back again.**.

### [ Using Bumblebee (bumblebee-nvidia) ]( Using Bumblebee (bumblebee-nvidia) )

After sorely missing bumblebee for some days, I took another hit at it. And was able to make it work with NVIDIA's 352.63 drivers. The reason was that, I mainly prefer to run on Intel HD Gfx, and for certain cases (like the OBS broadcaster, Lightworks, Android emulators) need NVIDIA, as an on-demand solution (and not a login/logout solution).

Here were the steps to get it to work. First need to purge away `nvidia-prime` as they both don't work together

    sudo apt-get remove --purge nvidia-prime
    

Now install `nvidia-352-updates`

    sudo apt-get remove --purge nvidia*
    #optional, not really needed as any nvidia driver uninstalls the previous
    sudo add-apt-repository ppa:graphics-drivers/ppa
    sudo apt-get update
    sudo apt-get install nvidia-352-updates
    

Let us go forward and now install bumblebee

    sudo apt-get install bumblebee bumblebee-nvidia bbswitch-dkms primus
    sudo systemctl enable bumblebeed #Enable bumblebee daemon in systemd
    sudo gpasswd -a $USER bumblebee #add yourself to bumblebee group
    

We need to make sure the i915 and bbswitch drivers get loaded to the kernel, so edit the file `/etc/modules` and the following

    i915
    bbswitch
    

Now is the important part where we need to make sure that Bumblebee handles loading/unloading of Gfx modules. So it has to be made sure that all installed graphics drivers including `nouveau` and `nvidia-352-updates` is blacklisted. Check the file `/etc/modprobe.d/bumblebee.conf` and ensure the following lines present

    blacklist nouveau
    blacklist nvidia-352
    blacklist nvidia-352-updates
    blacklist nvidia
    

*If these lines are not present, the kernel will automatically load the modules and bumblebee won't be able to handle the load/unload of modules.*

Now as a final step we need to inform Bumblebee which version of Nvidia drivers are we using, for doing that check the contents of the file `/etc/bumblebee/bumblebee.conf`

    
    # Configuration file for Bumblebee. Values should **not** be put between quotes
    
    ## Server options. Any change made in this section will need a server restart
    # to take effect.
    [bumblebeed]
    # The secondary Xorg server DISPLAY number
    VirtualDisplay=:8
    # Should the unused Xorg server be kept running? Set this to true if waiting
    # for X to be ready is too long and don't need power management at all.
    KeepUnusedXServer=false
    # The name of the Bumbleblee server group name (GID name)
    ServerGroup=bumblebee
    # Card power state at exit. Set to false if the card shoud be ON when Bumblebee
    # server exits.
    TurnCardOffAtExit=false
    # The default behavior of '-f' option on optirun. If set to "true", '-f' will
    # be ignored.
    NoEcoModeOverride=false
    # The Driver used by Bumblebee server. If this value is not set (or empty),
    # auto-detection is performed. The available drivers are nvidia and nouveau
    # (See also the driver-specific sections below)
    Driver=nvidia
    # Directory with a dummy config file to pass as a -configdir to secondary X
    XorgConfDir=/etc/bumblebee/xorg.conf.d
    
    ## Client options. Will take effect on the next optirun executed.
    [optirun]
    # Acceleration/ rendering bridge, possible values are auto, virtualgl and
    # primus.
    Bridge=auto
    # The method used for VirtualGL to transport frames between X servers.
    # Possible values are proxy, jpeg, rgb, xv and yuv.
    VGLTransport=proxy
    # List of paths which are searched for the primus libGL.so.1 when using
    # the primus bridge
    PrimusLibraryPath=/usr/lib/x86_64-linux-gnu/primus:/usr/lib/i386-linux-gnu/primus
    # Should the program run under optirun even if Bumblebee server or nvidia card
    # is not available?
    AllowFallbackToIGC=false
    
    
    # Driver-specific settings are grouped under [driver-NAME]. The sections are
    # parsed if the Driver setting in [bumblebeed] is set to NAME (or if auto-
    # detection resolves to NAME).
    # PMMethod: method to use for saving power by disabling the nvidia card, valid
    # values are: auto - automatically detect which PM method to use
    #         bbswitch - new in BB 3, recommended if available
    #       switcheroo - vga_switcheroo method, use at your own risk
    #             none - disable PM completely
    # https://github.com/Bumblebee-Project/Bumblebee/wiki/Comparison-of-PM-methods
    
    ## Section with nvidia driver specific options, only parsed if Driver=nvidia
    [driver-nvidia]
    # Module name to load, defaults to Driver if empty or unset
    KernelDriver=nvidia-352-updates
    PMMethod=auto
    # colon-separated path to the nvidia libraries
    LibraryPath=/usr/lib/nvidia-352-updates:/usr/lib32/nvidia-352-updates
    # comma-separated path of the directory containing nvidia_drv.so and the
    # default Xorg modules path
    XorgModulePath=/usr/lib/nvidia-352-updates/xorg,/usr/lib/xorg/modules
    XorgConfFile=/etc/bumblebee/xorg.conf.nvidia
    
    ## Section with nouveau driver specific options, only parsed if Driver=nouveau
    [driver-nouveau]
    KernelDriver=nouveau
    PMMethod=auto
    XorgConfFile=/etc/bumblebee/xorg.conf.nouveau
    
    

You need to change the lines highlighted in red accordingly.

And finaaaaaaly, reboot, and enjoy bumblebee.

To run any program with NVIDIA use `primusrun <program name>`. By default everything runs with Intel

HD Graphics, and NVIDIA card stays off.
