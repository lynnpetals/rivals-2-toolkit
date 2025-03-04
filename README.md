# rivals-2-toolkit
A bunch of assets for Rivals of Aether II work.

# Extracting JSONs using Fmodel

You'll need a copy of Rivals 2, and you'll need [FModel](https://fmodel.app/download). Make sure to have both. You'll also need a Unity Script Mappings (.usmap) file. Currently, these can be found in a [thread](https://discord.com/channels/935257484359245884/1344158785752797309) in the Dragdown Wiki Discord server, though instructions for how to get them yourself will be added later.

First, install FModel. Then, open FModel.
- FModel needs to know where your game is, so it'll show a prompt. Click below "ADD UNDETECTED GAME".
 - You'll need to find the path where your Rivals of Aether II is installed. For me, it's installed in "C:\Program Files (x86)\Steam\steamapps\common\Rivals 2\".
 - With that path, next to Directory, click "..." and paste in your Rivals of Aether II path.
 - The name can be whatever you want, "Rivals 2" for simplicity.
 - Make sure to select UE5_4 for the engine version. Then, hit "OK". It'll ask you to restart FModel.
 Great! Now you need to add your mapping file.
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

Congrats! Now you have your characters folder. You can move this wherever you would like, as long as it is comfortable to access. I put this in a folder called "RIVALS_DATA" on my Documents folder.

# Creating a Patch File
You'll need Python and a notebook interpreter to do that. Personally, I use VSCodium, an open source version of VSCode to avoid any telemetry stuff if you're not a fan of that.
- Open up `patch_making.iypnb` in your interpreter.
- You'll need to update some paths. 
 - Edit the home_path variable to match where you stored your character folder from before.
 - Edit the dest variable as well. For consistency, make this match the patch version that you are updating to. For example, Rivals on patch 1.0.3 was labelled as `r2data_patch_103.json` on my end.
 - Then, click "Run All" and run all the cells in the notebook. If no errors occur, good! If an error occurs, whoops, let me know.
 - Now you've got a patch file!

# Examining Frame Data
Open up `analysis.ipynb`, and then "Run All" on the notebook.
- The section under `Frame Data:` contains the cell that you'll want. It'll give frame data for every single move of every single character. If you want a specific character, you can go to `chare = x` and replace `x` with the character name you want. For example, Maypul would be `"Maypul"`.
- There's a guide below on how to read it. It contains all the relevant info.

# Updating Wiki Hit Data
Open up `wiki_mind_reader.ipynb`. Run all the cells except for the last one. On VS Code, you can do this by going to the last cell and finding the "Execute Above Cells" button.
- Navigate to the character's /Data wiki page and get the source for it by clicking "Edit". Copy everything on the page.
- Paste it into readerscript.txt, and save it.
- Then, run the bottom cell.
 - Sometimes, the wiki will use different names for certain hits, and they have to be renamed in the wiki_conversion.csv file. You'll need to add an entry for it if it's missing.
 - If you ever edit the wiki_conversion.csv file, you'll have to save it and rerun all the previous cells before.
- Once that's done, open up writerscript.txt. Copy its contents, paste it back to the /Data wiki page, and make sure to preview it.
- Do a manual inspection. It can get funky sometimes depending on some of the code written, or some of the formatting on the wiki page. If the correct changes show up (and they match the patch notes), everything should be good. From there, you can just save the wiki page and move on.
- You only have to run the last cell every time you do a new character which is pretty painless.
