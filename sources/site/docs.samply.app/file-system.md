# Source: https://docs.samply.app/file-system.html

# File Management [​](https://docs.samply.app/#file-management)

Samply’s cloud filesystem manages your files seamlessly, so you don’t have to. However, understanding its structure lets you take full advantage of its capabilities.

Like traditional filesystems, it supports **Files** and **Folders**, but it also introduces **Stacks** to help manage versions efficiently.

## Files [​](https://docs.samply.app/#files)

Add files by dragging and dropping or selecting an option from the "+ Add" button. Files can be renamed, downloaded or deleted by right-clicking and choosing an option from the menu.

## Folders [​](https://docs.samply.app/#folders)

Create folders by right clicking anywher and choosing "create folder". You can add files to folders by dragging and dropping them into their respective folders

## Stacks [​](https://docs.samply.app/#stacks)

Stacks are ordered collections of files where the bottom file is the first added, and the top file is the most recent version. When you share a file from a stack, the link always points to the latest version.

### Adding Versions [​](https://docs.samply.app/#adding-versions)

- **Drag and Drop:** To add a version, drag a new file onto the file you want to stack it with.
- **From the Stack Preview:** Open the version indicator ("wafer"), click **Add version**, and select a file.
- **Directly in File View:** You can also drag and drop a new version directly into the File view.

> Note: Dragging one stack onto another will combine the two stacks. The dragged stack is placed on top of the target stack.

### Removing Versions [​](https://docs.samply.app/#removing-versions)

Click the "X" on the version you wish to remove. The removed file will appear next to its original stack.

**Note:** On smaller screens, you may need to press **Edit** first.

### Re-ordering Versions [​](https://docs.samply.app/#re-ordering-versions)

Re-order versions by clicking and dragging the drag-indicator. The original version names remain unchanged to ensure clarity.

**Note:** On smaller screens, you may need to press **Edit** first.

### Renaming Versions [​](https://docs.samply.app/#renaming-versions)

- **File Name:** Click on a version's name and type the new name. On mobile, enable the edit state first.
- **Version Tags:** Similarly, click on a version tag to rename it.

## Inheritance Rules [​](https://docs.samply.app/#inheritance-rules)

In Samply, certain properties automatically inherit from other elements, streamlining file organization and version management.

### Files [​](https://docs.samply.app/#files-1)

By default, a file’s name is inherited from the original uploaded file. You can rename it at any time, but downloaded files will retain their original upload name. 
_Note:_ We are considering updating this so downloaded files match their Samply name.

### Stacks [​](https://docs.samply.app/#stacks-1)

Stacks do not have a default name. Instead, they inherit the name of their **primary version**—the file at the top of the stack.

- If you rename a stack, only that name will be displayed.
- Clearing the stack name will revert it to the inherited behavior.