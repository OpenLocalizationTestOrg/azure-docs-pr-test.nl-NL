---
title: een Azure-cloud service-project met Visual Studio aaaCreating | Microsoft Docs
description: Meer informatie over toocreate nu een Azure-cloud service-project met Visual Studio
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a>Een Azure-cloud service-project maken met Visual Studio
Hello Azure-Tools voor Visual Studio biedt een projectsjabloon waarmee u een Azure-cloudservice maken. Zodra het Hallo-project is gemaakt, Visual Studio kunt u tooconfigure, fouten opsporen en Hallo cloud service tooAzure implementeren.

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a>Stappen toocreate een Azure-cloud service-project in Visual Studio
Deze sectie helpt u bij het maken van een Azure-cloud service-project in Visual Studio met een of meer webrollen.  

1. Start Visual Studio als beheerder.

1. Selecteer in het hoofdmenu hello, **bestand** > **nieuw** > **Project**.

1. Selecteer **Cloud** van Hallo Visual C# of Visual Basic project knooppunten van de sjabloon en selecteer **Azure Cloud Service** uit Hallo lijst met sjablonen.

    ![Nieuwe Azure-cloud-service](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. Geef op welke versie van .NET Framework gewenste toouse toodevelop uw project Hallo.

1. Voer een naam en locatie voor uw project en een naam voor het Hallo-oplossing. 

1. Selecteer **OK**.

1. In Hallo **nieuwe Microsoft Azure Cloud Service** dialoogvenster, selecteer Hallo rollen die u tooadd wilt en kies Hallo pijl naar rechts knop tooadd ze tooyour oplossing.

    ![Selecteer de nieuwe Azure-cloud service-rollen](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. toorename een rol die u hebt toegevoegd, aanwijzen op Hallo-rol in Hallo **nieuwe Microsoft Azure Cloud Service** dialoogvenster, en selecteer in het contextmenu hello, **naam**. U kunt ook een rol wijzigen binnen uw oplossing (in Hallo **Solution Explorer**) nadat deze is toegevoegd.

    ![Wijzig de naam van de rol van de Azure-cloud-service](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

Hello Azure met Visual Studio-project bevat koppelingen toohello rol projecten Hallo-oplossing. Hallo-project bevat ook Hallo *servicedefinitiebestand* en *serviceconfiguratiebestand*:

- **Servicedefinitiebestand** -Hallo runtime-instellingen voor uw toepassing, met inbegrip van welke rollen zijn vereist, de eindpunten en de grootte van de virtuele machine worden gedefinieerd. 
- **Serviceconfiguratiebestand** -hoeveel exemplaren van een rol worden uitgevoerd en Hallo waarden van het Hallo-instellingen die zijn gedefinieerd voor een functie configureert. 

Zie voor meer informatie over deze bestanden [Hallo rollen configureert voor een Azure-cloudservice met Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).

## <a name="next-steps"></a>Volgende stappen
- [Het beheren van rollen in Azure cloudserviceprojecten met Visual Studio](./vs-azure-tools-cloud-service-project-managing-roles.md)
