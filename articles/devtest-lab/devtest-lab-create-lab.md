---
title: aaaCreate een lab in Azure DevTest Labs | Microsoft Docs
description: Een lab voor virtuele machines maken in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a>Een lab maken in Azure DevTest Labs
Een lab in Azure DevTest Labs is Hallo-infrastructuur die een groep resources omvat, zoals virtuele Machines (VM's), waarmee u betere die bronnen beheren door te geven limieten en quota's. In dit artikel begeleidt u bij Hallo-proces voor het maken van een testomgeving met hello Azure-portal.

## <a name="prerequisites"></a>Vereisten
een lab toocreate, moet u de:

* Een Azure-abonnement. Zie toolearn over Azure-Aankoopopties [hoe toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) of [gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/). U moet eigenaar van de Hallo Hallo abonnement toocreate Hallo Lab.

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a>Stappen toocreate een lab in Azure DevTest Labs
Hallo stappen laten zien hoe toouse hello Azure portal toocreate een lab in Azure DevTest Labs. 

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecteer in het hoofdmenu Hallo aan de linkerkant Hallo **meer Services** (onderaan Hallo Hallo lijst).

    ![Menuoptie Meer services](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. Uit de lijst met beschikbare services Hallo **DevTest Labs**.
1. Op Hallo **DevTest Labs** blade Selecteer **toevoegen**.
   
    ![Een lab toevoegen](./media/devtest-lab-create-lab/add-lab-button.png)

1. Op Hallo **een DevTest Lab maken** blade:
   
    1. Voer een **Labnaam** voor Hallo nieuwe lab.
    2. Selecteer Hallo **abonnement** tooassociate met Hallo lab.
    3. Selecteer een **locatie** in welke toostore Hallo-testomgeving.
    4. Selecteer **automatisch afsluiten** toospecify als u wilt dat tooenable - en Hallo parameters definiëren voor - Hallo automatisch afsluiten van alle Hallo lab van virtuele machines. Hallo automatisch afsluiten functie is vooral een kostenbesparende waarbij u kunt opgeven wanneer het gewenste VM Hallo tooautomatically worden afgesloten. U kunt instellingen voor automatisch afsluiten wijzigen na het maken van Hallo lab Hallo stappen die worden beschreven in artikel Hallo [beheren van alle beleidsregels voor een testomgeving in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).
    5. Selecteer **pincode tooDashboard** als u wilt dat een snelkoppeling van Hallo lab tooappear op Hallo-portaldashboard.
    6. Selecteer **automatiseringsopties** tooget Azure Resource Manager-sjablonen voor het automatiseren van de configuratie. 
    7. Selecteer **Maken**. Na het selecteren van **maken**, Hallo **DevTest Labs** blade wordt weergegeven. U kunt de status Hallo van proces voor het maken van lab Hallo bewaken door bekijkt hello **meldingen** gebied. Als voltooid, vernieuwen Hallo pagina toosee Hallo nieuw lab gemaakt in de lijst Hallo van labs.  
    
    ![Een labblade maken](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Volgende stappen
Als u uw lab hebt gemaakt, vindt hier u enkele tooconsider met volgende stappen:

* [Veilige toegang tooa lab](devtest-lab-add-devtest-user.md).
* [Labbeleidsregels instellen](devtest-lab-set-lab-policy.md).
* [Een labsjabloon maken](devtest-lab-create-template.md).
* [Aangepaste artefacten maken voor uw virtuele machines](devtest-lab-artifact-author.md).
* [Toevoegen van een VM met artefacten tooa lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).

