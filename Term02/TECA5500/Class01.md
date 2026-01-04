VSC to Maya 
-
install MayaCode extension in VSC 
https://marketplace.visualstudio.com/items?itemName=saviof.mayacode

Run Mel in Maya 
  commandPort -name "localhost:7001" -sourceType "mel" -echoOutput;
  commandPort -name "localhost:7002" -sourceType "pyton" -echoOutput;

this code to setup vs code sending to maya, this is using the standard number for sending to the computer itself so you don't need to change the number on different computer 

Environment Variables: Setup for the program
- 
// MEL // 
getenv "MAYA_MODULE_PATH"
getenv "MAYA_APP_DIR" // maya application directory  

https://help.autodesk.com/view/MAYAUL/2024/ENU/?guid=GUID-8EFB1AC1-ED7D-4099-9EEE-624097872C04

if i want change thing inside maya  
getenv "MAYA_CUSTOM_TEMPLATE_PATH"
putenv "MAYA_CUSTOM_TEMPLATE_PATH" ";Z:/test;Z:/hello" 
