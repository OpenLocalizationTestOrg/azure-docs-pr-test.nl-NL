---
title: aaaGet slag met persoonlijke sjablonen | Microsoft Docs
description: Toevoegen, beheren en delen van uw persoonlijke sjablonen met hello Azure-portal, hello Azure CLI of PowerShell.
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a>Aan de slag met persoonlijke sjablonen in hello Azure Portal
Een [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) sjabloon is een declaratief sjabloon gebruikt toodefine uw implementatie. U kunt definiëren Hallo resources toodeploy voor een oplossing en geef parameters en variabelen die u in staat tooinput waarden voor verschillende omgevingen stellen. Hallo sjabloon bestaat uit JSON en uitdrukkingen die u kunt tooconstruct waarden voor uw implementatie.

Kunt u Hallo nieuwe **sjablonen** mogelijkheden in Hallo [Azure Portal](https://portal.azure.com) samen met de Hallo **Microsoft.Gallery** resourceprovider als een uitbreiding van Hallo [ Azure Marketplace](https://azure.microsoft.com/marketplace/) toocreate tooenable gebruikers, beheren en implementeren van persoonlijke sjablonen vanuit een persoonlijke bibliotheek.

Dit document vindt u bij het toevoegen, beheren en delen van een persoonlijk **sjabloon** met behulp van hello Azure-Portal.

## <a name="guidance"></a>Richtlijnen
Hallo volgende tips kunt u profiteren van **sjablonen** bij het werken met uw oplossingen:

* Een **sjabloon** is een inkapselende resource met een Resource Manager-sjabloon en aanvullende metagegevens. Dit werkt op dezelfde manier tooan item in Hallo Marketplace. Hallo belangrijkste verschil is dat het een persoonlijk item als tegengestelde toohello openbaar Marketplace-item is.
* Hallo **sjablonen** bibliotheek geschikt is voor gebruikers hoeven toocustomize implementaties.
* **Sjablonen** zijn handig voor gebruikers die een eenvoudige opslagplaats in Azure nodig hebben.
* Begin met een bestaand Resource Manager-sjabloon. Zoek sjablonen in [github](https://github.com/Azure/azure-quickstart-templates) of [exporteer een sjabloon](../azure-resource-manager/resource-manager-export-template.md) vanuit een bestaande resourcegroep.
* **Sjablonen** gebonden toohello-gebruiker die deze publiceert. Hallo de naam van uitgever is zichtbaar tooeveryone die tooit leestoegang heeft.
* **Sjablonen** zijn resources van de Resource Manager en kunnen na publicatie niet meer worden gewijzigd.

## <a name="add-a-template-resource"></a>Een sjabloonresource toevoegen
Er zijn twee manieren toocreate een **sjabloon** resource in hello Azure-portal.

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a>Methode 1: Maak een nieuwe sjabloonresource vanuit een bestaande resourcegroep
1. Navigeer tooan bestaande resourcegroep in hello Azure-Portal. Klik op **Sjabloon exporteren** in **Instellingen**.
2. Zodra het Hallo Resource Manager-sjabloon is geëxporteerd, gebruikt u Hallo **sjabloon opslaan** knop toosave het toohello **sjablonen** opslagplaats. Meer informatie over het exporteren van sjablonen vindt u [hier](../azure-resource-manager/resource-manager-export-template.md).
   <br /><br />
   ![Resourcegroep exporteren](media/rg-export-portal1.PNG)  <br />
3. Selecteer Hallo **tooTemplate opslaan** opdrachtknop.
   <br /><br />
4. Voer Hallo volgende informatie:
   
   * Naam: naam van het object hello (Opmerking: dit is een naam op basis van Azure Resource Manager. Alle naamsbeperkingen zijn van toepassing en de naam kan achteraf niet meer worden gewijzigd).
   * Beschrijving – korte samenvatting van Hallo-sjabloon.
     
     ![Sjabloon opslaan](media/save-template-portal1.PNG)  <br />
5. Klik op **Opslaan**.
   
   > [!NOTE]
   > Hallo blade sjabloon exporteren geeft een melding weer wanneer hello geëxporteerde Resource Manager-sjabloon fouten bevat, maar u kunt nog steeds kunnen toosave deze Resource Manager-sjabloon toohello sjablonen. Zorg ervoor dat Controleer en corrigeer eventuele Resource Manager voordat opnieuw distribueren Hallo geëxporteerd Resource Manager-sjabloon sjabloonproblemen.
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a>Methode 2: Een nieuwe sjabloonresource toevoegen door middel van bladeren
U kunt ook toevoegen een nieuwe **sjabloon** helemaal met Hallo + knop toevoegen in **Bladeren > sjablonen**. U moet een naam, beschrijving en Hallo Resource Manager-sjabloon JSON tooprovide.

![Sjabloon toevoegen](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> Microsoft.Gallery is een op tenants gebaseerde resourceprovider van Azure. Hallo is sjabloonresource gebonden toohello-gebruiker die deze is gemaakt. Het is niet gebonden tooany bepaald abonnement. Een abonnement moet toobe ervoor gekozen alleen bij het implementeren van een sjabloon.
> 
> 

## <a name="view-template-resources"></a>Sjabloonresources bekijken
Alle **sjablonen** tooyou beschikbaar die kan worden weergegeven wanneer **Bladeren > sjablonen**. Dit zijn zowel **sjablonen** die u hebt gemaakt als sjablonen met verschillende bevoegdheidsniveaus die met u zijn gedeeld. Meer informatie in Hallo [toegangsbeheer](#access-control-for-a-tenant-resource-provider) hieronder.

![Sjabloon weergeven](media/view-template-portal1.PNG)  <br />

U kunt Hallo weergeven van een **sjabloon** door te klikken op een item in de lijst Hallo.

![Sjabloon weergeven](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a>Een sjabloonresource bewerken
U kunt starten Hallo bewerken stroom voor een **sjabloon** door Hallo-item op Hallo zoeklijst rechtermuisknop te klikken of door te kiezen opdrachtknop Hallo-bewerken.

![Sjabloon bewerken](media/edit-template-portal1a.PNG)  <br />

U kunt Hallo beschrijving of de sjabloontekst van Resource Manager-bewerken. U kunt Hallo-naam niet bewerken omdat deze de naam van een Resource Manager-resource. Wanneer u Hallo Resource Manager-sjabloon JSON bewerkt zullen we dit valideren tooensure dat het een geldige JSON is. Kies **OK** en vervolgens **opslaan** toosave uw bijgewerkte sjabloon.

![Sjabloon bewerken](media/edit-template-portal2a.PNG)  <br />

Eenmaal Hallo **sjabloon** wordt opgeslagen ziet u een bevestigingsbericht weergegeven.

![Sjabloon bewerken](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a>Een sjabloonresource implementeren
U kunt elk **sjabloon** implementeren waarvoor u een **lees**machtiging heeft. Hallo implementatie stroom wordt Hallo standaard Azure-sjabloon implementatie blade gestart. Vul Hallo waarden voor Hallo Resource Manager-sjabloon parameters tooproceed met Hallo-implementatie.

![Sjabloon implementeren](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a>Een sjabloonresource delen
U kunt een **sjabloon**resource delen met anderen. Delen gedraagt zich op dezelfde manier te[roltoewijzing voor een resource in Azure](../active-directory/role-based-access-control-configure.md). Hallo **sjabloon** eigenaar biedt machtigingen tooother gebruikers die kunnen communiceren met een sjabloonresource. Hallo persoon of groep personen die u deelt Hallo **sjabloon** met worden kunnen toosee Hallo Resource Manager-sjabloon en de galerie-eigenschappen.

### <a name="access-control-for-hello-microsoftgallery-resources"></a>Toegangsbeheer voor Microsoft.Gallery-resources Hallo
| Rol | Machtigingen |
| --- | --- |
| Eigenaar |Volledige controle over de sjabloonresource Hallo onder andere het delen |
| Lezer |Sjabloonresource lezen en kunnen op Hallo sjabloonresource |
| Inzender |Kunnen bewerken en verwijderen op Hallo sjabloonresource. Gebruiker delen Hallo sjabloon niet met anderen |

Selecteer **Share** op Hallo bladeritem met de rechtermuisknop te klikken of op Hallo weergave blade van een specifiek item. Hiermee opent u een omgeving om het sjabloon te delen.

![Sjabloon delen](media/share-template-portal1a.png)  <br />

 U kunt nu een rol en een gebruiker of groep tooprovide toegang tooa bepaalde **sjabloon**. Hallo beschikbare rollen zijn eigenaar, lezer en Inzender. Meer informatie in Hallo [toegangsbeheer](#access-control-for-a-tenant-resource-provider) sectie hierboven.

![Sjabloon delen](media/share-template-portal2b.png)  <br />

![Sjabloon delen](media/share-template-portal3b.png)  <br />

Klik op **Selecteren** en vervolgens op **Ok**. U kunt nu zien Hallo gebruikers of groepen hebt u toohello resource toegevoegd.

![Sjabloon delen](media/share-template-portal4b.png)  <br />

> [!NOTE]
> Een sjabloon kan alleen worden gedeeld met gebruikers en groepen in Hallo dezelfde Azure Active Directory-tenant. Als u een sjabloon met een e-mailadres dat zich niet in uw tenant deelt, wordt een uitnodiging verzonden hello gebruiker toojoin hello tenant als gast waarin wordt gevraagd.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* toolearn over het maken van Resource Manager-sjablonen, Zie [sjablonen te bewerken](../azure-resource-manager/resource-group-authoring-templates.md)
* Zie toounderstand Hallo functies die u kunt gebruiken in een Resource Manager-sjabloon [sjabloonfuncties](../azure-resource-manager/resource-group-template-functions.md)
* Zie [Best practices voor het ontwerpen van Azure Resource Manager-sjablonen](../azure-resource-manager/best-practices-resource-manager-design-templates.md) voor meer informatie over het ontwerpen van uw sjablonen

