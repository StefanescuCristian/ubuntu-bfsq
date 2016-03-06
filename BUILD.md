Ubuntu Kernel Source (http://kernel.ubuntu.com/git/ubuntu/ubuntu-xenial.git) with BFS and BFQ from Alfred Chen's branch (https://github.com/cchalpha/linux-gc)

Config changes from Ubuntu stock:
    - HZ_300 (Arch Linux)
    
    - Desktop Preemption (Arch Linux)
    
    - bfs + bfq enabled by default
    
    - disabled NUMA (I recommend leaving it disabled if you have only one _physical processor_)
    
    - disabled HyperThreading awareness (you should enable it if you CPU supports HT)
    
    - disabled some debugging
    
    - graysky native gcc optimizations (https://github.com/graysky2/kernel_gcc_patch). Defaults to Generic, you should choose Native when building

Build:
    - `cp config64 .config`
    - `make menuconfig` (to make what changes you like)
    - `time make-kpkg -j6 --initrd --rootcmd fakeroot kernel_image kernel_headers modules_image`

NOTE:
    - you *must* use the latest version of make-kpkg (kernel-package) from http://packages.ubuntu.com/xenial/kernel-package
    older versions have a bug (https://bugs.launchpad.net/ubuntu/+source/kernel-package/+bug/1308183) preventing build
    
    - I recommend using GCC > 5.0 (https://askubuntu.com/questions/618474/how-to-install-the-latest-gcurrently-5-1-in-ubuntucurrently-14-04
    or https://askubuntu.com/questions/623350/how-to-install-g-5-1-on-ubuntu-desktop-15-04-64-bit )
    
    - It seems that some AMD options got disabled in the config, will fix in a next release (enable them manually if you use AMD).
    Default Ubuntu config for AMD disabled options:
        - CONFIG_X86_AMD_FREQ_SENSITIVITY=m
        - CONFIG_AMD_MCE_INJ=m
        - CONFIG_AGP_AMD64=y

Install:
    `sudo dpkg -i ../linux-*`
Make-kpkg names the files something like linux-image-4.4.4+_4.4.4+-10.00.Custom_amd64.deb and copies them in the upper folder from where the source resides.
