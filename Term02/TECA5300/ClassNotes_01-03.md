Rendering Theory: Real Time Rendering
-

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

Week2 - 
Geometry Rendering 
-
- Frame 2 - Time 66 ms - GPU
- Now that the CPU has figured out where everything, now we have to do one of the most intensive part, and that is rendering the Geometry
- But before we can even do the rendering of Geometry we have to do a Prepass/Early Z pass
- The GPU now has a list of models and transforms but if we'd just render this info out we would cause a lot of redundant pixel rendering
- So we need to figure out which models will be displayed where in advance

Draw Calls
- 
<img width="1512" height="455" alt="image" src="https://github.com/user-attachments/assets/1d87bd6a-1cb7-4322-956d-356787ce92d1" />
<img width="1865" height="411" alt="image" src="https://github.com/user-attachments/assets/52d19cc8-afa8-496c-8986-79b8c34d1f58" />

- GPU now starts to render. It renders drawcall per drawcall which is essentially one "thing" at a time.
  - A group of polygons sharing the same properties, a material, a texture, etc...

<img width="440" height="483" alt="image" src="https://github.com/user-attachments/assets/89880ed4-4f92-4d46-87e5-44505f137b65" />
<img width="1024" height="509" alt="image" src="https://github.com/user-attachments/assets/fe4a3b60-8ac8-425f-9241-2e197271de22" />

- You can measure this with "stat RHI" (type in UE console : stat RHI)
- 2000-3000 is reasonable  
- 5K+ is getting high, more than 10K+ is probably a problem.   
- Drawcalls have a huge impact on performance  
- Each time the renderer is done it needs to receive commands from the render thread which adds overhead  
- Drawcalls have a much bigger impact than polycount in many scenarios  
- It used to matter in the 90s, it used to matter, but nowadays it's more about drawcalls.  
- Imagine copying 1 single 1 GB file (2-3 minutes?) VS Copying 1 million 1 KB files (1 days?)  
- Drawcall Performance Implications  
  - The cost to Rendering many polygons is often lower than the drawcall expense  
  - 50k triangles can run worse than 50 million dependent on implementation  
  - Drawcalls have a base expense thus optimizing low poly to super low poly may make zero difference  
  - Using a modular mesh workflow you can always merge meshes later on if needed and if the content is near final  
  - Use the Statistics and Stat commands to find the best choices for merging  
  - Once merged, you cannot easily go back. Only do this at the end.  
  - If you merge meshes following rules make better choices: The more common a mesh AND the lower poly the better  
  - Merge only meshes within the same area and/or sharing the same material  
  - Meshes with no or simple collision are better for merging  
  - Smaller meshes or meshes receiving only dynamic are better choices  
  - Distant geometry (far away) is usually great to merge  
  - You can merge things by simply exporting: Select Objects, Export, then merge in Maya and/or In UE, Select objects -> Tools -> Merge Actors    
  - But, how much to merge and exactly how to is greatly dependant on many factors  
  - Oftend there is no need to merge anything. The majority of content knows no or little merging  
  - On very low end hardware you might merge almost everything  
  - Balance is Key  
  - Why not just figure out which objects are which? - You can do that. It's called **Instance Static Mesh rendering**  
  - It Automatically groups models together in single drawcalls  
  - It is not enabled standard because it gives overhead   
  - Finally, there is LOD'ing - Level of Detail  
    - Simplifies a model or Bunch of models in given conditions  
    - Usually means a model becomes lower poly in the distances  
    - Essentially swaps on model for another simpler model  
    - HLOD is bigger version, it groups model together in the distance to lower the drawcalls   
