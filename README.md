# aosp-module-dependency-graph
A tool generating the module dependency graph from android open source tree.  
  
This project is inspired by https://github.com/qinshulei/aosp-makefile-tree but aims to develop a tool to summary/demonstrate the modules dependencies in aosp.  

Most of tasks are all working in progress.  
Action TODO:  
1. Manually generate module*-info.json which contain the module dependency info via building aosp.(DONE). 
2. Creates a graph of dependencies(gexf) from module*.json.(reference: https://graphology.github.io/). 
3. Generate visualize graph by using https://github.com/raphv/gexf-js. 
4. A script to continuously generate module*.json from various android versions.  
  
## The dependency info in modules*.json
There are three kinds of module json in aosp which are all the intermediate files generated while building android source.
- module-info.json, created by make build system
- module_bp_cc_deps.json, created by Soong build system
- module_bp_java_deps.json, crewated by Soong build system 

make build system is going to be deprecated and will be replaced by [Soong build](https://source.android.com/setup/build). Before that we still consider supporting the module-info.json created for make.

One dependency example in module_bp_java_deps.json could be as below:
```
	"Stk": {
		"dependencies": [
			"telephony-common",
			"com.google.android.material_material"
		],
		"srcs": [
			"packages/apps/Stk/src/com/android/stk/BootCompletedReceiver.java",
			"packages/apps/Stk/src/com/android/stk/StkApp.java",
			"packages/apps/Stk/src/com/android/stk/StkAppInstaller.java",
			"packages/apps/Stk/src/com/android/stk/StkAppService.java",
			"packages/apps/Stk/src/com/android/stk/StkCmdReceiver.java",
			"packages/apps/Stk/src/com/android/stk/StkDialogActivity.java",
			"packages/apps/Stk/src/com/android/stk/StkDigitsKeyListener.java",
			"packages/apps/Stk/src/com/android/stk/StkInputActivity.java",
			"packages/apps/Stk/src/com/android/stk/StkLauncherActivity.java",
			"packages/apps/Stk/src/com/android/stk/StkMain.java",
			"packages/apps/Stk/src/com/android/stk/StkMenuActivity.java",
			"packages/apps/Stk/src/com/android/stk/StkMenuAdapter.java",
			"packages/apps/Stk/src/com/android/stk/StkMenuConfig.java",
			"packages/apps/Stk/src/com/android/stk/ToneDialog.java",
			"packages/apps/Stk/src/com/android/stk/TonePlayer.java"
		],
		"srcjars": [
			"out/soong/.intermediates/packages/apps/Stk/Stk/android_common/gen/android/R.srcjar"
		]
	},
```

"Stk" is one of android modules, the modules are playing different role in aosp, e.g. They could be Apps, library or tools.  
"srcs" under "Stk" is listing all the source code in Stk module.
"dependencies" under "Stk" is listing what other modules this Stk is depending on. In this case, "Stk" is depending on "telephony-common" and "com.google.android.material_material" so we could keep looking into "telephony-common" for digging out more implict dependencies.

### How to generate module*.json
(TBD)
