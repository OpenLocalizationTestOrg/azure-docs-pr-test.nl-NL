---
title: "aaaAccessing Azure privéclouds met Visual Studio | Microsoft Docs"
description: "Meer informatie over hoe tooaccess privécloud resources met behulp van Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: kraigb
ms.openlocfilehash: 5cfd6439afdcf98c6f7d7f29ab6c4256ed02533a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a>Toegang tot persoonlijke Azure-clouds met Visual Studio
Visual Studio ondersteunt standaard openbare Azure-cloud REST-eindpunten. In dit onderwerp leert u hoe toouse uw privécloud de tooaccess certificaat - en communiceren met - Hallo privécloud vanuit Visual Studio.

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a>tooaccess een persoonlijke Azure-cloud in Visual Studio
1. In Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885) download het bestand met publicatie-instellingen voor Hallo privécloud, of neem contact op met uw beheerder voor een bestand met publicatie-instellingen. Hallo op Hallo openbare-versie van Azure koppeling toodownload dit [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/). (het gedownloade bestand Hallo moet een extensie van `.publishsettings`)

1. Open Visual Studio

1. In **Server Explorer**, klik met de rechtermuisknop Hallo **Azure** knooppunt en selecteer in het contextmenu hello, **beheren en Filter abonnementen**.
   
    ![Opdracht voor abonnementen beheren](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. In Hallo **Microsoft Azure-abonnementen beheren** dialoogvenster, selecteer Hallo **certificaten** tabblad en selecteer vervolgens **importeren**.
   
    ![Azure certificaten importeren](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. In Hallo **importeren Microsoft Azure-abonnementen** dialoogvenster Selecteer **Bladeren**.

    ![Knop op Hallo importeren Microsoft Azure-abonnementen dialoogvenster Bladeren](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. In Hallo **Open** dialoogvenster Bladeren toohello map waar u opgeslagen Hallo publish-settings-bestand, selecteer Hallo bestand en selecteer vervolgens **Open**.

    ![Hallo publiceren instellingenbestand selecteren](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. Wanneer geretourneerd toohello **importeren Microsoft Azure-abonnementen** dialoogvenster Selecteer **importeren**.

    ![Hallo publiceren-settings-bestand importeren](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    Hallo-certificaten van Hallo publiceren instellingenbestand in Visual Studio worden ingevoerd en u kunt nu werken met de resources van uw privécloud.
   
## <a name="next-steps"></a>Volgende stappen
- [Publishing tooan Azure Cloud Service vanuit Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- [How to: downloaden en importeren van instellingen en abonnementsgegevens publiceren](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)
