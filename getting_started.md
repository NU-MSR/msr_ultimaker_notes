# Software to Install #

The software that the Ultimaker recommends is called
[cura](https://ultimaker.com/en/products/cura-software). Cura is responsible for
*slicing* a 3D model into layers and generating the GCode required to print your
part. To install cura, visit
[this page](https://ultimaker.com/en/products/cura-software) and select
download. If you are on your MSR laptop, be sure that the file that they
automatically serve you is a 64-bit deb. Once the file is downloaded `cd` to
your download directory and install the package with `dpkg`. Your command should
look something like `sudo dpkg -i cura_15.04.2-debian_amd64.deb`. If the install
completes successfully, you should be able to launch cura just by typing `cura`
at a command line.
 
There are many other slicing software packages that are compatible with the
Ultimaker 2. In the mechatronics lab, they use
[Simplify3D](https://www.simplify3d.com/). If you have some reason to think that
MSR should get a copy of this, let
[@jarvisschultz](https://github.com/jarvisschultz) know.

# Generating a Solid Model #

The first step in creating a 3D print is to have a solid model of the object
that you want to print. Typically you are trying to generate a 3D model that is
a standard filetype -- likely, an STL file. Any 3D modeling software that is
capable of generating an STL file should be sufficient for this part. If you are
already an experienced SOLIDWORKS user, that would work great.

Here are a few free tools that work well in Linux that you can try as SOLIDWORKS
alternatives/supplements.

1. [Onshape](https://www.onshape.com/about-us): This is a cloud-powered,
   in-browser solid modeling tool. It is very similar to SOLIDWORKS and offers a
   free license.
2. [MeshLab](http://meshlab.sourceforge.net/): MeshLab is a great, free tool for
   viewing, simplifying, and working with STL files and other 3D data formats.
   It is installable via `apt-get`.
3. [Blender](https://www.blender.org/): Blender is an awesome, cross-platform,
   free software tool for 3D animation. Once you learn to use its somewhat
   complex interface, you can make amazing 3D models.

# Creating the gcode #

Once you have a 3D model, you need a piece of slicing software to generate the
code that the machine will use to actually print something. We will only discuss
cura.

### Loading Part in Cura ###

The first step is to open cura and select `File->Load model file` and select
your 3D model. Your model should automatically appear in the main window. The
next step is to orient and locate your part. Generally, you'll want this part in
the center of the print bed, and oriented in a passively stable configuration.
You need sufficient material on the bottom side to allow the piece to stick to
the print bed when you are printing. Note that if you have a lot of overhangs,
you'll want to be sure to enable printing of a support structure.

Note that you can add many parts to a single print volume. This can be helpful
for printing multiple copies of the same part, or a variety of parts at once.

### Adjusting and Choosing Settings ###

Cura has many settings governing things like print speed, fill volume, support
structure, and print bed adhesion structures. Going over all of these settings
is outside the scope of this document. Note that if you hover over an option in
cura it will give you a popup tooltip that describes what the setting does. You
can select `Expert->Switch to quickprint...` in the toolbar to remove most of
the options. You will be left with only a few presets. In an ideal world, these
presets would always *just work*, but in reality, for many parts, you will be
required to dig into the advanced options under `Expert->Switch to full
settings...` in order to achieve your desired part. One quick tip is that you
can visualize the toolpath that cura is actually generating by clicking the
`View mode` button in the upper right and selecting `Layers`.

Cura has [excellent documentation](https://ultimaker.com/en/support/software).

### Choosing a Material ###

Typically you will either be printing with PLA or ABS. The material you choose
will govern many of the settings that you will choose in cura. Here are a few
quick notes about PLA vs. ABS.

##### PLA #####

Generally, the rule of thumb is that you should always print with PLA. It sticks
to print beds better, it is easier to get dimensionally accurate prints, it can
print finer details, and it smells nice when you are using it. The primary
downsides of PLA (compared to ABS) are as follows:

1. It melts at lower temperatures. (Is your application going to expose your
part to a hot environment?)
2. PLA is not as amenable to post-printing machining/sanding/filing.
3. It isn't as strong as ABS.
4. It is more brittle than ABS.

##### ABS #####

ABS is tougher to get nice parts, it is more susceptible to warping/peeling, and
it stinks like melting plastic when used in a 3D printer. It is stronger, more
flexible, has better machinability, and is more temperature resistant than PLA.

# Printing a File #

After you have your model imported into cura, and set all of your options, it is
time to print!

### Loading Material ###

First, you'll need to make sure that the Ultimaker 2 is loaded with a roll of
your chosen material type filament. If the already-loaded filament is not what
you want, then you'll need to change the filament. This is done by using the
on-machine interface to navigate to `MATERIAL->CHANGE`. The on-machine display
will guide you through the process. The Ultimaker Get Started guide has a great
[set of instructions](https://ultimaker.com/nl/support/view/16955-changing-filament)
for loading filament.

By default the Ultimaker has settings built-in for the nozzle temperatures,
feedrates, and print bed temperatures for both ABS and PLA. Be sure to correctly
select the type of material you are loading.

### Prepping the Print Bed ###

Generally for PLA you don't need to do much in terms of prepping the print bed
other than making sure it is clean. If the bed is dirty you can clean it with
damp paper towels. If it is really dirty, you can actually remove the glass and
clean it with glass cleaner or rubbing alcohol. Check out
[this page](https://ultimaker.com/nl/support/view/156-installation) to see how
the glass comes out.

For ABS it is generally much more difficult to get a part to stay stuck to the
print bed surface during a print. Ultimaker recommends using a glue stick to
improve adhesion between ABS parts and the print bed. Check out
[Ultimaker's documentation](https://ultimaker.com/nl/support/view/16968-using-glue)
on when and how to use glue.

### Loading File ###

Once the bed is prepped, you are ready to actually print. The first step is
getting your gcode onto the SD card in the front of the machine. This can be
done by loading the SD card into a card adapter or card reader on your laptop,
and then manually copying a saved `.gcode` file to the SD card. Or you can use
cura to automatically save the `.gcode` file to the inserted SD card.

Note that printing directly from your computer to the Ultimaker is possible, but
it requires you to use a non-standard set of gcode interface. Unless the
constant copying to the SD card is really annoying you, I recommend just doing that.

# Maintaining the Printer #

The printer does need a little bit of regular maintenance. Check out the
official documentation on the following topics:

1. [Cleaning the glass plate](https://ultimaker.com/nl/support/view/152-cleaning-the-glass-plate)
2. [Maintaining the feeder](https://ultimaker.com/nl/support/view/151-the-feeder)
3. [Lubricating the axes](https://ultimaker.com/nl/support/view/150-lubricating-the-axes)
4. [Cleaning the Nozzle via the Atomic Method](https://ultimaker.com/nl/support/view/149-atomic-method)
5. [Leveling the Bed](https://ultimaker.com/nl/support/view/17083-bed-leveling)
