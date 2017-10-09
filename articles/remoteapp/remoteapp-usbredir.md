---
title: aaaHow leid USB-apparaten in Azure RemoteApp? | Microsoft Docs
description: Meer informatie over hoe toouse omleiding voor USB-apparaten in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 191d98af-2f5a-4307-9042-aae0e4049f9f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 661b90c0910167d76ac3886b5af7a32d00b3943f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-redirect-usb-devices-in-azure-remoteapp"></a>Hoe u in het omleiden van USB-apparaten in Azure RemoteApp?
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Omleiding van apparaten kan gebruikers Hallo USB-apparaten gekoppelde tootheir computer of tablet met Hallo-apps in Azure RemoteApp gebruiken. Bijvoorbeeld, als u Skype via Azure RemoteApp gedeelde, uw gebruikers moeten kunnen toouse toobe hun apparaat camera's.

Voordat u verder gaat, controleert u of u informatie Hallo USB-omleiding in [met Mapomleiding in Azure RemoteApp](remoteapp-redirection.md). Maar Hallo nusbdevicestoredirect:s aangeraden: * werkt niet voor USB-webcamera's en werken mogelijk niet voor bepaalde USB-printers of multifunctionele USB-apparaten. Aan het ontwerp en om veiligheidsredenen hello Azure RemoteApp-beheerder heeft tooenable omleiding door apparaatklasse-GUID of door de exemplaar-ID apparaat voordat uw gebruikers kunnen die apparaten gebruiken.

Hoewel dit artikel wordt gesproken over web camera omleiding, kunt u een soortgelijke benadering tooredirect USB-printers en andere multifunctionele USB-apparaten die niet worden omgeleid door Hallo **nusbdevicestoredirect:s:*** opdracht.

## <a name="redirection-options-for-usb-devices"></a>Opties voor Mapomleiding voor USB-apparaten
Azure RemoteApp gebruikt vergelijkbaar mechanismen voor het omleiden van USB-apparaten, zoals hello zijn beschikbaar voor extern bureaublad-Services. Hallo onderliggende technologie kunt u kiezen Hallo omleiding van de juiste methode voor een bepaald apparaat tooget Hallo beste van beide op hoog niveau en omleiding RemoteFX USB-apparaten met behulp van Hallo **usbdevicestoredirect:s:** opdracht. Er zijn vier elementen toothis-opdracht:

| Verwerkingsvolgorde | Parameter | Beschrijving |
| --- | --- | --- |
| 1 |* |Alle apparaten die niet worden opgehaald door op hoog niveau omleiding selecteert. Opmerking: standaard * werkt niet voor USB-webcamera's. |
| {Apparaatklasse GUID} |Hiermee selecteert u alle apparaten die voldoen aan opgegeven Hallo apparaat setup-klasse. | |
| USB\InstanceID |Hiermee selecteert u een USB-apparaat dat is opgegeven voor Hallo opgegeven serverexemplaar-ID. | |
| 2 |-USB\Instance ID |Hiermee verwijdert u Hallo-instellingen voor Mapomleiding voor Hallo opgegeven apparaat. |

## <a name="redirecting-a-usb-device-by-using-hello-device-class-guid"></a>Omleiden van een USB-apparaat met behulp van Hallo apparaatklasse GUID
Er zijn twee manieren toofind Hallo apparaatklasse GUID die kan worden gebruikt voor de omleiding van. 

de eerste optie Hallo is toouse hello [System-Defined apparaat Setup klassen beschikbaar tooVendors](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx). Kies Hallo-klasse die het meest overeenkomt met Hallo apparaat gekoppelde toohello lokale computer. Dit kan een apparaat Imaging klasse of vastleggen videoapparaat zijn voor digitale camera's. U moet toodo sommige experimenteren met Hallo apparaat klassen toofind Hallo juiste klasse-GUID die geschikt is voor Hallo lokaal aangesloten USB-apparaat (in ons geval Hallo-webcamera).

Een betere manier of Hallo tweede optie, wordt uw toofollow klasse-GUID voor deze stappen toofind Hallo specifiek apparaat:

1. Hallo Apparaatbeheer te openen, zoek Hallo-apparaat dat wordt omgeleid en met de rechtermuisknop en open vervolgens Hallo-eigenschappen.
   ![Hallo Apparaatbeheer openen](./media/remoteapp-usbredir/ra-devicemanager.png)
2. Op Hallo **Details** Kies Hallo eigenschap **klasse Guid**. Hallo-waarde die wordt weergegeven is Hallo klasse-GUID voor dat type apparaat.
   ![Camera-eigenschappen](./media/remoteapp-usbredir/ra-classguid.png)
3. Hallo klasse-Guid-waarde tooredirect apparaten die voldoen aan deze gebruiken.

Bijvoorbeeld:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s:<Class Guid value>"

U kunt meerdere apparaat omleidingen in Hallo combineren dezelfde cmdlet. Bijvoorbeeld: tooredirect lokale opslag, maar een USB-web-camera, cmdlet ziet er als volgt:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:<Class Guid value>"

Wanneer u apparaatomleiding door de klasse-GUID instellen worden alle apparaten die overeenkomen met die klasse GUID in Hallo verzameling opgegeven omgeleid. Bijvoorbeeld, als er meerdere computers in het lokale netwerk Hallo met Hallo dezelfde USB-webcamera's, kunt u uitvoeren een tooredirect één cmdlet alle Hallo webcamera.

## <a name="redirecting-a-usb-device-by-using-hello-device-instance-id"></a>Omleiden van een USB-apparaat met behulp van Hallo apparaat exemplaar-ID
Als u wilt dat nauwkeuriger beheer en toocontrol omleiding per apparaat wilt, kunt u Hallo **USB\InstanceID** omleiding-parameter.

Hallo lastigste onderdeel van deze methode vinden Hallo USB-apparaat exemplaar-ID. U moet openen toohello computer en Hallo specifiek USB-apparaat. Volg deze stappen:

1. Hallo apparaatomleiding in de sessie van extern bureaublad inschakelen, zoals beschreven in [hoe kan ik mijn apparaten en bronnen gebruiken in een extern bureaublad-sessie?](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)
2. Open een verbinding met extern bureaublad en klik op **opties weergeven**.
3. Klik op **opslaan als** toosave Hallo huidige verbinding instellingen tooan RDP-bestand.  
    ![Hallo-instellingen opslaan als een RDP-bestand](./media/remoteapp-usbredir/ra-saveasrdp.png)
4. Kies een bestandsnaam en locatie, bijvoorbeeld MyConnection.rdp en deze PC\Documents en sla Hallo-bestand.
5. Open hello MyConnection.rdp-bestand met een teksteditor en Hallo exemplaar-ID vinden Hallo-apparaat dat u wilt dat tooredirect.

Gebruik nu Hallo exemplaar-ID in Hallo volgende cmdlet:

    Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s: USB\<Device InstanceID value>"



### <a name="help-us-help-you"></a>Help ons u te helpen
Wist u dat in de toevoeging toorating in dit artikel en het toevoegen van opmerkingen omlaag hieronder, kunt u wijzigingen toohello artikel zelf? Ontbreekt er iets? Is er iets niet juist? Heb ik iets geschreven dat niet duidelijk is? Blader omhoog en klik op **Edit on GitHub** toomake wijzigingen - deze worden eerst nagekeken toous, en vervolgens wanneer uitgeschakeld op deze, ziet u uw wijzigingen en verbeteringen hier.

