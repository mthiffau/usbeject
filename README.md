[ WARNING: I have received several reports of this not working for people. I'm leaving this up in case it's a helpful starting point even if it is not working as-is. I seem to recall needing a paid teir license for Visual Studio in order to have support for these system APIs, and I no longer have access to that. I also haven't written any C# in about 2.5 years (after having only written in it for a few weeks), so I'm probably not the formost expert on how to go about fixing this for your own particular Windows version or hardware architecture. 

Since a bunch of people seem to be landing here and trying this code despite the reported issues, I'm happy to accept pull requests if the changes seem legit and are legitimately documented (as I cannot test the changes myself), so that future "yous" might find something working (or closer to it). Of course, one of you could be a total star and write some tests and some git push hooks to run the tests as a presbumit, so that it's easier to tell when future patches are good :P I'm half kidding, but you'll get credit in the README if you do. ]

# usbeject
C# code to safely eject removable storage (Windows 8.1, compiled 32-bit)

This is a class library of code stolen from a codeprojects page, and modified to fix a bug where it wasn't ejecting the drive it
claimed to be ejecting. All the copyright headers in it are from the original author. I'm providing this code here since aparently
the codeprojects page is dead (and the code posted there was broken anyways). 

I was running this code on Windows 8.1 Embedded Industrial (64-bit) compiled as a 32-bit dll. I received a pull request from somebody who looked like they knew what they were doing which apparently makes the code compile/work for AnyCPU. I have not tested this.

I'm distributing this software with NO WARRANTY and NO GUARANTEE of suitability for any purpose, etc, etc, yada, yada, don't sue me.

Usage example pulled from my code:

    VolumeDeviceClass volumes = new VolumeDeviceClass();
    foreach (Volume vol in volumes.Devices)
    {
      if (vol.LogicalDrive.Equals(eject_drive))
      {
        eventLog.WriteEntry("Attempting to eject drive: " + cur_write_drive);
        vol.Eject(false);
        eventLog.WriteEntry("Done ejecting drive.");
        break;
      }
    }
