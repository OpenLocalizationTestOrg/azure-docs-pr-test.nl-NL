---
title: Overzicht van Resource Manager aaaAzure | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Azure Resource Manager voor de implementatie, beheer- en toegangsbeheer van bronnen in Azure.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 76df7de1-1d3b-436e-9b44-e1b3766b3961
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: tomfitz
ms.openlocfilehash: a44fccd96d722c006224145d71cc44292255debf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-overview"></a>Overzicht van Azure Resource Manager
Hallo-infrastructuur voor uw toepassing wordt normaal gesproken bestaat uit veel onderdelen, zoals een virtuele machine, storage-account en virtueel netwerk of een web-app, database, databaseserver en 3e services van derden. Deze onderdelen moet u niet zien als afzonderlijke entiteiten, maar als onderdelen die één entiteit vormen en aan elkaar zijn gerelateerd en afhankelijk zijn van elkaar. U wilt dat toodeploy, beheren en ze als een groep te controleren. Azure Resource Manager kunt u toowork met Hallo resources in uw oplossing als een groep. U kunt implementeren, bijwerken of verwijderen van alle Hallo resources voor uw oplossing in een enkele, gecoördineerde bewerking. Voor implementatie gebruikt u een sjabloon. Deze sjabloon kan voor verschillende omgevingen worden gebruikt, zoals testen, faseren en productie. Resource Manager biedt beveiliging, controle en functies toohelp tagging u uw resources beheren na implementatie. 

## <a name="terminology"></a>Terminologie
Als u nieuwe tooAzure Resource Manager, zijn er mogelijk niet bekend bent met termen.

* **resource** - een beheerbaar item dat beschikbaar is via Azure. Sommige algemene resources zijn een virtuele machine, opslagaccount, webtoepassing en virtueel netwerk, maar er zijn er veel meer.
* **resourcegroep** - een container met gerelateerde resources voor een Azure-oplossing. Hallo resourcegroep kan alle Hallo resources voor Hallo oplossing of alleen de gewenste toomanage als een groep resources bevatten. U bepalen hoe u resources tooallocate tooresource groepen op basis van het wat zinvol Hallo meeste voor uw organisatie. Zie [Resourcegroepen](#resource-groups).
* **resourceprovider** -een service die Hallo resources levert die u kunt implementeren en beheren via Resource Manager. Elke resourceprovider biedt bewerkingen voor het werken met Hallo-resources die zijn geïmplementeerd. Sommige algemene resourceproviders zijn Microsoft.Compute die de bron van de virtuele machine Hallo levert, Microsoft.Storage die Hallo storage account resource levert, en Microsoft.Web die bronnen gerelateerde tooweb apps levert. Zie [Resourceproviders](#resource-providers).
* **Resource Manager-sjabloon** -A JSON JavaScript Object Notation ()-bestand dat een of meer resources toodeploy tooa resourcegroep definieert. Het definieert ook Hallo afhankelijkheden tussen resources Hallo geïmplementeerd. Hallo sjabloon zijn consistent en herhaaldelijk gebruikte toodeploy Hallo resources. Zie [Sjabloonimplementatie](#template-deployment).
* **declaratieve syntaxis** -syntaxis, waarmee u status ' Dit is wat ik van plan bent toocreate ' zonder toowrite Hallo reeks opdrachten toocreate programming deze. Hallo Resource Manager-sjabloon is een voorbeeld van een declaratieve syntaxis. In het Hallo-bestand definieert u Hallo-eigenschappen voor Hallo infrastructuur toodeploy tooAzure. 

## <a name="hello-benefits-of-using-resource-manager"></a>Hallo voordelen van het gebruik van Resource Manager
Resource Manager biedt diverse voordelen:

* U kunt implementeren, beheren en bewaken van alle Hallo resources voor uw oplossing als een groep in plaats van deze resources afzonderlijk te verwerken.
* U kunt herhaaldelijk implementeren van uw oplossing gedurende de ontwikkelingscyclus Hallo en erop vertrouwen dat uw resources worden geïmplementeerd in een consistente status.
* U kunt uw infrastructuur beheren via declaratieve sjablonen in plaats van scripts.
* U kunt Hallo afhankelijkheden tussen resources zo ze zijn geïmplementeerd in de juiste volgorde Hallo definiëren.
* Omdat op rollen gebaseerde toegangsbeheer (RBAC) is geïntegreerd in het beheerplatform hello, kunt u access control-tooall services toepassen in de resourcegroep.
* U kunt tags toepassen tooresources toologically organiseren alle Hallo resources in uw abonnement.
* U kunt facturering voor uw organisatie verduidelijken door het bekijken van de kosten voor een groep resources delen dezelfde tag Hallo.  

Resource Manager biedt een nieuwe manier toodeploy en beheren van uw oplossingen. Als u hebt gebruikt eerdere implementatiemodel Hallo en toolearn over Hallo wijzigingen, Zie [Understanding Resource Manager-implementatie en klassieke implementatie](resource-manager-deployment-model.md).

## <a name="consistent-management-layer"></a>Consistente beheerlaag
Resource Manager biedt een consistente beheerlaag voor Hallo taken die uit te via Azure PowerShell, Azure CLI, Azure-portal, REST-API en ontwikkelingsprogramma's voeren. Alle Hallo-hulpprogramma's gebruiken een gemeenschappelijke set van bewerkingen. U Hallo-hulpprogramma's die geschikt zijn voor u en kunnen ze gebruiken door elkaar zonder verwarring gebruiken. 

Hallo Hallo volgende afbeelding ziet u hoe alle Hallo hulpprogramma met communiceren dezelfde Azure Resource Manager-API. Hallo API aanvragen toohello Resource Manager-service, die worden geverifieerd en geautoriseerd Hallo aanvragen. Resource Manager stuurt vervolgens Hallo aanvragen toohello juiste resourceproviders.

![Resource Manager-aanvraagmodel](./media/resource-group-overview/consistent-management-layer.png)

## <a name="guidance"></a>Richtlijnen
Hallo kunnen volgende tips u profiteren van Resource Manager bij het werken met uw oplossingen.

1. Definieer en implementeer uw infrastructuur via Hallo declaratieve syntaxis in de Resource Manager-sjablonen in plaats van via imperatieve opdrachten.
2. Definieer alle implementatie- en configuratiestappen in Hallo-sjabloon. Handmatige stappen voor het installeren van uw oplossing zijn niet nodig.
3. Voer imperatieve opdrachten toomanage uw resources, zoals toostart of stoppen van een app of machine.
4. Breng resources met Hallo dezelfde levenscyclus in een resourcegroep. Gebruik tags voor het organiseren van alle andere resources.

Ga voor aanbevelingen over sjablonen naar [Aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](resource-manager-template-best-practices.md).

Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).

## <a name="resource-groups"></a>Resourcegroepen
Er zijn enkele tooconsider belangrijke factoren bij het definiëren van de resourcegroep:

1. Moeten alle Hallo resources in uw groep delen dezelfde levenscyclus Hallo. U implementeert ze samen, werkt ze samen bij en verwijdert ze samen. Als een resource, zoals een databaseserver tooexist op een andere implementatiecyclus moet moet zich bij een andere resourcegroep.
2. Elke resource kan in slechte één resourcegroep voorkomen.
3. U kunt toevoegen of verwijderen van een resourcegroep voor resource tooa op elk gewenst moment.
4. U kunt een resource verplaatsen van de ene groep tooanother. Zie voor meer informatie [verplaatsen van resources toonew resourcegroep of abonnement](resource-group-move-resources.md).
5. Een resourcegroep kan resources uit verschillende regio’s bevatten.
6. Een resourcegroep kan worden gebruikt tooscope toegangsbeheer voor beheertaken.
7. Een resource kan communiceren met resources in andere resourcegroepen. Deze interactie is gebruikelijk wanneer Hallo twee resources zijn gekoppeld, maar niet delen Hallo dezelfde levenscyclus (bijvoorbeeld WebApps die gebruikmaken van tooa database).

Bij het maken van een resourcegroep, moet u een locatie tooprovide voor die resourcegroep. U vraagt zich misschien af: 'Waarom heeft een resourcegroep een locatie nodig? En als Hallo resources verschillende locaties dan Hallo resourcegroep hebt kunnen, waarom maakt locatie voor resourcegroep Hallo uit op alle?' Hallo resourcegroep slaat metagegevens over Hallo resources. Daarom wanneer u een locatie voor resourcegroep Hallo opgeeft, geeft u aan waar de metagegevens worden opgeslagen. Om wettelijke redenen, moet u mogelijk tooensure die uw gegevens worden opgeslagen in een bepaald gebied.

## <a name="resource-providers"></a>Resourceproviders
Elke resourceprovider biedt een set resources en bewerkingen voor werken met een Azure-service. Bijvoorbeeld, als u wilt dat toostore sleutels en geheimen, werkt u met Hallo **Microsoft.KeyVault** resourceprovider. Deze resourceprovider biedt een resourcetype genaamd **kluizen** voor het maken van de sleutelkluis Hallo. 

Hallo-naam van een resourcetype heeft Hallo indeling: **{resourceprovider} / {resourcetype}**. Hallo sleutelkluis type is bijvoorbeeld **Microsoft.KeyVault/vaults**.

Voordat u aan de slag met het implementeren van uw resources, krijgt u inzicht hebben in Hallo beschikbare resourceproviders bekijken. Hallo-namen van de resource-providers en resources kunt u resources definiëren weten u toodeploy tooAzure. Bovendien moet u tooknow Hallo geldige locaties en API-versies voor elk resourcetype. Zie [Resourceproviders en -typen](resource-manager-supported-services.md) voor meer informatie.

## <a name="template-deployment"></a>Sjabloonimplementatie
Met Resource Manager kunt u een sjabloon (in JSON-indeling) die Hallo-infrastructuur en configuratie van uw Azure-oplossing bepaalt. Door het gebruik van een sjabloon kunt u gedurende de levenscyclus de oplossing herhaaldelijk implementeren en erop vertrouwen dat uw resources consistent worden geïmplementeerd. Wanneer u een oplossing vanuit de portal hello maakt, omvat Hallo oplossing automatisch een sjabloon voor de implementatie. U hebt geen toocreate uw sjabloon maken omdat u kunt met Hallo-sjabloon voor uw oplossing beginnen en pas deze toomeet uw specifieke behoeften. U kunt een sjabloon voor een bestaande resourcegroep ophalen door de huidige status van de resourcegroep Hallo Hallo exporteren of Hallo-sjabloon die wordt gebruikt voor een bepaalde implementatie weer te geven. Hallo weergeven [geëxporteerde sjabloon](resource-manager-export-template.md) is een handige manier toolearn over de sjabloonsyntaxis Hallo.

toolearn over Hallo-indeling van het Hallo-sjabloon en de manier waarop u samenstelt, Zie [maken van uw eerste Azure Resource Manager-sjabloon](resource-manager-create-first-template.md). tooview hello JSON-syntaxis voor de typen resources, Zie [resources in Azure Resource Manager-sjablonen definiëren](/azure/templates/).

Resource Manager Hallo sjabloon zoals een andere aanvraag verwerkt (Zie afbeelding Hallo voor [consistente beheerlaag](#consistent-management-layer)). Het Hallo-sjabloon parseert en converteert de syntaxis in REST-API-bewerkingen voor de juiste resourceproviders Hallo. Bijvoorbeeld, als Resource Manager krijgt een sjabloon Hello resourcedefinitie te volgen:

```json
"resources": [
  {
    "apiVersion": "2016-01-01",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "mystorageaccount",
    "location": "westus",
    "sku": {
      "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {
    }
  }
]
```

Hallo definitie toohello volgende REST-API-bewerking wordt verzonden toohello bronprovider Microsoft.Storage worden geconverteerd:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/mystorageaccount?api-version=2016-01-01
REQUEST BODY
{
  "location": "westus",
  "properties": {
  }
  "sku": {
    "name": "Standard_LRS"
  },   
  "kind": "Storage"
}
```

Hoe u sjablonen en -resourcegroepen definiëren zich volledig tooyou en hoe u wilt dat toomanage uw oplossing. U kunt bijvoorbeeld uw toepassing met drie lagen via één sjabloon tooa één resourcegroep implementeren.

![sjabloon met drie lagen](./media/resource-group-overview/3-tier-template.png)

Maar u hebt geen toodefine uw volledige infrastructuur in één sjabloon. Het is vaak uw vereisten voor de implementatie in een set van gerichte, doel-specifieke sjablonen zin toodivide. U kunt deze sjablonen eenvoudig opnieuw gebruiken voor verschillende oplossingen. een bepaalde oplossing toodeploy, dat u een basissjabloon gebruiken die is gekoppeld aan alle vereiste Hallo sjablonen maken. Hallo volgende afbeelding toont hoe toodeploy een oplossing met drie lagen via een sjabloon voor bovenliggend met drie geneste sjablonen.

![sjabloon met geneste lagen](./media/resource-group-overview/nested-tiers-template.png)

Als u voor ogen uw opslaglagen met afzonderlijke levenscycli hebt, kunt u uw drie lagen tooseparate-resourcegroepen kunt implementeren. Kennisgeving Hallo resources kunnen nog steeds gekoppelde tooresources in andere resourcegroepen.

![sjabloon met lagen](./media/resource-group-overview/tier-templates.png)

Zie [Patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md) (Patronen voor het ontwerpen van Azure Resource Manager-sjablonen) voor meer informatie over het ontwerpen van uw sjablonen. Zie [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md) (Gekoppelde sjablonen gebruiken met Azure Resource Manager) voor meer informatie over geneste sjablonen.

Azure Resource Manager analyseert afhankelijkheden tooensure resources in de juiste volgorde Hallo worden gemaakt. Als een resource afhankelijk is van een waarde uit een andere resource (zoals een virtuele machine die een opslagaccount nodig heeft voor schijven), stelt u een afhankelijkheid in. Zie voor meer informatie [Afhankelijkheden definiëren in Azure Resource Manager-sjablonen](resource-group-define-dependencies.md).

U kunt ook Hallo-sjabloon gebruiken voor updates toohello infrastructuur. U kunt bijvoorbeeld een resource tooyour oplossing toevoegen en configuratieregels toevoegen voor Hallo-resources die al zijn geïmplementeerd. Als Hallo-sjabloon maken van een bron, maar dat er bestaat al een resource, voert Azure Resource Manager een update in plaats van een nieuwe asset maken. Azure Resource Manager updates Hallo bestaande asset toohello dezelfde status zoals deze zou zijn als een nieuwe.  

Resource Manager biedt uitbreidingen voor scenario's als u aanvullende bewerkingen zoals het installeren van bepaalde software die niet is opgenomen in het Hallo-installatieprogramma nodig. Als u al een configuratiebeheerservice gebruikt, zoals DSC, Chef of Puppet, kunt u via uitbreidingen met deze service blijven werken. Zie voor meer informatie over de extensies van virtuele machines [Informatie over extensies en functies van virtuele machines](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Ten slotte uitmaakt Hallo-sjabloon deel van de broncode Hallo voor uw app. U kunt inchecken tooyour source code opslagplaats en deze bijwerken naarmate uw app zich verder ontwikkelt. U kunt de sjabloon Hallo met Visual Studio bewerken.

U bent klaar toodeploy Hallo resources tooAzure na het definiëren van uw sjabloon. Zie voor Hallo opdrachten toodeploy Hallo bronnen:

* [Resources implementeren met Resource Manager-sjablonen en Azure PowerShell](resource-group-template-deploy.md)
* [Resources implementeren met Resource Manager-sjablonen en Azure CLI](resource-group-template-deploy-cli.md)
* [Resources implementeren met Resource Manager-sjablonen en Azure Portal](resource-group-template-deploy-portal.md)
* [Resources implementeren met Resource Manager-sjablonen en Resource Manager REST API](resource-group-template-deploy-rest.md)

## <a name="tags"></a>Tags
Resource Manager biedt een tagfunctie waarmee u toocategorize bronnen op basis van tooyour vereisten voor het beheer of facturering. Labels gebruiken wanneer u een verzameling complexe resourcegroepen en resources hebben en moet toovisualize deze assets op Hallo handige manier Hallo meeste zin tooyou. U kunt bijvoorbeeld resources die een vergelijkbare rol vervullen in uw organisatie of toohello behoren labelen dezelfde afdeling. Zonder tags kunnen gebruikers in uw organisatie maken van kunnen meerdere resources die mogelijk moeilijk toolater identificeren en te beheren. Bijvoorbeeld, kunt u desgewenst toodelete alle Hallo bronnen voor een bepaald project. Als u deze resources zijn niet gelabeld voor Hallo-project, hebt u toomanually die ze vinden. Taggen kan een belangrijke manier tooreduce onnodige kosten in uw abonnement zijn. 

Resources hoeven niet tooreside in Hallo dezelfde resource groep tooshare een label. U kunt uw eigen code taxonomie tooensure dat alle gebruikers in uw organisatie gebruiken algemene labels in plaats van gebruikers die per ongeluk afwijkende tags (zoals 'Afd' in plaats van 'afdeling') toepassen maken.

Hallo volgende voorbeeld ziet u een label wordt toegepast tooa virtuele machine.

```json
"resources": [    
  {
    "type": "Microsoft.Compute/virtualMachines",
    "apiVersion": "2015-06-15",
    "name": "SimpleWindowsVM",
    "location": "[resourceGroup().location]",
    "tags": {
        "costCenter": "Finance"
    },
    ...
  }
]
```

tooretrieve alle Hallo resources met een tagwaarde gebruiken Hallo volgende PowerShell-cmdlet:

```powershell
Find-AzureRmResource -TagName costCenter -TagValue Finance
```

Of hello Azure CLI 2.0-opdracht te volgen:

```azurecli
az resource list --tag costCenter=Finance
```

U kunt ook met tags resources via hello Azure-portal bekijken.

Hallo [gebruiksrapport](../billing/billing-understand-your-bill.md) voor uw abonnement bevat labelnamen en waarden, waarmee u toobreak uit de kosten door tags. Zie voor meer informatie over tags [Using tags tooorganize uw Azure-resources](resource-group-using-tags.md).

## <a name="access-control"></a>Toegangsbeheer
Resource Manager kunt u toocontrol wie toegang tot toospecific acties voor uw organisatie heeft. Systeemeigen op rollen gebaseerde toegangsbeheer (RBAC) is geïntegreerd in het beheerplatform hello en geldt dat access control tooall-services in de resourcegroep. 

Er zijn twee belangrijkste concepten toounderstand bij het werken met toegangsbeheer op basis van rollen:

* Roldefinities: beschrijven een set machtigingen en kunnen worden gebruikt in meerdere toewijzingen.
* Roltoewijzingen: koppelen een definitie aan een identiteit (gebruiker of groep) voor een bepaald bereik (abonnement, resourcegroep of resource). Hallo-toewijzing wordt overgenomen door lagere scopes.

U kunt gebruikers toopre gedefinieerde platform en resourcespecifieke rollen toevoegen. U kunt bijvoorbeeld gebruikmaken van Hallo vooraf gedefinieerde rol met de naam lezer waarmee gebruikers tooview resources, maar niet wijzigen. U gebruikers in uw organisatie die dit type toegang toohello lezersrol toevoegen en Hallo rol toohello abonnement, resourcegroep of resource toe te passen.

Azure biedt Hallo vier platform rollen te volgen:

1. Eigenaar: kan alles beheren, inclusief toegang
2. Inzender: kan alles beheren behalve toegang
3. Lezer: kan alles weergeven, maar kan geen wijzigingen aanbrengen
4. Beheerder voor gebruikerstoegang - kunt gebruiker toegang tot tooAzure resources beheren

Azure biedt ook diverse resourcespecifieke rollen. Een aantal gangbare zijn:

1. Virtuele Machine Inzender - kunt virtuele machines beheren, maar niet verlenen toegang tot toothem en Hallo virtuele netwerk of opslag account toowhich ze zijn verbonden niet beheren
2. Network Contributor - alle netwerkbronnen beheren, maar niet verlenen toegang toothem
3. Storage-Account Inzender - storage-accounts beheren, maar niet verlenen toegang toothem
4. Inzender voor SQL Server: kan SQL-servers en -databases beheren, maar niet het beveiligingsbeleid
5. Website Inzender - websites beheren, maar niet Hallo web plannen toowhich ze zijn verbonden

Zie voor een volledige lijst met functies en de toegestane acties Hallo [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md). Zie voor meer informatie over op rollen gebaseerd toegangsbeheer [Op rollen gebaseerd Azure-toegangsbeheer](../active-directory/role-based-access-control-configure.md). 

In sommige gevallen die u wilt toorun code of het script dat toegang heeft tot resources, maar u niet wilt dat toorun in de referenties van een gebruiker. U wilt toocreate een identiteit van een service principal aangeroepen voor de toepassing hello en Hallo juiste rol voor service-principal Hallo toewijzen. Resource Manager kunt u referenties voor de toepassing hello toocreate en toepassing hello programmatisch te verifiëren. toolearn over het maken van service-principals, Zie een van de volgende onderwerpen:

* [Een service principal tooaccess-resources voor Azure PowerShell toocreate gebruiken](resource-group-authenticate-service-principal.md)
* [Een service principal tooaccess-resources voor Azure CLI toocreate gebruiken](resource-group-authenticate-service-principal-cli.md)
* [Gebruik portal toocreate Azure Active Directory-toepassing en service-principal die toegang bronnen tot](resource-group-create-service-principal-portal.md)

U kunt ook expliciet vergrendelen kritieke bronnen tooprevent gebruikers deze wijzigen of verwijderen. Zie voor meer informatie [Resources vergrendelen met Azure Resource Manager](resource-group-lock-resources.md).

## <a name="activity-logs"></a>Activiteitenlogboeken
Resource Manager registreert alle bewerkingen waarmee een resource wordt gemaakt, gewijzigd of verwijderd. U kunt gebruiken Hallo activiteit logboeken toofind een fout bij het oplossen van of toomonitor hoe een gebruiker in uw organisatie een resource gewijzigd. toosee hello Logboeken, selecteer **activiteitenlogboeken** in Hallo **instellingen** blade voor een resourcegroep. Hallo-Logboeken kunt u filteren op veel verschillende waarden, met inbegrip van welke gebruiker gestarte Hallo-bewerking. Zie voor meer informatie over het werken met Hallo activiteitenlogboeken [activiteit weergeven logboeken toomanage Azure resources](resource-group-audit.md).

## <a name="customized-policies"></a>Aangepast beleid
Resource Manager kunt u toocreate aangepast beleid voor het beheren van uw resources. Hallo typen beleidsregels die u kunnen diverse scenario's opnemen. U kunt een naamgevingsconventie voor resources afdwingen, u kunt beperken welke typen resources en resource-exemplaren kunnen worden geïmplementeerd of u kunt beperken welke regio's als host voor een bepaald type resource kunnen fungeren. U kunt een tagwaarde voor resources tooorganize facturering op afdelingsniveau vereisen. U maakt beleidsregels toohelp verlagen de kosten en consistentie in uw abonnement. 

U definieert beleid met JSON en past dat beleid vervolgens toe op uw abonnement of binnen een resourcegroep. Beleidsregels zijn anders dan de op rollen gebaseerde toegangsbeheer omdat ze toegepaste tooresource typen.

Hallo volgende voorbeeld ziet u een beleid dat zorgt voor consistentie van de code door te geven dat alle resources een tag costCenter bevatten.

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

Er zijn nog veel meer soorten beleid die u kunt maken. Zie voor meer informatie [beleid toomanage resources en toegang beheren](resource-manager-policy.md).

## <a name="sdks"></a>SDK's
Azure SDK's zijn beschikbaar voor meerdere talen en platforms. Elk van deze taalimplementaties is beschikbaar via zijn ecosystem package manager en GitHub.

Hier vindt u onze Open Source SDK-opslagplaatsen. We ontvangen graag uw feedback, vragen bij problemen en pull-aanvragen.

* [Azure-SDK voor .NET](https://github.com/Azure/azure-sdk-for-net)
* [Azure-beheerbibliotheken voor Java](https://github.com/Azure/azure-sdk-for-java)
* [Azure-SDK voor Node.js](https://github.com/Azure/azure-sdk-for-node)
* [Azure-SDK voor PHP](https://github.com/Azure/azure-sdk-for-php)
* [Azure-SDK voor Python](https://github.com/Azure/azure-sdk-for-python)
* [Azure-SDK voor Ruby](https://github.com/Azure/azure-sdk-for-ruby)

Zie voor informatie over het gebruik van deze talen met uw resources:

* [Azure voor .NET-ontwikkelaars](/dotnet/azure/?view=azure-dotnet)
* [Azure voor Java-ontwikkelaars](/java/azure/)
* [Azure voor Node.js-ontwikkelaars](/nodejs/azure/)
* [Azure voor Python-ontwikkelaars](/python/azure/)

> [!NOTE]
> Als Hallo SDK geen Hallo vereist functionaliteit biedt, kunt u ook toohello bellen [REST API van Azure](https://docs.microsoft.com/rest/api/resources/) rechtstreeks.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* Zie voor een eenvoudige introductie tooworking met sjablonen, [een Azure Resource Manager-sjabloon uit bestaande resources exporteren](resource-manager-export-template.md).
* Voor een uitgebreider overzicht van hoe u een sjabloon maakt, raadpleegt u [Uw eerste Azure Resource Manager-sjabloon maken](resource-manager-create-first-template.md).
* Zie toounderstand Hallo functies die u kunt gebruiken in een sjabloon [sjabloonfuncties](resource-group-template-functions.md)
* Zie voor meer informatie over het gebruik van Visual Studio met Resource Manager [Azure-resourcegroepen maken en implementeren met Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

Hier volgt een videodemonstratie van dit overzicht:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure-Documentation-Shorts/Azure-Resource-Manager-Overview/player]


[powershellref]: https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/azurerm.resources
