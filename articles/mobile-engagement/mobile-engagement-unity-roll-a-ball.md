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
# <a id="unity-roll-a-ball"></a>Maak Unity draaien een spel bDe volledige
Deze zelfstudie wordt begeleid Hallo belangrijke stappen voor een enigszins gewijzigd [Unity draaien een zelfstudie bDe volledige](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial). In dit voorbeeld van een game bestaat uit een bolvormige player-object dat wordt beheerd door Hallo app gebruiker en Hallo doel van Hallo spel is too'collect' Verzamel objecten op basis van tegenaan Hallo object player met deze Verzamel objecten. Hierbij wordt verondersteld enigszins bekend bent met Unity editor-omgeving. Als u problemen ondervindt uitvoert moet u de volledige zelfstudie toohello verwijzen. 

### <a name="setting-up-hello-game"></a>Hallo game instellen
Hallo onderstaande stappen zijn van Hallo [Unity-zelfstudie](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)

1. Open **Unity-Editor** en klik op **nieuw**. 
   
    ![][51] 
2. Geef een **projectnaam** & **locatie**, selecteer **3D** en klik op **project maken**.
   
    ![][52]
3. Hallo standaard scene zojuist hebt gemaakt als onderdeel van het Hallo-nieuw project met de naam van de Hallo opslaan **MiniGame** binnen een nieuwe  **\_schermen** map onder **activa** map:
   
    ![][53]
4. Maak een **3D-Object -> vlak** als Hallo spelen veld en de naam van dit object vlak als **compleet**
   
    ![][1]
5. Opnieuw instellen van Hallo transformatie-onderdeel voor dit **compleet** object zodat deze op Hallo oorsprong. 
   
    ![][3]
6. Schakel het selectievakje **raster weergeven** van **Gizmos menu** voor Hallo **compleet** object.
   
    ![][4]
7. Update Hallo **Scale** component voor Hallo **compleet** toobe object [X = 2, Y = 1, Z = 2]. 
   
    ![][5]
8. Voeg een nieuwe **3D-Object -> bol** toohello projecten en wijzig de naam van deze bol object in de vorm **Player**. 
   
    ![][6]
9. Selecteer Hallo **Player** object en klikt u op **transformatie opnieuw instellen** vergelijkbaar toohello vlak-object. 
10. Update **transformatie-positie > -> Y-coördinaat** component voor Hallo Player Y als 0,5.  
    
    ![][7]
11. Maak een nieuwe map **materialen** Hallo project waar we Hallo wezenlijke toocolor Hallo player zal maken. 
12. Maak een nieuwe **materiaal** aangeroepen **achtergrond** in deze map. 
    
    ![][8]
13. Hallo kleur van Hallo materiaal bijwerken door het bijwerken van Hallo **Albedo** eigenschap ervan. U kunt Hallo RGB-waarden van [0,32,64] selecteren. 
    
    ![][9]
14. Sleep dit materiaal naar Hallo scene weergave tooapply kleur toohello **compleet** object. 
    
    ![][10]
15. Ten slotte bijwerken Hallo **transformatie -> rotatie -> Y** too60 op Hallo gericht licht object voor de duidelijkheid. 
    
    ![][12]

### <a name="moving-hello-player"></a>Zwevend Hallo-speler
Hallo onderstaande stappen zijn van Hallo [Unity-zelfstudie](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)

1. Voeg een **RigidBody** onderdeel toohello **Player** object. 
   
    ![][13]
2. Maak een nieuwe map **Scripts** in Hallo Project. 
3. Klik op **onderdeel toevoegen -> nieuw Script-C# Script >**. Naam **PlayerController**, en klik op **maken en toevoegen**. Dit zal maken en koppelen van een script toohello Player-object.  
   
    ![][14]
4. Dit script onder Hallo verplaatsen **Scripts** map in het Hallo-project. 
5. Hallo-script voor het bewerken in uw favoriete scripteditor te openen, Hallo scriptcode bijwerken met de volgende code Hallo en opslaan. 
   
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
6. Houd er rekening mee Hallo script hierboven maakt gebruik van een **snelheid** eigenschap. Werk Hallo snelheid eigenschap too10 in Hallo Unity-editor.  
   
    ![][15]
7. Klik op **afspelen** in Hallo Unity-Editor. Nu moet u kunnen toocontrol Hallo bDe volledige Hallo toetsenbord gebruiken en moet draaien en verplaatsen. 

### <a name="moving-hello-camera"></a>Zwevend Hallo camera
Hallo onderstaande stappen zijn van Hallo [Unity-zelfstudie](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) en hello wordt binden **Main Camera** toohello **Player** object. 

1. Update Hallo **Transform.Position** toobe X = 0, Y = 10.5, Z =-10.  
2. Update Hallo **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.  
   
    ![][16]
3. Toevoegen van een script met de nieuwe naam **CameraController** toohello **MainCamera** en verplaats deze onder de map Hallo-Scripts. 
   
    ![][17]
4. Open Hallo-script voor het bewerken en Hallo code in het volgende toevoegen:
   
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
5. Sleep Hallo Player variabele in de omgeving Unity - in Hallo Player sleuf voor Hallo Main Camera-object zodat hello twee gekoppeld met elkaar zijn. 
   
    ![][18]
6. Nu als u in Hallo Unity-editor en draaien Hallo Player bDe volledige object op afspelen te drukken ziet vervolgens u Hallo Camera volgen in het Hallo-verkeer.  

### <a name="setting-up-hello-play-area"></a>Het instellen van Hallo Play gebied
Hallo onderstaande stappen zijn van Hallo [Unity-zelfstudie](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141). Hallo wanden Hallo compleet omringende zodat hello niet Player bDe volledige object uit Hallo play gebied in de verplaatsing verwijderen kunt maken. 

1. Klik op **Create-maken leeg >-Game Object >** en noem deze **wanden**
   
    ![][19]
2. Maak een nieuwe onder dit object wanden - **3D-Object-kubus >** en noem deze 'West wanden'. 
   
    ![][20]
3. Update Hallo **transformatie -> positie** en **transformatie -> Scale** voor dit object West wanden. 
   
    ![][21]
4. Dubbele Hallo West wanden toocreate een **Oost wanden** Hello bijgewerkt transformeren plaatsen en schalen. 
   
    ![][22]
5. Dubbele Hallo Oost wanden toocreate een **Noord wanden** transformeren positie & schaal Hello bijgewerkt. 
   
    ![][23]
6. Dubbele Hallo Noord wanden en maak een **Zuid wanden** transformeren positie & schaal Hello bijgewerkt. 
   
    ![][24]

### <a name="creating-collectible-objects"></a>Verzamel objecten maken
Hallo onderstaande stappen zijn van Hallo [Unity-zelfstudie](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141). Maken we enkele aantrekkelijke opzoeken-objecten die vormt Hallo set Verzamel objecten welk Hallo Player bDe volledige object too'collect moet ' door leesbewerkingen en ze. 

1. Maak een nieuwe **3D-kubus object** en noem deze ophalen. 
2. Hallo aanpassen **transformatie -> rotatie** & **transformatie -> Scale** van Hallo ophalen-object. 
   
    ![][25]
3. Maak en voeg een **nieuwe C# Script** aangeroepen **Rotator** toohello ophalen-object. Zorg ervoor dat tooput Hallo script onder Hallo scriptmap. 
   
    ![][26]
4. Open dit script voor het bewerken en bijwerken toobe hello te volgen: 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. Treffers Hallo Play-modus in Hallo Unity-Editor en het weergeven van uw ophalen-object worden nu draaien op de as.
6. Maak een nieuwe map **Prefabs** 
   
    ![][27]
7. Sleep Hallo **ophalen** object en plaats deze in Hallo Prefabs map.
   
    ![][28]
8. Maak een nieuwe **leeg Game object** aangeroepen **overdracht op**. Opnieuw instellen van de positie tooorigin en sleep Hallo ophalen object onder dit spel object.  
   
    ![][29]
9. Dubbele Hallo **ophalen** object en deze verspreiden op Hallo **compleet** object rond Hallo **Player** object door bij te werken Hallo **van Transform.Position X & Z**  waarden op de juiste wijze. 
   
    ![][30]
10. Maakt een **nieuw materiaal** aangeroepen **ophalen** en toobe rood in kleur door bij te werken Hallo bijwerken **Albedo eigenschap** vergelijkbare toowhat we voor het bijwerken van Hallo compleet object. 
    
    ![][31]
11. Toepassing hello wezenlijke tooall Hallo 4 ophalen objecten.
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a>Hallo ophalen objecten verzamelen
Hallo onderstaande stappen zijn van Hallo [Unity-zelfstudie](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141). Hallo Player wordt bijgewerkt zodat deze kunnen too'collect' Hallo ophalen objecten door leesbewerkingen en ze. 

1. Open Hallo **PlayerController** gekoppelde toohello object Player om het bewerken van een script bij te werken toohello te volgen:  
   
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
2. Maak een nieuwe **Tag** aangeroepen **Kies Up** (moet overeenkomen met wat is er in Hallo script)  
   
    ![][33]
   
    ![][34]
3. Deze toepassen **Tag** toohello Prefab ophalen-object. 
   
    ![][35]
4. Schakel **IsTrigger** selectievakje voor Hallo Prefab-object.
   
    ![][36]
5. Een object Rigid hoofdtekst tooPickup Prefab toevoegen. Voor de optimalisatie van de prestaties wordt Hallo statische collider dat we tooa dynamische collider gebruikt bijgewerkt. 
   
    ![][37]
6. Controleer ten slotte Hallo **IsKinematic** eigenschap voor prefab Hallo-object. 
   
    ![][38]
7. Bereikt **afspelen** in Hallo Unity-editor en u niet kunt tooplay dit **draaien geen** game door verplaatsen Hallo Player-object op met de toetsen voor invoer van de richting. 

### <a name="updating-hello-game-for-mobile-play"></a>Hallo game voor mobiele play bijwerken
Hallo secties hierboven gesloten Hallo basic zelfstudie uit Unity. Nu we zullen wijzigen Hallo game toomake deze beschrijvende van mobiele apparaten. Houd er rekening mee dat we toetsenbordinvoer voor Hallo game tot nu toe voor het testen gebruikt. Nu we zullen dit zodanig aanpassen dat we kunt beheren telefoon Hallo player via Hallo beweging van Hallo dat wil zeggen met versnellingsmeter als Hallo-invoer. 

Open Hallo **PlayerController** script voor bewerken en update Hallo **FixedUpdate** methode toouse Hallo beweging van Hallo versnellingsmeter toomove Hallo Player-object. 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

Deze zelfstudie concludeert de domeincontroller een basic game maken met Unity en kunt u dit implementeren op een apparaat van uw keuze tooplay Hallo spel. 

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













