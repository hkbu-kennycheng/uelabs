# Lab2 Solar System and Texture Mapping

# Solar System

Today, we are going to develop an animation for the **Solar System (Sun, Earth and Moon)**. We will also apply **lighting and textures** to make the animation more realistic.

## Basic Setting

Let's **create a new Unreal project** with `Game -> Blank` template, or you could use the previous project if you want to avoid slow loading. Please download [UE02.zip](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab2/UE02.zip) and extract it, which contains texture files for sun, earth and moon.

Let's **create a new Level** by clicking on **<span style="color:white; background:green">Add New</span>** button in **Content Browser**. After that, please double-click on it.


Let's **import the texture files** to the project by drag-and-drop them to **Content Browser**. Please create Material only for the following textures:

- texture_sun
- texture_earth
- texture_moon

Let's **create a new Blueprint** for the Solar System by clicking on **<span style="color:white; background:green">Add New</span>** button in **Content Browser**. Please select **pawn** as parent class in the dialog and **name** it as **Solar**.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab2/Pick%20Parent%20Class%204_8_2020%2010_22_46%20pm.png)

So that we have the following resources for the project.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab2/lab2-basic.png)

Let's double-click Solar to begin.

## Modeling Solar System with Blueprint

### Adding essential objects

Let's try to place the essential objects to this Blueprint. We will need a **camera**, a **sphere** and **a point light**. The **point light** is place at the **same position as sun**. Please organize them like the following.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab2/Solar%205_8_2020%205_44_53%20am.png)

After that, please map **texture_sun_Mat** to **Sun**.

### Setting default view target as the Blueprint

In order to rendering perspective of this camera as default, we need to set the **target view** of **player controller** to this blueprint during **Event BeginPlay**

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab2/Solar%205_8_2020%205_54_27%20am.png).

Here are the detail step to create above event graph.

1. Right click on anywhere near **Event BeginPlay**, search for **Get Player Controller** and select it.
2. Drag from **Return value** of **Get Player Controller** node to somewhere, search for **Set View Target With Blend** and select it.
3. Drag from **New view target** of  **Set View Target With Blend**, search for **self** and select it.
4. Connect the execution from **Event BeginPlay** to **Set View Target With Blend**

After that, it would view from the blueprint camera when the game start.

### Exercise 1

Please Earth sphere, adjust the scale/position and map its texture.


## Animation of Solar System

#### Revolution

![](http://www.scienceisart.com/B_Tides/EarthMoonCOG.png)

The main question is how to make our Earth spin around the Sun. In fact, the Earth doesn't spin around the Sun. Physics tells us that both the Sun and the Earth orbit around the center of masses of the Solar system. Thus, in order of simulate this behavior, the Earth is added under the Group of Sun.

### Self-rotation

We learnt how to move an object last lab. Let's simply apply similar technique to perform self-rotation on the Sun.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab2/Solar%205_8_2020%206_16_16%20am.png)

The steps to create above Event Graph as follows.

1. Drag **Sun** from Components of **Variable** to somewhere in Event Graph, select **Get Sun**
2. Drag from the newly created **Sun** node to somewhere, search for **AddLocalRotation** and select it.
3. Setting the **Delta value of Z** to **0.05** in **AddLocalRotation** node, and connect the execution to **Event Tick**.

After that, we could switch back to **Viewport** and click on **Simulation** on the top to see result.

### Exercise 2

Please add Moon and make it rotation around the center of mass of Earth.

# Basic shader and texture mapping

In fact, we still can't see Sun when added Solar system to Level. It's because the point light is wrapped inside the Sun sphere and the specular is 0.5  by default. Meaning that, the Sun surface also need a light covering it in order to make it visible. But it's not the concept for our Solar system. Instead, the Sun should emit light.

## Basic shader properties

### Base color

Base color defines the overall color of the material in Vector3 data structure. There are 3 (r,g,b) color channels ranged from 0 to 1 in floating point.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab2/NewMaterial%205_8_2020%209_41_03%20am.png)

Above example show you how to use normal vector of surface as base color.

### Metallic

![](https://docs.unrealengine.com/Images/Resources/ContentExamples/MaterialNodes/1_2/1_2_Metallic.webp)

Metallic controls how "metal-like" the surface look like. The value is ranged from 0 to 1 in floating point. For pure surfaces, such as pure metal, pure stone, pure plastic, etc. this value will be 0 or 1, not anything in between. When creating hybrid surfaces like corroded, dusty, or rusty metals, you may find that you need some value between 0 and 1.

### Specular

![](https://docs.unrealengine.com/Images/Resources/ContentExamples/MaterialNodes/1_3/1_3_Specular.webp)

For non-metallic surface material, you could controls how your surface reflect lights. You could input a scalar value between 0 (non-reflective) and 1 (fully reflective). Note that a Material's default Specular value is 0.5.

### Roughness

![](https://docs.unrealengine.com/Images/Resources/ContentExamples/MaterialNodes/1_4/1_4_Roughness.webp)

Roughness controls how rough or smooth a Material's surface is. Rough Materials scatter reflected light in more directions than smooth Materials, which controls how blurry or sharp a reflection is (or how broad or tight a specular highlight is). A Roughness of 0 (smooth) results in a mirror reflection and roughness of 1 (rough) results in a diffuse (or matte) surface.

### Emissive

![](https://docs.unrealengine.com/Images/Resources/ContentExamples/MaterialNodes/1_5/1_5_Emissive.webp)

Emissive Color in a material node controls which parts of your material will appear to glow. Ideally, this will receive a masked texture (mostly black except in the areas that need to glow).

## Emissive Color for the Sun

Let's make the Sun Emissive using texture h-alpha-2k that we have already imported. Please **double-click** on **texture_sun_Mat** to open up the shader editor.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab2/texture_sun_Mat%204_8_2020%209_47_45%20pm.png)


### Exercise 3

Let's try it out by adding Solar to Level. Please adjust the scalar to make it realistic.

<video width="800" height="480" controls>
    <source src="https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab2/MyProject3%20-%20Unreal%20Editor%202020-08-05%2006-36-55.mp4" type="video/mp4" />
</video>

## Texture Mapping

Let's visit NormalMap-Online (http://cpetry.github.io/NormalMap-Online/) and simply provide any image. This web app is able to generate all the useful maps for you by uploading photo to the website. Simply select each map from the middle panel and hit Download. 

Here is another option for you to download user-made texture. You could found completely free texture image for modeling different materials on [https://cc0textures.com/](https://cc0textures.com/).

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab2/Search%20Results%20on%20CC0%20Textures%20-%20Google%20Chrome%205_8_2020%208_31_25%20am.png)

<!-- <iframe src="https://cc0textures.com/list?sort=Popular" style="width:100%; height:500px" border=0></iframe> -->

Let's **choose one to download** as you like and **import to your project**. Each texture zip would contains base color image, normal map, displacement map, ambient occlusion and roughness map / specular map.

Please **create material** using the base color image. 

### Normal

![](https://docs.unrealengine.com/Images/Resources/ContentExamples/MaterialNodes/1_9/1_9_Normal.webp)

Normal is used to provide significant physical detail to the surface by perturbing the "normal," or facing direction, of each individual pixel. It require you to provide a normal map for the material.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab2/Bricks051_2K_Color_Mat%205_8_2020%209_23_41%20am.png)

Let's drag it out from **Normal** to somewhere, search for **Texture Sample** and select it. In the **Details panel** on the left, select the **imported normal map file** for the texture.


### World Position Offset

![](https://docs.unrealengine.com/Images/Resources/ContentExamples/MaterialNodes/1_10/1_10_WPO.webp)

World Position Offset input allows for the vertices of a mesh to be manipulated in world space by the Material. This is useful for making objects move, change shape, rotate, and a variety of other effects. This is useful for things like ambient animation.

### World displacement

World Displacement works very much like World Position Offset, but it uses Tessellation vertices rather than the base vertices of the mesh. In order for this to be enabled, the Tessellation property on the Material must be set to something other than No Tessellation.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab2/tessellation.png)

Please find the setting in the **Details panel** on the left.

Let's try it out with the imported displacement map by the following graph. Please note that, the **Distance** node is a **ScalarParam**.

![](https://docs.unrealengine.com/Images/Engine/Rendering/Materials/MaterialInputs/DisplacementNetwork.webp)

### Tessellation Multiplier

![](https://docs.unrealengine.com/Images/Resources/ContentExamples/MaterialNodes/1_12/1_12_TessMult.webp)

Tessellation Multiplier controls the amount tessellation along the surface, allowing more detail to be added where needed. It's depends on World displacement setting.