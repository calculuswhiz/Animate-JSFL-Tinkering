Animate doesn't check your JavaScript for HTML5 Canvas projects. Furthermore, all JS gets dumped to one file. This means that if you accidentally open a comment in some frame's action panel:

```js
console.log('Hello.');
/*
```

This can cause errors that are hard to debug in the final export. To ease this, you can integrate a globally installed eslint into Animate while you work. The following can be created as a JSFL command.

Lint.jsfl

```js
/* Requires ESLint to be installed on your system. */

(function () 
{	
	fl.outputPanel.clear();

	// Figure out localappdata config directory
	var tempDirPath = 
		fl.configDirectory
			.replace(/(AppData\\Local)\\.*/, '$1') 
		+ '\\Temp\\animate-eslint'; 
	var tempDirURI = FLfile.platformPathToURI(tempDirPath);
	var srcFile = 'lint_me.js';
	var outFileName = 'lintout.txt'

	// Linter Setup
	if (!FLfile.exists(tempDirURI))
		FLfile.createFolder(tempDirURI);

	var source = fl.actionsPanel.getText();
	if (!FLfile.write(tempDirURI + '/' + srcFile, source))
		throw new Error('Could not write source file');

	// Run and display
	FLfile.remove(tempDirURI + '/' + outFileName);

	var esLint = 'npx eslint ' + 
	[
		'-o "' + outFileName + '"',
		srcFile,
		'--no-eslintrc',
		'--no-color',
		'--parser-options=ecmaVersion:6'
	].join(' ');

	var command = 
	[
		'cd /D "' + tempDirPath + '"',
		esLint
	].join(' & ');
	
	FLfile.runCommandLine(command);

	var lintResults = FLfile.read(tempDirURI + '/' + outFileName);
	fl.trace(command);
	fl.outputPanel.trace(lintResults || 'eslint reported no problems');
})();
```
