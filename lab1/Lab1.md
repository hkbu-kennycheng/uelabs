# Lab 1 - Beginning Unreal Engine

<iframe width="560" height="315" src="https://www.youtube.com/embed/qC5KtatMcUw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

As you can see from the demonstration, **Unreal Engine** is very powerful computer graphic engine, which is designed for professionals like game developers, film producers and civil engineers. Now, it's time to get our hands dirty and start development with Unreal Engine.

## My first Unreal project

Let's download the [`UE01.zip`](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/UE01.zip) from our course-room. Then, start **Unreal Engine** editor and open the extracted `UE01` folder. Create a new **Film** project with name **ue01**. Please use **Blank** as template, and select **No Starter content**. It would load faster without Starter content

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/new%20project.png)


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

**Scene** is a concept in film, and games. The basic component in a scene consists of light source, camera and actor. In **Unreal Engine**, a scene is called ** Level**. The blank template provide us more than the essential components, so that it looks cool. Let's take a look at the Main Level.

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

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/MyProject%20-%20Unreal%20Editor%203_8_2020%207_30_31%20am.png)

Clicking on  **Level**, then select **Empty Level**.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/New%20Level%203_8_2020%206_45_04%20am.png)

We name the new Level as **NewWorld**. Please double click to open it. As you could see, it is showing a dark scene because of no actor and light source within the scene.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/newworld.png)


## Loading External Materials

Materials are resources used in your project. It could be 3D models, textures, images, animations and etc. To import materials, you may simply **drag-n-drop** material files in the **Content browser**. For texture images, it could be JPEG, png or other image file formats.


### Import texture for Orochimaru
Unreal engine supports various texture file format. To import model texture file, please **drag and drop** **orochimaru-texture.png** file to **Content browser**. After that, you need to  **right click**, then **Create Material**.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/MyProject%20-%20Unreal%20Editor%203_8_2020%207_29_55%20am.png)

### Import 3D model of Orochimaru

For 3D models, Unreal Engine supports FBX file format. After you **drop the FBX file in Content browser**, there would be a option dialog.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/FBX%20Import%20Options%201_8_2020%201_46_58%20am.png)

Please adjust the following options:(You need to **expend the Mesh section**)

- Mesh
    - **Combine Meshes**: Enable
- Material
    - **Material Import Method**: Do Not Create Material
    - **Import Texture**: Disable

Then simply click **Import** to import it as static mesh object.

### Mapping texture

In order to have a nice appearance for Orochimaru, we need to map corresponding texture for the model.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/orochimaru%203_8_2020%207_46_09%20am.png)

Please select **Orochimaru-texture_Mat** as Material in the **first Material slot**.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/orochimaru%203_8_2020%208_02_42%20am.png)

After that, please remember to click **save** button on top left corner.


## Composing a basic scene

We now try to make a simple scene by adding the essential components to the scene.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/orc.png)

### Adding Orochimaru to Scene

Simply drag `Orochimaru` from Content browser to scene. You could **move** it around with mouse by pressing **w** key, or **rotate** it by pressing **e** key and **scale** it by pressing **r** key. Please make it facing to front.

### Adding light source to scene

Please simply drag a **point light** to the scene from Place Actor panel.

### Adding Camera

Please drag a **Player Start** to the scene from Place Actor panel.

## Exercise 1

Load the **snake** model with similar procedure. The snake model **need 3 texture files** for different body part.

<!--
	**Hint:** Move , rotate and scale  the model as needed. -->

# Blueprint

![](https://docs.unrealengine.com/Images/Engine/Blueprints/HowTo/BPCommTopic.jpg)


Blueprint is a **visual scripting system** used in Unreal Engine. It is a **node-based visual programming interface** for you to create dynamic components from within Unreal Editor. As with many common scripting languages, it is used to define **object-oriented (OO) classes or objects** in the engine.

## Creating a Blueprint class for making the snake move

To add a Blueprint class, please click on the green **Add New** button in **Content Browser**.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/MyProject%20-%20Unreal%20Editor%203_8_2020%207_30_36%20am.png)

Please select **Actor** and name it as **MovingSnake**.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/Pick%20Parent%20Class%203_8_2020%208_25_15%20am.png)

Please **double-click to open it** after created.

## Adding component to Actor

Please add a **Static Mesh** component by clicking the grenn **Add Component** button in top left **Content** panel. Then name it as **Snake**.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/MovingSnake%203_8_2020%208_40_46%20am.png)

After that, Please select **snake** as static mesh in **Static Mesh section** of the right panel.

## Basic events in Event Graph

Before the program the snake to move, let's take a look to the **Event Graph**.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/MovingSnake%203_8_2020%206_24_39%20am.png)

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

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/MovingSnake%203_8_2020%206_34_04%20am.png)

Here are the steps for creating above programming graph.

1. **Drag in initial location variable** from variable panel **to Event Graph**, Select **set initial location**
2. Connect the execution from **Event BeginPlay** to **Set** node
3. Drag in **Snake** from component to Event Graph
4. Drag out from the **Snake node** to somewhere,  search for **GetWorldLocation** and select it.
5. Connect the **return value** of **GetWorldLocation** node to **initial location** of **Set** node.

### Random snake location in Event tick

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/random-snake-location.png)

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
    <source src="https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/MyProject%20-%20Unreal%20Editor 2020-08-03%2009-17-41.mp4" type="video/mp4" />
</video>
 
## Exercises 2

Move the point light and change color to simulate a **glowing flame** effect.

<video width="800" height="480" controls>
    <source src="https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab1/MyFirstProject%20-%20Unreal%20Editor%202020-08-03%2006-11-20.mp4" type="video/mp4" />
</video>

Don't forget to submit your work to our course room.
.