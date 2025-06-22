# rivals-2-toolkit
A bunch of assets for Rivals of Aether II work.

# Building Fmodel Mappings File
- First, download [Cheat Engine](https://www.cheatengine.org/downloads.php) and install.
- Once you have Cheat Engine, open it.
- Open Rivals 2.
- Locate the icon on the toolbar that reads "Select a process to open", and click it.
- From the Applications tab, select the Rivals 2 process and double-click it.
- That panel should close. In the Cheat Engine window, click "Memory View".
- A window titled "Memory Viewer" should be open. Go to the top ribbon and locate Tools > Inject DLL, or use the shortcut Ctrl+I.
- Select the Dumper-7.dll file from this repo. Click "Yes" when prompted.
- After seeing a successful injection, locate to the drive location where the mappings file is. For me, it's located under "C:\Dumper-7\5.4.2-0+UE5-Rivals2\Mappings\5.4.2-0+UE5-Rivals2.usmap".
- Tada! You have your Unity Script Mappings file now.

# Extracting JSONs using Fmodel
You'll need a copy of Rivals 2, and you'll need [FModel](https://fmodel.app/download). Make sure to have both.
First, install FModel. Then, open FModel.
- FModel needs to know where your game is, so it'll show a prompt. Click below "ADD UNDETECTED GAME".
 - You'll need to find the path where your Rivals of Aether II is installed. For me, it's installed in "C:\Program Files (x86)\Steam\steamapps\common\Rivals 2\".
 - With that path, next to Directory, click "..." and paste in your Rivals of Aether II path.
 - The name can be whatever you want, "Rivals 2" for simplicity.
 - Make sure to select UE5_4 for the engine version. Then, hit "OK". It'll ask you to restart FModel.
 Great! Now you need to add your mapping file, either obtained from Discord through someone posting it, or by doing the above method to build it yourself.
 - If you have it, you can simply navigate to the top ribbon of the window. Settings > General > Advanced > Local Mapping File [x]. Enable this checkbox if it is not enabled.
 - The mapping file path field should now show up. Click on "..." and navigate to your mappings file to select it.
 - Hit "OK".
- Once this is done, you can simply double click "Rivals2-Window.pak" on the left side. You now have access to all of the character data. But how do we make it useful? We need to convert the game assets to JSON files and export them.
- Through the folders, navigate Rivals2 > Content > Characters.
  - We want the attacks, the articles, and the character stats.
  - There's a painless way to do this. Hit "Ctrl+Shift+F" to pull up the Search View window.
  - Then, input the regex `Attacks/A[^N]`. Make sure to turn on the `.*` symbol that says "Regex" when hover over it. Hit "Enter".
  - Once you do that, you should have all of the attacks and the articles available. Left click on the first file, hit "Ctrl+A" to select all the files, right click, and select "Save Properties (.json)".
  - To get the character stats, just input `CD_` into the search box, left click on the first file, hit "Ctrl+A" to select all the files, right click, and select "Save Properties (.json)".
- Where is it exported? If you look at the bottom right, there is an icon that when highlighted, reads "Open Output Folder". Click that icon, and then navigate through Exports > Rivals2 > Content > Characters. This "Characters" folder is the one we want.

Congrats! Now you have your characters folder. You can move this wherever you would like, as long as it is comfortable to access. I put this in a folder called "RIVALS_DATA" on my machine.

# Creating a Patch File
Most of the work here is going to be relevant for getting the data for the wiki, since with the above JSON files, you should be able to do whatever you want with it now that you know what's going on. Here, we're just doing some simple ways to interact with it.
You'll need Python and a notebook interpreter. Personally, I use VSCodium.
- Open up `patch_making.ipynb` in your interpreter.
- You'll need to update some paths. 
 - Edit the home_path variable to match where you stored your character folder from before.
 - Edit the dest variable as well. For consistency, make this match the patch version that you are updating to. For example, Rivals on patch 1.0.3 was labelled as `r2data_patch_103.json` on my end.
 - You'll want to go through each of the cells that you want to run.
 - Alternatively, you can click "Run All" and run all the cells in the notebook, as long as you configured the first cell correctly. If no errors occur, good! If an error occurs, whoops, let me know.

# Other files
Some other files are now obsolete due to the wiki format and will be cleaned up at some point. Only one that wiki users need pay attention to is probably `patch_making.ipynb`.
