---
title: aaaUnity een zelfstudie bDe volledige draaien
description: Stappen toocreate Hallo een bDe volledige spel dit is een vereiste voor alle zelfstudies over Mobile Engagement Unity klassieke Unity draaien
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0afd0eca-f74a-43aa-bba8-436a0265c312
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 10d923682432961207594886b08e5db60cf60d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="f5982-103"><a id="unity-roll-a-ball"></a>Maak Unity draaien een spel bDe volledige</span><span class="sxs-lookup"><span data-stu-id="f5982-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="f5982-104">Deze zelfstudie wordt begeleid Hallo belangrijke stappen voor een enigszins gewijzigd [Unity draaien een zelfstudie bDe volledige](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span><span class="sxs-lookup"><span data-stu-id="f5982-104">This tutorial walks through hello main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="f5982-105">In dit voorbeeld van een game bestaat uit een bolvormige player-object dat wordt beheerd door Hallo app gebruiker en Hallo doel van Hallo spel is too'collect' Verzamel objecten op basis van tegenaan Hallo object player met deze Verzamel objecten.</span><span class="sxs-lookup"><span data-stu-id="f5982-105">This sample game consists of a spherical 'player' object which is controlled by hello app user and hello objective of hello game is too'collect' collectible objects by colliding hello player object with these collectible objects.</span></span> <span data-ttu-id="f5982-106">Hierbij wordt verondersteld enigszins bekend bent met Unity editor-omgeving.</span><span class="sxs-lookup"><span data-stu-id="f5982-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="f5982-107">Als u problemen ondervindt uitvoert moet u de volledige zelfstudie toohello verwijzen.</span><span class="sxs-lookup"><span data-stu-id="f5982-107">If you run into any issues then you should refer toohello full tutorial.</span></span> 

### <a name="setting-up-hello-game"></a><span data-ttu-id="f5982-108">Hallo game instellen</span><span class="sxs-lookup"><span data-stu-id="f5982-108">Setting up hello game</span></span>
<span data-ttu-id="f5982-109">Hallo onderstaande stappen zijn van Hallo [Unity-zelfstudie](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="f5982-109">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="f5982-110">Open **Unity-Editor** en klik op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="f5982-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="f5982-111">Geef een **projectnaam** & **locatie**, selecteer **3D** en klik op **project maken**.</span><span class="sxs-lookup"><span data-stu-id="f5982-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="f5982-112">Hallo standaard scene zojuist hebt gemaakt als onderdeel van het Hallo-nieuw project met de naam van de Hallo opslaan **MiniGame** binnen een nieuwe  **\_schermen** map onder **activa** map:</span><span class="sxs-lookup"><span data-stu-id="f5982-112">Save hello default scene just created as part of hello new project as with hello name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="f5982-113">Maak een **3D-Object -> vlak** als Hallo spelen veld en de naam van dit object vlak als **compleet**</span><span class="sxs-lookup"><span data-stu-id="f5982-113">Create a **3D Object -> Plane** as hello playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="f5982-114">Opnieuw instellen van Hallo transformatie-onderdeel voor dit **compleet** object zodat deze op Hallo oorsprong.</span><span class="sxs-lookup"><span data-stu-id="f5982-114">Reset hello transform component for this **Ground** object so that it is at hello Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="f5982-115">Schakel het selectievakje **raster weergeven** van **Gizmos menu** voor Hallo **compleet** object.</span><span class="sxs-lookup"><span data-stu-id="f5982-115">Uncheck **Show Grid** from **Gizmos menu** for hello **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="f5982-116">Update Hallo **Scale** component voor Hallo **compleet** toobe object [X = 2, Y = 1, Z = 2].</span><span class="sxs-lookup"><span data-stu-id="f5982-116">Update hello **Scale** component for hello **Ground** object toobe [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="f5982-117">Voeg een nieuwe **3D-Object -> bol** toohello projecten en wijzig de naam van deze bol object in de vorm **Player**.</span><span class="sxs-lookup"><span data-stu-id="f5982-117">Add a new **3D Object -> Sphere** toohello project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="f5982-118">Selecteer Hallo **Player** object en klikt u op **transformatie opnieuw instellen** vergelijkbaar toohello vlak-object.</span><span class="sxs-lookup"><span data-stu-id="f5982-118">Select hello **Player** object and click **Reset Transform** similar toohello Plane object.</span></span> 
10. <span data-ttu-id="f5982-119">Update **transformatie-positie > -> Y-coördinaat** component voor Hallo Player Y als 0,5.</span><span class="sxs-lookup"><span data-stu-id="f5982-119">Update **Transform -> Position -> Y Coordinate** component for hello Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="f5982-120">Maak een nieuwe map **materialen** Hallo project waar we Hallo wezenlijke toocolor Hallo player zal maken.</span><span class="sxs-lookup"><span data-stu-id="f5982-120">Create a new folder called **Materials** in hello project where we will create hello material toocolor hello player.</span></span> 
12. <span data-ttu-id="f5982-121">Maak een nieuwe **materiaal** aangeroepen **achtergrond** in deze map.</span><span class="sxs-lookup"><span data-stu-id="f5982-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="f5982-122">Hallo kleur van Hallo materiaal bijwerken door het bijwerken van Hallo **Albedo** eigenschap ervan.</span><span class="sxs-lookup"><span data-stu-id="f5982-122">Update hello color of hello material by updating hello **Albedo** property of it.</span></span> <span data-ttu-id="f5982-123">U kunt Hallo RGB-waarden van [0,32,64] selecteren.</span><span class="sxs-lookup"><span data-stu-id="f5982-123">You can select hello RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="f5982-124">Sleep dit materiaal naar Hallo scene weergave tooapply kleur toohello **compleet** object.</span><span class="sxs-lookup"><span data-stu-id="f5982-124">Drag this material into hello scene view tooapply color toohello **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="f5982-125">Ten slotte bijwerken Hallo **transformatie -> rotatie -> Y** too60 op Hallo gericht licht object voor de duidelijkheid.</span><span class="sxs-lookup"><span data-stu-id="f5982-125">Finally update hello **Transform -> Rotation -> Y** too60 on hello Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-hello-player"></a><span data-ttu-id="f5982-126">Zwevend Hallo-speler</span><span class="sxs-lookup"><span data-stu-id="f5982-126">Moving hello player</span></span>
<span data-ttu-id="f5982-127">Hallo onderstaande stappen zijn van Hallo [Unity-zelfstudie](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="f5982-127">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="f5982-128">Voeg een **RigidBody** onderdeel toohello **Player** object.</span><span class="sxs-lookup"><span data-stu-id="f5982-128">Add a **RigidBody** component toohello **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="f5982-129">Maak een nieuwe map **Scripts** in Hallo Project.</span><span class="sxs-lookup"><span data-stu-id="f5982-129">Create a new folder called **Scripts** in hello Project.</span></span> 
3. <span data-ttu-id="f5982-130">Klik op **onderdeel toevoegen -> nieuw Script-C# Script >**.</span><span class="sxs-lookup"><span data-stu-id="f5982-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="f5982-131">Naam **PlayerController**, en klik op **maken en toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f5982-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="f5982-132">Dit zal maken en koppelen van een script toohello Player-object.</span><span class="sxs-lookup"><span data-stu-id="f5982-132">This will create and attach a script toohello Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="f5982-133">Dit script onder Hallo verplaatsen **Scripts** map in het Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="f5982-133">Move this script under hello **Scripts** folder in hello project.</span></span> 
5. <span data-ttu-id="f5982-134">Hallo-script voor het bewerken in uw favoriete scripteditor te openen, Hallo scriptcode bijwerken met de volgende code Hallo en opslaan.</span><span class="sxs-lookup"><span data-stu-id="f5982-134">Open hello script for editing in your favorite script editor, update hello script code with hello following code and save it.</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour 
        {
            public float speed;
            private Rigidbody rb;
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
                rb.AddForce (movement * speed);
            }
        }
6. <span data-ttu-id="f5982-135">Houd er rekening mee Hallo script hierboven maakt gebruik van een **snelheid** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="f5982-135">Note that hello script above uses a **Speed** property.</span></span> <span data-ttu-id="f5982-136">Werk Hallo snelheid eigenschap too10 in Hallo Unity-editor.</span><span class="sxs-lookup"><span data-stu-id="f5982-136">In hello Unity editor, update hello speed property too10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="f5982-137">Klik op **afspelen** in Hallo Unity-Editor.</span><span class="sxs-lookup"><span data-stu-id="f5982-137">Hit **Play** in hello Unity Editor.</span></span> <span data-ttu-id="f5982-138">Nu moet u kunnen toocontrol Hallo bDe volledige Hallo toetsenbord gebruiken en moet draaien en verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="f5982-138">Now you should be able toocontrol hello ball using hello keyboard and it should rotate and move around.</span></span> 

### <a name="moving-hello-camera"></a><span data-ttu-id="f5982-139">Zwevend Hallo camera</span><span class="sxs-lookup"><span data-stu-id="f5982-139">Moving hello camera</span></span>
<span data-ttu-id="f5982-140">Hallo onderstaande stappen zijn van Hallo [Unity-zelfstudie](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) en hello wordt binden **Main Camera** toohello **Player** object.</span><span class="sxs-lookup"><span data-stu-id="f5982-140">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie hello **Main Camera** toohello **Player** object.</span></span> 

1. <span data-ttu-id="f5982-141">Update Hallo **Transform.Position** toobe X = 0, Y = 10.5, Z =-10.</span><span class="sxs-lookup"><span data-stu-id="f5982-141">Update hello **Transform.Position** toobe X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="f5982-142">Update Hallo **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span><span class="sxs-lookup"><span data-stu-id="f5982-142">Update hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="f5982-143">Toevoegen van een script met de nieuwe naam **CameraController** toohello **MainCamera** en verplaats deze onder de map Hallo-Scripts.</span><span class="sxs-lookup"><span data-stu-id="f5982-143">Add a new script called **CameraController** toohello **MainCamera** and move it under hello Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="f5982-144">Open Hallo-script voor het bewerken en Hallo code in het volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="f5982-144">Open up hello script for editing and add hello following code in it:</span></span>
   
        using UnityEngine;
        using System.Collections;
   
        public class CameraController : MonoBehaviour {
   
            public GameObject player;
   
            private Vector3 offset;
   
            void Start ()
            {
                offset = transform.position - player.transform.position;
            }
   
            void LateUpdate ()
            {
                transform.position = player.transform.position + offset;
            }
        }
5. <span data-ttu-id="f5982-145">Sleep Hallo Player variabele in de omgeving Unity - in Hallo Player sleuf voor Hallo Main Camera-object zodat hello twee gekoppeld met elkaar zijn.</span><span class="sxs-lookup"><span data-stu-id="f5982-145">In Unity environment - drag hello Player variable into hello Player slot for hello Main Camera object so that hello two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="f5982-146">Nu als u in Hallo Unity-editor en draaien Hallo Player bDe volledige object op afspelen te drukken ziet vervolgens u Hallo Camera volgen in het Hallo-verkeer.</span><span class="sxs-lookup"><span data-stu-id="f5982-146">Now if you hit Play in hello Unity editor and rotate hello Player Ball object then you will see hello Camera following it in hello movement.</span></span>  

### <a name="setting-up-hello-play-area"></a><span data-ttu-id="f5982-147">Het instellen van Hallo Play gebied</span><span class="sxs-lookup"><span data-stu-id="f5982-147">Setting up hello Play area</span></span>
<span data-ttu-id="f5982-148">Hallo onderstaande stappen zijn van Hallo [Unity-zelfstudie](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="f5982-148">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="f5982-149">Hallo wanden Hallo compleet omringende zodat hello niet Player bDe volledige object uit Hallo play gebied in de verplaatsing verwijderen kunt maken.</span><span class="sxs-lookup"><span data-stu-id="f5982-149">We will create hello Walls surrounding hello Ground so that hello Player Ball object doesn't drop off hello play area in its movement.</span></span> 

1. <span data-ttu-id="f5982-150">Klik op **Create-maken leeg >-Game Object >** en noem deze **wanden**</span><span class="sxs-lookup"><span data-stu-id="f5982-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="f5982-151">Maak een nieuwe onder dit object wanden - **3D-Object-kubus >** en noem deze 'West wanden'.</span><span class="sxs-lookup"><span data-stu-id="f5982-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="f5982-152">Update Hallo **transformatie -> positie** en **transformatie -> Scale** voor dit object West wanden.</span><span class="sxs-lookup"><span data-stu-id="f5982-152">Update hello **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="f5982-153">Dubbele Hallo West wanden toocreate een **Oost wanden** Hello bijgewerkt transformeren plaatsen en schalen.</span><span class="sxs-lookup"><span data-stu-id="f5982-153">Duplicate hello West wall toocreate an **East wall** with hello updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="f5982-154">Dubbele Hallo Oost wanden toocreate een **Noord wanden** transformeren positie & schaal Hello bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f5982-154">Duplicate hello East wall toocreate a **North wall** with hello updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="f5982-155">Dubbele Hallo Noord wanden en maak een **Zuid wanden** transformeren positie & schaal Hello bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f5982-155">Duplicate hello North wall and create a **South wall** with hello updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="f5982-156">Verzamel objecten maken</span><span class="sxs-lookup"><span data-stu-id="f5982-156">Creating Collectible objects</span></span>
<span data-ttu-id="f5982-157">Hallo onderstaande stappen zijn van Hallo [Unity-zelfstudie](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="f5982-157">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="f5982-158">Maken we enkele aantrekkelijke opzoeken-objecten die vormt Hallo set Verzamel objecten welk Hallo Player bDe volledige object too'collect moet ' door leesbewerkingen en ze.</span><span class="sxs-lookup"><span data-stu-id="f5982-158">We will create some attractive looking objects which will form hello set of collectible objects which hello Player Ball object needs too'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="f5982-159">Maak een nieuwe **3D-kubus object** en noem deze ophalen.</span><span class="sxs-lookup"><span data-stu-id="f5982-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="f5982-160">Hallo aanpassen **transformatie -> rotatie** & **transformatie -> Scale** van Hallo ophalen-object.</span><span class="sxs-lookup"><span data-stu-id="f5982-160">Adjust hello **Transform -> Rotation** & **Transform -> Scale** of hello Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="f5982-161">Maak en voeg een **nieuwe C# Script** aangeroepen **Rotator** toohello ophalen-object.</span><span class="sxs-lookup"><span data-stu-id="f5982-161">Create and attach a **new C# Script** called **Rotator** toohello Pickup object.</span></span> <span data-ttu-id="f5982-162">Zorg ervoor dat tooput Hallo script onder Hallo scriptmap.</span><span class="sxs-lookup"><span data-stu-id="f5982-162">Make sure tooput hello script under hello Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="f5982-163">Open dit script voor het bewerken en bijwerken toobe hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="f5982-163">Open this script for editing and update it toobe hello following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="f5982-164">Treffers Hallo Play-modus in Hallo Unity-Editor en het weergeven van uw ophalen-object worden nu draaien op de as.</span><span class="sxs-lookup"><span data-stu-id="f5982-164">Now hit hello Play mode in hello Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="f5982-165">Maak een nieuwe map **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="f5982-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="f5982-166">Sleep Hallo **ophalen** object en plaats deze in Hallo Prefabs map.</span><span class="sxs-lookup"><span data-stu-id="f5982-166">Drag hello **Pickup** object and put it in hello Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="f5982-167">Maak een nieuwe **leeg Game object** aangeroepen **overdracht op**.</span><span class="sxs-lookup"><span data-stu-id="f5982-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="f5982-168">Opnieuw instellen van de positie tooorigin en sleep Hallo ophalen object onder dit spel object.</span><span class="sxs-lookup"><span data-stu-id="f5982-168">Reset its position tooorigin and then drag hello Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="f5982-169">Dubbele Hallo **ophalen** object en deze verspreiden op Hallo **compleet** object rond Hallo **Player** object door bij te werken Hallo **van Transform.Position X & Z**  waarden op de juiste wijze.</span><span class="sxs-lookup"><span data-stu-id="f5982-169">Duplicate hello **Pickup** object and spread it on hello **Ground** object around hello **Player** object by updating hello **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="f5982-170">Maakt een **nieuw materiaal** aangeroepen **ophalen** en toobe rood in kleur door bij te werken Hallo bijwerken **Albedo eigenschap** vergelijkbare toowhat we voor het bijwerken van Hallo compleet object.</span><span class="sxs-lookup"><span data-stu-id="f5982-170">Create a **new material** called **Pickup** and update it toobe Red in color by updating hello **Albedo property** similar toowhat we did for updating hello Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="f5982-171">Toepassing hello wezenlijke tooall Hallo 4 ophalen objecten.</span><span class="sxs-lookup"><span data-stu-id="f5982-171">Apply hello material tooall hello 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a><span data-ttu-id="f5982-172">Hallo ophalen objecten verzamelen</span><span class="sxs-lookup"><span data-stu-id="f5982-172">Collecting hello Pickup objects</span></span>
<span data-ttu-id="f5982-173">Hallo onderstaande stappen zijn van Hallo [Unity-zelfstudie](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="f5982-173">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="f5982-174">Hallo Player wordt bijgewerkt zodat deze kunnen too'collect' Hallo ophalen objecten door leesbewerkingen en ze.</span><span class="sxs-lookup"><span data-stu-id="f5982-174">We will update hello Player so that it is able too'collect' hello pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="f5982-175">Open Hallo **PlayerController** gekoppelde toohello object Player om het bewerken van een script bij te werken toohello te volgen:</span><span class="sxs-lookup"><span data-stu-id="f5982-175">Open up hello **PlayerController** script attached toohello Player object for editing and update it toohello following:</span></span>  
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour {
   
            public float speed;
   
            private Rigidbody rb;
   
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
   
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
   
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
   
                rb.AddForce (movement * speed);
            }
   
            void OnTriggerEnter(Collider other) 
            {
                if (other.gameObject.CompareTag ("Pick Up"))
                {
                    other.gameObject.SetActive (false);
                }
            }
        }
2. <span data-ttu-id="f5982-176">Maak een nieuwe **Tag** aangeroepen **Kies Up** (moet overeenkomen met wat is er in Hallo script)</span><span class="sxs-lookup"><span data-stu-id="f5982-176">Create a new **Tag** called **Pick Up** (it must match what is in hello script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="f5982-177">Deze toepassen **Tag** toohello Prefab ophalen-object.</span><span class="sxs-lookup"><span data-stu-id="f5982-177">Apply this **Tag** toohello Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="f5982-178">Schakel **IsTrigger** selectievakje voor Hallo Prefab-object.</span><span class="sxs-lookup"><span data-stu-id="f5982-178">Enable **IsTrigger** checkbox for hello Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="f5982-179">Een object Rigid hoofdtekst tooPickup Prefab toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f5982-179">Add a Rigid body tooPickup Prefab object.</span></span> <span data-ttu-id="f5982-180">Voor de optimalisatie van de prestaties wordt Hallo statische collider dat we tooa dynamische collider gebruikt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f5982-180">For performance optimization we will update hello static collider that we used tooa Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="f5982-181">Controleer ten slotte Hallo **IsKinematic** eigenschap voor prefab Hallo-object.</span><span class="sxs-lookup"><span data-stu-id="f5982-181">Finally check hello **IsKinematic** property for hello prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="f5982-182">Bereikt **afspelen** in Hallo Unity-editor en u niet kunt tooplay dit **draaien geen** game door verplaatsen Hallo Player-object op met de toetsen voor invoer van de richting.</span><span class="sxs-lookup"><span data-stu-id="f5982-182">Hit **Play** in hello Unity editor and you will be able tooplay this **Roll a Ball** game by moving hello Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-hello-game-for-mobile-play"></a><span data-ttu-id="f5982-183">Hallo game voor mobiele play bijwerken</span><span class="sxs-lookup"><span data-stu-id="f5982-183">Updating hello game for mobile play</span></span>
<span data-ttu-id="f5982-184">Hallo secties hierboven gesloten Hallo basic zelfstudie uit Unity.</span><span class="sxs-lookup"><span data-stu-id="f5982-184">hello sections above concluded hello basic tutorial from Unity.</span></span> <span data-ttu-id="f5982-185">Nu we zullen wijzigen Hallo game toomake deze beschrijvende van mobiele apparaten.</span><span class="sxs-lookup"><span data-stu-id="f5982-185">Now we will modify hello game toomake it mobile device friendly.</span></span> <span data-ttu-id="f5982-186">Houd er rekening mee dat we toetsenbordinvoer voor Hallo game tot nu toe voor het testen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f5982-186">Note that we used keyboard input for hello game so far for testing.</span></span> <span data-ttu-id="f5982-187">Nu we zullen dit zodanig aanpassen dat we kunt beheren telefoon Hallo player via Hallo beweging van Hallo dat wil zeggen met versnellingsmeter als Hallo-invoer.</span><span class="sxs-lookup"><span data-stu-id="f5982-187">Now we will modify it so that we can control hello player by using hello motion of hello phone i.e. using Accelerometer as hello input.</span></span> 

<span data-ttu-id="f5982-188">Open Hallo **PlayerController** script voor bewerken en update Hallo **FixedUpdate** methode toouse Hallo beweging van Hallo versnellingsmeter toomove Hallo Player-object.</span><span class="sxs-lookup"><span data-stu-id="f5982-188">Open up hello **PlayerController** script for editing and update hello **FixedUpdate** method toouse hello motion from hello accelerometer toomove hello Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="f5982-189">Deze zelfstudie concludeert de domeincontroller een basic game maken met Unity en kunt u dit implementeren op een apparaat van uw keuze tooplay Hallo spel.</span><span class="sxs-lookup"><span data-stu-id="f5982-189">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice tooplay hello game.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-unity-roll-a-ball/1.png    
[2]: ./media/mobile-engagement-unity-roll-a-ball/2.png
[3]: ./media/mobile-engagement-unity-roll-a-ball/3.png
[4]: ./media/mobile-engagement-unity-roll-a-ball/4.png
[5]: ./media/mobile-engagement-unity-roll-a-ball/5.png
[6]: ./media/mobile-engagement-unity-roll-a-ball/6.png
[7]: ./media/mobile-engagement-unity-roll-a-ball/7.png
[8]: ./media/mobile-engagement-unity-roll-a-ball/8.png
[9]: ./media/mobile-engagement-unity-roll-a-ball/9.png    
[10]: ./media/mobile-engagement-unity-roll-a-ball/10.png    
[11]: ./media/mobile-engagement-unity-roll-a-ball/11.png    
[12]: ./media/mobile-engagement-unity-roll-a-ball/12.png
[13]: ./media/mobile-engagement-unity-roll-a-ball/13.png
[14]: ./media/mobile-engagement-unity-roll-a-ball/14.png
[15]: ./media/mobile-engagement-unity-roll-a-ball/15.png
[16]: ./media/mobile-engagement-unity-roll-a-ball/16.png
[17]: ./media/mobile-engagement-unity-roll-a-ball/17.png
[18]: ./media/mobile-engagement-unity-roll-a-ball/18.png
[19]: ./media/mobile-engagement-unity-roll-a-ball/19.png    
[20]: ./media/mobile-engagement-unity-roll-a-ball/20.png    
[21]: ./media/mobile-engagement-unity-roll-a-ball/21.png    
[22]: ./media/mobile-engagement-unity-roll-a-ball/22.png    
[23]: ./media/mobile-engagement-unity-roll-a-ball/23.png    
[24]: ./media/mobile-engagement-unity-roll-a-ball/24.png    
[25]: ./media/mobile-engagement-unity-roll-a-ball/25.png    
[26]: ./media/mobile-engagement-unity-roll-a-ball/26.png    
[27]: ./media/mobile-engagement-unity-roll-a-ball/27.png    
[28]: ./media/mobile-engagement-unity-roll-a-ball/28.png    
[29]: ./media/mobile-engagement-unity-roll-a-ball/29.png    
[30]: ./media/mobile-engagement-unity-roll-a-ball/30.png    
[31]: ./media/mobile-engagement-unity-roll-a-ball/31.png    
[32]: ./media/mobile-engagement-unity-roll-a-ball/32.png    
[33]: ./media/mobile-engagement-unity-roll-a-ball/33.png    
[34]: ./media/mobile-engagement-unity-roll-a-ball/34.png    
[35]: ./media/mobile-engagement-unity-roll-a-ball/35.png    
[36]: ./media/mobile-engagement-unity-roll-a-ball/36.png    
[37]: ./media/mobile-engagement-unity-roll-a-ball/37.png    
[38]: ./media/mobile-engagement-unity-roll-a-ball/38.png    
[51]: ./media/mobile-engagement-unity-roll-a-ball/new-project.png
[52]: ./media/mobile-engagement-unity-roll-a-ball/new-project-properties.png
[53]: ./media/mobile-engagement-unity-roll-a-ball/save-scene.png













