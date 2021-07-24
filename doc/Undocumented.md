Here, you'll find undocumented stuff (commands, events, etc.) that aren't found in the [official docs](https://www.adobe.io/apis/creativecloud/animate/docs.html).

# Commands

## FLfile.runCommandLine(command)

### Usage

Runs a command from CMD. `command` is the string that get run. If you want to pass multiple commands in the same prompt, you can use the `&` character like this:

```js
FLfile.runCommandLine('echo hello world & pause');
```

The CMD prompt will block the script until the prompt closes.

### Returns

Always returns `1` for me. Perhaps this would be `0` if I didn't have permissions to open CMD.

## FLFile.readBinary(fileName)

### Usage

Read binary data from a file.

### Returns

The binary content of the file as a base-64 encoded string. As of now, I don't know of any native way to decode base64, though. That's probably why it's undocumented.

# Events

For the [`fl.addEventListener()`](https://www.adobe.io/apis/creativecloud/animate/docs.html#!AdobeDocs/developers-animatesdk-docs/master/flash_object_(fl)/fl1.md) command, 
there are several events not mentioned by the docs.

The following strings were found using Ghidra. I haven't tested them yet though.

```
debugExecutionChanged
deleteSyncSettingsSuccess
documentChanged
documentClosed
documentContentChanged
documentNew
documentOpened
documentRedo
documentSaved
documentUndo
dpiChanged
frameChanged
layerChanged
libraryChanged
postPublish
prePublish
selectionChanged
syncApplyPending
syncError
syncIdle
themeChanged
timelineChanged
```
