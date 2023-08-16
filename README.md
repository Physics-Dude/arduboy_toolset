# Arduboy toolset

<p float="left">
<img alt="Main window" src="https://github.com/randomouscrap98/arduboy_toolset/blob/main/appresource/screenshot_tools_main.png?raw=true" height=250>
<img alt="Cart builder" src="https://github.com/randomouscrap98/arduboy_toolset/blob/main/appresource/screenshot_cartbuilder_main.png?raw=true" height=250>
</p>

A set of personal tools derived heavily from https://github.com/MrBlinky/Arduboy-Python-Utilities
made as a learning exercise. I wanted to understand what makes Arduboy tick, while also maybe
providing a slightly easier way to manage Arduboy. 

The toolset allows you to:
* Upload and backup sketches
* Upload and backup FX flash data (carts of games)
* Upload, backup, and erase eeprom
* Add extra games to your Arduboy FX
* Update existing games on your Arduboy FX
* Create custom flashcarts with custom categories

## Quickstart

* Get the latest release from https://github.com/randomouscrap98/arduboy_toolset/releases. There are releases for 
Windows, Linux, and the latest MacOS (sorry if you have an older MacOS, toolchains sort of lock me in!!)
* Extract to a folder somewhere
* Run `arduboy_toolset.exe` for the standard GUI application

The first window is the basic toolset, letting you upload and download stuff from your Arduboy. 

If you want to add or update games on your Arduboy FX, use the `File` menu to open the cart builder. From here, you 
can use the newly opened window's `File` menu to read the FX cart off your Arduboy FX. It will take sometime to load.
Once it's complete, you can browse the **local copy** of your FX games in the window. Changes you make here are not 
immediately put onto your Arduboy. 

You can add games by dragging and dropping `.hex` or `.arduboy` files into the window. They will be inserted below
the currently focused menu item. If you accidently place a game where you don't want it, you can drag the games around
in the list, or press `Ctrl-delete` or use the `Cart` menu to remove them. When you're ready to put everything back on 
your Arduboy, use the `File` menu again to `Flash to Arduboy`. 

## Caveats

While I've done as much as I can to ensure the tool works appropriately, I can't promise it will work flawlessly,
I don't take any responsibility for lost data (I'm sorry!). 

### Prince of Arabia + other FX titles, 2023

Using this tool will usually preserve the FX saves used by the more complex "FX" games, such as 
[Prince Of Arabia](https://github.com/Press-Play-On-Tape/PrinceOfArabia). However, we've found that sometimes
the carts were not configured properly from the cart builder website, and your save data may be located in the
development area at the end of the flashcart. As such, there is a chance that updating your cart will
make you lose this save. You can check if your Prince of Arabia game is correct by loading the cart in
the cart builder, using `Ctrl-F` to search for `Arabia`, then checking the 3 numbers under the game's 
title image on the left. If the last number is **4096 or higher**, your game is **correct**. If it's 0, it is
development mode and you may lose the save.

If you wish to backup a "Development" save, you will need to make a **complete** backup of your FX, without trimming.
The Arduboy toolset defaults to trimming the FX backup, just uncheck the trim option before you backup you flash and
the save data will be included. This is because the save is stored at the very end of the cart, so trimming the backup
would remove that part from the file.


## Running From Source

If you have python already and just want to run from source, or want to run the command line 
(clone repo first ofc):

```shell
cd arduboy_toolset
# Optional: create and activate a virtual environment
# python -m venv .venv
# source .venv/bin/activate
pip install -r requirements.txt
python main_cli.py
# Or for gui, use main_gui.py
```

## Creating a standalone

This has to be done for each operating system, there is no cross compiler. Note that because of weird 
nonsense with Windows, I have to build the CLI and the GUI separately.

```shell
cd arduboy_toolset
# Optional: create and activate a virtual environment
# python -m venv .venv
# source .venv/bin/activate
pip install -r requirements.txt
pyinstaller arduboy_toolset_cli.spec
pyinstaller arduboy_toolset.spec
mv dist/arduboy_toolset_cli dist/arduboy_toolset
mv dist/arduboy_tooset/arduboy_toolset dist/arduboy_toolset/
```

Notes: 
- The GUI is a "onefile" app, it will startup slower but you can take that single file
  and put it anywhere.
- The GUI has the console removed; this is the main reason for having a separate GUI
  and CLI application
- The CLI application, to increase startup speed (because of how it might be used),
  requires all files in that folder (other than the GUI)
- The MacOS release, due to difficulties on that OS, does not have the CLI program (sorry!)
- The icon HAS to be a .ico file for windows

## Plans
- Add some of the cool extra features still left from Mr.Blinky's tools (like image display, development FX stuff, etc)
- Maybe spruce up the UI a bit?
