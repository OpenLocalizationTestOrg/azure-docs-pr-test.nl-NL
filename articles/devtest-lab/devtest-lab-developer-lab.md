---
title: aaaUse Azure DevTest Labs voor ontwikkelaars | Microsoft Docs
description: Meer informatie over hoe Azure DevTest Labs toouse voor scenario's voor ontwikkelaars.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 22e070e5-3d1a-49fe-9d4c-5e07cb0b7fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: tarcher
ms.openlocfilehash: 16a3ef47c9fcbca3050dd50db5b472a9a1e3c62c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a>Gebruik Azure DevTest Labs voor ontwikkelaars
Azure DevTest Labs kunnen worden gebruikt tooimplement veel belangrijke scenario's, maar een van de primaire Hallo-scenario's omvat het gebruik van DevTest Labs toohost ontwikkeling machines voor ontwikkelaars. In dit scenario biedt DevTest Labs de volgende voordelen:

- Ontwikkelaars kunnen hun computers ontwikkeling op aanvraag snel inrichten.
- Ontwikkelaars kunnen hun computers ontwikkeling als dat nodig is gemakkelijk aanpassen.
- Beheerders kunnen kosten beheren door ervoor te zorgen dat:
  - Ontwikkelaars kunnen niet meer virtuele machines dan ze nodig hebben voor de ontwikkeling van ophalen.
  - Virtuele machines worden afgesloten wanneer deze niet in gebruik. 

![DevTest Labs gebruiken voor training](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

In dit artikel leert u verschillende functies van Azure DevTest Labs die kunnen worden gebruikt toomeet developer-vereisten en Hallo gedetailleerde stappen dat u tooset van een testomgeving kunt volgen.

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a>Implementatie van ontwikkelaars omgevingen met Azure DevTest Labs
1. **Hallo lab maken** 
   
    Labs zijn Hallo beginpunt in Azure DevTest Labs. Wanneer u een testomgeving maakt, kunt u taken zoals het toevoegen van gebruikers (ontwikkelaars) toohello lab, instelling beleid toocontrol kosten, het definiëren van de VM-installatiekopieën die snel kunnen maken en meer uitvoeren.  
   
    Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:
   
   | Taak | Wat u leert |
   | --- | --- |
   | [Een lab maken in Azure DevTest Labs](devtest-lab-create-lab.md) |Meer informatie over hoe toocreate een lab in Azure DevTest Labs in hello Azure-portal. |
2. **Virtuele machines in minuten met behulp van vooraf gedefinieerde marketplace-installatiekopieën en aangepaste installatiekopieën maken** 
   
    U kunt vooraf gedefinieerde installatiekopieën van een groot aantal afbeeldingen kiezen in hello Azure Marketplace en zodat ze beschikbaar zijn in de testomgeving Hallo. Als Hallo kant-en-afbeeldingen niet aan uw vereisten voldoet, kunt u een aangepaste installatiekopie maken door het maken van een testomgeving met de installatiekopie van een vooraf gedefinieerde vanuit Azure Marketplace, alle Hallo software installeren die u nodig hebt, en opslaan Hallo VM als een aangepaste installatiekopie in de testomgeving Hallo VM.

    Als u aangepaste installatiekopieën gebruikt, overweeg het gebruik van een installatiekopie factory toocreate en distribueren van uw afbeeldingen. De fabrieksinstellingen van een installatiekopie is een configuratie als code-oplossing die regelmatig bouwt en uw geconfigureerde installatiekopieën automatisch distribueert. Dit bespaart Hallo tijd die nodig is toomanually Hallo system configureren nadat een virtuele machine is gemaakt met de Hallo OS baseren.
  
    Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:
   
   | Taak | Wat u leert |
   | --- | --- |
   | [Azure Marketplace-installatiekopieën configureren](devtest-lab-configure-marketplace-images.md) |Meer informatie over hoe u kunt geaccepteerde Azure Marketplace-installatiekopieën, beschikbaar voor selectie alleen Hallo afbeeldingen die u voor Hallo ontwikkelaars maken.|
   | [Een aangepaste installatiekopie maken](devtest-lab-create-template.md) |Maak een aangepaste installatiekopie vooraf Hallo door software te installeren u moet zodat ontwikkelaars snel een virtuele machine met behulp van de aangepaste installatiekopie Hallo kunnen maken.|
   | [Meer informatie over de installatiekopie-factory](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |Bekijk een video waarin wordt beschreven hoe tooset boven en een installatiekopie factory gebruiken.|

3. **Herbruikbare sjablonen maken voor ontwikkelaars machines** 
   
    Een formule in Azure DevTest Labs is dat een lijst met standaardwaarden voor de eigenschap toocreate een virtuele machine gebruikt. U kunt een formule in Hallo lab maken door het verzamelen van een installatiekopie van een VM-grootte (een combinatie van CPU en RAM) en een virtueel netwerk. Elke ontwikkelaar kan zien Hallo formule in Hallo lab en toocreate een virtuele machine worden gebruikt. 
   
    Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:
   
   | Taak | Wat u leert |
   | --- | --- |
   | [DevTest Labs formules toocreate VM's beheren](devtest-lab-manage-formulas.md) |Meer informatie over hoe u een formule kunt maken met een installatiekopie van een VM-grootte (combinatie van CPU en RAM) en een virtueel netwerk ophalen.|

4. **Artefacten tooenable flexibele VM aanpassing maken**

   Artefacten zijn gebruikte toodeploy en uw toepassing configureren nadat een virtuele machine is ingericht. Artefacten kunnen het volgende zijn:

   - Hulpprogramma's die u tooinstall op Hallo VM, zoals agents, Fiddler en Visual Studio wilt.
   - Acties die u wilt de toorun op Hallo VM, zoals het klonen van een opslagplaats.
   - Toepassingen die u tootest wilt.

   Veel artefacten zijn al beschikbaar out-of-the-box. U kunt uw eigen aangepaste artefacten maken als u wilt dat meer aanpassen voor uw specifieke behoeften.

   Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:
   
   | Taak | Wat u leert |
   | --- | --- |
   | [Aangepaste artefacten maken voor uw DevTest Labs VM](devtest-lab-artifact-author.md) |Maak uw eigen aangepaste artefacten voor Hallo virtuele machines in uw testomgeving.|
   | [Voeg een Git-opslagplaats toostore aangepaste artefacten en Azure Resource Manager-sjablonen voor gebruik in Azure DevTest Labs](devtest-lab-add-artifact-repo.md) |Meer informatie over hoe toostore uw aangepaste artefacten in uw eigen persoonlijke Git-opslagplaats.|

5. **Beheer van kosten**
   
    Azure DevTest Labs kunt u tooset een beleid Hallo lab toospecify Hallo maximum aantal VM's die kunnen worden gemaakt door een ontwikkelaar in Hallo-testomgeving. 
   
    Als uw developer-team heeft een set werkschema en u wilt dat toostop alle Hallo virtuele machines op een bepaald tijdstip Hallo en vervolgens automatisch opnieuw opgestart ze Hallo na dag, kunt u die gemakkelijk door instelling automatisch afsluiten en automatisch starten van beleid in Hallo lab uitvoeren. 
   
    Ten slotte, als ontwikkeling van apps voltooid is, kunt u verwijderen alle Hallo VM's in één keer een één PowerShell-script uit te voeren. 
   
    Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:
   
   | Taak | Wat u leert |
   | --- | --- |
   | [Beleid voor lab maken](devtest-lab-set-lab-policy.md) |Kosten door het instellen van beleidsregels in Hallo lab te controleren. |
   | [Verwijder alle Hallo lab virtuele machines met een PowerShell-script](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Verwijder alle Hallo labs in één bewerking als ontwikkeling voltooid is.|

1. **Toevoegen van een virtueel netwerk tooa VM** 
   
    DevTest Labs maakt een nieuw virtueel netwerk (VNET) als een lab is gemaakt. Als u uw eigen VNET hebt geconfigureerd: bijvoorbeeld via ExpressRoute of site-naar-site VPN-kunt u instellingen voor dit VNET tooyour lab virtuele netwerk kunt toevoegen, zodat deze beschikbaar is bij het maken van virtuele machines.

    Daarnaast is er een beschikbaar die wordt lid van een VM tooa domein wanneer Hallo VM wordt gemaakt van Azure Active Directory domain join artefact. 
   
    Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:
   
   | Taak | Wat u leert |
   | --- | --- |
   | [Een virtueel netwerk configureren in Azure DevTest Labs](devtest-lab-configure-vnet.md) |Meer informatie over hoe een virtueel netwerk in Azure DevTest Labs met behulp van tooconfigure hello Azure-portal.|

6. **Hallo lab delen met elke ontwikkelaar**
   
    Labs zijn rechtstreeks toegankelijk via een koppeling die u met uw ontwikkelaars deelt. Ze niet zelfs toohave Azure-account hebt, zolang ze beschikken over een [Microsoft-account](devtest-lab-faq.md#what-is-a-microsoft-account). Ontwikkelaars zichtbaar niet voor virtuele machines die zijn gemaakt door andere ontwikkelaars.  
   
    Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:
   
   | Taak | Wat u leert |
   | --- | --- |
   | [Een ontwikkelaar tooa lab toevoegen in Azure DevTest Labs](devtest-lab-add-devtest-user.md) |Gebruik hello Azure portal tooadd ontwikkelaars tooyour lab.|
   | [Ontwikkelaars toohello testomgeving met een PowerShell-script toevoegen](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |Gebruik PowerShell tooautomate ontwikkelaars tooyour lab toe te voegen. |
   | [Een koppeling toohello lab ophalen](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |Meer informatie over hoe ontwikkelaars rechtstreeks toegang tot een lab via een hyperlink.|

7. **Lab maken voor meer teams automatiseren** 
   
    U kunt maken van de testomgeving, met inbegrip van aangepaste instellingen door te maken van een Resource Manager-sjabloon en het toocreate identiek labs opnieuw kunt automatiseren. 
   
    Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:
   
   | Taak | Wat u leert |
   | --- | --- |
   | [Een lab met een Resource Manager-sjabloon maken](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Labs in Azure DevTest Labs met Resource Manager-sjablonen maken. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

