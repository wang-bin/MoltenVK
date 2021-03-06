<a class="site-logo" href="https://github.com/KhronosGroup/MoltenVK" title="MoltenVK">
	<img src="images/MoltenVK-Logo-Banner.png" alt="MoltenVK" style="width:256px;height:auto">
</a>

Copyright (c) 2014-2018 [The Brenwill Workshop Ltd.](http://www.brenwill.com)

*This document is written in [Markdown](http://en.wikipedia.org/wiki/Markdown) format.
For best results, use a Markdown reader.*


Table of Contents
-----------------

- *Vulkan-Hpp*
	- [Using the *Vulkan-Hpp* Spec Repository with **MoltenVK**](#install_vulkan_spec)
	- [Updating the *Vulkan-Hpp* library version](#update_vulkan_spec)

- *Vulkan-LoaderAndValidationLayers*
	- [Using the *Vulkan-LoaderAndValidationLayers* Repository with **MoltenVK**](#install_vulkan_lvl)
	- [Updating the *Vulkan-LoaderAndValidationLayers* library version](#update_vulkan_lvl)

- *SPIRV-Cross*
	- [Using the *SPIRV-Cross* library with **MoltenVKShaderConverter**](#install_spirv-cross)
	- [Updating the *SPIRV-Cross* library version](#update_spirv-cross)
	- [Adding the *SPIRV-Cross* library to a new *Xcode* project](#add_spirv-cross)

- *SPIRV-Tools*
	- [Using the *SPIRV-Tools* library with **MoltenVKShaderConverter**](#install_spirv-tools)
	- [Updating the *SPIRV-Tools* library version](#update_spirv-tools)
	- [Adding the *SPIRV-Tools* library to a new *Xcode* project](#add_spirv-tools)

- *glslang*
	- [Using the *glslang* library with **MoltenVKShaderConverter**](#install_glslang)
	- [Updating the *glslang* library version](#update_glslang)
	- [Adding the *glslang* library to a new *Xcode* project](#add_glslang)


<a name="install_vulkan_spec"></a>
Using the *Vulkan-Hpp* Spec Repository with *MoltenVK*
------------------------------------------------------

**MoltenVK** uses the official *Khronos Vulkan* specification repository to provide the standard
*Vulkan* API header files and *Vulkan Specification* documentation.

To add the *Khronos Vulkan* specification repository to **MoltenVK**, open a *Terminal* 
session and perform the following command-line steps:

1. Ensure you have `python3` and `asciidoctor` installed:

		brew install python3
		sudo gem install asciidoctor

2. If you used the `--recursive` option when cloning the `MoltenVK` repository, you should already 
   have the `Vulkan-Hpp` submodule, and you can skip to *Step 3* below. If you did **_not_** 
   use the `--recursive` option when cloning the `MoltenVK` repository, retrieve the `Vulkan-Hpp` 
   submodule into the `External` directory as follows, from within the `MoltenVK` repository directory:

		git submodule update --init --recursive External/Vulkan-Hpp

3. In the `Externals` folder within the `MoltenVK` repository, build the spec and header files 
   as follows from the main directory of this `MoltenVK` repository:

		cd External
		./makeVulkanSpec



<a name="update_vulkan_spec"></a>
Updating the *Vulkan-Hpp* library version
-----------------------------------------

If you are developing enhancements to **MoltenVK**, you can update the version of `Vulkan-Hpp` 
used by **MoltenVK** to the latest version available by re-cloning and re-building the
`Vulkan-Hpp` submodule using the `getLatestVulkanSpec` script:

	cd External
	./getLatestVulkanSpec

The updated version will then be "locked in" the next time the `MoltenVK` repository is committed to `git`.



<a name="install_vulkan_lvl"></a>
Using the *Vulkan-LoaderAndValidationLayers* Spec Repository with *MoltenVK*
----------------------------------------------------------------------------

**MoltenVK** uses the *Khronos Vulkan Loader and Validation Layers* repository to allow **MoltenVK** 
to act as an *Installable Client Driver* to support the *Vulkan Loader API*.

If you used the `--recursive` option when cloning the `MoltenVK` repository, you should already
have the `Vulkan-LoaderAndValidationLayers` submodule. If you did **_not_** use the `--recursive` 
option when cloning the `MoltenVK` repository, retrieve the `Vulkan-LoaderAndValidationLayers` 
submodule into the `External` directory as follows, from within the `MoltenVK` repository directory:

	git submodule update --init External/Vulkan-LoaderAndValidationLayers



<a name="update_vulkan_lvl"></a>
Updating the *Vulkan-LoaderAndValidationLayers* library version
---------------------------------------------------------------

If you are developing enhancements to **MoltenVK**, you can update the version of `Vulkan-LoaderAndValidationLayers` 
used by **MoltenVK** to the latest version available by re-cloning and re-building the `Vulkan-LoaderAndValidationLayers` 
submodule using the `getLatestVulkanLVL` script:

	cd External
	./getLatestVulkanLVL

The updated version will then be "locked in" the next time the `MoltenVK` repository is committed to `git`.



<a name="install_spirv-cross"></a>
Using the *SPIRV-Cross* library with *MoltenVKShaderConverter*
--------------------------------------------------------------

**MoltenVKShaderConverter** uses `SPIRV-Cross` to convert *SPIR-V* code to *Metal Shading Language (MSL)* source code.

If you used the `--recursive` option when cloning the `MoltenVK` repository, you should already
have the `SPIRV-Cross` submodule. If you did **_not_** use the `--recursive` option when cloning
the `MoltenVK` repository, retrieve the `SPIRV-Cross` submodule into the `External` directory 
as follows, from within the `MoltenVK` repository directory:

	git submodule update --init External/SPIRV-Cross



<a name="update_spirv-cross"></a>
Updating the *SPIRV-Cross* library version
------------------------------------------

If you are developing enhancements to **MoltenVKShaderConverter**, you can update the version of 
`SPIRV-Cross` used by **MoltenVKShaderConverter** to the latest version available by re-cloning 
and re-building the `SPIRV-Cross` submodule using the `getLatestSPIRVCross` script:

	cd External
	./getLatestSPIRVCross

The updated version will then be "locked in" the next time the `MoltenVK` repository is committed to `git`.

>***Note:*** If after updating to a new verions of `SPIRV-Cross`, you encounter build errors when 
 building **MoltenVKShaderConverter**, review the [instructions below](#add_spirv-cross) to ensure 
 all necessary `SPIRV-Cross` files are included in the **MoltenVKShaderConverter** builds.

>***Note:*** As new features are added to **MoltenVK**, many are powered by the ability to convert 
 sophisticated *SPIRV* code into *MSL* code. Sometimes new **MoltenVK** features and capabilities are 
 provided solely via new `SPIRV-Cross` features. ***If you are developing enhancements for 
 MoltenVKShaderConverter, be sure to update the `SPIRV-Cross` submodule often***.


### Regression Testing Your Changes to *SPIRV-Cross*

If you make changes to the `SPIRV-Cross` submodule, you can regression test your changes 
using the following steps:

1. Load and build the versions of `SPRIV-Tools` and `glslang` that are used by the `SPIRV-Cross` tests:

		cd External/SPIRV-Cross
		./checkout_glslang_spirv_tools.sh

2. Run the regression tests:

		./test_shaders.sh

3. If your changes result in different expected output for a reference shader, and the new results
   are correct, you can update the reference shader for a particular regression test by deleting
   that reference shader, in either `External/SPIRV-Cross/reference/shaders-msl` or 
   `External/SPIRV-Cross/reference/opt/shaders-msl`, and running the test again. The test will
   replace the deleted reference shader.



<a name="add_spirv-cross"></a>
Adding the *SPIRV-Cross* library to a new *Xcode* project
---------------------------------------------------------

The `MoltenVKShaderConverter` project is already configured to use the `SPIRV-Cross` library. 
However, to add the `SPIRV-Cross` library to a new *Xcode* project:

1. Follow the [instructions above](#install_spirv-cross) to create a symlink from your project
   to the location of your local clone of the `SPIRV-Cross` repository.

2. In the project navigator, add a new *Group* named `SPIRV-Cross`.

3. Add the following files from the `SPIRV-Cross` file folder to the `SPIRV-Cross` 
   group in the *Project Navigator* panel:

		spirv_cfg.cpp
		spirv_cfg.hpp
		spirv_common.hpp
		spirv_cross.cpp
		spirv_cross.hpp
		spirv_glsl.cpp
		spirv_glsl.hpp
		spirv_msl.cpp
		spirv_msl.hpp

   In the ***Choose options for adding these files*** dialog that opens, select the 
   ***Create groups*** option, add the files to *both* the `MoltenVKSPIRVToMSLConverter-iOS` 
   and `MoltenVKSPIRVToMSLConverter-macOS` targets, and click the ***Finish*** button.

4. ***(Optional)*** If you want *Xcode* to reference the added files through symlinks (to increase
   portability) instead of resolving them, perform the following steps:
   
   1. **Create a backup of your project!** This is an intrusive and dangerous operation!
   2. In the *Finder*, right-click your `MyApp.xcodeproj` file and select *Show Package Contents*.
   3. Open the `project.pbxproj` file in a text editor.
   4. Replace all occurrences of the `path-to-SPIRV-Cross-repo-folder` (as defined by the symlink added
      [above](#install_spirv-cross)) with simply `SPIRV-Cross` (the name of the symlink). Be sure you only
      replace the part of the path that matches the `path-to-SPIRV-Cross-repo-folder`. Do not replace 
      any part of the path that indicates a subfolder within that repository folder.



<a name="install_spirv-tools"></a>
Using the *SPIRV-Tools* library with *MoltenVKShaderConverter*
--------------------------------------------------------------

**MoltenVKShaderConverter** uses `SPIRV-Tools` to log *SPIR-V* code during conversion to *Metal Shading Language (MSL)* 
source code. The `SPIRV-Tools` also requires the `SPIRV-Headers` library.

To add the `SPIRV-Tools` and `SPIRV-Headers` libraries to **MoltenVK**, open a *Terminal* session and 
perform the following command-line steps:

1. If you used the `--recursive` option when cloning the `MoltenVK` repository, you should already 
   have the `SPIRV-Tools` and `SPIRV-Headers` submodules, and you can skip to *Step 2* below. 
   If you did **_not_** use the `--recursive` option when cloning the `MoltenVK` repository, 
   retrieve the `SPIRV-Tools` and `SPIRV-Headers` submodules into the `External` directory 
   as follows, from within the `MoltenVK` repository directory:

		git submodule update --init External/SPIRV-Headers
		git submodule update --init External/SPIRV-Tools

3. In the `Externals` folder within the `MoltenVK` repository, build `SPIRV-Tools` 
   as follows from the main directory of this `MoltenVK` repository:

		cd External
		./makeSPIRVTools



<a name="update_spirv-tools"></a>
Updating the *SPIRV-Tools* library version
------------------------------------------

If you are developing enhancements to **MoltenVKShaderConverter**, you can update the version of 
`SPIRV-Tools` used by **MoltenVKShaderConverter** to the latest version available by re-cloning 
and re-building the `SPIRV-Tools` submodule using the `getLatestSPIRVTools` script:

	cd External
	./getLatestSPIRVTools

The updated version will then be "locked in" the next time the `MoltenVK` repository is committed to `git`.

>***Note:*** If after updating to a new verions of `SPIRV-Tools`, you encounter build errors when 
>building **MoltenVKShaderConverter**, review the [instructions below](#add_spirv-tools) to ensure 
>all necessary `SPIRV-Tools` files are included in the **MoltenVKShaderConverter** builds.



<a name="add_spirv-tools"></a>
Adding the *SPIRV-Tools* library to a new *Xcode* project
---------------------------------------------------------

The `MoltenVKShaderConverter` project is already configured to use the `SPIRV-Tools` library. 
However, to add the `SPIRV-Tools` library to a new *Xcode* project:

1. Follow the [instructions above](#install_spirv) to create a symlink from your project
   to the location of your local clone of the `SPIRV-Tools` repository.

2. In the project navigator, add a new *Group* named `SPIRV-Tools`.

3. Drag the `SPIRV-Tools/source` folder to the `SPIRV-Tools` group in the *Project Navigator* panel.
   In the _**Choose options for adding these files**_ dialog that opens, select the 
   _**Create groups**_ option, add the files to *both* the `MoltenVKSPIRVToMSLConverter-iOS` 
   and `MoltenVKSPIRVToMSLConverter-macOS` targets, and click the ***Finish*** button.

4. In the *Project Navigator* panel, select your application's target, and open the 
   *Build Settings* tab. Locate the build setting entry **Header Search Paths** 
   (`HEADER_SEARCH_PATHS`) and add the following paths:
   
		"$(SRCROOT)/MoltenVKSPIRVToMSLConverter/SPIRV-Tools/include"
		"$(SRCROOT)/MoltenVKSPIRVToMSLConverter/SPIRV-Tools/source"
		"$(SRCROOT)/MoltenVKSPIRVToMSLConverter/SPIRV-Tools/build"
		"$(SRCROOT)/MoltenVKSPIRVToMSLConverter/SPIRV-Headers/include"

5. ***(Optional)*** If you want *Xcode* to reference the added files through symlinks (to increase
   portability) instead of resolving them, perform the following steps:
   
   1. **Create a backup of your project!** This is an intrusive and dangerous operation!
   2. In the *Finder*, right-click your `MyApp.xcodeproj` file and select *Show Package Contents*.
   3. Open the `project.pbxproj` file in a text editor.
   4. Replace all occurrences of the `path-to-SPIRV-Tools-repo-folder` (as defined by the symlink added
      [above](#install_spirv)) with simply `SPIRV-Tools` (the name of the symlink). Be sure you only
      replace the part of the path that matches the `path-to-SPIRV-Tools-repo-folder`. Do not replace 
      any part of the path that indicates a subfolder within that repository folder.



<a name="install_glslang"></a>
Using the *glslang* library with **MoltenVKShaderConverter**
------------------------------------------------------------

**MoltenVKShaderConverter** uses `glslang`, the Khronos *GLSL* reference compiler, to parse *GLSL* source code 
and convert it to *SPIR-V*.

If you used the `--recursive` option when cloning the `MoltenVK` repository, you should already have
the `glslang` submodule. If you did **_not_** use the `--recursive` option when cloning the 
`MoltenVK` repository, retrieve the `glslang` submodule into the `External` directory as follows, 
from within the `MoltenVK` repository directory:

	git submodule update --init External/glslang



<a name="update_glslang"></a>
Updating the *glslang* library version
--------------------------------------

If you are developing enhancements to **MoltenVKShaderConverter**, you can update the version of 
`glslang` used by **MoltenVKShaderConverter** to the latest version available by re-cloning 
and re-building the `glslang` submodule using the `getLatestglslang` script:

	cd External
	./getLatestglslang

The updated version will then be "locked in" the next time the `MoltenVK` repository is committed to `git`.

>***Note:*** If after updating to a new verions of `glslang`, you encounter build errors when 
>building **MoltenVKShaderConverter**, review the [instructions below](#add_glslang) to ensure 
>all necessary `glslang` files are included in the **MoltenVKShaderConverter** builds.



<a name="add_glslang"></a>
Adding the *glslang* library to a new *Xcode* project
-----------------------------------------------------

The `MoltenVKShaderConverter` project is already configured to use the `glslang` library. 
However, to add the `glslang` library to a new *Xcode* project:

1. Follow the [instructions above](#install_glslang) to create a symlink from your project
   to the location of your local clone of the `glslang` repository, and make the required 
   modifications to the `glslang` code.

2. In the project navigator, add a new *Group* named `glslang`.

3. Add the following folders from the `glslang` file folder to the `glslang` *Group* in
   the *Project Navigator* panel:

		glslang
		OGLCompilersDLL
		SPIRV

   In the ***Choose options for adding these files*** dialog that opens, select the 
   ***Create groups*** option, add the files to *both* the `MoltenVKGLSLToSPIRVConverter-iOS` 
   and `MoltenVKGLSLToSPIRVConverter-macOS` targets, and click the ***Finish*** button.

4. In the *Project Navigator* panel, remove the references to the following files and folders:

		glslang/glslang/MachineIndependant/glslang.y
		glslang/glslang/OSDependent/Windows

5. ***(Optional)*** If you want *Xcode* to reference the added files through symlinks (to increase
   portability) instead of resolving them, perform the following steps:
   
   1. **Create a backup of your project!** This is an intrusive and dangerous operation!
   2. In the *Finder*, right-click your `MyApp.xcodeproj` file and select *Show Package Contents*.
   3. Open the `project.pbxproj` file in a text editor.
   4. Replace all occurrences of the `path-to-glslang-repo-folder` (as defined by the symlink added
      [above](#install_glslang)) with simply `glslang` (the name of the symlink). Be sure you only 
      replace the part of the path that matches the `path-to-glslang-repo-folder`. Do not replace 
      any part of the path that indicates a subfolder within that repository folder.

