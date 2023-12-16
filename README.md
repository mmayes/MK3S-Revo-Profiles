# MK3S+ Revo Profiles
E3D Revo nozzle profiles for the MK3S+ using PrusaSlicer

### Sources for settings
* 0.15 profile based on https://github.com/trudslev/prusaslicer-profiles
* [E3D article "How to Prepare Prusaslicer for Revo High Flow"](https://e3d-online.com/blogs/news/how-to-prepare-prusaslicer-for-revo-high-flow)
* [E3D Revo high flow slicer starter settings](https://e3d-online.com/pages/revo-high-flow-filament-starter-settings)
* [E3D Revo *non*-high flow slicer starter settings](https://e3d-online.zendesk.com/hc/en-us/articles/4777443097757-Filament-Starter-Settings)
* [Prusa article "Creating profiles for different nozzles"](https://help.prusa3d.com/article/creating-profiles-for-different-nozzles_127540)
* [E3D article "Start and End G-code for faster nozzle changes"](https://e3d-online.zendesk.com/hc/en-us/articles/4406857421213-Start-and-End-G-code-for-faster-nozzle-changes)


### Steps for setting up PrusaSlicer for Revo HF nozzles
1. First step is to create a new printer profile for the new nozzle
  * Select the existing preset for 0.8 nozzle
  * Adjust start and end G-code as shown in this article. This allows you to change nozzles and/or remove filament while cold because it slightly ejects the filament, but still keeps it in far enough in the extruder that you don't have to reload the filament if you don't change filaments. [E3D article "Start and End G-code for faster nozzle changes"](https://e3d-online.zendesk.com/hc/en-us/articles/4406857421213-Start-and-End-G-code-for-faster-nozzle-changes)
  * Adjust the start G-code to remove the nozzle size check since the MK3S hardware doesn't support the non-standard nozzle sizes in settings. [Prusa article on creating profiles for difference nozzles](https://help.prusa3d.com/article/creating-profiles-for-different-nozzles_127540)
  * Change the nozzle diameter to whatever you purchased
  * Change min and max layer heights to match what's listed in this table. [E3D Revo high flow slicer starter settings](https://e3d-online.com/pages/revo-high-flow-filament-starter-settings)
  * Go to dependencies and click "Detach from system preset". I'm not sure if this step is necessary.
  * Save the changes to the printer settings as a new printer
2. Now we'll create the proper Print Settings for the printer you created in the last step. This will set up the newly possible layer heights.
  * With the newly created printer set in "Printer Settings", go to "Print Settings" and you'll probably just see "default" in the dropdown box.
  * Under "Layers and perimeters", set the "Layer height" equal to whichever of the Fine/Medium/Coarse settings you are making a profile for from [E3D Revo high flow slicer starter settings](https://e3d-online.com/pages/revo-high-flow-filament-starter-settings).
  * Still under "Layers and perimeters", I set the "First layer height" to 1/2 of the nozzle diameter. That seems like roughly a number used in other nozzle profiles.
  * Under "Speed", I'm guessing at these numbers. I put "0" for everything not greted out in the "Speed for print moves" section. This should set them to be auto.
  * Still under "Speed", I went down to the "Modifiers" section and set the "First layer speed" to 50%
  * For the final change under "Speed", I went down to "Auto Speed (advanced)" and set "Max print speed" to the value from the table in [E3D Revo high flow slicer starter settings](https://e3d-online.com/pages/revo-high-flow-filament-starter-settings).
  * Go to the Dependencies tab and uncheck the "All" box for both "Compatible printers". Then press the "Set" button and check the box for the printer you created in the first step.
  * Save the changes and give it a new name.
3. Now we'll create the proper Filament Settings for the new nozzle because the generic profiles limit the output.
  * With the newly created printer set in "Printer Settings", go to Filament Settings and select the profile for "Generic PLA @Template"
  * Go to the Cooling tab and uncheck "Enable auto cooling" as mentioned in the [E3D article "How to Prepare Prusaslicer for Revo High Flow"](https://e3d-online.com/blogs/news/how-to-prepare-prusaslicer-for-revo-high-flow)
  * Go to the Advanced tab and set the max volumentric speed as listed in the [E3D article "Revo Nozzle Maximum Volumetric Flow Rates"](https://e3d-online.com/pages/revo-nozzle-maximum-flow-rates)
  * Go to the Dependencies tab and uncheck the "All" box for both "Compatible printers". Then press the "Set" button and check the box for the printer you created in the first step.
  * Still on the Dependencies tab, uncheck the "All" box for "Compatible print profiles". Then press the "Set" button and check the boxes for the print profiles you created in the second step.
4. For the final step, you need to actually test with your setup. E3D has a [page that discusses this](https://e3d-online.zendesk.com/hc/en-us/articles/6467176228253-Revo-Nozzle-Maximum-Flow-Rates-) The model used for the test can be found [here](https://www.printables.com/model/281016-flow-rate-test-geometry)
  * As you tweak settings, you can see what percentage of the max possible flow rate you are utilizing by plugging in your values into E3D's [Revo Volumetric Flow Rate Calculator](https://e3d-online.com/pages/revo-high-flow-volumetric-flow-rate-calculator)
