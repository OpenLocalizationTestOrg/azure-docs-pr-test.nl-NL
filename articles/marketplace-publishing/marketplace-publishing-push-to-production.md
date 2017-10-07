---
title: aaaDeploy uw aanbieding toohello Azure Marketplace | Microsoft Docs
description: Informatie over en doorloop Hallo instructies toodeploy uw aanbieding--de installatiekopie van virtuele machine, developer-service, data-service, enzovoort--toohello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 8f79b891-84e2-4f41-ba0d-66420e2c6b2e
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2016
ms.author: hascipio
ms.openlocfilehash: ab0bb7c78020187505c2d5f09c4de246987ecd97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-offer-toohello-azure-marketplace"></a>Implementeer uw aanbieding toohello Azure Marketplace
Wanneer u tevreden bent met uw aanbieding (dat wil zeggen, u hebt getest scenario's van klanten, marketing inhoud, enz.) en u bent klaar toolaunch aanvraag **Push tooproduction** op Hallo **publiceren** tabblad.  

1. Hallo vier stappen onder Hallo SCENARIO pagina in Hallo portal publiceren moet zijn voltooid en groen. Voor aanbiedingen van de virtuele Machine, moet u ervoor zorgen dat Hallo richtlijnen worden gevolgd.
   
    ![tekenen][img-pubportal-walkthru-checked]
2. Selecteer Hallo **publiceren** tabblad in de lijst Hallo op Hallo linkerkant.
   
    ![tekenen][img-pubportal-menu-publish]
3. Klik op de knop Hallo **aanvragen van goedkeuring toopush tooproduction**. Zodra het Hallo-aanvraag wordt gedaan, Hallo goedkeuring wordt uitgevoerd door een definitieve beoordeling en vervolgens uw aanbieding is beschikbaar in hello Azure Marketplace.
   
    ![tekenen][img-pubportal-publish-pushproduction]

> [!IMPORTANT]
> In geval van virtuele Machines, wanneer u op Hallo knop aanvraag goedkeuring toopush tooproduction Hallo stappen te volgen uitgevoerd achter Hallo scene. U zult kunnen tooview Hallo voortgang van elke stap Hallo publiceren tabblad in Hallo portal publiceren. U moet controleren op deze pagina op een vast interval (totdat het Hallo-status geeft 'Hier') voor alle foutinformatie die nodig correctie van uw.
> 
> * In eerste instantie gaat uw productie-aanvraag toohello certificeringsinstantie team dat Hallo vhd valideren. Echter, als u uw al genoemde aanbieding bijwerken wilt en Hallo-aanvraag heeft kreeg alleen marketing wijzigen, klikt u vervolgens Hallo certificeringsinstantie stap overgeslagen.
> * Op de volgende stap Hallo komen Hallo aanvraag toohello inhoudsvalidatie team dat inhoud van de aanbieding Hallo marketing Hallo controleren.
> * Als Hallo bovenstaande stappen voltooid zijn, klikt u vervolgens Hallo aanbieding goedgekeurd in productie. Op dit moment Hallo status worden 'weergegeven' in de portal voor het publiceren van Hallo. Deze status 'Hier' betekent echter niet dat Hallo-proces is voltooid. volgende stappen nodig toobe voltooid voordat de aanbieding Hallo Hallo is beschikbaar in hello Azure Marketplace.
> * Zodra Hallo aanbieding is goedgekeurd in de productieomgeving in Hallo stap hierboven, Hallo replicatie van Hallo aanbieding starten voor alle Azure-datacenters. In het algemeen neemt 24-48hours voor Hallo replicatie toocomplete maar tooa week, afhankelijk van de grootte op Hallo van Hallo vhd kan duren. Als u uw al genoemde aanbieding bijwerken wilt en die bevat immers alleen marketing wijzigen, klikt u vervolgens is Hallo-replicatie echter sneller.
> * Wanneer het Hallo-replicatie is voltooid, klikt u vervolgens is Hallo aanbieding beschikbaar in hello Azure Marketplace.
> 
> U kunt altijd Hallo aanbieding verwijderen wanneer deze is in een **concept** status (dat wil zeggen, nooit **Push toostaging** of **tooproduction Push**). Op Hallo **geschiedenis** en klik op Hallo **concept verwijderen** knop Hallo Hallo pagina toodelete onderaan in een concept.
> 
> 

## <a name="production-checklist-for-all-virtual-machine-offers"></a>Productie controlelijst voor alle aanbiedingen voor virtuele Machine
* Zorg ervoor dat u een Microsoft Azure Certified partner
* Hallo-SKU's tabblad moeten Hallo optie 'verbergen de SKU van Hallo Marketplace omdat moet altijd worden aangekocht via een oplossingssjabloon' worden gemarkeerd als alleen Ja als Hallo SKU deel van een oplossingssjabloon uitmaakt. Hallo in alle andere gevallen, deze optie moet altijd worden gemarkeerd als Nee.
* Onthouden: Moet u Hallo SKU zichtbaarheidsinstelling niet wijzigen zodra Hallo SKU wordt vermeld. We ondersteund deze functionaliteit niet.
* Zorg ervoor dat Hallo logo's toohello Azure Marketplace richtlijnen voor het logo hieronder voldoen.
* Aanbieding en SKU beschrijving mag niet hetzelfde zijn.
* SKU van titel en bieden lange samenvatting mag niet hetzelfde zijn.
* SKU titel en bieden samenvatting mag niet hetzelfde zijn.
* SKU titels mag niet zijn identiek voor een aanbieding met meerdere SKU's.

**Richtlijnen voor Azure Marketplace-logo**

* Hello Azure ontwerp heeft een eenvoudige kleurenpalet. Houd Hallo van de primaire en secundaire kleuren op uw logo laag.
* Hallo themakleuren hello Azure-portal zijn wit en zwarte. Daarom Vermijd het gebruik van deze kleuren als achtergrondkleur Hallo van uw logo's. Gebruik een kleur die uw logo's prominent op Hallo Azure-portal zou maken. Het wordt aangeraden de eenvoudige primaire kleuren. Als u met behulp van transparante achtergrond, moet u ervoor zorgen dat Hallo logo/tekst is niet witte of zwarte.
* Een achtergrond met kleurovergang niet gebruiken op Hallo-logo.
* Vermijd tekst, zelfs uw bedrijf of de naam van het merk, plaatsen op Hallo-logo.
* Hallo-uiterlijk van uw logo moet 'platte' en moet niet verlopen.
* Hallo-logo mag niet worden uitgerekt.

**Aanvullende richtlijnen voor het Hallo Hero logo:**

* Hallo Hero logo is optioneel. Hallo-uitgever kunt niet tooupload een Hero-logo. **Maar één keer geüploade Hallo hero pictogram kan niet worden verwijderd uit Hallo portal publiceren. Op dat moment Hallo partner hello Azure Marketplace richtlijnen moet volgen voor Hero pictogrammen anders Hallo aanbieding niet worden goedgekeurd tooproduction.**
* Hallo Publisher weergavenaam, SKU titel en Hallo bieden lange samenvatting worden weergegeven in wit tekstkleur. Daarom moet u niet een lichte kleur op de achtergrond Hallo Hallo Hero pictogram houden. Zwart, wit en transparante achtergrond is niet toegestaan voor Hero pictogrammen.
* Hello weergavenaam van de uitgever, SKU-titel, Hallo aanbieding lange samenvatting en Hallo knop maken via een programma in Hallo Hero-logo zijn ingesloten zodra Hallo aanbieding vermelde gaat. U moet dus niet alle tekst invoeren bij het ontwerpen van Hallo Hero-logo. Stelt u lege ruimte aan de rechterkant Hallo omdat tekst hello (dat wil zeggen weergavenaam van de uitgever, SKU titel, Hallo aanbieding lange samenvatting) wordt opgenomen via programmacode door ons hier. Hallo lege ruimte voor de tekst hello moet 415 x 100 op Hallo rechts (en deze worden gecompenseerd via 370px van Hallo links).

## <a name="additional-production-checklist-for-already-listed-virtual-machine-offers"></a>Biedt extra productie controlelijst voor het al genoemde virtuele Machine
* Controleer dat als er al een aanbieding met Hallo dezelfde naam van uw bedrijf wilt bieden. Zo ja, moet u een nieuwe versie van Hallo SKU toevoegen Hallo bestaande aanbieding in plaats van een nieuwe aanbieding dubbele maken.
* Gegevensschijf moet niet wijzigen tussen twee versies van Hallo dezelfde SKU.
* Hello Azure Marketplace biedt geen ondersteuning voor SKU's wijziging Hallo prijzen worden weergegeven als het Hallo-facturering met bestaande klanten Hallo heeft impact op. Zorg ervoor dat u niet wijzigt Hallo prijzen van SKU's Hallo vermeld in Hallo regio's waar Hallo SKU beschikbaar is. U kunt echter nieuwe SKU's toevoegen of toevoegen van nieuwe regio's tooan bestaande SKU.

## <a name="next-steps"></a>Volgende stappen
Zodra Hallo aanbieding live gaat, testen Hallo klant scenario's toovalidate Hallo opdrachten en functionaliteit werkt goed in de productieomgeving Hallo als geteste en gevalideerde in Hallo-testomgeving.

## <a name="see-also"></a>Zie ook
* [Aan de slag: hoe toopublish een aanbieding toohello Azure Marketplace](marketplace-publishing-getting-started.md)

[img-pubportal-walkthru-checked]:media/marketplace-publishing-push-to-production/pubportal-walkthru-checked.png
[img-pubportal-menu-publish]:media/marketplace-publishing-push-to-production/pubportal-menu-publish.png
[img-pubportal-publish-pushproduction]:media/marketplace-publishing-push-to-production/pubportal-publish-pushproduction.png
