---
title: concepten van aaaDevTest Labs | Microsoft Docs
description: Leer de basisconcepten Hallo van DevTest Labs en hoe deze het eenvoudig toocreate zodat kan, beheren en bewaken van virtuele machines in Azure
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 105919e8-3617-4ce3-a29f-a289fa608fb2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: d9f1d948002c4d3121e5bdd4e65eb8b54cd91f9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="devtest-labs-concepts"></a>DevTest Labs-concepten
## <a name="overview"></a>Overzicht
Hallo volgende lijst bevat DevTest Labs hoofdconcepten en definities:

## <a name="labs"></a>Labs
Een lab is Hallo-infrastructuur die een groep resources omvat, zoals virtuele Machines (VM's), waarmee u betere die bronnen beheren door te geven limieten en quota's.

## <a name="virtual-machine"></a>Virtuele machine
Een Azure VM is een van de verschillende soorten [op aanvraag, schaalbare computerbronnen](https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm) die Azure biedt. Azure VM's kunt u de flexibiliteit van virtualisatie zonder toobuy Hallo en onderhouden Hallo fysieke hardware die wordt uitgevoerd, maar u nog steeds toomaintain moet Hallo VM door bepaalde taken uitvoeren, zoals het configureren, patchen en Hallo software installeren die op deze wordt uitgevoerd.

[Overzicht van Windows virtuele machines in Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-overview) biedt u informatie over wat u moet overwegen voordat u maakt een virtuele machine, hoe u het maken en beheren.

## <a name="claimable-vm"></a>Claimable VM
Een Azure Claimable VM is een virtuele machine die beschikbaar is voor gebruik door een lab-gebruiker met machtigingen. Een lab-beheerder kan virtuele machines voorbereiden met specifieke basisinstallatiekopieën en artefacten en sla ze tooa gedeelde groep. Een lab-gebruiker kan vervolgens een actieve virtuele machine uit de groep Hallo claim wanneer ze met die specifieke configuratie nodig.

Een virtuele machine die is claimable tooany bepaalde gebruiker in eerste instantie niet is toegewezen, maar wordt weergegeven in de lijst van elke gebruiker onder 'Claimable virtuele machines'. Nadat een virtuele machine wordt opgeëist door een gebruiker, is het verplaatst up tootheir area 'Mijn virtuele machines' en niet langer claimable door een andere gebruiker.

## <a name="environment"></a>Omgeving
Een omgeving verwijst in DevTest Labs tooa verzameling Azure-resources in een testomgeving. [Dit blogbericht](https://blogs.msdn.microsoft.com/devtestlab/2016/11/16/connect-2016-news-for-azure-devtest-labs-azure-resource-manager-template-based-environments-vm-auto-shutdown-and-more/) wordt beschreven hoe toocreate multi-VM omgevingen van uw Azure Resource Manager-sjablonen.

## <a name="base-images"></a>Basisinstallatiekopieën
Basisinstallatiekopieën VM-installatiekopieën met alle Hallo-hulpprogramma's en instellingen vooraf geïnstalleerd zijn en geconfigureerde tooquickly een virtuele machine maken. U kunt een virtuele machine inrichten door een bestaande base verzamelen en het toevoegen van een artefact tooinstall uw test-agent. U kunt vervolgens opslaan Hallo ingericht VM als een base zodat hello base kan worden gebruikt zonder dat u tooreinstall Hallo test agent voor elke inrichting van Hallo VM.

## <a name="artifacts"></a>Artefacten
Artefacten zijn gebruikte toodeploy en uw toepassing configureren nadat een virtuele machine is ingericht. Artefacten kunnen het volgende zijn:

* Hulpprogramma's die u tooinstall op Hallo VM, zoals agents, Fiddler en Visual Studio wilt.
* Acties die u wilt de toorun op Hallo VM, zoals het klonen van een opslagplaats.
* Toepassingen die u tootest wilt.

Artefacten zijn [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) JSON-bestanden die bevatten instructies tooperform implementatie en configuratie toepassen.

## <a name="artifact-repositories"></a>Artefact-opslagplaatsen
Artefact-opslagplaatsen zijn git-opslagplaatsen waar de artefacten in worden gecontroleerd. Artefact-opslagplaatsen kunnen toomultiple labs in uw organisatie voor het inschakelen van hergebruik en delen worden toegevoegd.

## <a name="formulas"></a>Formules
Formules in toevoeging toobase afbeeldingen bieden een mechanisme voor snelle VM-inrichting. Een formule in DevTest Labs is een lijst met standaard eigenschap waarden gebruikt toocreate een lab VM.
Met formules, virtuele machines met dezelfde van eigenschappen - zoals basisinstallatiekopie, VM-grootte, virtueel netwerk en artefacten set - Hallo kan worden gemaakt zonder toospecify die eigenschappen telkens. Wanneer u een virtuele machine maakt van een formule, Hallo standaardwaarden kunnen worden gebruikt als-is of gewijzigd.

## <a name="policies"></a>Beleidsregels
Beleidsregels helpen bij het beheren van kosten in uw testomgeving. U kunt bijvoorbeeld een beleid tooautomatically afgesloten VM's op basis van een ingesteld schema maken.

## <a name="caps"></a>Hoofdletters
Caps is een mechanisme toominimize afval in uw testomgeving. U kunt bijvoorbeeld instellen dat een cap toorestrict Hallo aantal virtuele machines die per gebruiker of in een testomgeving kunnen worden gemaakt.

## <a name="security-levels"></a>Beveiligingsniveaus
Toegang wordt bepaald door gebaseerd toegangsbeheer (RBAC). toounderstand access hoe werkt, het helpt toounderstand Hallo verschillen tussen een machtiging voor een rol en een bereik, zoals gedefinieerd door RBAC.

* Machtiging - een machtiging is een gedefinieerde toegang tooa specifieke actie (bijvoorbeeld leestoegang tooall virtuele machines).
* Functie - een rol is een reeks machtigingen die kunnen worden gegroepeerd en tooa gebruiker toegewezen. Bijvoorbeeld, Hallo *eigenaar abonnement* rol heeft toegang tot tooall bronnen binnen een abonnement.
* Scope - een scope is een niveau binnen de hiërarchie van een Azure-resource, zoals een resourcegroep, een enkel lab of het hele abonnement Hallo Hallo.

Binnen het bereik van de Hallo van DevTest Labs, er zijn twee typen rollen toodefine gebruikersmachtigingen: labeigenaar en lab-gebruiker.

* Labeigenaar - een labeigenaar heeft toegang tot tooany bronnen in Hallo lab. Daarom kunt de eigenaar van een testomgeving beleid wijzigen, lezen en schrijven van alle virtuele machines, Hallo virtueel netwerk wijzigen, enzovoort.
* Lab-gebruiker - lab-gebruiker kunt weergeven alle lab-resources, zoals virtuele machines, beleid en virtuele netwerken, maar niet wijzigen beleid of alle virtuele machines die zijn gemaakt door andere gebruikers.

toosee hoe toocreate aangepaste rollen in DevTest Labs verwijzen toohello artikel [gebruikersmachtigingen verlenen toospecific labbeleidsregels](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).

Aangezien scopes hiërarchische, wanneer een gebruiker machtigingen op een bepaalde scope heeft, krijgen ze automatisch deze machtigingen voor elke laag niveau scope die zijn opgenomen. Bijvoorbeeld, als een gebruiker is toegewezen toohello rol van eigenaar abonnement, hebben vervolgens ze toegang tot tooall bronnen in een abonnement, inclusief alle virtuele machines, alle virtuele netwerken en alle labs. De eigenaar van een abonnement neemt daarom automatisch Hallo-rol van de labeigenaar van het. Hallo tegengestelde is echter niet het geval. Een labeigenaar heeft toegang tooa lab, een lagere bereik dan Hallo-abonnement is. De eigenaar van een testomgeving worden daarom niet kunnen toosee virtuele machines of virtuele netwerken of alle bronnen die zich buiten het Hallo-testomgeving.

## <a name="azure-resource-manager-templates"></a>Azure Resource Manager-sjablonen
Alle concepten die worden beschreven in dit artikel kunnen worden geconfigureerd met behulp van Azure Resource Manager-sjablonen waarmee u Hallo Hallo infrastructuur of de configuratie van uw Azure-oplossing te definiëren en herhaaldelijk implementeren in een consistente status.

[Begrijpen Hallo structuur en syntaxis van Azure Resource Manager-sjablonen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates#template-format) Hallo structuur van een Azure Resource Manager-sjabloon en Hallo eigenschappen die beschikbaar zijn in verschillende secties van een sjabloon Hallo wordt beschreven.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Volgende stappen
[Een lab maken in DevTest Labs](devtest-lab-create-lab.md)
