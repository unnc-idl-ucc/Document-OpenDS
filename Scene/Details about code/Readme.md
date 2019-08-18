
<!--ts-->

   * [Demonstration to Set Up](#Demonstration_to_Set_Up)
      * [Geometry](#Geometry)
      * [Textures](#Textures)
      * [Models](#Models)
      * [Light](#Light)
      * [Export](#Export)

<!--ts-->

Demonstration_to_Set_Up
========

To set up the scene, you need to change the corresponding code. The code file is loacated at "\Scences-OpenDS\src\net\jmecn\physics3d" with name "*.java".

Geometry
-----
<br>
The Geometry is the basic element in the scene. Every object is a geometry or the combination of geometries in the scene. We can set the mesh shape,  size, material, position and rotation angle of the geometry in the code.
<br>

Geometry set up demonstration:

```bash
        Mesh Grand = new Box (3000f,0.1f,3000f);
        Material Grand_brick = new Material(
        assetManager, "Common/MatDefs/Misc/Unshaded.j3md");	
        Geometry grand = new Geometry("floor", Grand); 
        grand.setMaterial(Grand_brick);
        grand.rotate(0.0f,0.0f,0.0f);
        grand.setLocalTranslation(400, -0.11f, 398);
```
mesh shape|	Box
:- | :-
size in 3 dimensions|	(3000f,0.1f,3000f);
Rotation in 3 dimensions	|(0.0f,0.0f,0.0f);
Position in 3 dimensions	|(400, -0.11f, 398);


Textures
-----
<br>
The Textures are some 2D image and we paste the texture onto the geometry to show different objects. We can set pasted mode(Clamp/Repeat)
<br>

Textures set up demonstration:

```bash
        Texture grasst = assetManager.loadTexture("Scenes/Task/two/grass.png");
        grasst.setWrap(WrapMode.Repeat);
        Grand.scaleTextureCoordinates(new Vector2f(3000, 3000));
        Grand_brick.setTexture("ColorMap", grasst);
```
Wrap Mode|	Repeat
:- | :-
Texture flie path|	Scenes/Task/two/grass.png
Texture mode|  Repeat
repeat number in 2 dimensions|	(3000,3000);

Models
-----
<br>
Some models can be imported to the scene by code. The supported model files are *.j3o, *.mesh.xml, *.scene, *.obj+*.mtl, *.blender.
We can reset up models' size, rotation and position.
<br>

Models Imported demonstration:

```bash
        String model_path = "Scenes/Task/speedLimit50/speedLimit50.scene";
        assetManager.registerLocator("assets", FileLocator.class);
        Spatial speed_limit = (Spatial) assetManager.loadModel(model_path);
        speed_limit.scale(2f, 2f, 2f);
        speed_limit.rotate(0f, 3.1415f, 0)
        speed_limit.setLocalTranslation(-5f, -1.1f, -200f);
        rootNode.attachChild(speed_limit);
```
Model type|	.scene
:- | :-
Model flie path|Scenes/Task/speedLimit50/speedLimit50.scene
size scale in 3 dimensions|	(2f, 2f, 2f);
Rotation in 3 dimensions	|(0f, 3.1415f, 0);
Position in 3 dimensions	|(-5f, -1.1f, -200f);

Light
-----
<br>
We can add lighting in different directions to make the photosensitive material show the original color.
<br>

Light set up demonstration:

```bash
        DirectionalLight light = new DirectionalLight();                        
        sun1.setDirection(new Vector3f(0.1f, 0.7f, 1.0f).normalizeLocal());
        rootNode.addLight(sun1);
```
Light|	Light
:- | :-
Light attitude |(0.1f, 0.7f, 1.0f);


Export
-----
<br>
In order to use in OpenDS, we need to export the scene file as .j3o file. The export function is used to save the sceneto a custom path as .j3o file.
<br>

Export set up demonstration:

```bash
    export_path = "Result/scene.j3o";
    public void Export(String export_path){
        
        BinaryExporter exporter = BinaryExporter.getInstance(); 
        assetManager.registerLocator("assets", FileLocator.class);
        File file = new File("assets" + export_path.replace("Scene", "j3o"));
        try {
            exporter.save(rootNode, file);
        } catch (IOException ex) {
            ex.printStackTrace();
    }
```
save type|	.j3o
:- | :-
save path|	./assets/Result/
file name	| scene.j3o
