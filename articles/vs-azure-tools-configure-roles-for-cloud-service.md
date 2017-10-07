---
title: aaaConfigure hello rollen voor een Azure-cloudservice met Visual Studio | Microsoft Docs
description: Meer informatie over hoe tooset boven en rollen voor Azure cloudservices met Visual Studio configureren.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: d3c62eb57040ebe987787e73b17b468bb82122bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a>Azure cloud service-rollen configureren met Visual Studio
Een Azure-cloud-service kan een of meer werkprocessen of webrollen hebben. Voor elke rol moet toodefine hoe die rol is ingesteld en ook configureren hoe die rol wordt uitgevoerd. toolearn meer informatie over de rollen in de cloud-services, Zie Hallo video [inleiding tooAzure Cloudservices](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services). 

Hallo-informatie voor uw cloudservice wordt opgeslagen in Hallo volgende bestanden:

- **ServiceDefinition.csdef** -Hallo servicedefinitiebestand definieert Hallo runtime-instellingen voor uw cloudservice, met inbegrip van welke rollen zijn vereist, de eindpunten en de grootte van de virtuele machine. Geen van Hallo-gegevens die zijn opgeslagen in `ServiceDefinition.csdef` kunnen worden gewijzigd wanneer de functie wordt uitgevoerd.
- **ServiceConfiguration.cscfg** - Hallo serviceconfiguratiebestand wordt geconfigureerd hoeveel exemplaren van een rol worden uitgevoerd en Hallo waarden van Hallo-instellingen voor een rol gedefinieerd. gegevens die zijn opgeslagen Hallo `ServiceConfiguration.cscfg` kan worden gewijzigd terwijl uw rol wordt uitgevoerd.

toostore verschillende waarden voor Hallo-instellingen die bepalen hoe een rol wordt uitgevoerd, kunt u meerdere configuraties definiëren. U kunt een andere service-configuratie gebruiken voor elke implementatieomgeving. U kunt bijvoorbeeld uw storage account connection string toouse Hallo lokale Azure-opslagemulator ingesteld in de configuratie van een lokale service en het maken van een andere service configuration toouse Azure-opslag in Hallo cloud.

Wanneer u een Azure cloudservice in Visual Studio maakt, worden twee configuraties worden automatisch gemaakt en toegevoegd tooyour Azure-project:

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a>Een Azure cloudservice configureren
U kunt een Azure-cloud-service in Solution Explorer in Visual Studio configureren zoals wordt weergegeven in de volgende stappen uit Hallo:

1. Maak of open een Azure-cloud service-project in Visual Studio.

1. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer in het contextmenu hello, **eigenschappen**.
   
    ![Solution Explorer project contextmenu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. Selecteer in de pagina eigenschappen van het project Hallo Hallo **ontwikkeling** tabblad. 

    ![Pagina in de project-eigenschappen - ontwikkeling tabblad](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. In Hallo **serviceconfiguratie** lijst, selecteer Hallo-naam van de serviceconfiguratie Hallo dat u wilt dat tooedit. (Als u wilt dat toomake tooall Hallo-configuraties voor deze rol wordt gewijzigd, selecteert u **alle configuraties**.)
   
    > [!IMPORTANT]
    > Als u een specifieke service-configuratie kiest, worden sommige eigenschappen zijn uitgeschakeld omdat ze kunnen alleen worden ingesteld voor alle configuraties. tooedit deze eigenschappen, moet u **alle configuraties**.
    > 
    > 
   
    ![Lijst van de configuratie van de service voor een Azure cloudservice](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a>Het aantal rolinstanties Hallo wijzigen
tooimprove hello prestaties van uw cloudservice, het aantal exemplaren van een rol die worden uitgevoerd op basis van Hallo aantal gebruikers of Hallo load verwacht voor een bepaalde rol Hallo kunt wijzigen. Een afzonderlijke virtuele machine wordt gemaakt voor elk exemplaar van een rol wanneer Hallo cloudservice wordt uitgevoerd in Azure. Dit geldt voor Hallo facturering voor Hallo-implementatie van deze cloudservice. Zie voor meer informatie over facturering [inzicht in uw factuur voor Microsoft Azure](billing/billing-understand-your-bill.md).

1. Maak of open een Azure-cloud service-project in Visual Studio.

1. In **Solution Explorer**, Hallo projectknooppunt uitvouwen. Onder Hallo **rollen** knooppunt, klik met de rechtermuisknop Hallo functie u wilt tooupdate en, in het contextmenu hello, selecteer **eigenschappen**.

    ![Solution Explorer Azure rol contextmenu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Selecteer Hallo **configuratie** tabblad.

    ![Tabblad configuratie](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. In Hallo **serviceconfiguratie** lijst, selecteer Hallo serviceconfiguratie dat u wilt dat tooupdate.
   
    ![Lijst van de configuratie van de service](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. In Hallo **aantal exemplaar** tekst Voer Hallo aantal instanties dat toostart voor deze rol. Elk exemplaar wordt uitgevoerd op een afzonderlijke virtuele machine als u Hallo cloud service tooAzure publiceren.

    ![Hallo exemplaren bijwerken](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. In Visual Studio Hallo werkbalk, selecteer **opslaan**.

## <a name="manage-connection-strings-for-storage-accounts"></a>Tekenreeksen voor databaseverbindingen voor storage-accounts beheren
U kunt toevoegen, verwijderen of wijzigen van tekenreeksen voor databaseverbindingen voor uw serviceconfiguraties. Bijvoorbeeld, wilt u mogelijk een lokale verbindingsreeks voor de configuratie van een lokale service die een waarde van heeft `UseDevelopmentStorage=true`. U kunt ook tooconfigure een cloud service-configuratie die gebruikmaakt van een opslagaccount in Azure.

> [!WARNING]
> Wanneer u hello Azure storage-account belangrijke informatie voor een verbindingsreeks voor opslag account opgeeft, wordt deze informatie lokaal opgeslagen in het configuratiebestand Hallo-service. Deze informatie wordt echter momenteel niet opgeslagen als gecodeerde tekst.
> 
> 

Met behulp van een andere waarde voor de configuratie van elke service, u niet hebt toouse verschillende verbindingsreeksen in uw cloudservice of uw code te wijzigen wanneer u uw cloud service tooAzure publiceert. U kunt dezelfde naam voor de verbindingsreeks Hallo in uw code en Hallo-waarde op basis van de serviceconfiguratie Hallo die u selecteert verschilt wanneer u uw cloudservice maakt of wanneer u deze hebt gepubliceerd hello gebruiken.

1. Maak of open een Azure-cloud service-project in Visual Studio.

1. In **Solution Explorer**, Hallo projectknooppunt uitvouwen. Onder Hallo **rollen** knooppunt, klik met de rechtermuisknop Hallo functie u wilt tooupdate en, in het contextmenu hello, selecteer **eigenschappen**.

    ![Solution Explorer Azure rol contextmenu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Selecteer Hallo **instellingen** tabblad.

    ![Tabblad instellingen](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. In Hallo **serviceconfiguratie** lijst, selecteer Hallo serviceconfiguratie dat u wilt dat tooupdate.

    ![Configuratie van de service](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. Selecteer tooadd een verbindingsreeks **instelling toevoegen**.

    ![Verbindingsreeks toevoegen](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Wanneer de nieuwe instelling Hallo toohello lijst is toegevoegd, bijwerken Hallo rij in de lijst Hallo Hallo nodige informatie.

    ![Nieuwe verbindingsreeks](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Naam** -Hallo naam wilt u toouse voor Hallo verbindingsreeks invoeren.
    - **Type** : Selecteer **verbindingsreeks** uit de vervolgkeuzelijst Hallo.
    - **Waarde** -kunt u de verbindingsreeks Hallo invoeren rechtstreeks in Hallo **waarde** cel of selecteer Hallo weglatingsteken (...) toowork in Hallo **Create Storage Connection String** dialoogvenster.  

1. In Hallo **Create Storage Connection String** dialoogvenster, selecteert u een optie voor **verbinding maken via**. Volg daarna de instructies Hallo voor Hallo-optie die u selecteert:

    - **Microsoft Azure-opslagemulator** -als u deze optie selecteert, Hallo overige instellingen in het dialoogvenster Hallo zijn uitgeschakeld omdat ze alleen tooAzure van toepassing. Selecteer **OK**.
    - **Uw abonnement** : als u deze optie, gebruiken Hallo dropdown of lijst tooeither te selecteren en meld u bij een Microsoft-account selecteren of toevoegen van een Microsoft-account. Selecteer een Azure-abonnement en storage-account. Selecteer **OK**.
    - **Referenties handmatig worden ingevoerd** : Voer opslagaccountnaam hello en een primaire of tweede sleutel Hallo. Selecteer een optie voor **verbinding** (HTTPS wordt aanbevolen voor de meeste scenario's.) Selecteer **OK**.

1. een verbindingsreeks toodelete Hallo verbindingsreeks selecteren en selecteer vervolgens **instelling verwijderen**.

1. In Visual Studio Hallo werkbalk, selecteer **opslaan**.

## <a name="programmatically-access-a-connection-string"></a>Programmatisch toegang verkrijgen tot een verbindingsreeks

Hallo volgende stappen laten zien hoe tooprogrammatically toegang krijgen tot een verbindingsreeks met C#.

1. Voeg de volgende Hallo richtlijnen tooa C#-bestand waarin u toouse Hallo instelling gaat gebruiken:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. Hallo volgende code ziet u een voorbeeld van hoe tooaccess een verbindingsreeks. Vervang Hallo &lt;ConnectionStringName > aanduiding voor items met de juiste waarde Hallo. 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a>Toevoegen van aangepaste instellingen toouse in uw Azure-cloud-service
Aangepaste instellingen in het serviceconfiguratiebestand Hallo kunt u een naam en waarde voor een tekenreeks op voor de configuratie van een specifieke service toevoegen. U kunt deze instelling tooconfigure een functie in uw cloudservice lezen Hallo van Hallo instellen en het gebruik van deze waarde toocontrol Hallo logica in uw code toouse. U kunt de configuratiewaarden van deze service wijzigen zonder toorebuild het servicepakket of wanneer uw cloudservice wordt uitgevoerd. Uw code kunt meldingen van controleren wanneer een instelling wordt gewijzigd. Zie [RoleEnvironment.Changing gebeurtenis](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).

U kunt toevoegen, verwijderen of wijzigen van de aangepaste instellingen voor uw serviceconfiguraties. Wilt u mogelijk verschillende waarden voor deze tekenreeksen voor verschillende configuraties.

Met behulp van een andere waarde voor de configuratie van elke service, u geen andere tekenreeksen toouse hebt in uw cloudservice of uw code te wijzigen wanneer u uw cloud service tooAzure publiceert. U kunt dezelfde naam voor de tekenreeks in de waarde van de code en Hallo Hallo verschillend zijn is, op basis van de serviceconfiguratie Hallo die u selecteert wanneer u uw cloudservice maakt of wanneer u deze hebt gepubliceerd hello gebruiken.

1. Maak of open een Azure-cloud service-project in Visual Studio.

1. In **Solution Explorer**, Hallo projectknooppunt uitvouwen. Onder Hallo **rollen** knooppunt, klik met de rechtermuisknop Hallo functie u wilt tooupdate en, in het contextmenu hello, selecteer **eigenschappen**.

    ![Solution Explorer Azure rol contextmenu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Selecteer Hallo **instellingen** tabblad.

    ![Tabblad instellingen](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. In Hallo **serviceconfiguratie** lijst, selecteer Hallo serviceconfiguratie dat u wilt dat tooupdate.

    ![Lijst van de configuratie van de service](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. selecteert u een aangepaste instelling tooadd **instelling toevoegen**.

    ![Aangepaste instelling toevoegen](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Wanneer de nieuwe instelling Hallo toohello lijst is toegevoegd, bijwerken Hallo rij in de lijst Hallo Hallo nodige informatie.

    ![Nieuwe aangepaste instelling](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Naam** -Hallo-naam van instelling Hallo invoeren.
    - **Type** : Selecteer **tekenreeks** uit de vervolgkeuzelijst Hallo.
    - **Waarde** -Hallo waarde Hallo-instelling. U kunt Hallo waarde invoeren rechtstreeks in Hallo **waarde** cel, of selecteer Hallo weglatingsteken (...) tooenter Hallo waarde in Hallo **tekenreeks bewerken** dialoogvenster.  

1. een aangepaste instelling toodelete Hallo instelling selecteren en selecteer vervolgens **instelling verwijderen**.

1. In Visual Studio Hallo werkbalk, selecteer **opslaan**.

## <a name="programmatically-access-a-custom-settings-value"></a>Programmatisch toegang biedt tot de waarde van een aangepaste instelling
 
Hallo volgende stappen laten zien hoe tooprogrammatically toegang krijgen tot een aangepaste met C#-instelling.

1. Voeg de volgende Hallo richtlijnen tooa C#-bestand waarin u toouse Hallo instelling gaat gebruiken:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. Hallo volgende code ziet u een voorbeeld van hoe u een aangepaste instelling tooaccess. Vervang Hallo &lt;Instellingsnaam > aanduiding voor items met de juiste waarde Hallo. 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a>Lokale opslag voor elk rolexemplaar beheren
U kunt de lokale system-bestandsopslag voor elk exemplaar van een rol toevoegen. Hallo-gegevens die zijn opgeslagen in de betreffende opslag is niet toegankelijk door andere exemplaren van Hallo-rol voor welke Hallo gegevens worden opgeslagen of door andere rollen.  

1. Maak of open een Azure-cloud service-project in Visual Studio.

1. In **Solution Explorer**, Hallo projectknooppunt uitvouwen. Onder Hallo **rollen** knooppunt, klik met de rechtermuisknop Hallo functie u wilt tooupdate en, in het contextmenu hello, selecteer **eigenschappen**.

    ![Solution Explorer Azure rol contextmenu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Selecteer Hallo **lokale opslag** tabblad.

    ![Tabblad lokale opslag](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. In Hallo **serviceconfiguratie** lijst **alle configuraties** is geselecteerd als de instellingen voor de lokale opslag Hallo tooall-configuraties van toepassing. Een andere waarde resulteert in alle Hallo invoervelden op Hallo pagina wordt uitgeschakeld. 

    ![Lijst van de configuratie van de service](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. selecteert u een vermelding lokale opslag tooadd **lokale opslag toevoegen**.

    ![Lokale opslag toevoegen](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. Wanneer het nieuwe lokale opslag vermelding Hallo toohello lijst is toegevoegd, bijwerken Hallo rij in de lijst Hallo Hallo nodige informatie.

    ![Nieuw item voor lokale opslag](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - **Naam** -Voer Hallo naam wilt u toouse voor Hallo nieuwe lokale opslag.
    - **Grootte (MB)** -Voer Hallo-grootte in MB, die u nodig hebt voor Hallo nieuwe lokale opslag.
    - **Schoon op functie Prullenbak** -Selecteer deze optie tooremove Hallo-gegevens in Hallo nieuwe lokale opslag wanneer Hallo virtuele machine voor de rol hello gerecycled wordt.

1. Selecteer Hallo post toodelete een lokale opslag, post en selecteer vervolgens **lokale opslag verwijderen**.

1. In Visual Studio Hallo werkbalk, selecteer **opslaan**.

## <a name="programmatically-accessing-local-storage"></a>Programmatisch toegang tot lokale opslag

Deze sectie ziet u hoe tooprogrammatically toegang krijgen tot lokale opslag met C# met het schrijven van een Testtekstbestand `MyLocalStorageTest.txt`.  

### <a name="write-a-text-file-toolocal-storage"></a>Een tekst-bestandsopslag toolocal schrijven

Hallo volgende code toont een voorbeeld van hoe een tekst toowrite toolocal bestandsopslag. Vervang Hallo &lt;LocalStorageName > aanduiding voor items met de juiste waarde Hallo. 

    ```csharp
    // Retrieve an object that points toohello local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define hello file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-toolocal-storage"></a>Zoeken naar een bestand geschreven toolocal opslag

tooview Hallo-bestand is gemaakt door Hallo-code in de vorige sectie hello, als volgt te werk:
    
1.  In Windows-systeemvak Hallo, met de rechtermuisknop op het pictogram voor Azure Hallo en, in het contextmenu hello, selecteert u **weergeven Compute-Emulator UI**. 

    ![Azure-rekenemulator weergeven](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. Selecteer de Webrol Hallo.

    ![Azure-rekenemulator](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. Op Hallo **Microsoft Azure Compute-Emulator** selecteert u **extra** > **Open lokale archief**.

    ![Open lokale archief menu-item](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. Wanneer Hallo Windows Verkenner-venster wordt geopend, typt u ' MyLocalStorageTest.txt'' in Hallo **Search** tekstvak in en selecteer **Enter** toostart Hallo zoeken. 

## <a name="next-steps"></a>Volgende stappen
Meer informatie over Azure projecten in Visual Studio door te lezen [configureren van een Azure-Project](vs-azure-tools-configuring-an-azure-project.md). Meer informatie over Hallo cloud service schema door te lezen [schemaverwijzing](https://msdn.microsoft.com/library/azure/dd179398).

