---
title: aaaUse hello toocreate met Azure portal een IoT Hub | Microsoft Docs
description: "Hoe toocreate, beheren en verwijderen van Azure IoT hubs via hello Azure-portal. Bevat informatie over Prijscategorieën, schaalbaarheid, beveiliging en configuratie-berichten."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a>Een iothub met hello Azure-portal maken

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Dit artikel wordt beschreven:

* Hoe Hallo toofind service IoT Hub in hello Azure-portal.
* Hoe toocreate en beheren van IoT hubs.

## <a name="where-toofind-hello-iot-hub-service"></a>Waar toofind Hallo service IoT Hub

U vindt Hallo service IoT Hub in de volgende locaties in de portal Hallo Hallo:

* Kies **+ nieuw**, en kies vervolgens **Internet der dingen**.
* Kies in Hallo Marketplace, **Internet der dingen**.

## <a name="create-an-iot-hub"></a>Een IoT Hub maken

U kunt een iothub met behulp van de volgende methoden Hallo maken:

* Hallo **+ nieuw** optie wordt weergegeven in de volgende schermopname Hallo Hallo-blade geopend. Hallo-stappen voor het maken van IoT-hub Hallo via deze methode en Hallo marketplace zijn identiek.
* Kies in Hallo Marketplace, **maken** tooopen Hallo blade wordt weergegeven in de volgende schermopname Hallo.

Hallo volgende secties beschrijven Hallo verschillende stappen toocreate een IoT-hub:

### <a name="choose-hello-name-of-hello-iot-hub"></a>Kies de naam Hallo van Hallo iothub

een IoT-hub toocreate, moet u een naam Hallo IoT-hub. Deze naam moet uniek zijn in alle IoT hubs.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a>Hallo prijscategorie kiezen

U kunt kiezen uit vier lagen: **vrije**, **Standard 1** en **standaard 2**, en **Standard-S3**. gratis laag Hallo kan alleen 500 apparaten toobe toohello IoT-hub verbonden en up too8, 000 berichten per dag.

**Standard-S1**: gebruik Hallo S1 edition voor IoT-oplossingen met een groot aantal apparaten dat elke kleine hoeveelheden gegevens genereren. Elke eenheid van Hallo S1 edition kunt up too400, 000 berichten per dag op alle verbonden apparaten.

**Standard S2**: gebruik Hallo S2 edition voor op waarin apparaten grote hoeveelheden gegevens genereren IoT-oplossingen. Elke eenheid van Hallo S2 edition kunt up too6 miljoen berichten per dag tussen alle verbonden apparaten.

**Standard-S3**: gebruik Hallo S3 edition voor IoT-oplossingen die grote hoeveelheden gegevens genereren. Elke eenheid van Hallo S3 edition kunt up too300 miljoen berichten per dag tussen alle verbonden apparaten.

![][4]

> [!NOTE]
> IoT Hub staat slechts één gratis hub per Azure-abonnement.

### <a name="iot-hub-units"></a>IoT hub-eenheden

Hallo aantal berichten dat is toegestaan per eenheid per dag, is afhankelijk van uw hub prijscategorie. Als u Hallo IoT hub toosupport instroom van 700.000 berichten, kiest u bijvoorbeeld twee S1 laag eenheden.

### <a name="device-toocloud-partitions-and-resource-group"></a>Apparaat toocloud partities en resourcegroep

U kunt het aantal partities voor een IoT-hub Hallo wijzigen. Hallo standaardaantal partities is 4, u kunt een ander nummer kiezen uit de vervolgkeuzelijst Hallo.

U hoeft geen tooexplicitly een lege resourcegroep maken. Wanneer u een resource maakt, kunt u beide toocreate een nieuwe kiezen of een bestaande resourcegroep gebruiken.

![][5]

### <a name="choose-subscription"></a>Abonnement kiezen

Azure IoT Hub automatisch een lijst met hello Azure-abonnementen Hallo-gebruikersaccount is gekoppeld aan. U kunt hello Azure-abonnement tooassociate Hallo iothub.

### <a name="choose-hello-location"></a>Hallo locatie kiezen

Hallo locatie optie biedt een lijst met Hallo regio's waar IoT Hub beschikbaar is.

### <a name="create-hello-iot-hub"></a>Hallo iothub maken

Wanneer alle voorgaande stappen voltooid zijn, kunt u Hallo IoT-hub kunt maken. Klik op **maken** toostart Hallo back-endproces toocreate en implementeren van Hallo iothub met Hallo-opties die u hebt gekozen.

Het kan enkele minuten toocreate Hallo IoT-hub duren als het duurt voor Hallo back-end-implementatie toorun op Hallo juiste Locationservers.

## <a name="change-hello-settings-of-hello-iot-hub"></a>Hallo-instellingen van Hallo iothub wijzigen

U kunt Hallo-instellingen van een bestaande IoT-hub wijzigen nadat deze is gemaakt van Hallo blade IoT Hub.

![][8]

**Gedeeld toegangsbeleid**: dit beleid definiëren Hallo machtigingen voor apparaten en services tooconnect tooIoT Hub. U kunt dit beleid openen door te klikken op **gedeeld toegangsbeleid** onder **algemene**. In deze blade kunt u bestaande beleidsregels wijzigen of toevoegen van een nieuw beleid.

### <a name="create-a-policy"></a>Een beleid maken

* Klik op **toevoegen** tooopen een blade. Hier kunt u nieuwe beleidsnaam Hallo en dat het gewenste tooassociate aan dit beleid, zoals wordt weergegeven in de volgende Hallo Hallo machtigingen afbeelding:

    Er zijn enkele machtigingen die gekoppeld aan deze gedeelde beleidsregels worden kunnen. Hallo **register gelezen** en **register schrijven** beleid verlenen lees- en schrijftoegang rechten toohello id-register. Optie Hallo schrijven automatisch kiest Hallo optie lezen.

    Hallo **Service verbinding** beleid verleent machtiging tooaccess service-eindpunten zoals **ontvangen van apparaat-naar-cloud**. Hallo **apparaat verbinding kan maken** beleid verleent machtigingen voor het verzenden en ontvangen van berichten met behulp van Hallo IoT Hub apparaat-side '-eindpunten.

* Klik op **maken** tooadd dit nieuw beleid toohello bestaande lijst gemaakt.

![][10]

## <a name="endpoints"></a>Eindpunten

Klik op **eindpunten** toodisplay een lijst met eindpunten voor Hallo IoT-hub die u wilt wijzigen. Er zijn twee soorten eindpunten: eindpunten die zijn ingebouwd in Hallo IoT-hub en eindpunten u toohello IoT-hub toevoegen na het maken ervan.

![][11]

### <a name="built-in-endpoints"></a>Ingebouwde eindpunten

Er zijn twee ingebouwde eindpunten: **toodevice feedback Cloud** en **gebeurtenissen**.

* **Cloud toodevice feedback** instellingen: deze instelling heeft twee subsettings: **tooDevice TTL Cloud** (time-to-live) en **bewaartijd** (in uren) voor Hallo-berichten. Wanneer uw eerste een iothub maakt, hebben beide deze instellingen standaardwaarde Hallo van één uur. tooadjust deze instellingen Hallo schuifregelaars gebruiken of typ Hallo waarden.
* **Gebeurtenissen** instellingen: deze instelling heeft verschillende subsettings, waarvan sommige alleen-lezen zijn. Hallo volgende lijst beschrijft deze instellingen:

  * **Partities**: een standaardwaarde is ingesteld wanneer Hallo IoT-hub is gemaakt. U kunt Hallo aantal partities via deze instelling wijzigen.

  * **Event Hub-compatibele naam en een eindpunt**: wanneer Hallo IoT-hub is gemaakt, een Event Hub intern wordt gemaakt dat u mogelijk moet toegang hebben tot toounder bepaalde omstandigheden. Hallo Event Hub-compatibele naam en het eindpunt waarden kan niet worden aangepast, maar u kunt deze kopiëren door te klikken op **kopie**.

  * **Bewaartijd**: tooone dag standaard ingesteld, maar u kunt met behulp van de vervolgkeuzelijst Hallo wijzigen. Deze waarde is in dagen voor het Hallo-apparaat-naar-cloud-instelling.

  * **Consumergroepen**: consumergroepen meerdere lezers tooread berichten onafhankelijk van de IoT-hub Hallo inschakelen. Elke iothub is gemaakt met een standaard consumergroep. U kunt echter toevoegen of verwijderen van de consument groepen tooyour IoT hubs die gebruikmaken van deze instelling.

  > [!NOTE]
  > Hallo standaard consumergroep kan niet worden bewerkt of verwijderd.

### <a name="custom-endpoints"></a>Aangepaste eindpunten

U kunt aangepaste eindpunten toevoegen op uw IoT-hub met Hallo-portal. Van Hallo **eindpunten** blade, klikt u op **toevoegen** op Hallo bovenste tooopen hello **eindpunt toevoegen** blade. Geef informatie op Hallo vereist en klik vervolgens op **OK**. Uw aangepaste eindpunt wordt nu weergegeven in de belangrijkste Hallo **eindpunten** blade.

![][13]

Meer informatie over aangepaste eindpunten in [referentie - IoT-hubeindpunten][lnk-devguide-endpoints].

## <a name="routes"></a>Routes

Klik op **Routes** toomanage hoe IoT Hub verzendt uw apparaat-naar-cloud-berichten.

![][14]

U kunt routes tooyour IoT-hub toevoegen door te klikken op **toevoegen** bovenaan Hallo Hallo **Routes*** blade Hallo vereist gegevens invoeren en op **OK**. Uw route wordt vervolgens weergegeven in de belangrijkste Hallo **Routes** blade. U kunt een route door erop te klikken in de lijst met routes Hallo bewerken. een route tooenable klikt u in de lijst met routes Hallo op en stel Hallo **ingeschakeld** te schakelen**uit**. toosave hello wijzigen, klikt u op **OK** Hallo Hallo blade onderaan in.

![][15]

## <a name="pricing-and-scale"></a>Prijzen en schaal

Hallo prijzen van een iothub kan worden gewijzigd via Hallo **prijzen** instellingen Hello volgende uitzonderingen:

* In de huidige implementatie hello, een iothub met een gratis SKU lagen tooone Hallo betaald SKU's, niet wijzigen of vice versa.
* Er kan alleen worden één laag gratis IoT-hub in hello Azure-abonnement.

![][12]

U kunt verplaatsen van een hogere toolower categorie alleen wanneer het aantal berichten die dag Hallo Hallo quotum voor de onderste laag Hallo overschrijden. Hallo bijvoorbeeld laag voor Hallo IoT hub kan worden gewijzigd op als het aantal berichten per dag Hallo 400.000 overschrijdt, vervolgens. Echter, als u toohello S1 laag wijzigt vervolgens Hallo IoT-hub is beperkt voor die dag.

## <a name="delete-hello-iot-hub"></a>Hallo IoT-hub verwijderen

U kunt toohello IoT-hub gewenste toodelete door te klikken op Bladeren **Bladeren**, en vervolgens te kiezen Hallo juiste hub toodelete. toodelete Hallo IoT-hub, klikt u op Hallo **verwijderen** knop onder naam Hallo IoT-hub.

## <a name="next-steps"></a>Volgende stappen

Volg deze koppelingen toolearn meer over het beheren van Azure IoT Hub:

* [Bulksgewijs IoT-apparaten beheren][lnk-bulk]
* [IoT Hub metrische gegevens][lnk-metrics]
* [Bewerkingen controleren][lnk-monitor]

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]
* [Een apparaat simuleren met IoT rand][lnk-iotedge]
* [Uw IoT-oplossing van Hallo gemalen beveiligen][lnk-securing]

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
