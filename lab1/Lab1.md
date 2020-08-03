# Lab 1 - Beginning Unreal Engine

As you can see from the demonstrations, **Unreal Engine** is very powerful computer graphic engine, which is designed for professionals like game developers, film producers and civil engineers. Now, it's time to get our hands dirty and start development with Unreal Engine.

## My first Unreal project

Let's download the `UE01.zip` from our course-room. Then, start **Unreal Engine** editor and open the extracted `UE01` folder. Create a new **Film** project with name **ue01**. Please use **Blank** as template, and select **No Starter content**. It would load faster without Starter content

![](https://drive.google.com/uc?export=download&id=11GlwUcoNsvTIMsvavRtnKzv9LKgbDNdl)


- Place Actors panel
    - A panel listing all **actors** for you to quickly place in the **scene**

- Content Browser panel
    - the primary area of the Unreal Editor for **creating**, **importing**, **organizing**, **viewing**, and **modifying** content assets within Unreal Editor

- World Outlineer panel
    - Interface for hierarchical tree-view of all Actors within the current level used for selection, attachment, and more.
    - It contains a text box that is used to search and quickly filter the list of **Actors in the scene**.

- Details panel
    - For showing details of an Actor in ** World Outliner**.

## Scene

**Scene** is a concept in film, and games. The basic component in a scene consisting of light source, camera and actor. In **Unreal Engine**, a scene is called ** Level**. The blank template provide us more than the essential components, so that it looks cool. Let's take a look at the Main Level.

### Components in the Main level

- Fog
    - provide a realistic sense of atmosphere, air density, and light scattering through atmospheric media
- Floor
    - a static mash
- Light source
    -  To simulate light, the scene would rendered as dark without any light source
- Player Start
    - is a capsule representing a player
    - a initial camera position
- Sky Sphere
    - To simulate sky of world
    - it  is a big sphere surrounding to show the cloud texture

### Creating new Level

Please click on the grean **Add New** button in **Content Browser**.

![](https://drive.google.com/uc?export=download&id=1IO_uJlyvZPlGJsOJsaS27Ml05VwI91nk)

Clicking on  **Level**, then select **Empty Level**.

![](https://drive.google.com/uc?export=download&id=1TSmMVuw9DV8kY91aoqmccai75EKEOs2m)

We name the new Level as **NewWorld**. Please double click to open it. As you could see, it is showing a dark scene because of no actor and light source within the scene.

![](https://drive.google.com/uc?export=download&id=1XTZbL5fP6pabfMb-38OP9UpVBAqrZn1N)


## Loading External Materials

Materials are resources used in your project. It could be 3D models, textures, images, animations and etc. To import materials, you may simply **drag-n-drop** material files in the **Content browser**. For texture images, it could be JPEG, png or other image file formats.


### Import texture for Orochimaru
Unreal engine supports various texture file format. To import model texture file, please **drag and drop** **orochimaru-texture.png** file to **Content browser**. After that, you need to  **right click**, then **Create Material**.

![](https://drive.google.com/uc?export=download&id=1qvRbYJZASIrtS_3vHwzWrbisbHoXlRIk)

### Import 3D model of Orochimaru

For 3D models, Unreal Engine supports FBX file format. After you **drop the FBX file in Content browser**, there would be a option dialog.

![](https://drive.google.com/uc?export=download&id=11Oo3qHFrD7UuTRNKrywXmu1ZqtHoXdCM)

Please adjust the following options:(You need to **expend the Mesh section**)

- Mesh
    - **Combine Meshes**: Enable
- Material
    - **Material Import Method**: Do Not Create Material
    - **Import Texture**: Disable

Then simply click **Import** to import it as static mesh object.

### Mapping texture

In order to have a nice appearance for Orochimaru, we need to map corresponding texture for the model.

![](https://drive.google.com/uc?export=download&id=1SZFKDtiZO_H9JX_6eCnWn1OEqm7_Ir-O)

Please select **Orochimaru-texture_Mat** as Material in the **first Material slot**.

![](https://drive.google.com/uc?export=download&id=1lIaCt_vYiL9d-VYex73z_5JA_IpxDSQC)

After that, please remember to click **save** button on top left corner.


## Composing a basic scene

We now try to make a simple scene by adding the essential components to the scene.

![](https://drive.google.com/uc?export=download&id=1nFu5oAJgZKlyguqxAls7ovLCF4hZFt5Z)

### Adding Orochimaru to Scene

Simply drag `Orochimaru` from Content browser to scene. You could **move** it around with mouse by pressing **w** key, or **rotate** it by pressing **e** key and **scale** it by pressing **r** key. Please make it facing to front.

### Adding light source to scene

Please simply drag a **point light** to the scene from Place Actor panel.

### Adding Camera

Please drag a  **Player Start** to the scene from Place Actor panel.




## Exercise 1

Load the **snake** model with similar procedure. The snake model **need 3 texture files** for different body part.

<!--
	**Hint:** Move , rotate and scale  the model as needed. -->

# Blueprint

![](https://docs.unrealengine.com/Images/Engine/Blueprints/HowTo/BPCommTopic.jpg)


Blueprint is a **visual scripting system** used in Unreal Engine. It is a **node-based visual programming interface** for you to create dynamic components from within Unreal Editor. As with many common scripting languages, it is used to define **object-oriented (OO) classes or objects** in the engine.

## Creating a Blueprint class for making the snake move

To add a Blueprint class, please click on the green **Add New** button in **Content Browser**.

![](https://drive.google.com/uc?export=download&id=10wQtTznmUnZCj_chVLJHxy34z0gDdNsH)

Please select **Actor** and name it as **MovingSnake**.

![](https://drive.google.com/uc?export=download&id=1L-uLK670_GlufSoQ9uaKJt9n8PBLuW1C)

Please **double-click to open it** after created.

## Adding component to Actor

Please add a **Static Mesh** component by clicking the grenn **Add Component** button in top left **Content** panel. Then name it as **Snake**.

![](https://drive.google.com/uc?export=download&id=1Gxt1z8e5uyQUkDRz960y5Y4VcoSS5_yw)

After that, Please select **snake** as static mesh in **Static Mesh section** of the right panel.

## Basic events in Event Graph

Before the program the snake to move, let's take a look to the **Event Graph**.

![](https://drive.google.com/uc?export=download&id=1jXC37gZyr38rFpMT6NoeXq-aV2F6VVPr)

- Event Begin Play
    - This event is triggered for all Actors when the game is started,
    - Actors spawned after the game is started will have this called immediately

- Event ActorBeginOverlay
    - Fired when this actor overlaps another actor, for example a player walking into a trigger.
    - Other actor gives you the overlaying actor

- Event Tick
    - called every frame, if ticking is enabled
    - Delta Seconds gives you the second between the previous tick

## Creating our first Program: Making snake move

### Creating Variable used to store the initial location of snake

In programming, a variable is a value that can change, depending on conditions or on information passed to the program.

Please click on `+` button in **My Blueprint** panel on the left. Name it as `initial location` and set **Variable type** to **Vector** in **Details** panel on the right.

### Setting variable value at **Event Begin Play**

![](https://drive.google.com/uc?export=download&id=1_g-90tFUd9dsBS7IyYS1mGUIjaQy2jsD)

Here are the steps for creating above programming graph.

1. **Drag in initial location variable** from variable panel **to Event Graph**, Select **set initial location**
2. Connect the execution from **Event BeginPlay** to **Set** node
3. Drag in **Snake** from component to Event Graph
4. Drag out from the **Snake node** to somewhere,  search for **GetWorldLocation** and select it.
5. Connect the **return value** of **GetWorldLocation** node to **initial location** of **Set** node.

### Random snake location in Event tick

![](https://drive.google.com/uc?export=download&id=15DkHpUvtFHE8UjlfjY_IiyCHdjfq-yG6)

Here are the steps for creating above programming graph.

1. Drag in **Snake** from component to Event Graph
2. Drag out from the **Snake node** to somewhere,  search for **SetWorldLocation** and select it
3. Connect execution from **Event Tick** to **SetWorldLocation** node
4. **Drag in initial location variable** from variable panel **to Event Graph** and select **get initial location**
5. Drag out from **initial location node** to somewhere, search for **Break Vector**  and select it
6. Drag out from **New Location** of **SetWorldLocation node** to somewhere, search for **Make Vector**  and select it
7. Connect **X** from **Break Vector** node to **Make Vector** node
8. Drag out **Y** from **Break Vector** to somewhere, search for `-` and select it
9. Drag out **Y** from **Break Vector** to somewhere, search for `+` and select it
10. Drag out **Y** from **Make Vector** to somewhere, search for **Random Float in Range** and select it
11. Connect **Result value** From `-` node to **Min** of  **Random Float in Range**.
12. Connect **Result value** From `+` node to **Max** of  **Random Float in Range**.
13. Repeat step 10 to 12 for **Z** in **Break Vector** 


After that, remember to click **compile** and  **save** before closing it.

<video width="800" height="480" controls>
    <source src="https://drive.google.com/uc?export=download&id=1Bz9ABNS-61jUSfVl5mpf52_xYLa52I0L" type="video/mp4" />
</video>
 
## Exercises 2

Move the point light and change color to simulate a **glowing flame** effect.

<video width="800" height="480" controls>
    <source src="https://drive.google.com/uc?export=download&id=1kOWhJbE5vKWBT6YomHcFYcmYqoFxh4i7" type="video/mp4" />
</video>

Don't forget to submit your work to our course room.
.