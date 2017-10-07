---
title: aaaUse Azure DevTest Labs voor training | Microsoft Docs
description: Meer informatie over hoe Azure DevTest Labs toouse voor training scenario's.
services: devtest-lab,virtual-machines
documentationcenter: na
author: steved0x
manager: douge
editor: 
ms.assetid: 57ff4e30-7e33-453f-9867-e19b3fdb9fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2016
ms.author: sdanie
ms.openlocfilehash: 4a5f44a282d8f6a58849c730ff89237ccff39ca8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-training"></a>Azure DevTest Labs gebruiken voor training
Azure DevTest Labs gebruikte tooimplement in toevoeging toodev en testen van veel belangrijke scenario's kan worden. Een van de scenario's is tooset van een testomgeving voor training. Kunt u in Azure DevTest Labs toocreate een testomgeving waarin u aangepaste sjablonen kunt opgeven dat elke leerling toocreate identiek en geïsoleerde omgeving voor training gebruiken kunt. U kunt beleidsregels tooensure dat training omgevingen beschikbaar tooeach leerling alleen zijn wanneer ze deze nodig en voldoende resources - zoals virtuele machines - vereist voor Hallo training bevatten toepassen. Ten slotte kunt u eenvoudig hello lab delen met stagiairs die ze in één klik kunnen openen.

![DevTest Labs gebruiken voor training](./media/devtest-lab-training-lab/devtest-lab-training.png)

Azure DevTest Labs voldoet aan Hallo volgens de vereisten die vereist tooconduct training in een virtuele omgeving zijn: 

* Stagiairs zien virtuele machines die zijn gemaakt door andere stagiairs niet
* Elke machine training moet identiek zijn
* Stagiairs kunnen hun omgeving training snel inrichten
* Kosten beheren door ervoor te zorgen dat stagiairs kunnen niet worden gebruikt voor het ophalen van meer virtuele machines dan ze nodig hebben om Hallo trainings- en ook virtuele machines afsluiten wanneer ze niet gebruiken
* Hallo training lab eenvoudig delen met elke leerling
* Hallo training lab opnieuw gebruiken

In dit artikel hebt u meer informatie over diverse Azure DevTest Labs-functies die kunnen worden gebruikt toomeet Hallo eerder is beschreven training vereisten en gedetailleerde stappen dat u tooset van een testomgeving voor training kan volgen.  

## <a name="implementing-training-with-azure-devtest-labs"></a>Training met Azure DevTest Labs implementeren
1. **Hallo lab maken** 
   
    Labs zijn Hallo beginpunt in Azure DevTest Labs. Wanneer u een testomgeving maakt, kunt u die zoals zoals het toevoegen van gebruikers (stagiairs) toohello lab, set beleidsregels toocontrol kosten Definieer VM-installatiekopieën die snel kunnen maken, en andere taken kunt uitvoeren.   
   
    Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:
   
   | Taak | Wat u leert |
   | --- | --- |
   | [Een lab maken in Azure DevTest Labs](devtest-lab-create-lab.md) |Meer informatie over hoe toocreate een lab in Azure DevTest Labs in hello Azure-portal. |
2. **Training virtuele machines in minuten met behulp van vooraf gedefinieerde marketplace-installatiekopieën en aangepaste installatiekopieën maken** 
   
    U kunt vooraf gedefinieerde installatiekopieën van een groot aantal afbeeldingen kiezen in hello Azure Marketplace en beschikbaar maken voor Hallo stagiairs in Hallo-testomgeving. Als Hallo kant-en-afbeeldingen niet aan uw vereisten voldoet, kunt u een aangepaste installatiekopie maken door het maken van een testomgeving met de installatiekopie van een vooraf gedefinieerde uit Azure Marketplace, alle Hallo software installeren die u nodig hebt voor Hallo training en Hallo VM op te slaan als aangepaste installatiekopie in de testomgeving Hallo VM. 
   
    Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:
   
   | Taak | Wat u leert |
   | --- | --- |
   | [Azure Marketplace-installatiekopieën configureren](devtest-lab-configure-marketplace-images.md) |Meer informatie over hoe u kunt de Azure Marketplace-installatiekopieën geaccepteerde; beschikbaar voor selectie alleen Hallo afbeeldingen maken die u wilt voor Hallo training. |
   | [Een aangepaste installatiekopie maken](devtest-lab-create-template.md) |Maak een aangepaste installatiekopie vooraf Hallo door software te installeren u voor Hallo training moet zodat stagiairs kunnen snel een virtuele machine maken met de aangepaste installatiekopie Hallo. |
3. **Herbruikbare sjablonen maken voor training machines** 
   
    Een formule in Azure DevTest Labs is dat een lijst met standaardwaarden voor de eigenschap toocreate een virtuele machine gebruikt. U kunt een formule in Hallo lab maken door het verzamelen van een installatiekopie van een VM-grootte (een combinatie van CPU en RAM) en een virtueel netwerk. Elke leerling kan zien Hallo formule in Hallo lab en toocreate een virtuele machine worden gebruikt. 
   
    Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:
   
   | Taak | Wat u leert |
   | --- | --- |
   | [DevTest Labs formules toocreate VM's beheren](devtest-lab-manage-formulas.md) |Meer informatie over hoe u een formule kunt maken met een installatiekopie van een VM-grootte (combinatie van CPU en RAM) en een virtueel netwerk ophalen. |
4. **Beheer van kosten**
   
    Azure DevTest Labs kunt u tooset een beleid Hallo lab toospecify Hallo maximum aantal VM's die kunnen worden gemaakt door de toetsen in Hallo-testomgeving. 
   
    Als u bent bezig met Meerdaags training en toostop wilt dat alle Hallo-virtuele machines op een bepaald tijdstip Hallo en vervolgens automatisch opnieuw opgestart ze Hallo na dag, kunt u eenvoudig bereiken die door de instelling automatisch afsluiten en -beleid in Hallo lab automatisch starten. 
   
    Ten slotte is het zo dat als training voltooid is u alle Hallo VM's in één keer kunt verwijderen door het uitvoeren van een enkel PowerShell-script. 
   
    Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:
   
   | Taak | Wat u leert |
   | --- | --- |
   | [Beleid voor lab maken](devtest-lab-set-lab-policy.md) |Kosten door het instellen van beleidsregels in Hallo lab te controleren. |
   | [Verwijder alle Hallo lab virtuele machines met een PowerShell-script](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Verwijder alle Hallo labs in één bewerking als Hallo training voltooid is. |
5. **Hallo lab delen met elke leerling**
   
    Labs zijn rechtstreeks toegankelijk via een koppeling die u met uw stagiairs deelt. Uw stagiairs niet zelfs toohave Azure-account hebt, zolang ze beschikken over een [Microsoft-account](devtest-lab-faq.md#what-is-a-microsoft-account). Stagiairs zichtbaar niet voor virtuele machines die zijn gemaakt door andere stagiairs.  
   
    Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:
   
   | Taak | Wat u leert |
   | --- | --- |
   | [Een leerling tooa lab toevoegen in Azure DevTest Labs](devtest-lab-add-devtest-user.md) |Gebruik hello Azure portal tooadd stagiairs tooyour training lab. |
   | [Stagiairs toohello testomgeving met een PowerShell-script toevoegen](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |Gebruik PowerShell tooautomate stagiairs tooyour training lab toe te voegen. |
   | [Een koppeling toohello lab ophalen](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |Meer informatie over hoe een lab rechtstreeks toegankelijk zijn via een hyperlink. |
6. **Hallo lab opnieuw gebruiken** 
   
    U kunt maken van de testomgeving, met inbegrip van aangepaste instellingen door te maken van een Resource Manager-sjabloon en het toocreate identiek labs opnieuw kunt automatiseren. 
   
    Meer informatie door te klikken op koppelingen in de volgende tabel Hallo Hallo:
   
   | Taak | Wat u leert |
   | --- | --- |
   | [Een lab met een Resource Manager-sjabloon maken](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Labs in Azure DevTest Labs met Resource Manager-sjablonen maken. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

