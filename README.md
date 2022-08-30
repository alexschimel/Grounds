# *Grounds*

Elevation Change Analysis.

## Description

*Grounds* is a free and open-source app to visualize and analyze change between Digital Elevation Models (DEM), that is, bathymetric/topographic grids. *Grounds* uses the [CoFFee multibeam data processing toolbox](https://github.com/alexschimel/CoFFee) (hence the name). It is coded in [MATLAB](https://www.mathworks.com/products/matlab.html), but is also available as a standalone application that does not require a MATLAB licence (see the Dependencies and Installing sections).

With *Grounds*, you can visualize the regions of your datasets that experienced vertical change (erosion, deposition, etc.), and calculate the surface and volumes of those changes, considering fixed or variable Limits of Detection (LoDs). *Grounds* also provides uncertainty estimates for these measures. This app implements the methods described in [Schimel et al. (2015)](https://doi.org/10.1016/j.csr.2015.10.019).

## Getting Started

### Dependencies

* For the source code:
  * [MATLAB](https://www.mathworks.com/products/matlab.html). The code was developed with version R2020b, but it may work on earlier/later versions.
  * Some [MATLAB toolboxes](https://www.mathworks.com/products.html):
    * Mapping Toolbox
    * Image Processing Toolbox
    * Statistics and Machine Learning Toolbox
  * [The *CoFFee* toolbox](https://github.com/alexschimel/CoFFee)
* For the compiled executable: [MATLAB Runtime v9.9](https://www.mathworks.com/products/compiler/matlab-runtime.html).
  * Note: if you install the app using the binary installer, the setup wizard will automatically detect whether you have the correct version of MATLAB Runtime installed and, if not, allow you to download and install it then.

### Installing

* For the source code: 
  * Clone or download this repository, as well as the repository of [*CoFFee*](https://github.com/alexschimel/CoFFee), onto your machine.
* For the compiled executable: 
  * Preferably, [download the binary installer from the releases page](https://github.com/alexschimel/Grounds/releases), execute the installer, and follow the instructions of the setup wizard. The setup wizard will check if you have the appropriate version of MATLAB Runtime installed and, if not, let you download and install it. Note that the setup wizard requires an internet connection.
  * Alternatively, you can simply [download the binary executable and accompanying files from the releases page](https://github.com/alexschimel/Grounds/releases) and double-click the .exe file to run the application without installing it. Note that you still need to have the appropriate version of MATLAB Runtime installed.

### Executing program

* For the source code: Start MATLAB, navigate to the root directory of the *Grounds* code, and type `Grounds` in the Command Window.
  * Note: The first time you run *Grounds* from the source code, you will be prompted to provide the location of a folder containing the *CoFFee* toolbox. *Grounds* will check if the version of that toolbox is the one with which the app was built. If the version of *CoFFee* is not the one expected, you will receive a warning letting you know you might experience issues, and recommending you download (or check out) the appropriate version.
* For the compiled executable: Execute the installed program.
  * Note: The first time you run *Grounds* after installation, it might take a while for the app to appear. Be patient. It will be faster the next times.

## Help

There is a short documentation available by clicking on the `?` (question mark) button in the menu.

There is an example dataset (2x DEMs, 2x spatially-variable uncertainty grids, 1x example polygon) [available for download from the releases page](https://github.com/alexschimel/Grounds/releases).

For more information, contact the authors.

## Authors

* Alexandre Schimel ([The Geological Survey of Norway](https://www.ngu.no), alexandre.schimel@ngu.no)
* Rozaimi Che Hasan (Universiti Teknologi Malaysia)
* Daniel Ierodiaconou (Deakin University)
* Joshu Mountjoy (NIWA)

## Version History

[See the releases page](https://github.com/alexschimel/Grounds/releases)

## License

Distributed under the MIT License. See `LICENSE.txt` for more information.

## See Also

All apps based on CoFFee:
* *Grounds*: https://github.com/alexschimel/Grounds
* *Espresso* (private)
* *Iskaffe*: https://github.com/alexschimel/Iskaffe

## References 

Articles using *Grounds*:
* Mountjoy, J. J., Howarth, J. D., Orpin, A. R., Barnes, P. M., Bowden, D. A., Rowden, A. A., Schimel, A. C. G., Holden, C., Horgan, H. J., Nodder, S. D., Patton, J. R., Lamarche, G., Gerstenberger, M., Micallef, A., Pallentin, A., & Kane, T. (2018). Earthquakes drive large-scale submarine canyon development and sediment supply to deep-ocean basins. Science Advances, 4(3). https://doi.org/10.1126/sciadv.aar3748
* Schimel, A. C. G., Ierodiaconou, D., Hulands, L., & Kennedy, D. M. (2015). Accounting for uncertainty in volumes of seabed change measured with repeat multibeam sonar surveys. Continental Shelf Research, 111, 52–68. https://doi.org/10.1016/j.csr.2015.10.019

## For developers

*Grounds* is not the only application built on *CoFFee* (see list above). The philosophy behind their development is that all back-end (processing) goes in *CoFFee* while all front-end (display, user interface, application) goes in those apps. As a result, it is possible that *CoFFee* gets ahead of *Grounds* in terms of development, so careful version controlling is necessary.

We use [Semantic Versioning](https://semver.org/) to attribute version numbers:
* The version of CoFFee is hard-coded in function `CFF_coffee_version.m`.
* The version of *Grounds* is a static property of the app (`Version`), alongside the CoFFee version it was built on (`CoffeeVersion`).

A careful sequence to develop *Grounds* is the following:

1. Checkout the latest commits on the main branches of both *CoFFee* and *Grounds*.
2. Check if that latest version of *Grounds* uses the latest version of *CoFFee* (in the code, or warning at start-up). 
3. If *Grounds* is running on an older version of *CoFFee*:
    * Start with updating *Grounds* to use that latest version of *CoFFee*.
    * Before committing those changes, increase *Grounds*'s version number and update which *CoFFee* version it runs on. 
    * After committing, remember to add the new tag on git.
4. Develop *Grounds* as you wish. Remember that all processing goes ideally in *CoFFee* and all display and user interface on *Grounds*.
5. When done, if *CoFFee* was modified:
    * Increase its version number.
    * Push it up on git first. Add a tag.
6. Increase version number for *Grounds* (and update which *CoFFee* version it was built on).
7. If you wish to compile this new version of *Grounds*:
    * In MATLAB, run `restoredefaultpath` to ensure you get a clean path. 
    * Run *Grounds* and check a last time it all works fine.
    * Double-click on the file `Grounds.prj` to run the application compiler with existing settings:
      * Remove the main file `Grounds.mlapp` and add it again for the application compiler to find all dependencies.
      * Update the version number in the setup filename, the application information, and the default installation folder.
      * Save.
      * Click on `Package`.
    * Install the new executable with the setup file.
    * Test that the setup works correctly.
    * Test that the installed software runs correctly.
8. Push *Grounds* up on git. Add a version tag.
9. If you compiled that new version:
    * Create a new release on github from the tag. 
    * Add the binary setup, and a zipped version of the `for_redistribution_files_only` folder.
