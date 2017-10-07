---
title: aaaHow toomanage service en -profielen | Microsoft Docs
description: Meer informatie over hoe toowork met de service en -profielen configuratiebestanden | die instellingen voor Hallo implementatieomgevingen opslaan en publicatie-instellingen voor cloud-services.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7da8c551-fb06-4057-b5c7-c77f4b39d803
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/11/2017
ms.author: kraigb
ms.openlocfilehash: 1dba9df2fa57fe94dacc90ae74b05ccdc28270c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-service-configurations-and-profiles"></a>Hoe toomanage service en -profielen
## <a name="overview"></a>Overzicht
Wanneer u een service in de cloud publiceert, Visual Studio configuratie-informatie opslaat in twee soorten configuratiebestanden: service en -profielen. Instellingen voor Hallo implementatieomgevingen voor een Azure cloudservice opslaan,-configuraties (.cscfg-bestanden). Azure maakt gebruik van deze configuratiebestanden bij het beheren van uw cloudservices. Op Hallo daarentegen, profielen (.azurePubxml-bestanden) store publicatie-instellingen voor cloud-services. Deze instellingen zijn een record van wat u kiest wanneer u Hallo wizard Publiceren en lokaal worden gebruikt door Visual Studio. Dit onderwerp wordt uitgelegd hoe toowork met beide typen configuratiebestanden.

## <a name="service-configurations"></a>-Configuraties
U kunt meerdere service configuraties toouse maken voor elk van uw implementatieomgevingen. U kunt bijvoorbeeld een serviceconfiguratie voor de lokale omgeving Hallo toorun te gebruiken en testen van een Azure-toepassing en een andere serviceconfiguratie voor uw productieomgeving maken.

U kunt toevoegen, verwijderen, wijzigen en wijzigen van deze serviceconfiguraties op basis van uw vereisten. Zoals wordt weergegeven in de volgende illustratie Hallo, kunt u deze serviceconfiguraties beheren vanuit Visual Studio.

![-Configuraties beheren](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-service-config.png)

U kunt ook openen Hallo **configuraties beheren** in het dialoogvenster van eigenschappenpagina Hallo-rol. open Hallo snelmenu voor die functie tooopen Hallo eigenschappen voor een rol in uw Azure-project en kies vervolgens **eigenschappen**. Op Hallo **instellingen** tabblad uit, vouw Hallo **serviceconfiguratie** lijst, en selecteer vervolgens **beheren** tooopen hello **beheren configuraties**in het dialoogvenster.

### <a name="tooadd-a-service-configuration"></a>tooadd een serviceconfiguratie
1. Open de snelmenu Hallo voor hello Azure-project in Solution Explorer en selecteer **configuraties beheren**.
   
    Hallo **beheren-configuraties** dialoogvenster wordt weergegeven.
2. de configuratie van een service tooadd, moet u een kopie van een bestaande configuratie maken. toodo, kiest u Hallo configuratie u toocopy uit de lijst naam hello wilt gebruiken en selecteer vervolgens **kopie maken**.
3. (Optioneel) toogive Hallo serviceconfiguratie een andere naam Hallo nieuwe serviceconfiguratie kiezen uit de lijst naam Hallo en selecteer vervolgens **naam**. In Hallo **naam** tekstvak, Hallo naam dat u toouse voor deze serviceconfiguratie wilt en selecteer vervolgens **OK**.
   
    Een nieuwe serviceconfiguratiebestand met de naam serviceconfiguration zijn. [Nieuwe Name] .cscfg toohello Azure-project in Solution Explorer wordt toegevoegd.

### <a name="toodelete-a-service-configuration"></a>toodelete een serviceconfiguratie
1. Open de snelmenu Hallo voor hello Azure-project in Solution Explorer en selecteer **configuraties beheren**.
   
    Hallo **beheren-configuraties** dialoogvenster wordt weergegeven.
2. toodelete een serviceconfiguratie Hallo configuratie kiest die u wilt dat toodelete van Hallo **naam** lijst en selecteer vervolgens **verwijderen**. Een dialoogvenster weergegeven dat u wilt dat toodelete deze configuratie tooverify.
3. Selecteer **Verwijderen**.
   
     Hallo serviceconfiguratiebestand wordt verwijderd uit hello Azure-project in Solution Explorer.

### <a name="toorename-a-service-configuration"></a>toorename een serviceconfiguratie
1. Open de snelmenu Hallo voor hello Azure-project in Solution Explorer en selecteer vervolgens **configuraties beheren**.
   
    Hallo **beheren-configuraties** dialoogvenster wordt weergegeven.
2. toorename een serviceconfiguratie Hallo nieuwe serviceconfiguratie kiezen uit Hallo **naam** lijst, en selecteer vervolgens **naam**. In Hallo **naam** tekstvak, typenaam van hello wilt toouse voor deze serviceconfiguratie en selecteer vervolgens **OK**.
   
    Hallo-naam van het serviceconfiguratiebestand Hallo is gewijzigd in hello Azure-project in Solution Explorer.

### <a name="toochange-a-service-configuration"></a>toochange een serviceconfiguratie
* Als u een serviceconfiguratie toochange wilt, opent u de snelmenu Hallo voor Hallo specifieke rol u wilt toochange in hello Azure-project en selecteer vervolgens **eigenschappen**. Zie [hoe: Hallo rollen configureren voor een Azure Cloud Service met Visual Studio](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) voor meer informatie.

## <a name="make-different-setting-combinations-by-using-profiles"></a>Verschillende combinaties instellen met behulp van profielen maken
Met behulp van een profiel, kunt u automatisch invullen Hallo **Wizard publiceren** met verschillende combinaties van instellingen voor verschillende doeleinden. Bijvoorbeeld, u kunt een profiel hebt voor foutopsporing en een andere versie is gebaseerd. In dat geval uw **Debug** profiel zou hebben **IntelliTrace** ingeschakeld en Hallo **Debug** configuratie die is geselecteerd, en uw **Release** profiel zou hebben **IntelliTrace** uitgeschakeld en Hallo **Release** configuratie die is geselecteerd. U kunt verschillende profielen toodeploy ook een service met een ander opslagaccount gebruiken.

Wanneer u Hallo-wizard voor Hallo eerst uitvoert, wordt een standaard-profiel gemaakt. Visual Studio Hallo profiel opslaat in een bestand met een extensie .azurePubXml, die wordt toegevoegd onder hello Azure-project tooyour **profielen** map. Als u verschillende mogelijkheden handmatig opgeven wanneer u de wizard hello later uitvoert, wordt Hallo-bestand automatisch bijgewerkt. Voordat u Hallo na procedure uitvoert, moet u al hebt gepubliceerd uw cloudservice ten minste één keer.

### <a name="tooadd-a-profile"></a>een profiel tooadd
1. Open de snelmenu Hallo voor uw Azure-project en selecteer vervolgens **publiceren**.
2. Volgende toohello **profiel als doel** lijst, selecteer Hallo **profiel opslaan** knop als de volgende afbeelding ziet u Hallo. Hiermee maakt u een profiel voor u.
   
    ![Een nieuw profiel maken](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/create-new-profile.png)
3. Nadat het Hallo-profiel is gemaakt, selecteert u **< beheren... >** in Hallo **profiel als doel** lijst.
   
    Hallo **profielen beheren** dialoogvenster wordt weergegeven, als de volgende afbeelding ziet u Hallo.
   
    ![Dialoogvenster profielen beheren](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-profiles.png)
4. In Hallo **naam** lijst, kiest u een profiel en selecteer vervolgens **kopie maken**.
5. Kies Hallo **sluiten** knop.
   
    Hallo nieuw profiel wordt weergegeven in de doellijst profiel Hallo.
6. In Hallo **profiel als doel** wilt weergeven, selecteer Hallo-profiel dat u zojuist hebt gemaakt. instellingen van de Wizard publiceren Hallo worden gevuld met Hallo keuzes uit Hallo profiel die u hebt geselecteerd.
7. Selecteer Hallo **vorige** en **volgende** knoppen toodisplay elke pagina van Wizard publiceren Hallo en vervolgens aanpassen Hallo-instellingen voor dit profiel. Zie [Publish Azure Application Wizard](http://go.microsoft.com/fwlink/p/?LinkID=623085) voor meer informatie.
8. Nadat u klaar bent met het Hallo-instellingen aanpassen, selecteert u **volgende** toogo back toohello instellingenpagina. Hallo-profiel wordt opgeslagen wanneer u Hallo-service publiceert met behulp van deze instellingen of als u selecteert **opslaan** volgende toohello lijst met profielen.

### <a name="toorename-or-delete-a-profile"></a>toorename of een profiel verwijderen
1. Open de snelmenu Hallo voor uw Azure-project en selecteer vervolgens **publiceren**.
2. In Hallo **profiel als doel** selecteert **beheren**.
3. In Hallo **profielen beheren** dialoogvenster, selecteer Hallo-profiel dat u toodelete wilt en selecteer vervolgens **verwijderen**.
4. Selecteer in het bevestigingsdialoogvenster Hallo die wordt weergegeven, **OK**.
5. Selecteer **sluiten**.

### <a name="toochange-a-profile"></a>een profiel toochange
1. Open de snelmenu Hallo voor uw Azure-project en selecteer vervolgens **publiceren**.
2. In Hallo **profiel als doel** wilt weergeven, selecteer Hallo-profiel dat u wilt dat toochange.
3. Selecteer Hallo **vorige** en **volgende** toodisplay elke pagina van Wizard publiceren en gewenste-instellingen wijzigen Hallo Hallo knoppen. Zie [Publish Azure Application Wizard](http://go.microsoft.com/fwlink/p/?LinkID=623085) voor meer informatie.
4. Nadat u klaar bent met het Hallo-instellingen wijzigen, selecteert u **volgende** toogo back toohello **instellingen** pagina.
5. (Optioneel) Selecteer **publiceren** toopublish Hallo-cloudservice met de nieuwe instellingen Hallo. Als u niet wilt dat uw cloudservice op dit moment, en sluit toopublish Hallo Wizard publiceren, Visual Studio wordt u gevraagd als u wilt dat toosave Hallo wijzigingen toohello profiel.

## <a name="next-steps"></a>Volgende stappen
toolearn over het configureren van andere onderdelen van uw Azure-project in Visual Studio, Zie [configureren van een Azure-Project](http://go.microsoft.com/fwlink/p/?LinkID=623075)

