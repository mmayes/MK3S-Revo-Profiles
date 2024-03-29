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
  * Save the changes to the printer settings as a new printer
2. Now we'll create the proper Print Settings for the printer you created in the last step. This will set up the newly possible layer heights.
  * With the newly created printer set in "Printer Settings", go to "Print Settings" and you'll probably just see "default" in the dropdown box.
  * Under "Layers and perimeters", set the "Layer height" equal to whichever of the Fine/Medium/Coarse settings you are making a profile for from [E3D Revo high flow slicer starter settings](https://e3d-online.com/pages/revo-high-flow-filament-starter-settings).
  * Still under "Layers and perimeters", I set the "First layer height" to 1/2 of the nozzle diameter. That seems like roughly a number used in other nozzle profiles.
  * Under "Speed", I'm guessing at these numbers. I put "0" for everything not greyed out in the "Speed for print moves" section. This should set them to be auto.
  * Still under "Speed", I went down to the "Modifiers" section and set the "First layer speed" to 50%.
  * For the final change under "Speed", I went down to "Auto Speed (advanced)" and set "Max print speed" to the value from the table in [E3D Revo high flow slicer starter settings](https://e3d-online.com/pages/revo-high-flow-filament-starter-settings).
  * Under "Advanced", I set all of the line widths equal to the values for the nozzle from the table in [E3D Revo high flow slicer starter settings](https://e3d-online.com/pages/revo-high-flow-filament-starter-settings).
  * Go to the Dependencies tab and uncheck the "All" box for both "Compatible printers". Then press the "Set" button and check the box for the printer you created in the first step.
  * Save the changes and give it a new name.
3. Now we'll create the proper Filament Settings for the new nozzle because the generic profiles limit the output.
  * With the newly created printer set in "Printer Settings", go to Filament Settings and select the profile for "Generic PLA @Template"
  * So far for generic PLA I'm printing the first and subsequent layers all at 220 degrees. For PETG, I'm using 240. One of the tables from E3D shows 220 for PETG and another shows 240 for PETG. My assumption is they wouldn't print PETG at the same temp as PLA so it's just an error in the one table that shows 220.
    * REIFY 3D has a note about increasing temperatures by 5% from what you normally print at in order to avoid clogs. [Link](https://www.reify3d.com/blogs/news/faq-about-e3d-revo#:~:text=What%20is%20the%20flow%20rate,sec%20using%20their%20testing%20methodology.)
  * Go to the Cooling tab and uncheck "Enable auto cooling" as mentioned in the [E3D article "How to Prepare Prusaslicer for Revo High Flow"](https://e3d-online.com/blogs/news/how-to-prepare-prusaslicer-for-revo-high-flow)
  * Go to the Advanced tab and set the max volumentric speed as listed in the [E3D article "Revo Nozzle Maximum Volumetric Flow Rates"](https://e3d-online.com/pages/revo-nozzle-maximum-flow-rates)
  * Go to the Dependencies tab and uncheck the "All" box for both "Compatible printers". Then press the "Set" button and check the box for the printer you created in the first step.
  * Still on the Dependencies tab, uncheck the "All" box for "Compatible print profiles". Then press the "Set" button and check the boxes for the print profiles you created in the second step.
4. For the final step, you need to actually test with your setup. E3D has a [page that discusses this](https://e3d-online.zendesk.com/hc/en-us/articles/6467176228253-Revo-Nozzle-Maximum-Flow-Rates-) The model used for the test can be found [here](https://www.printables.com/model/281016-flow-rate-test-geometry)
  * As you tweak settings, you can see what percentage of the max possible flow rate you are utilizing by plugging in your values into E3D's [Revo Volumetric Flow Rate Calculator](https://e3d-online.com/pages/revo-high-flow-volumetric-flow-rate-calculator)
  * Another great test model is from CNC Kitchen. He made a [video](https://youtube.com/watch?v=ZgIlSpb-A2Y) where he looked at the Revo high flow nozzles. The model he used is similar to the E3D one above, but in the pictures for the model he shows how he set up the custom gcode for speed changes. [Model Link](https://www.printables.com/model/342075-extrusion-test-structure)

### My results for a Prusa MK3S+ with stock extruder using a Revo hot end with 60w heater.
* For the 1.4mm HF nozzle with PLA, the highest volumetric flow rate (mm³/s) I could get with just occasional skips was about 28 mm³/s. I settled on 27 to give a little margin. Advertised values were 37.
  * Interestingly, for the fine setting (0.35 layer height) it seems like the slicer would allow for higher speeds if the volumetric rate was higher. However, for the 1.05 layer height, it seems like the print speed is actually the limiting factor. Even if I increase the volumentric rate all the way up to the theoretical max, the max it ever shows in the preview once sliced is 25.7.
  * Note: The volumetric limit tables shown by E3D don't differentiate between layer height. So it seems like smaller layer heights would mean it can move faster in order to reach the same output volume.
* For the 1.4mm HF nozzle with PETG, advertised flow rate is 49.
* For the 1.0mm HF nozzle with PLA, advertised flow rate is 35. I settled on 25. Similar to the 1.4 nozzle, even with 25 set as the max flow rate, the system automatically limits it to 24 when doing the fatter layers.
* For the 1.0mm HF nozzle with PETG, advertised flow rate is 42. I kept slowing things down by 1 and settled on 27. When I did 29, it was about 95% defect free. 28 was 99% defect free. 
