RedstoneChips 
=============

RedstoneChips is a Bukkit plugin that allows you to build custom redstone chips on your craftbukkit minecraft server.
Circuits can be built with any number of inputs and outputs and in almost any imaginable structure. RedstoneChips currently consists of the following plugins:

- RedstoneChips - The core plugin that handles circuit detection and activation, managing preferences and handling player commands. You must install this plugin to be able to build redstone chips.
- [BasicCircuits](http://github.com/eisental/BasicCircuits) - The base circuit library containing many different circuit classes. 

- [SensorLibrary](http://github.com/eisental/SensorLibrary) - An extra circuit library for sensor chips.

Check out the [circuitdocs](http://eisental.github.com/RedstoneChips/circuitdocs) for more info about the circuit libraries.

__For much more information, visit the [RedstoneChips](http://eisental.github.com/RedstoneChips) site.__

Installation
------------
* Download latest [RedstoneChips jar file](https://github.com/downloads/eisental/RedstoneChips/RedstoneChips-beta.jar).
* Download latest [BasicCircuits jar file](https://github.com/downloads/eisental/BasicCircuits/BasicCircuits-beta.jar).
* Copy both jar files to the plugins folder of your craftbukkit installation. 

Changelog
----------
#### RedstoneChips 0.88 (07/04/11)
- New /rcsel command for mass editing circuits in a cuboid. It's possible to use it for activating, destroying reseting or fixing i/o block types of circuits.
- New /rcactivate command for activating circuits possibly with different i/o block types than currently set.
- New /rcarg command for editing/adding/clearing sign arguments of a circuit.
- New /rcfixioblocks command for changing input, output and interface block types of a circuit to match the current setting. 
- Active circuits will have their class name colored (in red by default). It's possible to change the color using the signColor preference key.
- Removed dashes from command names. /rc-debug becomes /rcdebug, /rc-info becomes /rcinfo, etc.
- Circuit activation is now done by LEFT-clicking the circuit's sign. A preference key can be set to revert back to right-click.
- Any kind of loading error will now trigger a circuits file backup.
- Added hex representation of input and output states in /rcinfo.
- Fixed bug where receivers with 0 outputs were allowed and caused an exception.

#### RedstoneChips 0.87 (30/03/11)
- Complete rewrite of the broadcast channels system.
- transmitters and receivers can work with a selected part of the broadcast channel. Use <channel name>:<start bit> as the channel sign arg to set the 1st bit in the channel 
the circuit will work on.
- `/rc-channels` now displays the number of bits used by each channel.
- `/rc-channels <channel name>` prints additional information about a specific channel.
- Using plugin name and version on circuit library load message
- Sepearated between circuit shutdown, which happens each time the plugin is disabled, and circuit destroy - when the circuit is permanently removed from the circuit list.
- Updated for craftbukkit #602.

#### RedstoneChips 0.86 (19/03/11)
- Wool color or any other block with data value can be used as an indicator block (input/output/interface). For example: /rc-prefs inputBlockType wool:silver will now work.
- `/rc-list` will now show only the circuits in the current world by default. Using `/rc-list all` would show circuits in all worlds and display each circuit's world.
- `/rc-list` shows each circuits sign arguments (or at least part of them).
- `/rc-channels` shows how many receivers and transmitters are communicating on each broadcast channel.
- Using /rc-debug on a circuit you're already debugging will turn debug for the circuit off.
- Added hex values and changed the message format of input-change debug messages
- Changed the circuit id system. Circuits will keep their id numbers after rc-reset or server restart.
- New backup redstonechips.circuits files won't overwrite older ones.
- Invalid pref values entered using /rc-prefs are now caught properly.
- Some command format changes and bug fixes.
- Fixed a little bug when removing rc-type circuits.

#### RedstoneChips 0.84 (10/03/11)
- New circuit library interface mechanism (again). Plugin jar file can be renamed to anything now. 
- The plugin will now backup the circuits file when it encounters a loading error.

#### RedstoneChips 0.83 (07/03/11)
- Changed maven version to beta so I won't need to recompile every circuit library whenever there's a new RedstoneChips version. This means that the jar filename is changed to RedstoneChips-beta.jar and it will stay that way on the next versions as well.
- Works with multiworld plugins. Using same fix as ControllerBlock, thanks @Hell_Fire
- Saves circuits also when the plugin is disabled. You can use the reload command without losing changes.
- New rc-save and rc-load commands.

#### RedstoneChips 0.82 (28/02/11)
- Every chip can now use a different block as a chip block. The chip's block type is determined by the block type the sign is attached to. 
- /rc-debug can be used with a circuit id number and /rc-debug alloff can be used to stop receiving debug messages from all circuits.
- Uses the new Bukkit Player.getTargetBlock().
- Supports /rc-reset with circuit id as an argument; New /rc-help command for some info about RC commands.
-  Temporary fix for yet another circuit library load order problem. Many changes to the way circuit libraries behave. Check [LibraryTemplate](https://github.com/eisental/LibraryTemplate) for info.
- Changed Circuit.init() to use CommandSender instead of player. If you're working on a circuit library you need to change your circuits to use `public void init(CommandSender sender, String[] args) {}`
- Don't need to use ChatFixUtil anymore.
- Doesn't use the old constructor. Good riddance.

#### RedstoneChips 0.8 (14/02/11)
- Many internal changes in the way input pins are handled and their lookup maps.
- Using ChatFixUtil by Olof Larsson prevent chat color client crashes.
- When scanning a chip, chip blocks are first looked for to the right and to the left instead of in the original direction. This means that branches closer to the sign will have lower pin numbers.
- any IO block (input, output or interaction) can now be placed on top or below a chip block.
- Circuits can now register themselves as receivers or transmitters on a specific broadcast channel to receive bits wirelessly. 
- Circuits can now register themselves as type receivers to receive text entered by using the /rc-type command.
- Moved /rc-channels command into RedstoneChips to work with the new ReceivingCircuit and TransmittingCircuit interfaces.
- Moved /rc-type command into RedstoneChips to work with the new rcTypeReceiver interface.
- Uses <craftbukkit>/plugins/RedstoneChips as the data folder. The version number is no longer part of the folder name.
- Saves the circuit state whenever the world is saved instead of doing it on every circuit activation/deactivation.
- Shorter command names: redchips-active -> rc-list, redchips-classes -> rc-classes, redchips-prefs -> rc-prefs, redchips-debug -> rc-debug, redchips-pin -> rc-pin, redchips-destroy -> rc-destroy, redchips-deactivate -> rc-break, redchips-channels -> rc-channels.
- New commands: /rc-reset to reactivate a circuit. Useful for applying changes to the circuit structure or sign arguments; /rc-info print's a lot of information about a circuit. Used by pointing at a circuit or with a circuit id.
- Material names in the preferences can be entered without spearating underscores.
- Added a check for infinite feedback loops, such as a not gate in which the output is connected straight to the input. This will no longer cause the server to crash and the offending circuit will now be disabled. To use it again it needs to be reactivated.
- Circuits will behave much more nicely on server restarts.

#### RedstoneChips 0.77 (7/02/11)
- Moved CircuitIndex and CircuitLibrary classes to package org.tal.redstonechips.circuit
- Using the new scheduler for turning off buttons that are directly connected to an input block.
- Some message text / color changes.
- Removed log message when storing circuits after circuit activate/deactivate 
- Added javadocs to most classes
- Circuit libraries can add their own preferences keys.

#### RedstoneChips 0.76 (and 0.75) (4/02/11)
- New circuit library loading mechanism for solving startup issues. Adding new circuit libraries should be a bit easier.
- Circuits can receive redstone current from the top or any side of an input block.
- Output levers can be attached to any side or on top of an output block.
- Controlled blocks can be attached to any side (including top and bottom) of an interface block.
- Circuits will now update their output levers when their chunk is loaded.
- After activating a circuit its outputs are now immediately updated according to the current state of its inputs.
- Fixed some bugs dealing with chunk load / unload and other stuff.

#### RedstoneChips 0.71 (31/01/11)
* Updated to work with new bukkit command api.
* New /redchips-deactivate command for deactivating circuits without destroying them, activated either by pointing at the circuit or remotely for admins, by using `/redchips-deactivate <circuit id>`.
* New /redchips-destroy command to destroy a circuit and all of its blocks. The command is disabled by default. Set preference key 'enableDestroyCircuit' to 'true' to enable.
* Circuit debuggers are now notified when the circuit is destroyed including info about who destroyed it and where.


#### RedstoneChips 0.7 (27/01/11)
* Completely new circuit detection algorithm. Circuits can now be built in almost any shape.
* New storage format for the active circuits file (now named redstonechips.circuits).
* Interface blocks replace the output block used by circuits such as pixel, print and synth. More than one interface block per chip is now possible. Interface blocks are placed the same way as input and output blocks and they're indicated by a block of material interfaceBlockType (also added to preferences).
* Fixed print order of binary numbers. LSB is now the rightmost character.
* Missing output levers will now cause an error message to be displayed.
* Output levers will now turn off after a circuit is destroyed.
* A circuit will now deactivate when one of its structure blocks burns down.
* Chat colors are added to the preferences file and can be modified using /redchips-prefs.

#### RedstoneChips 0.6 (24/01/11)
* new command /redchips-debug for getting debug messages from a circuit.
* new command /redchips-pin for getting info about a specific chip pin.


#### RedstoneChips 0.5 (22/01/11)
* improved circuit detection algorithm.
* improved performance of circuit destruction.
* circuits are now destroyed when one of their blocks get exploded.
* new /redchips-classes command.
* renamed active circuits list command to /redchips-active
* new /redchips-prefs command, for viewing and editing the preferences file from within the game.    
* moved plugin files to the plugin folder.
* preferences are now a yaml file.
* added color to player messages.
* fixed error message when creating a bit-set circuit with no outputs.
* catching concurrent modification exception when setting lever data

#### RedstoneChips 0.4 (20/01/11)
* temporary fix for the button bug.
* better performance when working with a large number of circuits.



