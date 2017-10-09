---
title: een Azure-cloud service-project met Visual Studio aaaConfigure | Microsoft Docs
description: Meer informatie over hoe tooconfigure een Azure cloud service-project in Visual Studio, afhankelijk van uw vereisten voor dat project.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a>Een Azure-cloud service-project met Visual Studio configureren
U kunt een Azure-cloud service-project, afhankelijk van uw vereisten voor dat project configureren. U kunt eigenschappen instellen voor Hallo-project voor Hallo volgende categorieën:

- **Publiceren van een cloud service tooAzure** -u kunt instellen dat een eigenschap toomake of dat een bestaande cloud service geïmplementeerd tooAzure niet per ongeluk is verwijderd.
- **Uitvoeren of fouten opsporen in een cloudservice op de lokale computer Hallo** -kunt u een service configuration toouse selecteren en aangeven of u wilt dat toostart hello Azure-opslagemulator.
- **Valideren van een pakket met cloud-service wanneer deze wordt gemaakt** -u kunt ervoor kiezen eventuele waarschuwingen als fouten zodat u kunt ervoor zorgen dat Hallo cloud service-pakket wordt geïmplementeerd zonder problemen tootreat. 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a>Stappen tooconfigure een Azure-cloud service-project
1. Open of maak een cloudserviceproject in Visual Studio

1. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer in het contextmenu hello, **eigenschappen**.
   
1. Selecteer in de pagina eigenschappen van het project Hallo Hallo **ontwikkeling** tabblad.

    ![Menu Project-eigenschappen](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. Stel **vragen voor het verwijderen van een bestaande implementatie** te**True**. Deze instelling helpt tooensure u per ongeluk een bestaande implementatie in Azure niet verwijderen

1. Selecteer Hallo gewenst **serviceconfiguratie** tooindicate welke serviceconfiguratie toouse gewenste tijdens het uitvoeren of fouten opsporen in uw cloudservice lokaal. Voor meer informatie over het toomodify een serviceconfiguratie voor een rol, Zie [hoe tooconfigure Hallo rollen voor een Azure cloud service met Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).

1. Stel **Start Azure-opslagemulator** te**True** toostart hello Azure-opslagemulator tijdens het uitvoeren of fouten opsporen in uw cloudservice lokaal.

1. Stel **waarschuwingen als fouten behandelen** te**True** toomake zeker dat u als er validatiefouten pakket niet publiceren.

1. Stel **web project poorten** te**True** toomake ervoor wordt gezorgd dat uw Webrol Hallo dezelfde elke poort keer dat er begint lokaal in IIS Express.

1. Selecteer in de werkbalk van de Visual Studio hello, **opslaan**.

## <a name="next-steps"></a>Volgende stappen
- [Een Azure-project met behulp van serviceconfiguraties met meerdere configureren](vs-azure-tools-multiple-services-project-configurations.md)

