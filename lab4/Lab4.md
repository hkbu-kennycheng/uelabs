# Lab4: Character animations and input handling

In  today's lab, we would create animations for the Naruto character and implement the shadow clone effect in the original story. Please create a new project using **`Game -> Third Person`** template.

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab4/lab4.png?raw=true)

# Game architecture in Unreal Engine

## Templates

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab4/New%20Project%2010_8_2020%202_50_58%20am.png?raw=true)

- First person

- Flying

- Puzzle

- Rolling

- Third Person

- Top Down

- Twin Stick Shooter

- Side Scroller

- 2D Side Scroller

- Vehicle

- Vehicle Advanced

## Class architecture

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab4/ThirdPersonGameMode%2010_8_2020%203_02_30%20am.png?raw=true)

### Classes in Game Mode

- Game Session Class
    - Handling Login and online game interface
- Game state Class
    - Game state associated with the GameMode, like game over, pause, etc.
- Player Controller Class
    - It is used by the player and spawn when the player logged in.
- Player State Class
    - for replicate relevant player information, like player name, score, etc
- HUD Class
    - It provides game user interface (UI)
- Default pawn class
    - The pawn class used by player
- Spectator Class
    - The pawn used by player in spectating mode
- Replay Spectator Player Controller 
    - It used by Spectator for networked game replay.
- Server stat replicator class
    - Used by game server for replicating information

# Working with Character animation

## Generating skeleton and animation with Mixamo.com

Since our Naruto model is a static model only. It did not contains any skeleton and animation information. Lucky, [mixamo.com](https://www.mixamo.com/) provides a free service for converting static character model to skeleton with animation. Please **upload the Naruto model** extracted from UE03.zip to Mixamo.com.

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab4/Mixamo%20-%20Google%20Chrome%2010_8_2020%2010_00_15%20am.png?raw=true)

Please simply click **Next** on the first step after uploading file, and define the joint positions in the following second step.

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab4/Mixamo%20-%20Google%20Chrome%2010_8_2020%2010_01_10%20am.png?raw=true)

Simply click next at the final step, and you will able to select animation from the left panel. Please select for **idle** and hit the download button.

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab4/Mixamo%20-%20Google%20Chrome%2010_8_2020%2010_11_04%20am.png?raw=true)

After downloading **idle** animation, please search for **run** and select the **Naruto run** animation.

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab4/Mixamo%20-%20Google%20Chrome%2010_8_2020%2010_11_23%20am.png?raw=true)

Please check the **In Place** checkbox and hit on **Download** button.


## Importing skeleton model with animations

In import skeleton mesh with animation, there are some differences in the FBX Import Options panel.

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab4/FBX%20Import%20Options%2010_8_2020%2010_04_26%20am.png?raw=true)

Please enable the following options:
- **Skeleton Mesh**
- **Import Mesh**
- **Import Animations**

### Exercise

Please **import the texture and material** by **copy-and-paste files in content folder** from our **previous project**.


## Animation Blueprint

Please click on **Add New** button in the **Content Browser**, and select **`Animation -> Animation Blueprint**.

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab4/Create%20Animation%20Blueprint%2010_8_2020%2010_34_16%20am.png?raw=true)

Please select **AnimInstance** as **Parent Class** and the imported **Naruto skeleton** before hitting `OK`.

### Event Graph

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab4/NewAnimBlueprint%2010_8_2020%2010_47_13%20am.png?raw=true)

Here are steps for creating above graph:

1. Add new variable from the left panel and name it as **isRunning**.
2. Drag from the execution of **Event Blueprint Update Animation**, search for **Is Valid** and select it.
3. Connect **Return Value** of **Try Get Pawn Owner** to the **Input Object** of **Is Valid** node.
4. **Return Value** of **Try Get Pawn Owner** to somewhere, search for **Get Velocity** and select it.
5. Drag from **Return Value** of **Get Velocity** to somewhere, search for **VectorLength** and select it.
6. Drag from **Return Value** of **VectorLength** to somewhere, search for **>** and select **float > float**.
7. Drag from the **right pin** of **>** node, search for **isRunning** and select **Set isRunning**.
8. Connect the execution from **Is Valid** pin of **Is Valid** node to the **Set** node.


### AnimGraph

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab4/NewAnimBlueprint%2010_8_2020%2010_47_21%20am.png?raw=true)

Here are steps for creating above graph:

1. Drag **Idle** and **Run** from **Asset Browser** panel on the bottom right to **empty area near Output Pose of AnimGraph**.
2. Drag **isRunning variable** from **My Blueprint** panel on the left to **empty area near Output Pose of AnimGraph**.
3. Drag from **isRunning** node to somewhere, search for **Blend Poses By bool** and select it.
4. Connect **Human pin** on the right of **Blend Poses By bool** to **Output Pose**.
5. Connect **Play Run** node to **True Pose** of **Blend Poses By bool**.
6. Connect **Play Idle** node to **False Pose** of **Blend Poses By bool**.

### Apply Naruto model to Third Person Character

Please switch to Naruto model in **Third Person Character**. You may locate it in **World Outliner** panel by searching for **Third Person Character**. After that ,please click on **Edit Third Person Character**.

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab4/ThirdPersonCharacter%2010_8_2020%2011_10_04%20am.png?raw=true)

Let's select **Mesh (Inherit)** in **Component** panel on the top left corner. Please adjust the following settings in **Details** panel on the right.

- Animation
    - Animation Mode -> Use Animation Blueprint
    - Anim Class -> Please select our newly created Animation Blueprint
- Mesh
    - Skeleton Mesh -> select the Naruto skeleton
- Materials
    - Element 0 -> Select our material for Naruto model

# Shadow Clone Technique

![](https://staticr1.blastingcdn.com/media/photogallery/2016/3/6/660x290/b_620x273/kage-bunshin-no-jutsu-de-naruto_632927.jpg)

Today, I'm going to show you the Shadow Clone Technique. The shadow clone technique isn't a skill in computer graphics, instead it is a symbolic jutsu (忍術) in the Naruto manga series.

## Handling Inputs

### Action mappings

Let's click on  top menu bar, select **`Edit -> Project Settings...`** to open up the following dialog. Please search for **`Input`** on the left panel and click on it.

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab4/Project Settings 10_8_2020 9_39_30 am.png?raw=true)

In **Binding** section, click on **`+`** button besides **`Action Mappings`**. Please name it as **`Fire`** and select **`F`** key from the pull down menu.

### Adding event node in Event Graph

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab4/ThirdPersonCharacter%2010_8_2020%209_51_36%20am.png?raw=true)

<!-- Here are the steps for above graph.

1. Right-click on blank area, search for **Fire** and select it.
2. 

-->

