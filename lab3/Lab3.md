# Lab3 Texture Mapping and more shader techniques

## Texture Mapping

Let's visit NormalMap-Online ([http://cpetry.github.io/NormalMap-Online/](http://cpetry.github.io/NormalMap-Online/)) and simply provide any image. This web app is able to generate all the useful maps for you by uploading photo to the website. Simply select each map from the middle panel and hit Download. 

Here is another option for you to download user-made texture. You could found completely free texture image for modeling different materials on [https://cc0textures.com/](https://cc0textures.com/).

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab2/Search%20Results%20on%20CC0%20Textures%20-%20Google%20Chrome%205_8_2020%208_31_25%20am.png)

<!-- <iframe src="https://cc0textures.com/list?sort=Popular" style="width:100%; height:500px" border=0></iframe> -->

Please download [UE03.zip](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab3/UE03.zip), which already contain the **bricks** texture files.

You may also **choose one to download** as you like and **import to your project**. Each texture zip would contains base color image, normal map, displacement map, ambient occlusion and roughness map / specular map.

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


# Shader techniques

There are many different techniques in implementing shader program. Let's take a look at the follow two examples.

## Masking Color channel

![](https://p1.pstatp.com/large/pgc-image/4ed1b6cea47f4a228a5b707a5a839dc3)

Let's  implement a shader program to perform color effect of 月讀. Please create **import** the **Naruto** model with texture in to our Unreal project first. After that please **create material** with the texture file.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab3/naruto-texture_Mat1%207_8_2020%206_48_11%20am.png)

Here are the steps for creating above graph.

1. Drag from **RGB** pin of **Texture Sample** node to somewhere, search for **component mask** and select it.
2. Please check only **R** in **Details** panel on the left
3. Drag from **right** pin of **Mask ( R )** node to somewhere, search for **Round** and select it.
4. Drag from **right** pin of **Round** node to somewhere, search for **Ceil** and select it.
5. Drag from **right** pin of **Ceil** node to **Base Color** and **Emissive Color** optionally.

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab3/MyProject6%20-%20Unreal%20Editor%207_8_2020%207_07_35%20am.png?raw=true)

This is an example demonstrating how to mask color using **Component Mask**. After masking the Red channel, it would retain only Green and Blue. It is monotone without any color. Finally we convert the value to 1 or 0 with **Round** and **Ceil**. So that it only remain white and black.

## Basic Toon / Cel shader

![](https://i.kinja-img.com/gawker-media/image/upload/t_original/fphocokn4ieej96zh9ai.jpg)

The most common method to implement toon / cel shader is to use the dot product of Light Vector and the Normal Vector of surface.

![](https://koenig-media.raywenderlich.com/uploads/2018/02/unreal-engine-cel-shading-06.jpg)

We could create the color bands by thresholding the dot product.

![](https://koenig-media.raywenderlich.com/uploads/2018/02/unreal-engine-cel-shading-07.jpg)

Let's **create a new material with naruto texture** and take a look to the following shader graph.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab3/naruto-texture_Mat_tone%207_8_2020%2010_00_57%20am.png?raw=true")

Here are steps for creating above shader graph.

1. Right on empty area, search for VectorParam and name it as light vector.
2. Drag from **RGB** pin of the **light vector** node to somewhere, search for **Dot product** and select it.
3. Drag from **B** pin of **Dot product** node to somewhere, search for **VertexNormalWS** and select it.
4. Drag from **right** pin of **Dot product** node to somewhere, search for **Clamp** and select it
5. Drag from **right** pin of **Clamp** node to some where, search for **Multiply** and select it
6. Select **Multiply** node, change the **B value** to **2** in **Details panel** on the left.
7. Drag from **right** pin of **Multiply** node to some where,, search for **Round** and select it.
8.  Drag from **right** pin of **Round** to some where, search for **Ceil** and select it.
9. Drag from **RGB** pin of **texture sample** node to some where, search for **Lerp** and select it.
10. Drag from **RGB** pin of **texture sample** node to some where again, search for **Multiply** and select it.
11. Drag from the **B** pin of newly created **Multiply** node to somewhere, search for **Vector parameter** and **name** it as **grey mask**.
12. **Double-click** on **grey mask**, **select a grey color** and **click** on **OK**.
13. Drag from the **right** pin of **Multiply**, connect it to **B** pin of **Lerp** node.
14. Drag from the **Alpha** pin of **Lerp**, connect it to **right** pin of **Ceil**.
15. Connect **right** pin of **Lerp** to **Base Color**, and **Emissive Color** optionally.

![](https://raw.githubusercontent.com/hkbu-kennycheng/uelabs/master/lab3/MyProject6%20-%20Unreal%20Editor%207_8_2020%209_33_16%20am.png)

In order to view the result, please **apply this material to Naruto model** in your **Level**.

We created a **2 bands toon shader** using **color mask**. By using **Lerp operation**, we could select the corresponding color band according to dot product value of Light Vector and Normal Vector of the surface. In case you don't know **Lerp**, you may take a look to [Wikipedia](https://en.wikipedia.org/wiki/Linear_interpolation).

## Exercise 1

Please try to combine Color Masking and Toon shader to create a better 月讀 effect.

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab3/MyProject6%20-%20Unreal%20Editor%207_8_2020%2010_13_49%20am.png?raw=true)

