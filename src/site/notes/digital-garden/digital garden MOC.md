---
{"dg-publish":true,"permalink":"/digital-garden/digital-garden-moc/","tags":["digital-garden"],"created":"","updated":""}
---


# Digital-garden

## About

This is a MOC containing workflows I use to build an maintain my personal Digital Garden. 

Current approach is that I maintain my main local vault separately. My digital garden that I publish online is located in a separate local folder (`digital garden`). Those files can be published online (do not contain private information). They are copied from main folder (vault `work`) using bash script (see below) and published using awesome plugin [GitHub - oleeskild/obsidian-digital-garden](https://github.com/oleeskild/obsidian-digital-garden) and free Vercel account. 

## Copy Files From Obsidian-sync Vault to Digital-garden Vault Using Automator

This code is for macOS Automator. It copies selected folders from main vault to `digital garden`. Existing files, folders will be replaced.

Original commands 

```Shell

rsync -aE --delete /Users/maksim/Library/Mobile\ Documents/iCloud\~md\~obsidian/Documents/obsidian-sync/resources/digital-garden/home.md ~/digital-garden/

rsync -aE --delete /Users/maksim/Library/Mobile\ Documents/iCloud~md~obsidian/Documents/obsidian-sync/resources/learning-tools/cypress ~/digital-garden/

rsync -aE --delete /Users/maksim/Library/Mobile\ Documents/iCloud~md~obsidian/Documents/obsidian-sync/resources/learning-tools/playwright ~/digital-garden/

rsync -aE --delete /Users/maksim/Library/Mobile\ Documents/iCloud~md~obsidian/Documents/obsidian-sync/resources/learning-tools/git ~/digital-garden/

rsync -aE --delete /Users/maksim/Library/Mobile\ Documents/iCloud~md~obsidian/Documents/obsidian-sync/resources/learning-tools/javascript ~/digital-garden/

```

Bash script

```Shell

source_path="$HOME/Library/Mobile Documents/iCloud~md~obsidian/Documents/obsidian-sync/resources"
destination_path="$HOME/digital-garden"

declare -a locations=("digital-garden/home.md" "learning-tools/cypress" "learning-tools/playwright" "learning-tools/git" "learning-tools/javascript" "learning-tools/feature-toggles")

for location in "${locations[@]}"
do
    rsync -aE --delete "$source_path/$location" "$destination_path/"
done

```

 Copy Automator the application into the startup items folder to run every time your computer starts.

```Shell
/Library/StartupItems
```

## Find and Replace Text to Resize Images in Multiple Files Using VS Code

In VS Code:

Hotkey: `Cmd+Shift+H`

Find: `(\w+)\.(jpeg|png)\b(?!.*\|\d{3}\]\])`

Replace: `$1.$2|500`

## Create MOC Automatically

1. Create moc file
2. In linked notes, reference MOC file
3. Use plugin [GitHub - dalcantara7/obsidian-auto-moc](https://github.com/dalcantara7/obsidian-auto-moc) to generate MOC file automatically using mentions or tags
4. Run command: `AutoMOC: Add  missing linked mentions at the coursor position`

## Move Files with the Same Tag to Separate Folder

Use File cooker plugin to move files in bulk

1. Ensure all files have tag
2. Run command: File Cooker: Move links in current file to ..

## Create Subdomain in Hostinger and Connect to Vercel App

View this note for more details: [[digital-garden/create subdomain in hostinger and connect to vercel app\|create subdomain in hostinger and connect to vercel app]]


