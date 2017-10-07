---
title: aaaManaging Azure-resources met Cloud Explorer | Microsoft Docs
description: Meer informatie over hoe toouse Cloud Explorer toobrowse Azure resources vanuit Visual Studio en beheren.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a>Hallo-resources die zijn gekoppeld aan uw Azure-accounts in Visual Studio Cloud Explorer beheren
Cloud Explorer kunt u tooview uw Azure-resources en resourcegroepen inspecteren van de eigenschappen en acties van diagnostische gegevens vanuit Visual Studio belangrijke ontwikkelaar uitvoeren. 

Zoals Hallo [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is gebouwd op Hallo Azure Resource Manager-stack. Daarom Cloud Explorer begrijpt resources, zoals Azure-resourcegroepen en Azure-services zoals Logic apps en API apps en ondersteunt de [toegangsbeheer op basis van rollen](active-directory/role-based-access-control-configure.md) (RBAC). 

## <a name="prerequisites"></a>Vereisten
- [Visual Studio 2017](https://www.visualstudio.com/downloads/) Hello **Azure-workload** geselecteerd, of een eerdere versie van Visual Studio met Hallo [Microsoft Azure SDK voor .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).
- Microsoft Azure-account: als u geen account hebt, kunt u [aanmelden voor een gratis proefversie](http://go.microsoft.com/fwlink/?LinkId=623901) of [uw voordelen als Visual Studio-abonnee activeren](http://go.microsoft.com/fwlink/?LinkId=623901).

> [!NOTE]
> Selecteer tooview Cloud Explorer **weergave** > **Cloud Explorer** op de menubalk Hallo.   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a>Een Azure-account tooCloud Explorer toevoegen
tooview hello resources die zijn gekoppeld aan een Azure-account, moet u eerst Hallo account tooCloud Explorer toevoegen. 

1. In **Cloud Explorer**, selecteer **Azure Accountinstellingen**.

    ![Pictogram instellingen cloud Explorer Azure-account](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Selecteer **nieuwe account toevoegt**. 

    ![Koppeling voor cloud Explorer account toevoegen](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. Meld u bij de Azure-account waarvan u de gewenste bronnen toohello toobrowse. 

1. Zodra tooan Azure-account aangemeld, wordt Hallo-abonnementen die zijn gekoppeld aan dit account weergegeven. Selecteer de selectievakjes voor abonnementen van Hallo account u wilt toobrowse en selecteer vervolgens Hallo **toepassen**. 
 
    ![Cloud Explorer: Selecteer een Azure-abonnementen toodisplay](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. Na het selecteren van Hallo abonnementen waarvan u de gewenste bronnen weergegeven toobrowse, deze abonnementen en bronnen in Hallo Cloud Explorer.

    ![Cloud Explorer resource weergeven voor een Azure-account](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a>Een Azure-account verwijderen uit Cloud Explorer 

1. In **Cloud Explorer**, selecteer **Azure Accountinstellingen**.

    ![Pictogram instellingen cloud Explorer Azure-account](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Selecteer volgende toohello account u wilt dat tooremove, **verwijderen**.

    ![Pictogram instellingen cloud Explorer Azure-account](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a>Brontypen of resourcegroepen weergeven
tooview uw Azure-resources kunt u ofwel **brontypen** of **resourcegroepen** weergeven.

1. In **Cloud Explorer**, selecteer Hallo resource vervolgkeuzelijsten.

    ![Cloud Explorer dropdown tooselect Hallo gewenste bronnen lijstweergave](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. Selecteer in het contextmenu hello, Hallo gewenst weergave: 

    - **Brontypen** weergave - Hallo algemene gebruikt op Hallo [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), ziet u uw Azure-resources ingedeeld volgens hun type, zoals web-apps, storage-accounts en virtuele machines. 
    - **Resourcegroepen** view - categoriseert Azure-bronnen door hello Azure-resourcegroep waaraan ze gekoppeld zijn. Een resourcegroep is een bundel van Azure-resources, meestal worden gebruikt door een specifieke toepassing. Zie toolearn meer informatie over Azure-resourcegroepen [overzicht van Azure Resource Manager](./azure-resource-manager/resource-group-overview.md).

    Hallo volgende afbeelding toont een vergelijking van Hallo twee resourceweergaven:

    ![Cloud Explorer resource weergaven vergelijking](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a>Weergeven en bronnen in de Cloud Explorer navigeert
toonavigate tooan Azure-resource en de informatie in de Cloud Explorer bekijken, vouwt u het type of de bijbehorende brongroep Hallo-item en selecteer vervolgens Hallo resource. Wanneer u een resource selecteert, informatie wordt weergegeven in tabbladen Hallo twee - **acties** en **eigenschappen** - Hallo onderaan Cloud Explorer in. 

- **Acties** tabblad - lijsten Hallo acties u kunt uitvoeren in de Cloud Explorer voor de resource Hallo geselecteerd. U kunt ook weergeven deze opties met de rechtermuisknop op Hallo resource tooview het contextmenu.

- **Eigenschappen** tabblad - toont Hallo eigenschappen van Hallo resource, zoals de type Landinstellingen en resource-groep waaraan deze gekoppeld is.

Hallo toont volgende afbeelding een voorbeeld van de vergelijking van wat u op elk tabblad voor een App Service ziet:

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

Elke resource heeft Hallo actie **openen in de portal**. Als u deze actie kiest, Cloud Explorer Hallo geselecteerd resource weergegeven in Hallo [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040). Hallo **openen in de portal** functie is handig voor toodeeply genest resources navigeren.

Aanvullende acties en eigenschapswaarden mogelijk ook weergegeven op basis van hello Azure-resource. Web-apps en logic apps ook bijvoorbeeld Hallo acties **openen in browser** en **foutopsporingsprogramma koppelen** bovendien te**openen in de portal**. Acties tooopen editors worden weergegeven wanneer u een account-opslag-blob, wachtrij of tabel. Apps van Azure hebben **URL** en **Status** eigenschappen, terwijl de opslagbronnen eigenschappen van sleutel en verbinding-tekenreeks zijn.

## <a name="find-resources-in-cloud-explorer"></a>Resources zoeken in de Cloud Explorer
toolocate resources met een specifieke naam in uw Azure-account-abonnementen, voer de naam van de Hallo in Hallo **Search** vak in Cloud Explorer.

![Resources zoeken in de Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

Als u tekens in Hallo **Search** vak alleen bronnen die overeenkomen met die tekens worden weergegeven in Hallo resourcestructuur.
