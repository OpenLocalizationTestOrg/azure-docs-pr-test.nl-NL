---
title: aaaPrepare toopublish of implementeren van een Azure-toepassing vanuit Visual Studio | Microsoft Docs
description: Informatie over Hallo procedures tooset cloud- en storage-Accountservices installeren en configureren van uw Azure-toepassing.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 92ee2f9e-ec49-4c7a-900d-620abe5e9d8a
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: b5231d400e2ad9e20c3f21bad48a77c328b1f7a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-toopublish-or-deploy-an-azure-application-from-visual-studio"></a>Een Azure-toepassing vanuit Visual Studio implementeren of tooPublish voorbereiden
## <a name="overview"></a>Overzicht
Voordat u een cloudserviceproject publiceren kunt, moet u Hallo services volgende instellen:

* Een **cloudservice** toorun uw rollen in hello Azure-omgeving
* Een **opslagaccount** die toegang tot de services Blob, wachtrijen en tabellen toohello biedt.

Gebruik Hallo tooset procedures van deze services te volgen en uw toepassing configureren

## <a name="create-a-cloud-service"></a>Een cloudservice maken
een cloud service tooAzure toopublish, moet u eerst een cloudservice, die wordt uitgevoerd van de rollen in hello Azure-omgeving maken. U kunt een cloudservice maken in Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), zoals beschreven in de sectie Hallo **toocreate een cloudservice met behulp van de klassieke Azure-portal Hallo**verderop in dit onderwerp. U kunt ook een cloudservice maken in Visual Studio met behulp van de wizard voor het publiceren van Hallo.

### <a name="toocreate-a-cloud-service-by-using-visual-studio"></a>toocreate een cloudservice met behulp van Visual Studio
1. Open de snelmenu Hallo voor hello Azure-project en kies **publiceren**.

    ![VST_PublishMenu](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/vst-publish-menu.png)
2. Als u dit nog niet hebt aangemeld, aanmelden met uw gebruikersnaam en wachtwoord voor het Hallo-Microsoft-account of organisatie-account dat is gekoppeld aan uw Azure-abonnement.
3. Kies Hallo **volgende** knop tooadvance toohello **instellingen** pagina.

    ![Publishing algemene instellingen van de Wizard](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/publish-settings-page.png)
4. In Hallo **Cloudservices** Kies **nieuw**. Hallo **Azure-Services maken** dialoogvenster wordt weergegeven.
5. Voer Hallo-naam van uw cloudservice. Hallo-naam maakt deel uit van het Hallo-URL voor uw service en moet daarom globaal uniek zijn. Hallo-naam is niet hoofdlettergevoelig.

### <a name="toocreate-a-cloud-service-by-using-hello-azure-classic-portal"></a>toocreate een cloudservice met behulp van Hallo klassieke Azure-portal
1. Meld u aan toohello [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkId=253103) op Hallo Microsoft-website.
2. (optioneel) toodisplay een lijst met cloud-services die u al hebt gemaakt, kiest u Hallo Cloud Services-koppeling aan de linkerkant Hallo van Hallo pagina.
3. Kies Hallo  **+**  pictogram in de linkerbenedenhoek Hallo hoek en kies vervolgens **Cloudservice** op Hallo menu dat verschijnt. Een ander scherm met twee opties **snelle invoer** en **aangepast maken**, wordt weergegeven. Als u ervoor kiest **snelle invoer**, kunt u een cloudservice maken door te geven van de URL en het Hallo-regio waar deze fysiek worden gehost. Als u ervoor kiest **aangepast maken**, kunt u een cloudservice onmiddellijk publiceren door te geven van een pakket (.cspkg-bestand), een configuratiebestand (.cscfg) en een certificaat. Aangepast maken is niet vereist als u van plan toopublish uw cloudservice bent met behulp van Hallo **publiceren** opdracht in een Azure-project. Hallo **publiceren** opdracht is beschikbaar in het snelmenu Hallo voor een Azure-project.
4. Kies **snelle invoer** toolater uw cloudservice publiceren met behulp van Visual Studio.
5. Geef een naam voor uw cloudservice. Hallo volledige URL weergegeven naam van de volgende toohello.
6. Kies in Hallo lijst Hallo regio waar de meeste gebruikers zich bevinden.
7. Aan de onderkant van de Hallo van Hallo-venster, kies Hallo **Cloudservice maken** koppeling.

## <a name="create-a-storage-account"></a>Een opslagaccount maken
Een opslagaccount biedt toegang tot de services Blob, wachtrijen en tabellen toohello. U kunt een opslagaccount maken met behulp van Visual Studio of Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkId=253103).

### <a name="toocreate-a-storage-account-by-using-visual-studio"></a>toocreate een opslagaccount met behulp van Visual Studio
1. In **Solution Explorer**Open Hallo snelmenu voor Hallo **opslag** knooppunt, en kies vervolgens **Storage-Account maken**.

    ![Een nieuw Azure storage-account maken](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/IC744166.png)
2. Selecteer of typ de volgende informatie voor het nieuwe opslagaccount in Hallo HALLO hallo **Storage-Account maken** in het dialoogvenster.

   * Hello Azure-abonnement toowhich gewenste tooadd Hallo storage-account.
   * Hallo naam toouse voor Hallo nieuw opslagaccount.
   * Hallo regio of affiniteitsgroep (zoals VS-West of Oost-Azië).
   * type Hallo van replicatie gewenste toouse voor Hallo storage-account, zoals geografisch redundante.
3. Als u bent klaar, kiest u **maken**.hello nieuw opslagaccount wordt weergegeven in Hallo **opslag** in lijst **Server Explorer**.

### <a name="toocreate-a-storage-account-by-using-hello-azure-classic-portal"></a>toocreate een opslagaccount met behulp van Hallo klassieke Azure-portal
1. Meld u aan toohello [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkId=253103) op Hallo Microsoft-website.
2. (Optioneel) tooview uw opslagaccounts kiezen Hallo **opslag** koppeling in het Configuratiescherm op de linkerkant van de pagina Hallo HALLO hallo.
3. Kies in Hallo linkerbenedenhoek van Hallo pagina, Hallo  **+**  pictogram.
4. Kies in het menu dat verschijnt Hallo **opslag**, en kies vervolgens **snelle invoer**.
5. Hallo storage-account een naam die in een unieke url resulteren geven.
6. Geef een naam op uw cloudservice. Hallo volledige URL weergegeven naam van de volgende toohello.
7. Kies een regio waar de meeste gebruikers zich bevinden in Hallo lijst met regio's.
8. Geef op of tooenable geo-replicatie. Als u geo-replicatie inschakelt, worden uw gegevens wordt opgeslagen in meerdere fysieke locaties tooreduce Hallo kans verloren zijn gegaan. Deze functie kunt u opslag duurder, maar u kunt Hallo kosten reduceren doordat geografische locatie bij het maken van Hallo storage-account in plaats van het onderdeel hello later toevoegen. Zie voor meer informatie [Geo-replicatie](http://go.microsoft.com/fwlink/?LinkId=253108).
9. Aan de onderkant van de Hallo van Hallo-venster, kies Hallo **Storage-Account maken** koppeling.

Nadat u uw storage-account maakt, ziet u Hallo URL's u kunt tooaccess resources gebruiken in elk hello Azure storage-services en ook Hallo primaire en secundaire toegangssleutels voor uw account. Gebruik van deze sleutels tooauthenticate aanvragen op basis van Hallo storage-services.

> [!NOTE]
> de secundaire toegangssleutel Hallo biedt Hallo dezelfde toegang tot de opslagaccount tooyour als de primaire toegangssleutel Hallo en wordt gegenereerd als een back-up van uw primaire toegangssleutel verdacht. Bovendien is het raadzaam dat u de toegangssleutels regelmatig opnieuw genereert. U kunt een tekenreeks instelling toouse Hallo secundaire verbindingssleutel wijzigen tijdens het genereren van de primaire sleutel hello, en vervolgens kunt u deze primaire sleutel voor toouse Hallo opnieuw gegenereerd tijdens het genereren van de secundaire sleutel Hallo.
>
>

## <a name="configure-your-app-toouse-services-provided-by-hello-storage-account"></a>Configureer uw app toouse services geleverd door Hallo storage-account
Functies die toegang heeft tot storage services toouse hello Azure storage-services die u hebt gemaakt, moet u configureren. toodo, kunt u meerdere configuraties voor uw Azure-project. Standaard worden twee gemaakt in uw Azure-project. Met behulp van serviceconfiguraties met meerdere, kunt u Hallo dezelfde verbinding string in uw code, maar hebben een andere waarde voor een verbindingsreeks in de configuratie van elke service. U kunt bijvoorbeeld één service configuration toorun gebruiken en fouten opsporen in uw toepassing lokaal via hello Azure-opslagemulator en een andere service configuration toopublish uw toepassing tooAzure. Zie voor meer informatie over configuraties [configureren van uw Azure-Project met behulp van serviceconfiguraties met meerdere](vs-azure-tools-multiple-services-project-configurations.md).

### <a name="tooconfigure-your-application-toouse-services-that-hello-storage-account-provides"></a>tooconfigure uw toouse toepassingsservices die Hallo storage-account biedt
1. Open uw Azure-oplossing in Visual Studio. Klik in Solution Explorer open Hallo snelmenu voor elke rol in uw Azure-project die toegang heeft tot de opslagservices Hallo en kies **eigenschappen**. Een pagina met de naam van de rol Hallo Hallo wordt weergegeven in Hallo Visual Studio-editor. Hallo-pagina wordt weergegeven Hallo velden voor Hallo **configuratie** tabblad.
2. Kies in de eigenschappenpagina voor de rol Hallo Hallo **instellingen**.
3. In Hallo **serviceconfiguratie** Kies Hallo-naam van de serviceconfiguratie Hallo dat u wilt dat tooedit. Als u wilt dat toomake wijzigingen tooall van Hallo-configuraties voor deze rol, kunt u kiezen **alle configuraties**.  Zie voor meer informatie over hoe tooupdate configuraties service Hallo sectie **verbindingsreeksen voor Storage-Accounts beheren** in Hallo onderwerp [Hallo rollen configureren voor een Azure Cloud Service met Visual Studio ](vs-azure-tools-configure-roles-for-cloud-service.md).
4. toomodify eventuele verbindingstekenreeksinstellingen kiezen Hallo **...** de knop volgende toohello-instelling. Hallo **Create Storage Connection String** dialoogvenster wordt weergegeven.
5. Onder **verbinding maken via**, kies Hallo **uw abonnement** optie.
6. In Hallo **abonnement** kiest u uw abonnement. Als het Hallo-lijst met abonnementen niet Hallo besturingselement dat u wilt opnemen, kiest u Hallo **publicatie-Downloadinstellingen** koppeling.
7. In Hallo **accountnaam** Kies de naam van uw opslagaccount. Azure-hulpprogramma's verkrijgt opslagaccountreferenties automatisch via Hallo .publishsettings-bestand. toospecify handmatig, referenties voor uw opslagaccount kiezen Hallo **referenties handmatig worden ingevoerd** optie en ga verder met deze procedure. U kunt de naam van het opslagaccount en de primaire sleutel ophalen uit Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=213885). Als u niet toospecify wilt handmatig, kiest u de instellingen van uw storage-account Hallo **OK** knop tooclose Hallo dialoogvenster.
8. Kies Hallo **storage-account invoeren** referenties koppeling.
9. In Hallo **accountnaam** Hallo- naam van uw opslagaccount.

   > [!NOTE]
   > Meld u aan bij Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), en kies vervolgens Hallo **opslag** knop. Hallo portal bevat een overzicht van de storage-accounts. Als u een account kiest, wordt er een pagina voor het geopend. Op deze pagina kunt u Hallo-naam van de opslagaccount Hallo kopiëren. Als u van een eerdere versie van de klassieke portal hello gebruikmaakt, Hallo-naam van uw opslagaccount wordt weergegeven in Hallo **Opslagaccounts** weergeven. toocopy dit naam, markeer deze in Hallo **eigenschappen** venster hiervan weergeven en kies vervolgens Hallo Ctrl-C-sleutels. toopaste Hallo de naam in Visual Studio, kies Hallo **accountnaam** tekst vak in en kies vervolgens Hallo Ctrl + V sleutels.
   >
   >
10. In Hallo **accountsleutel** vak, Voer uw primaire sleutel of kopiëren en plakken uit Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885).
     Deze sleutel toocopy:

    1. Aan de onderkant van de Hallo van Hallo-pagina voor de juiste opslagaccount hello, kies Hallo **sleutels beheren** knop.
    2. Op Hallo **sleutels toegang beheren** pagina, selecteert u de tekst hello van de primaire toegangssleutel Hallo en kies vervolgens Hallo Ctrl + C sleutels.
    3. In Azure extra, plak Hallo sleutel Hallo **accountsleutel** vak.
    4. U moet een Hallo na toodetermine opties selecteren hoe Hallo-service toegang tot Hallo storage-account:

       * **HTTP gebruiken**. Dit is standaard Hallo-optie. Bijvoorbeeld `http://<account name>.blob.core.windows.net`.
       * **Gebruik van HTTPS** voor een beveiligde verbinding. Bijvoorbeeld `https://<accountname>.blob.core.windows.net`.
       * **Geef aangepaste eindpunten** voor elk Hallo drie services. Vervolgens kunt u deze eindpunten typen naar Hallo veld voor specifieke Hallo-service.

         > [!NOTE]
         > Als u aangepaste eindpunten maakt, kunt u een complexere verbindingsreeks kunt maken. Wanneer u deze tekenreeksindeling gebruikt, kunt u de service-eindpunten voor opslag met een aangepaste domeinnaam die u hebt geregistreerd voor uw opslagaccount Hello Blob-service opgeven. Ook kunt u toegang verlenen alleen tooblob resources in een enkele container via een shared access signature. Voor meer informatie over het toocreate aangepaste eindpunten, Zie [Azure Storage-verbindingsreeksen configureren](storage/common/storage-configure-connection-string.md).
         >
         >
11. toosave deze wijzigingen van de tekenreeks verbinding kiezen Hallo **OK** knop en kies vervolgens Hallo **opslaan** op de werkbalk Hallo. Nadat u deze wijzigingen hebt opgeslagen, kunt u Hallo-waarde van deze verbindingsreeks verkrijgen in uw code met behulp van [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx). Wanneer u uw toepassing tooAzure publiceert, kies Hallo-serviceconfiguratie hello Azure storage-account voor Hallo-verbindingsreeks bevat. Nadat de toepassing is gepubliceerd, moet u controleren dat de toepassing hello werkt zoals verwacht tegen hello Azure storage-services

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over het publiceren van apps tooAzure vanuit Visual Studio, Zie [publiceren van een Cloudservice met behulp van hulpprogramma's van Azure Hallo](vs-azure-tools-publishing-a-cloud-service.md).
