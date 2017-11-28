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
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a><span data-ttu-id="7b377-103">Azure cloud service-rollen configureren met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b377-103">Configure Azure cloud service roles with Visual Studio</span></span>
<span data-ttu-id="7b377-104">Een Azure-cloud-service kan een of meer werkprocessen of webrollen hebben.</span><span class="sxs-lookup"><span data-stu-id="7b377-104">An Azure cloud service can have one or more worker or web roles.</span></span> <span data-ttu-id="7b377-105">Voor elke rol moet toodefine hoe die rol is ingesteld en ook configureren hoe die rol wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b377-105">For each role, you need toodefine how that role is set up and also configure how that role runs.</span></span> <span data-ttu-id="7b377-106">toolearn meer informatie over de rollen in de cloud-services, Zie Hallo video [inleiding tooAzure Cloudservices](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span><span class="sxs-lookup"><span data-stu-id="7b377-106">toolearn more about roles in cloud services, see hello video [Introduction tooAzure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span></span> 

<span data-ttu-id="7b377-107">Hallo-informatie voor uw cloudservice wordt opgeslagen in Hallo volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="7b377-107">hello information for your cloud service is stored in hello following files:</span></span>

- <span data-ttu-id="7b377-108">**ServiceDefinition.csdef** -Hallo servicedefinitiebestand definieert Hallo runtime-instellingen voor uw cloudservice, met inbegrip van welke rollen zijn vereist, de eindpunten en de grootte van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7b377-108">**ServiceDefinition.csdef** - hello service definition file defines hello runtime settings for your cloud service including what roles are required, endpoints, and virtual machine size.</span></span> <span data-ttu-id="7b377-109">Geen van Hallo-gegevens die zijn opgeslagen in `ServiceDefinition.csdef` kunnen worden gewijzigd wanneer de functie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b377-109">None of hello data stored in `ServiceDefinition.csdef` can be changed when your role is running.</span></span>
- <span data-ttu-id="7b377-110">**ServiceConfiguration.cscfg** - Hallo serviceconfiguratiebestand wordt geconfigureerd hoeveel exemplaren van een rol worden uitgevoerd en Hallo waarden van Hallo-instellingen voor een rol gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="7b377-110">**ServiceConfiguration.cscfg** - hello service configuration file configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> <span data-ttu-id="7b377-111">gegevens die zijn opgeslagen Hallo `ServiceConfiguration.cscfg` kan worden gewijzigd terwijl uw rol wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b377-111">hello data stored in `ServiceConfiguration.cscfg` can be changed while your role is running.</span></span>

<span data-ttu-id="7b377-112">toostore verschillende waarden voor Hallo-instellingen die bepalen hoe een rol wordt uitgevoerd, kunt u meerdere configuraties definiëren.</span><span class="sxs-lookup"><span data-stu-id="7b377-112">toostore different values for hello settings that control how a role runs, you can define multiple service configurations.</span></span> <span data-ttu-id="7b377-113">U kunt een andere service-configuratie gebruiken voor elke implementatieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7b377-113">You can use a different service configuration for each deployment environment.</span></span> <span data-ttu-id="7b377-114">U kunt bijvoorbeeld uw storage account connection string toouse Hallo lokale Azure-opslagemulator ingesteld in de configuratie van een lokale service en het maken van een andere service configuration toouse Azure-opslag in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="7b377-114">For example, you can set your storage account connection string toouse hello local Azure storage emulator in a local service configuration and create another service configuration toouse Azure storage in hello cloud.</span></span>

<span data-ttu-id="7b377-115">Wanneer u een Azure cloudservice in Visual Studio maakt, worden twee configuraties worden automatisch gemaakt en toegevoegd tooyour Azure-project:</span><span class="sxs-lookup"><span data-stu-id="7b377-115">When you create an Azure cloud service in Visual Studio, two service configurations are automatically created and added tooyour Azure project:</span></span>

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a><span data-ttu-id="7b377-116">Een Azure cloudservice configureren</span><span class="sxs-lookup"><span data-stu-id="7b377-116">Configure an Azure cloud service</span></span>
<span data-ttu-id="7b377-117">U kunt een Azure-cloud-service in Solution Explorer in Visual Studio configureren zoals wordt weergegeven in de volgende stappen uit Hallo:</span><span class="sxs-lookup"><span data-stu-id="7b377-117">You can configure an Azure cloud service from Solution Explorer in Visual Studio, as shown in hello following steps:</span></span>

1. <span data-ttu-id="7b377-118">Maak of open een Azure-cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b377-118">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="7b377-119">In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer in het contextmenu hello, **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="7b377-119">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
    ![Solution Explorer project contextmenu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. <span data-ttu-id="7b377-121">Selecteer in de pagina eigenschappen van het project Hallo Hallo **ontwikkeling** tabblad.</span><span class="sxs-lookup"><span data-stu-id="7b377-121">In hello project's properties page, select hello **Development** tab.</span></span> 

    ![Pagina in de project-eigenschappen - ontwikkeling tabblad](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. <span data-ttu-id="7b377-123">In Hallo **serviceconfiguratie** lijst, selecteer Hallo-naam van de serviceconfiguratie Hallo dat u wilt dat tooedit.</span><span class="sxs-lookup"><span data-stu-id="7b377-123">In hello **Service Configuration** list, select hello name of hello service configuration that you want tooedit.</span></span> <span data-ttu-id="7b377-124">(Als u wilt dat toomake tooall Hallo-configuraties voor deze rol wordt gewijzigd, selecteert u **alle configuraties**.)</span><span class="sxs-lookup"><span data-stu-id="7b377-124">(If you want toomake changes tooall hello service configurations for this role, select **All Configurations**.)</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="7b377-125">Als u een specifieke service-configuratie kiest, worden sommige eigenschappen zijn uitgeschakeld omdat ze kunnen alleen worden ingesteld voor alle configuraties.</span><span class="sxs-lookup"><span data-stu-id="7b377-125">If you choose a specific service configuration, some properties are disabled because they can only be set for all configurations.</span></span> <span data-ttu-id="7b377-126">tooedit deze eigenschappen, moet u **alle configuraties**.</span><span class="sxs-lookup"><span data-stu-id="7b377-126">tooedit these properties, you must select **All Configurations**.</span></span>
    > 
    > 
   
    ![Lijst van de configuratie van de service voor een Azure cloudservice](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a><span data-ttu-id="7b377-128">Het aantal rolinstanties Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="7b377-128">Change hello number of role instances</span></span>
<span data-ttu-id="7b377-129">tooimprove hello prestaties van uw cloudservice, het aantal exemplaren van een rol die worden uitgevoerd op basis van Hallo aantal gebruikers of Hallo load verwacht voor een bepaalde rol Hallo kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7b377-129">tooimprove hello performance of your cloud service, you can change hello number of instances of a role that are running, based on hello number of users or hello load expected for a particular role.</span></span> <span data-ttu-id="7b377-130">Een afzonderlijke virtuele machine wordt gemaakt voor elk exemplaar van een rol wanneer Hallo cloudservice wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="7b377-130">A separate virtual machine is created for each instance of a role when hello cloud service runs in Azure.</span></span> <span data-ttu-id="7b377-131">Dit geldt voor Hallo facturering voor Hallo-implementatie van deze cloudservice.</span><span class="sxs-lookup"><span data-stu-id="7b377-131">This affects hello billing for hello deployment of this cloud service.</span></span> <span data-ttu-id="7b377-132">Zie voor meer informatie over facturering [inzicht in uw factuur voor Microsoft Azure](billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="7b377-132">For more information about billing, see [Understand your bill for Microsoft Azure](billing/billing-understand-your-bill.md).</span></span>

1. <span data-ttu-id="7b377-133">Maak of open een Azure-cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b377-133">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="7b377-134">In **Solution Explorer**, Hallo projectknooppunt uitvouwen.</span><span class="sxs-lookup"><span data-stu-id="7b377-134">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="7b377-135">Onder Hallo **rollen** knooppunt, klik met de rechtermuisknop Hallo functie u wilt tooupdate en, in het contextmenu hello, selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="7b377-135">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Solution Explorer Azure rol contextmenu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="7b377-137">Selecteer Hallo **configuratie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="7b377-137">Select hello **Configuration** tab.</span></span>

    ![Tabblad configuratie](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. <span data-ttu-id="7b377-139">In Hallo **serviceconfiguratie** lijst, selecteer Hallo serviceconfiguratie dat u wilt dat tooupdate.</span><span class="sxs-lookup"><span data-stu-id="7b377-139">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>
   
    ![Lijst van de configuratie van de service](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. <span data-ttu-id="7b377-141">In Hallo **aantal exemplaar** tekst Voer Hallo aantal instanties dat toostart voor deze rol.</span><span class="sxs-lookup"><span data-stu-id="7b377-141">In hello **Instance count** text box, enter hello number of instances that you want toostart for this role.</span></span> <span data-ttu-id="7b377-142">Elk exemplaar wordt uitgevoerd op een afzonderlijke virtuele machine als u Hallo cloud service tooAzure publiceren.</span><span class="sxs-lookup"><span data-stu-id="7b377-142">Each instance runs on a separate virtual machine when you publish hello cloud service tooAzure.</span></span>

    ![Hallo exemplaren bijwerken](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. <span data-ttu-id="7b377-144">In Visual Studio Hallo werkbalk, selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7b377-144">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="manage-connection-strings-for-storage-accounts"></a><span data-ttu-id="7b377-145">Tekenreeksen voor databaseverbindingen voor storage-accounts beheren</span><span class="sxs-lookup"><span data-stu-id="7b377-145">Manage connection strings for storage accounts</span></span>
<span data-ttu-id="7b377-146">U kunt toevoegen, verwijderen of wijzigen van tekenreeksen voor databaseverbindingen voor uw serviceconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="7b377-146">You can add, remove, or modify connection strings for your service configurations.</span></span> <span data-ttu-id="7b377-147">Bijvoorbeeld, wilt u mogelijk een lokale verbindingsreeks voor de configuratie van een lokale service die een waarde van heeft `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="7b377-147">For example, you might want a local connection string for a local service configuration that has a value of `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="7b377-148">U kunt ook tooconfigure een cloud service-configuratie die gebruikmaakt van een opslagaccount in Azure.</span><span class="sxs-lookup"><span data-stu-id="7b377-148">You might also want tooconfigure a cloud service configuration that uses a storage account in Azure.</span></span>

> [!WARNING]
> <span data-ttu-id="7b377-149">Wanneer u hello Azure storage-account belangrijke informatie voor een verbindingsreeks voor opslag account opgeeft, wordt deze informatie lokaal opgeslagen in het configuratiebestand Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="7b377-149">When you enter hello Azure storage account key information for a storage account connection string, this information is stored locally in hello service configuration file.</span></span> <span data-ttu-id="7b377-150">Deze informatie wordt echter momenteel niet opgeslagen als gecodeerde tekst.</span><span class="sxs-lookup"><span data-stu-id="7b377-150">However, this information is currently not stored as encrypted text.</span></span>
> 
> 

<span data-ttu-id="7b377-151">Met behulp van een andere waarde voor de configuratie van elke service, u niet hebt toouse verschillende verbindingsreeksen in uw cloudservice of uw code te wijzigen wanneer u uw cloud service tooAzure publiceert.</span><span class="sxs-lookup"><span data-stu-id="7b377-151">By using a different value for each service configuration, you do not have toouse different connection strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="7b377-152">U kunt dezelfde naam voor de verbindingsreeks Hallo in uw code en Hallo-waarde op basis van de serviceconfiguratie Hallo die u selecteert verschilt wanneer u uw cloudservice maakt of wanneer u deze hebt gepubliceerd hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7b377-152">You can use hello same name for hello connection string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="7b377-153">Maak of open een Azure-cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b377-153">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="7b377-154">In **Solution Explorer**, Hallo projectknooppunt uitvouwen.</span><span class="sxs-lookup"><span data-stu-id="7b377-154">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="7b377-155">Onder Hallo **rollen** knooppunt, klik met de rechtermuisknop Hallo functie u wilt tooupdate en, in het contextmenu hello, selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="7b377-155">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Solution Explorer Azure rol contextmenu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="7b377-157">Selecteer Hallo **instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="7b377-157">Select hello **Settings** tab.</span></span>

    ![Tabblad instellingen](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="7b377-159">In Hallo **serviceconfiguratie** lijst, selecteer Hallo serviceconfiguratie dat u wilt dat tooupdate.</span><span class="sxs-lookup"><span data-stu-id="7b377-159">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![Configuratie van de service](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="7b377-161">Selecteer tooadd een verbindingsreeks **instelling toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7b377-161">tooadd a connection string, select **Add Setting**.</span></span>

    ![Verbindingsreeks toevoegen](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="7b377-163">Wanneer de nieuwe instelling Hallo toohello lijst is toegevoegd, bijwerken Hallo rij in de lijst Hallo Hallo nodige informatie.</span><span class="sxs-lookup"><span data-stu-id="7b377-163">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Nieuwe verbindingsreeks](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="7b377-165">**Naam** -Hallo naam wilt u toouse voor Hallo verbindingsreeks invoeren.</span><span class="sxs-lookup"><span data-stu-id="7b377-165">**Name** - Enter hello name that you want toouse for hello connection string.</span></span>
    - <span data-ttu-id="7b377-166">**Type** : Selecteer **verbindingsreeks** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b377-166">**Type** - Select **Connection String** from hello drop-down list.</span></span>
    - <span data-ttu-id="7b377-167">**Waarde** -kunt u de verbindingsreeks Hallo invoeren rechtstreeks in Hallo **waarde** cel of selecteer Hallo weglatingsteken (...) toowork in Hallo **Create Storage Connection String** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7b377-167">**Value** - You can either enter hello connection string directly into hello **Value** cell, or select hello ellipsis (...) toowork in hello **Create Storage Connection String** dialog.</span></span>  

1. <span data-ttu-id="7b377-168">In Hallo **Create Storage Connection String** dialoogvenster, selecteert u een optie voor **verbinding maken via**.</span><span class="sxs-lookup"><span data-stu-id="7b377-168">In hello **Create Storage Connection String** dialog, select an option for **Connect using**.</span></span> <span data-ttu-id="7b377-169">Volg daarna de instructies Hallo voor Hallo-optie die u selecteert:</span><span class="sxs-lookup"><span data-stu-id="7b377-169">Then follow hello instructions for hello option you select:</span></span>

    - <span data-ttu-id="7b377-170">**Microsoft Azure-opslagemulator** -als u deze optie selecteert, Hallo overige instellingen in het dialoogvenster Hallo zijn uitgeschakeld omdat ze alleen tooAzure van toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b377-170">**Microsoft Azure storage emulator** - If you select this option, hello remaining settings on hello dialog are disabled as they apply only tooAzure.</span></span> <span data-ttu-id="7b377-171">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b377-171">Select **OK**.</span></span>
    - <span data-ttu-id="7b377-172">**Uw abonnement** : als u deze optie, gebruiken Hallo dropdown of lijst tooeither te selecteren en meld u bij een Microsoft-account selecteren of toevoegen van een Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="7b377-172">**Your subscription** - If you select this option, use hello dropdown list tooeither select and sign into a Microsoft account, or add a Microsoft account.</span></span> <span data-ttu-id="7b377-173">Selecteer een Azure-abonnement en storage-account.</span><span class="sxs-lookup"><span data-stu-id="7b377-173">Select an Azure subscription and storage account.</span></span> <span data-ttu-id="7b377-174">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b377-174">Select **OK**.</span></span>
    - <span data-ttu-id="7b377-175">**Referenties handmatig worden ingevoerd** : Voer opslagaccountnaam hello en een primaire of tweede sleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b377-175">**Manually entered credentials** - Enter hello storage account name, and either hello primary or second key.</span></span> <span data-ttu-id="7b377-176">Selecteer een optie voor **verbinding** (HTTPS wordt aanbevolen voor de meeste scenario's.) Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b377-176">Select an option for **Connection** (HTTPS is recommended for most scenarios.) Select **OK**.</span></span>

1. <span data-ttu-id="7b377-177">een verbindingsreeks toodelete Hallo verbindingsreeks selecteren en selecteer vervolgens **instelling verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="7b377-177">toodelete a connection string, select hello connection string, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="7b377-178">In Visual Studio Hallo werkbalk, selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7b377-178">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-connection-string"></a><span data-ttu-id="7b377-179">Programmatisch toegang verkrijgen tot een verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="7b377-179">Programmatically access a connection string</span></span>

<span data-ttu-id="7b377-180">Hallo volgende stappen laten zien hoe tooprogrammatically toegang krijgen tot een verbindingsreeks met C#.</span><span class="sxs-lookup"><span data-stu-id="7b377-180">hello following steps show how tooprogrammatically access a connection string using C#.</span></span>

1. <span data-ttu-id="7b377-181">Voeg de volgende Hallo richtlijnen tooa C#-bestand waarin u toouse Hallo instelling gaat gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7b377-181">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="7b377-182">Hallo volgende code ziet u een voorbeeld van hoe tooaccess een verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="7b377-182">hello following code illustrates an example of how tooaccess a connection string.</span></span> <span data-ttu-id="7b377-183">Vervang Hallo &lt;ConnectionStringName > aanduiding voor items met de juiste waarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b377-183">Replace hello &lt;ConnectionStringName> placeholder with hello appropriate value.</span></span> 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a><span data-ttu-id="7b377-184">Toevoegen van aangepaste instellingen toouse in uw Azure-cloud-service</span><span class="sxs-lookup"><span data-stu-id="7b377-184">Add custom settings toouse in your Azure cloud service</span></span>
<span data-ttu-id="7b377-185">Aangepaste instellingen in het serviceconfiguratiebestand Hallo kunt u een naam en waarde voor een tekenreeks op voor de configuratie van een specifieke service toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7b377-185">Custom settings in hello service configuration file let you add a name and value for a string for a specific service configuration.</span></span> <span data-ttu-id="7b377-186">U kunt deze instelling tooconfigure een functie in uw cloudservice lezen Hallo van Hallo instellen en het gebruik van deze waarde toocontrol Hallo logica in uw code toouse.</span><span class="sxs-lookup"><span data-stu-id="7b377-186">You might choose toouse this setting tooconfigure a feature in your cloud service by reading hello value of hello setting and using this value toocontrol hello logic in your code.</span></span> <span data-ttu-id="7b377-187">U kunt de configuratiewaarden van deze service wijzigen zonder toorebuild het servicepakket of wanneer uw cloudservice wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b377-187">You can change these service configuration values without having toorebuild your service package or when your cloud service is running.</span></span> <span data-ttu-id="7b377-188">Uw code kunt meldingen van controleren wanneer een instelling wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="7b377-188">Your code can check for notifications of when a setting changes.</span></span> <span data-ttu-id="7b377-189">Zie [RoleEnvironment.Changing gebeurtenis](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b377-189">See [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span></span>

<span data-ttu-id="7b377-190">U kunt toevoegen, verwijderen of wijzigen van de aangepaste instellingen voor uw serviceconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="7b377-190">You can add, remove, or modify custom settings for your service configurations.</span></span> <span data-ttu-id="7b377-191">Wilt u mogelijk verschillende waarden voor deze tekenreeksen voor verschillende configuraties.</span><span class="sxs-lookup"><span data-stu-id="7b377-191">You might want different values for these strings for different service configurations.</span></span>

<span data-ttu-id="7b377-192">Met behulp van een andere waarde voor de configuratie van elke service, u geen andere tekenreeksen toouse hebt in uw cloudservice of uw code te wijzigen wanneer u uw cloud service tooAzure publiceert.</span><span class="sxs-lookup"><span data-stu-id="7b377-192">By using a different value for each service configuration, you do not have toouse different strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="7b377-193">U kunt dezelfde naam voor de tekenreeks in de waarde van de code en Hallo Hallo verschillend zijn is, op basis van de serviceconfiguratie Hallo die u selecteert wanneer u uw cloudservice maakt of wanneer u deze hebt gepubliceerd hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7b377-193">You can use hello same name for hello string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="7b377-194">Maak of open een Azure-cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b377-194">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="7b377-195">In **Solution Explorer**, Hallo projectknooppunt uitvouwen.</span><span class="sxs-lookup"><span data-stu-id="7b377-195">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="7b377-196">Onder Hallo **rollen** knooppunt, klik met de rechtermuisknop Hallo functie u wilt tooupdate en, in het contextmenu hello, selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="7b377-196">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Solution Explorer Azure rol contextmenu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="7b377-198">Selecteer Hallo **instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="7b377-198">Select hello **Settings** tab.</span></span>

    ![Tabblad instellingen](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="7b377-200">In Hallo **serviceconfiguratie** lijst, selecteer Hallo serviceconfiguratie dat u wilt dat tooupdate.</span><span class="sxs-lookup"><span data-stu-id="7b377-200">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![Lijst van de configuratie van de service](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="7b377-202">selecteert u een aangepaste instelling tooadd **instelling toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7b377-202">tooadd a custom setting, select **Add Setting**.</span></span>

    ![Aangepaste instelling toevoegen](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="7b377-204">Wanneer de nieuwe instelling Hallo toohello lijst is toegevoegd, bijwerken Hallo rij in de lijst Hallo Hallo nodige informatie.</span><span class="sxs-lookup"><span data-stu-id="7b377-204">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Nieuwe aangepaste instelling](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="7b377-206">**Naam** -Hallo-naam van instelling Hallo invoeren.</span><span class="sxs-lookup"><span data-stu-id="7b377-206">**Name** - Enter hello name of hello setting.</span></span>
    - <span data-ttu-id="7b377-207">**Type** : Selecteer **tekenreeks** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b377-207">**Type** - Select **String** from hello drop-down list.</span></span>
    - <span data-ttu-id="7b377-208">**Waarde** -Hallo waarde Hallo-instelling.</span><span class="sxs-lookup"><span data-stu-id="7b377-208">**Value** - Enter hello value of hello setting.</span></span> <span data-ttu-id="7b377-209">U kunt Hallo waarde invoeren rechtstreeks in Hallo **waarde** cel, of selecteer Hallo weglatingsteken (...) tooenter Hallo waarde in Hallo **tekenreeks bewerken** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7b377-209">You can either enter hello value directly into hello **Value** cell, or select hello ellipsis (...) tooenter hello value in hello **Edit String** dialog.</span></span>  

1. <span data-ttu-id="7b377-210">een aangepaste instelling toodelete Hallo instelling selecteren en selecteer vervolgens **instelling verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="7b377-210">toodelete a custom setting, select hello setting, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="7b377-211">In Visual Studio Hallo werkbalk, selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7b377-211">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-custom-settings-value"></a><span data-ttu-id="7b377-212">Programmatisch toegang biedt tot de waarde van een aangepaste instelling</span><span class="sxs-lookup"><span data-stu-id="7b377-212">Programmatically access a custom setting's value</span></span>
 
<span data-ttu-id="7b377-213">Hallo volgende stappen laten zien hoe tooprogrammatically toegang krijgen tot een aangepaste met C#-instelling.</span><span class="sxs-lookup"><span data-stu-id="7b377-213">hello following steps show how tooprogrammatically access a custom setting using C#.</span></span>

1. <span data-ttu-id="7b377-214">Voeg de volgende Hallo richtlijnen tooa C#-bestand waarin u toouse Hallo instelling gaat gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7b377-214">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="7b377-215">Hallo volgende code ziet u een voorbeeld van hoe u een aangepaste instelling tooaccess.</span><span class="sxs-lookup"><span data-stu-id="7b377-215">hello following code illustrates an example of how tooaccess a custom setting.</span></span> <span data-ttu-id="7b377-216">Vervang Hallo &lt;Instellingsnaam > aanduiding voor items met de juiste waarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b377-216">Replace hello &lt;SettingName> placeholder with hello appropriate value.</span></span> 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a><span data-ttu-id="7b377-217">Lokale opslag voor elk rolexemplaar beheren</span><span class="sxs-lookup"><span data-stu-id="7b377-217">Manage local storage for each role instance</span></span>
<span data-ttu-id="7b377-218">U kunt de lokale system-bestandsopslag voor elk exemplaar van een rol toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7b377-218">You can add local file system storage for each instance of a role.</span></span> <span data-ttu-id="7b377-219">Hallo-gegevens die zijn opgeslagen in de betreffende opslag is niet toegankelijk door andere exemplaren van Hallo-rol voor welke Hallo gegevens worden opgeslagen of door andere rollen.</span><span class="sxs-lookup"><span data-stu-id="7b377-219">hello data stored in that storage is not accessible by other instances of hello role for which hello data is stored, or by other roles.</span></span>  

1. <span data-ttu-id="7b377-220">Maak of open een Azure-cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b377-220">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="7b377-221">In **Solution Explorer**, Hallo projectknooppunt uitvouwen.</span><span class="sxs-lookup"><span data-stu-id="7b377-221">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="7b377-222">Onder Hallo **rollen** knooppunt, klik met de rechtermuisknop Hallo functie u wilt tooupdate en, in het contextmenu hello, selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="7b377-222">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Solution Explorer Azure rol contextmenu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="7b377-224">Selecteer Hallo **lokale opslag** tabblad.</span><span class="sxs-lookup"><span data-stu-id="7b377-224">Select hello **Local Storage** tab.</span></span>

    ![Tabblad lokale opslag](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. <span data-ttu-id="7b377-226">In Hallo **serviceconfiguratie** lijst **alle configuraties** is geselecteerd als de instellingen voor de lokale opslag Hallo tooall-configuraties van toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b377-226">In hello **Service Configuration** list, ensure that **All Configurations** is selected as hello local storage settings apply tooall service configurations.</span></span> <span data-ttu-id="7b377-227">Een andere waarde resulteert in alle Hallo invoervelden op Hallo pagina wordt uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="7b377-227">Any other value results in all hello input fields on hello page being disabled.</span></span> 

    ![Lijst van de configuratie van de service](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. <span data-ttu-id="7b377-229">selecteert u een vermelding lokale opslag tooadd **lokale opslag toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7b377-229">tooadd a local storage entry, select **Add Local Storage**.</span></span>

    ![Lokale opslag toevoegen](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. <span data-ttu-id="7b377-231">Wanneer het nieuwe lokale opslag vermelding Hallo toohello lijst is toegevoegd, bijwerken Hallo rij in de lijst Hallo Hallo nodige informatie.</span><span class="sxs-lookup"><span data-stu-id="7b377-231">Once hello new local storage entry has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Nieuw item voor lokale opslag](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - <span data-ttu-id="7b377-233">**Naam** -Voer Hallo naam wilt u toouse voor Hallo nieuwe lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="7b377-233">**Name** - Enter hello name that you want toouse for hello new local storage.</span></span>
    - <span data-ttu-id="7b377-234">**Grootte (MB)** -Voer Hallo-grootte in MB, die u nodig hebt voor Hallo nieuwe lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="7b377-234">**Size (MB)** - Enter hello size in MB that you need for hello new local storage.</span></span>
    - <span data-ttu-id="7b377-235">**Schoon op functie Prullenbak** -Selecteer deze optie tooremove Hallo-gegevens in Hallo nieuwe lokale opslag wanneer Hallo virtuele machine voor de rol hello gerecycled wordt.</span><span class="sxs-lookup"><span data-stu-id="7b377-235">**Clean on role recycle** - Select this option tooremove hello data in hello new local storage when hello virtual machine for hello role is recycled.</span></span>

1. <span data-ttu-id="7b377-236">Selecteer Hallo post toodelete een lokale opslag, post en selecteer vervolgens **lokale opslag verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="7b377-236">toodelete a local storage entry, select hello entry, and then select **Remove Local Storage**.</span></span>

1. <span data-ttu-id="7b377-237">In Visual Studio Hallo werkbalk, selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7b377-237">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-accessing-local-storage"></a><span data-ttu-id="7b377-238">Programmatisch toegang tot lokale opslag</span><span class="sxs-lookup"><span data-stu-id="7b377-238">Programmatically accessing local storage</span></span>

<span data-ttu-id="7b377-239">Deze sectie ziet u hoe tooprogrammatically toegang krijgen tot lokale opslag met C# met het schrijven van een Testtekstbestand `MyLocalStorageTest.txt`.</span><span class="sxs-lookup"><span data-stu-id="7b377-239">This section illustrates how tooprogrammatically access local storage using C# by writing a test text file `MyLocalStorageTest.txt`.</span></span>  

### <a name="write-a-text-file-toolocal-storage"></a><span data-ttu-id="7b377-240">Een tekst-bestandsopslag toolocal schrijven</span><span class="sxs-lookup"><span data-stu-id="7b377-240">Write a text file toolocal storage</span></span>

<span data-ttu-id="7b377-241">Hallo volgende code toont een voorbeeld van hoe een tekst toowrite toolocal bestandsopslag.</span><span class="sxs-lookup"><span data-stu-id="7b377-241">hello following code shows an example of how toowrite a text file toolocal storage.</span></span> <span data-ttu-id="7b377-242">Vervang Hallo &lt;LocalStorageName > aanduiding voor items met de juiste waarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b377-242">Replace hello &lt;LocalStorageName> placeholder with hello appropriate value.</span></span> 

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

### <a name="find-a-file-written-toolocal-storage"></a><span data-ttu-id="7b377-243">Zoeken naar een bestand geschreven toolocal opslag</span><span class="sxs-lookup"><span data-stu-id="7b377-243">Find a file written toolocal storage</span></span>

<span data-ttu-id="7b377-244">tooview Hallo-bestand is gemaakt door Hallo-code in de vorige sectie hello, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="7b377-244">tooview hello file created by hello code in hello previous section, follow these steps:</span></span>
    
1.  <span data-ttu-id="7b377-245">In Windows-systeemvak Hallo, met de rechtermuisknop op het pictogram voor Azure Hallo en, in het contextmenu hello, selecteert u **weergeven Compute-Emulator UI**.</span><span class="sxs-lookup"><span data-stu-id="7b377-245">In hello Windows notification area, right-click hello Azure icon, and, from hello context menu, select **Show Compute Emulator UI**.</span></span> 

    ![Azure-rekenemulator weergeven](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. <span data-ttu-id="7b377-247">Selecteer de Webrol Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b377-247">Select hello web role.</span></span>

    ![Azure-rekenemulator](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. <span data-ttu-id="7b377-249">Op Hallo **Microsoft Azure Compute-Emulator** selecteert u **extra** > **Open lokale archief**.</span><span class="sxs-lookup"><span data-stu-id="7b377-249">On hello **Microsoft Azure Compute Emulator** menu, select **Tools** > **Open local store**.</span></span>

    ![Open lokale archief menu-item](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. <span data-ttu-id="7b377-251">Wanneer Hallo Windows Verkenner-venster wordt geopend, typt u ' MyLocalStorageTest.txt'' in Hallo **Search** tekstvak in en selecteer **Enter** toostart Hallo zoeken.</span><span class="sxs-lookup"><span data-stu-id="7b377-251">When hello Windows Explorer window opens, enter `MyLocalStorageTest.txt`\` into hello **Search** text box, and select **Enter** toostart hello search.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7b377-252">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7b377-252">Next steps</span></span>
<span data-ttu-id="7b377-253">Meer informatie over Azure projecten in Visual Studio door te lezen [configureren van een Azure-Project](vs-azure-tools-configuring-an-azure-project.md).</span><span class="sxs-lookup"><span data-stu-id="7b377-253">Learn more about Azure projects in Visual Studio by reading [Configuring an Azure Project](vs-azure-tools-configuring-an-azure-project.md).</span></span> <span data-ttu-id="7b377-254">Meer informatie over Hallo cloud service schema door te lezen [schemaverwijzing](https://msdn.microsoft.com/library/azure/dd179398).</span><span class="sxs-lookup"><span data-stu-id="7b377-254">Learn more about hello cloud service schema by reading [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span></span>

