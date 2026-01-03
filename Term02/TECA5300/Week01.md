01 UnderstandingRTR
- 
fdfdfdsfsd

02 DeferredVSForward
- 
sdfsdfsghsfh

03 CPU
-  
dsgdsgsgd

04 StaticMesh Overview ~ 05 LODs
- 
LOD - Level of Detail
<img width="1142" height="570" alt="image" src="https://github.com/user-attachments/assets/7469fac7-02e8-46b2-a889-224e781c4104" />
Highest LOD - LOD 0 - LOD 3 - LOD 5  
https://www.fab.com/listings/f5edf787-c6fe-4452-b952-ad66ce7581a0  


Collision 
- doesnt need to match exact depending on its use, colliders cannot be concave
  - to avoid this create multiple convex colliders
- you can add and remove collision defaults in UE inside the static mesh's option menu 
- you can have multiple colliders on same object 
- should not overlap each other
- you can make collider out of multiple boxes, they are seen as one collider as a whole.

- Naming convention in maya
<img width="179" height="66" alt="image" src="https://github.com/user-attachments/assets/59aca50b-f57e-43ea-920a-254a5ba19b92" />  
- UCX_ is prefix - custom collision meshes, Universal Collision(Convex)    
  - copy and paste the static mesh names

06 Grid System ~ 12 Exporting and Importing 
-
- USD pipeline
- 
  
- The colliders might import a material slot, if they do this just make sure the collider has the same material assigned as the object (or one of) so that it doesnt create an extra slot
<img width="1082" height="491" alt="image" src="https://github.com/user-attachments/assets/13176442-f9b1-46e8-be7e-28d2e9061d98" />
grid option in Maya  
1 unit is 1 cm  
Axes is length and width units  

<img width="1195" height="605" alt="image" src="https://github.com/user-attachments/assets/6ce24cc6-a20f-41f5-976f-b47af7ef4d34" />  
To snap to the grid, hlod down 'x' and with the grid lines its easy to know how big you object is without looking at measurments 

Pivot point
- pivot point dont all share one conrrect pivot location but objects having their correct pivot point is important
- pivot point is where the object literally points from where it will snap to the grid

<img width="652" height="660" alt="image" src="https://github.com/user-attachments/assets/b172c36f-41fd-4999-8865-4cbcf76bd694" />  

- When you try to export file from Maya to UE always use Game Exporter instead of General Export

* When you need to fix pivot point or material go back to source file *
