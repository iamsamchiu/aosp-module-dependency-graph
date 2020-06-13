# aosp-module-dependency-graph
A tool generating the module dependency graph from android open source tree.  
  
This project is inspired by https://github.com/qinshulei/aosp-makefile-tree but aims to develop a tool to summary/demonstrate the modules dependencies in aosp.  
  
TODO:  
1. Manually generate module*.json which contain the module dependency info via building aosp.(DONE). 
2. Creates a graph of dependencies(gexf) from module*.json.(reference: https://graphology.github.io/). 
3. Generate visualize graph by using https://github.com/raphv/gexf-js. 
4. A script to continuously generate module*.json from various android versions.  
  
