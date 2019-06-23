vmkSDK
==============

All in one sdk windows for esp32. Easy to install all dependencies. This sdk is based on git sub modules.

* toolchain xtensa-esp32-elf (20181001).
* openocd (v0.10.0)
* eclipse (Oxygen)
* msys32  (20181001)
* Library (esp-idf v3.2.1)


## Installation


* Clone repo

```
git clone --recursive https://github.com/ViaMonkey/vmkSDK.git
```

* Extract archives (assume sdk is installed on c:)

```
c:
cd /vmkSDK
.\tools\7-zip\7za.exe x .\editors\editors.zip -o.\editors
.\tools\7-zip\7za.exe x .\msys32\msys32.zip -o.\msys32
.\tools\7-zip\7za.exe x .\toolchains\toolchains.zip -o.\toolchains
.\tools\7-zip\7za.exe x .\tools\tools.zip -o.\tools
```

## Add Environment Variables (assume sdk is installed on c:).

* IDF_PATH = C:\vmkSDK\libs\esp-idf
* path = C:\vmkSDK\tools\openocd\bin;
* path = C:\vmkSDK\toolchains\xtensa-esp32-elf\bin
* path = C:\vmkSDK\msys32\mingw32\bin
* path = C:\vmkSDK\msys32\usr\bin


## Eclipse project.

### Import New Project

* Eclipse makes use of the Makefile support in ESP-IDF. This means you need to start by creating an ESP-IDF project. 
You can use the idf-template project from github, or open one of the examples in the esp-idf examples subdirectory.
* Once Eclipse is running, choose File -> Import…
* In the dialog that pops up, choose “C/C++” -> “Existing Code as Makefile Project” and click Next.
* On the next page, enter “Existing Code Location” to be the directory of your IDF project. 
Don’t specify the path to the ESP-IDF directory itself (that comes later). 
The directory you specify should contain a file named “Makefile” (the project Makefile).
* On the same page, under “Toolchain for Indexer Settings” choose “Cross GCC”. Then click Finish.

### Project Properties

* The new project will appear under Project Explorer. Right-click the project and choose Properties from the context menu.
* Click on the “Environment” properties page under “C/C++ Build”. Click “Add…” and enter name `BATCH_BUILD` and value `1`.
* Click the “Providers” tab
* In the list of providers, click “CDT Cross GCC Built-in Compiler Settings”. 
Under “Command to get compiler specs”, replace the text `${COMMAND}` at the beginning of the line with `xtensa-esp32-elf-gcc`. 
This means the full “Command to get compiler specs” should be `xtensa-esp32-elf-gcc ${FLAGS} -E -P -v -dD "${INPUTS}"`.

* In the list of providers, click “CDT GCC Build Output Parser” and type xtensa-esp32-elf- at the beginning of the Compiler command pattern. 
This means the full Compiler command pattern should be `xtensa-esp32-elf-(g?cc)|([gc]\+\+)|(clang)`