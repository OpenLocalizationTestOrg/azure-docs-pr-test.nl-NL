---
title: aaaAzure beheerde toepassingen in Hallo Marketplace | Microsoft Docs
description: Beschrijving van Azure beheerde toepassingen die beschikbaar via Hallo Marketplace zijn.
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a>Azure beheerde toepassingen in Hallo Marketplace

 MSPs, ISV's en systeemintegrators (SIs) kunnen gebruikmaken van Azure beheerde toepassingen toooffer hun klanten oplossingen tooall Azure Marketplace. Dergelijke oplossingen verminderd Hallo onderhoud en het onderhoud van de overhead voor klanten. Uitgevers kunnen verkopen infrastructuur- en software via Hallo Marketplace. Deze kunnen services en toepassingen van operationele ondersteuning toomanaged koppelen. Zie voor meer informatie [beheerde toepassingsoverzicht](managed-application-overview.md).

Dit artikel wordt uitgelegd hoe een MSP, ISV of SI kunt publiceren van een toepassing toohello Marketplace, waardoor het toocustomers schaal beschikbaar.

## <a name="prerequisites-for-publishing-a-managed-application"></a>Vereisten voor het publiceren van een beheerde toepassing

Vereisten toolisting in Hallo Marketplace:

* Technische

    *  Zie voor informatie over de basisstructuur Hallo en syntaxis van Azure Resource Manager-sjablonen, [Azure Resource Manager-sjablonen](resource-group-authoring-templates.md).
    *  oplossingen voor tooview volledige sjabloon, Zie [Azure-snelstartsjablonen](https://azure.microsoft.com/en-us/documentation/templates/) of Hallo [Quick Start sjabloon opslagplaats](https://github.com/azure/azure-quickstart-templates).
    *  Zie voor meer informatie over hoe toocreate interface voor het implementeren van uw toepassing via Hallo Marketplace-klanten Hallo [definitiebestand voor de interface van een gebruiker maken](managed-application-createuidefinition-overview.md).

* Niet-technische (bedrijfsvereisten)

    *   Uw bedrijf of de vestiging moet zich bevinden in een land waar verkoop worden ondersteund door Hallo Marketplace.
    *   Het product moet op een manier die compatibel is met factureringsmodellen ondersteund door Hallo Marketplace beschikken.
    *   U bent zelf verantwoordelijk voor het maken van de technische ondersteuning beschikbaar toocustomers in commercieel redelijke wijze. Hallo ondersteuning vrij, worden betaald, of via community ondersteunen.
    *   U bent zelf verantwoordelijk voor licentieverlening van uw software en eventuele afhankelijkheden software van derden.
    *   Inhoud die voldoet aan de criteria voor uw aanbieding toobe vermeld in de Marketplace hello en in hello Azure-portal, moet u opgeven.
    *   U moet akkoord gaan toohello gebruiksvoorwaarden hello Azure Marketplace deelname beleidsregels en uitgever overeenkomst.
    *   U moet akkoord gaan toocomply met gebruiksvoorwaarden hello, privacyverklaring van Microsoft en Microsoft Azure gecertificeerd programma overeenkomst.

## <a name="create-a-new-azure-application-offer"></a>Een nieuwe aanbieding voor Azure-toepassing maken

Wanneer u voldoet aan Hallo vereisten, bent u klaar toocreate uw aanbieding beheerde toepassing. U gaat nu een snel overzicht van een aanbieding en een SKU.

### <a name="offer"></a>Aanbieding

Hallo-aanbieding voor een beheerde toepassing komt overeen tooa klasse van het product aanbieden van een uitgever. Als u een nieuw type oplossing/toepassing die u wilt dat beschikbaar is in Hallo Marketplace toomake hebt, kunt u dit instellen als een nieuwe aanbieding. Een aanbieding is een verzameling van SKU's. Elke aanbieding wordt weergegeven als een eigen entiteit in Hallo Marketplace.

### <a name="sku"></a>SKU

Een SKU is Hallo kleinste over eenheid een aanbieding. U kunt een SKU binnen Hallo dezelfde product klasse (aanbieden) toodifferentiate tussen:

* Verschillende functies die worden ondersteund.
* Hiermee wordt aangegeven of de aanbieding Hallo beheerd of onbeheerd.
* Facturering modellen die worden ondersteund.

Een SKU wordt weergegeven onder Hallo bovenliggende aanbieding in Hallo Marketplace. Deze wordt weergegeven als een eigen over entiteit in hello Azure-portal.

### <a name="set-up-an-offer"></a>Instellen van een aanbieding

1. Meld u aan toohello [Cloud Partner-portal](https://cloudpartner.azure.com/).

2. Selecteer in het navigatievenster aan de linkerkant Hallo Hallo **+ een nieuwe aanbieding** > **Azure-toepassingen**.

    ![Nieuwe aanbieding](./media/managed-application-author-marketplace/newOffer.png)

3. Hallo-formulieren die worden weergegeven op de links in Hallo Hallo invullen **Editor** weergeven. Verplichte velden zijn gemarkeerd met een rode asterisk (*).

    ![Aanbieding-instellingen](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    Vier belangrijke formulieren zijn gebruikte toocreate een beheerde toepassing:

    a. Aanbieding-instellingen

    b. SKU 's

    c. Marketplace

    d. Ondersteuning

Deze formulieren worden in de volgende secties Hallo uitgebreider beschreven.

## <a name="offer-settings-form"></a>Formulier voor instellingen van aanbieding
Gebruik deze instellingen elementaire vorm toospecify Hallo aanbieding.

1. Vul Hallo **instellingen bieden** formulier. Hallo verschillende velden zijn:

    a. **ID bieden**: deze unieke id identificeert Hallo aanbieding binnen een publisher-profiel. Deze ID wordt weergegeven in de product-URL's, Resource Manager-sjablonen en facturering rapporteert. Deze kan alleen bestaan uit alfanumerieke tekens in kleine letters of streepjes (-). Hallo-ID mag niet eindigen op een streepje. Het is beperkt tooa maximum van 50 tekens. Nadat een aanbieding live gaat, wordt dit veld is vergrendeld.

    b. **Uitgevers-ID**: Gebruik deze vervolgkeuzelijst toochoose Hallo publisher gewenste profiel toopublish deze aanbieding onder. Nadat een aanbieding live gaat, wordt dit veld is vergrendeld.

    c. **Naam**: deze weergavenaam voor uw aanbieding weergegeven in de Marketplace hello en in Hallo-portal. Er kunnen maximaal 50 tekens. Een herkenbare naam merk voor het product bevatten. Neem geen hier de naam van uw bedrijf tenzij hoe deze wordt gebracht. Als u deze aanbieding bent marketing op uw eigen website, zorg ervoor dat Hallo naam exact hoe deze wordt weergegeven op uw website.

2. Selecteer **opslaan** toosave uw voortgang. 

## <a name="skus-form"></a>Formulier SKU 's
de volgende stap Hallo is tooadd SKU's voor uw aanbieding.

1. Selecteer **SKU's** > **nieuwe SKU**. 

    ![Selecteer nieuwe SKU](./media/managed-application-author-marketplace/newOffer_skus.png)

2. Voer een **SKU-ID**. Een SKU-ID is een unieke id voor Hallo SKU binnen een aanbieding. Deze ID wordt weergegeven in de product-URL's, Resource Manager-sjablonen en facturering rapporteert. Deze kan alleen bestaan uit alfanumerieke tekens in kleine letters of streepjes (-). Hallo-ID mag niet eindigen op een streepje en is beperkt tooa maximum van 50 tekens. Nadat een aanbieding live gaat, wordt dit veld is vergrendeld. U kunt meerdere SKU's binnen een aanbieding hebben. U moet een SKU voor elke installatiekopie u van plan bent toopublish.

3. Hallo invullen **SKU Details** sectie op Hallo formulier te volgen:

    ![Geef nieuwe SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    Vul Hallo velden te volgen:
    
    a. **Titel**: Voer een titel voor de SKU. Deze titel wordt weergegeven in de galerie Hallo voor dit item.

    b. **Samenvatting**: Voer een korte samenvatting voor de SKU. Deze tekst wordt weergegeven onder Hallo titel.

    c. **Beschrijving**: Voer een gedetailleerde beschrijving over Hallo SKU.

    d. **SKU-Type**: Hallo toegestane waarden zijn **beheerde toepassingen** en **Oplossingssjablonen**. Selecteer voor deze aanvraag **beheerde toepassing**.

4. Hallo invullen **pakketgegevens** sectie op Hallo formulier te volgen:

    ![Pakket](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    Vul Hallo velden te volgen:

    a. **Huidige versie**: Voer een versie voor u uploaden Hallo-pakket. Deze moet Hallo indeling `{number}.{number}.{number}{number}`.

    b. **Selecteer een pakketbestand**: dit pakket bevat de volgende bestanden die zijn gecomprimeerd in een ZIP-bestand Hallo:
    * **applianceMainTemplate.json**: Hallo implementatie sjabloonbestand die toodeploy Hallo oplossing/toepassing wordt gebruikt. Voor informatie over het toocreate implementatie sjabloonbestanden, Zie [maken van uw eerste Azure Resource Manager-sjabloon](resource-manager-create-first-template.md).
    * **appliancecreateUIDefinition.json**: dit bestand wordt gebruikt door hello Azure portal toogenerate Hallo-gebruikersinterface die tooprovision deze oplossing/toepassing heeft gebruikt. Zie voor meer informatie [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
    * **mainTemplate.json**: dit sjabloonbestand bevat alleen Hallo Microsoft.Solution/appliances resource. Hallo mainTemplate bestand bevat Hallo volgende eigenschappen:

        *  **type**: Gebruik **Marketplace** voor beheerde toepassingen in Hallo Marketplace.
        *  **ManagedResourceGroupId**: deze resourcegroep in het abonnement van de klant Hallo is waarin alle Hallo resources die zijn gedefinieerd in applianceMainTemplate.json zijn geïmplementeerd.
        *  **PublisherPackageId**: een unieke identificatie van deze tekenreeks Hallo-pakket. Geef een waarde Hallo Hallo-indeling van `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.

Hallo verkrijgen **bieden ID** en **uitgevers-ID** van Hallo publiceren portal, zoals wordt weergegeven in Hallo installatiekopie te volgen:

![Aanbieding-ID](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
Hallo verkrijgen **SKU-ID**, zoals weergegeven in Hallo installatiekopie te volgen:

![SKU-ID](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
Hallo pakket verkrijgen **versie**, zoals weergegeven in Hallo installatiekopie te volgen:

![Pakketversie](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  Op basis van de voorgaande voorbeelden hello, waarde van Hallo **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.

  Voorbeeld mainTemplate.json:

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

Dit pakket bevat geen geneste sjablonen of scripts die vereist toosuccessfully zijn inrichten van deze toepassing. Hallo zijn mainTemplate.json, applianceMainTemplate.json en applianceCreateUIDefinition.json bestanden aanwezig op Hallo-hoofdmap.

* **Autorisaties**: deze eigenschap wordt gedefinieerd wie er toegang en Hallo toegangsniveau toohello resources in klanten abonnementen. Hallo-uitgever kunt toomanage Hallo toepassing namens de klant hello gebruiken.
* **PrincipalId**: deze eigenschap is hello Azure Active Directory (Azure AD)-ID van een gebruiker, groep of toepassing die bepaalde machtigingen op Hallo bronnen in het abonnement van de klant Hallo heeft verleend. Hallo roldefinitie beschrijft Hallo machtigingen. 
* **Roldefinitie**: deze eigenschap is een lijst met alle Hallo ingebouwde rollen gebaseerd toegangsbeheer (RBAC) rollen verstrekt door Azure AD. Hallo-rol die meest geschikte toouse toomanage Hallo bronnen namens de klant Hallo is, kunt u selecteren.

U kunt meerdere autorisaties toevoegen. Het is raadzaam dat u een AD-gebruikersgroep maken en geef de bijbehorende ID in **PrincipalId**. Op deze manier kunt u meer gebruikers toohello gebruikersgroep zonder Hallo nodig tooupdate Hallo SKU toevoegen.

Zie voor meer informatie over RBAC [aan de slag met RBAC in Azure-portal Hallo](../active-directory/role-based-access-control-what-is.md).

## <a name="marketplace-form"></a>Formulier Marketplace

Hallo Marketplace formulier vraagt om de velden die worden weergegeven op Hallo [Azure Marketplace](https://azuremarketplace.microsoft.com) en op Hallo [Azure-portal](https://portal.azure.com/).

### <a name="preview-subscription-ids"></a>Preview abonnement-id 's

Geef een lijst met Azure-abonnement-id's die u toegang krijgen Hallo aanbieding tot kunt nadat deze gepubliceerd. U kunt deze aanbieding abonnementen wit vermeld tootest Hallo bekeken voordat u deze maakt live. U kunt een witte lijst van van abonnementen in de Partnerportal Hallo too100 compileren.

### <a name="suggested-categories"></a>Aanbevolen categorieën

Selecteer toofive categorieën van de lijst met Hallo die uw aanbieding beste kan worden gekoppeld aan. Deze categorieën gebruikt toomap zijn uw aanbieding toohello productcategorieën die beschikbaar in Hallo zijn [Azure Marketplace](https://azuremarketplace.microsoft.com) en Hallo [Azure-portal](https://portal.azure.com/).

#### <a name="azure-marketplace"></a>Azure Marketplace

Samenvatting van uw beheerde toepassing Hello weergegeven Hallo velden te volgen:

![Samenvatting van Marketplace](./media/managed-application-author-marketplace/publishvm10.png)

Hallo **overzicht** tabblad voor uw beheerde toepassing hello volgende velden worden weergegeven:

![Overzicht van Marketplace](./media/managed-application-author-marketplace/publishvm11.png)

Hallo **plannen + prijzen** tabblad voor uw beheerde toepassing hello volgende velden worden weergegeven:

![Marketplace-abonnementen](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a>Azure Portal

Samenvatting van uw beheerde toepassing Hello weergegeven Hallo velden te volgen:

![Portal-overzicht](./media/managed-application-author-marketplace/publishvm12.png)

overzicht voor de beheerde toepassing Hello weergegeven Hallo velden te volgen:

![Overzicht van de portal](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a>Richtlijnen voor het logo

Volg deze richtlijnen voor een logo dat u in de Cloud Partner-portal Hallo uploaden:

*   Hello Azure ontwerp heeft een eenvoudige kleurenpalet. Hallo-nummer van primaire en secundaire kleuren op uw logo beperken.
*   Hallo themakleuren van Hallo portal zijn wit en zwarte. Deze kleuren als achtergrondkleur Hallo niet worden gebruikt voor het logo. Gebruik een kleur die uw logo prominent op Hallo portal maakt. Het wordt aangeraden de eenvoudige primaire kleuren. *Als u een transparante achtergrond gebruikt, zorg ervoor dat Hallo-logo en tekst worden niet wit, zwart of blauw.*
*   Gebruik geen een kleurovergang achtergrond op Hallo-logo.
*   Plaats geen tekst in het Hallo-logo, zelfs niet uw bedrijf of de naam. Hallo-uiterlijk van uw logo moet platte en kleurovergangen voorkomen.
*   Zorg ervoor dat het Hallo-logo niet is gespreid.

#### <a name="hero-logo"></a>Hero-logo

Hallo hero logo is optioneel. Hallo-uitgever kunt niet tooupload een hero-logo. Nadat Hallo hero pictogram is geüpload, kan niet worden verwijderd. Op dat moment moet Hallo partner Hallo Marketplace richtlijnen voor het hero pictogrammen volgen.

Volg deze richtlijnen voor Hallo hero logo pictogram:

*   Hallo publisher weergavenaam, Hallo plan titel en Hallo aanbieding lange samenvatting worden in wit weergegeven. Daarom niet voor de achtergrond Hallo van Hallo hero pictogram een lichte kleur te gebruiken. Een zwarte, wit of transparante achtergrond is niet toegestaan voor hero pictogrammen.
*   Nadat het Hallo-aanbieding wordt weergegeven, Hallo publisher weergavenaam, Hallo plan titel, Hallo aanbieding lange samenvatting en Hallo **maken** knop programmatisch binnen Hallo hero-logo zijn ingesloten. Als gevolg daarvan kan niets invoert terwijl u Hallo hero logo ontwerpt. Laat leeg ruimte op Hallo rechts omdat tekst hello programmatisch is opgenomen in deze ruimte. Hallo lege ruimte voor de tekst hello moet 415 x 100 pixels op Hallo rechts. Er wordt met 370 pixels van Hallo links verschoven.

    ![Voorbeeld van Hero-logo](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a>Ondersteuning voor formulier

Hallo invullen **ondersteunen** formulier met ondersteuning voor contactpersonen van uw bedrijf. Deze informatie kan worden engineering, contactpersonen en contactpersonen voor ondersteuning van klant.

## <a name="publish-an-offer"></a>Een aanbieding publiceren

Nadat u alle Hallo secties invult, selecteert u **publiceren** toostart Hallo-proces waarmee uw aanbieding beschikbaar toocustomers.

## <a name="next-steps"></a>Volgende stappen

* Zie voor een inleiding toomanaged toepassingen, [beheerde toepassingsoverzicht](managed-application-overview.md).
* Zie voor meer informatie over het gebruiken van een beheerde toepassing hello Marketplace [Azure gebruiken beheerde toepassingen in Hallo Marketplace](managed-application-consume-marketplace.md).
* Zie voor meer informatie over het publiceren van een Servicecatalogus beheerde toepassing [maken en publiceren van een Servicecatalogus beheerde toepassing](managed-application-publishing.md).
* Zie voor meer informatie over het gebruiken van een Servicecatalogus beheerde toepassing [gebruiken van een Servicecatalogus beheerde toepassing](managed-application-consumption.md).
