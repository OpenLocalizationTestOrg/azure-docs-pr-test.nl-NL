---
title: De rollen configureert voor een Azure-cloudservice met Visual Studio | Microsoft Docs
description: Informatie over het instellen en configureren van rollen voor Azure-cloudservices met Visual Studio.
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
ms.openlocfilehash: 17da71ac0c5ab9330b9244c0354e4d161d98229e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a><span data-ttu-id="c9d90-103">Azure cloud service-rollen configureren met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c9d90-103">Configure Azure cloud service roles with Visual Studio</span></span>
<span data-ttu-id="c9d90-104">Een Azure-cloud-service kan een of meer werkprocessen of webrollen hebben.</span><span class="sxs-lookup"><span data-stu-id="c9d90-104">An Azure cloud service can have one or more worker or web roles.</span></span> <span data-ttu-id="c9d90-105">Voor elke rol moet u definiëren hoe die rol is ingesteld en te configureren hoe die rol wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9d90-105">For each role, you need to define how that role is set up and also configure how that role runs.</span></span> <span data-ttu-id="c9d90-106">Zie voor meer informatie over functies in cloudservices, de video [Inleiding tot Azure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span><span class="sxs-lookup"><span data-stu-id="c9d90-106">To learn more about roles in cloud services, see the video [Introduction to Azure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span></span> 

<span data-ttu-id="c9d90-107">De gegevens voor de cloudservice worden opgeslagen in de volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="c9d90-107">The information for your cloud service is stored in the following files:</span></span>

- <span data-ttu-id="c9d90-108">**ServiceDefinition.csdef** -het servicedefinitiebestand definieert de runtime-instellingen voor uw cloudservice, met inbegrip van welke rollen zijn vereist, de eindpunten en de grootte van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c9d90-108">**ServiceDefinition.csdef** - The service definition file defines the runtime settings for your cloud service including what roles are required, endpoints, and virtual machine size.</span></span> <span data-ttu-id="c9d90-109">Geen van de gegevens die zijn opgeslagen in `ServiceDefinition.csdef` kunnen worden gewijzigd wanneer de functie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9d90-109">None of the data stored in `ServiceDefinition.csdef` can be changed when your role is running.</span></span>
- <span data-ttu-id="c9d90-110">**ServiceConfiguration.cscfg** - configuratiebestand van de service wordt geconfigureerd hoeveel exemplaren van een rol worden uitgevoerd en de waarden van de instellingen voor een rol gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="c9d90-110">**ServiceConfiguration.cscfg** - The service configuration file configures how many instances of a role are run and the values of the settings defined for a role.</span></span> <span data-ttu-id="c9d90-111">De gegevens die zijn opgeslagen `ServiceConfiguration.cscfg` kan worden gewijzigd terwijl uw rol wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9d90-111">The data stored in `ServiceConfiguration.cscfg` can be changed while your role is running.</span></span>

<span data-ttu-id="c9d90-112">U kunt meerdere configuraties definiëren voor het opslaan van verschillende waarden voor de instellingen die bepalen hoe een rol wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9d90-112">To store different values for the settings that control how a role runs, you can define multiple service configurations.</span></span> <span data-ttu-id="c9d90-113">U kunt een andere service-configuratie gebruiken voor elke implementatieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c9d90-113">You can use a different service configuration for each deployment environment.</span></span> <span data-ttu-id="c9d90-114">U kunt bijvoorbeeld instellen dat de opslagverbindingsreeks voor een account op de lokale Azure-opslagemulator gebruiken in de configuratie van een lokale service en maak een andere serviceconfiguratie voor het gebruik van Azure-opslag in de cloud.</span><span class="sxs-lookup"><span data-stu-id="c9d90-114">For example, you can set your storage account connection string to use the local Azure storage emulator in a local service configuration and create another service configuration to use Azure storage in the cloud.</span></span>

<span data-ttu-id="c9d90-115">Wanneer u een Azure cloudservice in Visual Studio maakt, worden twee serviceconfiguraties automatisch gemaakt en toegevoegd aan uw Azure-project:</span><span class="sxs-lookup"><span data-stu-id="c9d90-115">When you create an Azure cloud service in Visual Studio, two service configurations are automatically created and added to your Azure project:</span></span>

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a><span data-ttu-id="c9d90-116">Een Azure cloudservice configureren</span><span class="sxs-lookup"><span data-stu-id="c9d90-116">Configure an Azure cloud service</span></span>
<span data-ttu-id="c9d90-117">U kunt een Azure-cloud-service in Solution Explorer in Visual Studio configureren zoals wordt weergegeven in de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c9d90-117">You can configure an Azure cloud service from Solution Explorer in Visual Studio, as shown in the following steps:</span></span>

1. <span data-ttu-id="c9d90-118">Maak of open een Azure-cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c9d90-118">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="c9d90-119">In **Solution Explorer**, met de rechtermuisknop op het project en selecteer in het contextmenu **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-119">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>
   
    ![Solution Explorer project contextmenu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. <span data-ttu-id="c9d90-121">Selecteer in de pagina eigenschappen van het project de **ontwikkeling** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c9d90-121">In the project's properties page, select the **Development** tab.</span></span> 

    ![Pagina in de project-eigenschappen - ontwikkeling tabblad](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. <span data-ttu-id="c9d90-123">In de **serviceconfiguratie** , selecteert u de naam van de configuratie van de service die u wilt bewerken.</span><span class="sxs-lookup"><span data-stu-id="c9d90-123">In the **Service Configuration** list, select the name of the service configuration that you want to edit.</span></span> <span data-ttu-id="c9d90-124">(Als u wijzigingen aanbrengen op de serviceconfiguraties voor deze rol wilt, selecteert u **alle configuraties**.)</span><span class="sxs-lookup"><span data-stu-id="c9d90-124">(If you want to make changes to all the service configurations for this role, select **All Configurations**.)</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="c9d90-125">Als u een specifieke service-configuratie kiest, worden sommige eigenschappen zijn uitgeschakeld omdat ze kunnen alleen worden ingesteld voor alle configuraties.</span><span class="sxs-lookup"><span data-stu-id="c9d90-125">If you choose a specific service configuration, some properties are disabled because they can only be set for all configurations.</span></span> <span data-ttu-id="c9d90-126">Deze eigenschappen bewerken, moet u **alle configuraties**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-126">To edit these properties, you must select **All Configurations**.</span></span>
    > 
    > 
   
    ![Lijst van de configuratie van de service voor een Azure cloudservice](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-the-number-of-role-instances"></a><span data-ttu-id="c9d90-128">Het aantal rolinstanties wijzigen</span><span class="sxs-lookup"><span data-stu-id="c9d90-128">Change the number of role instances</span></span>
<span data-ttu-id="c9d90-129">Om te verbeteren de prestaties van uw cloudservice, kunt u het aantal exemplaren van een rol die worden uitgevoerd op basis van het aantal gebruikers of de belasting voor een bepaalde functie verwacht.</span><span class="sxs-lookup"><span data-stu-id="c9d90-129">To improve the performance of your cloud service, you can change the number of instances of a role that are running, based on the number of users or the load expected for a particular role.</span></span> <span data-ttu-id="c9d90-130">Een afzonderlijke virtuele machine wordt gemaakt voor elk exemplaar van een rol wanneer de cloudservice wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="c9d90-130">A separate virtual machine is created for each instance of a role when the cloud service runs in Azure.</span></span> <span data-ttu-id="c9d90-131">Dit is van invloed op de facturering voor de implementatie van deze cloudservice.</span><span class="sxs-lookup"><span data-stu-id="c9d90-131">This affects the billing for the deployment of this cloud service.</span></span> <span data-ttu-id="c9d90-132">Zie voor meer informatie over facturering [inzicht in uw factuur voor Microsoft Azure](billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="c9d90-132">For more information about billing, see [Understand your bill for Microsoft Azure](billing/billing-understand-your-bill.md).</span></span>

1. <span data-ttu-id="c9d90-133">Maak of open een Azure-cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c9d90-133">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="c9d90-134">In **Solution Explorer**, vouw het projectknooppunt.</span><span class="sxs-lookup"><span data-stu-id="c9d90-134">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="c9d90-135">Onder de **rollen** knooppunt met de rechtermuisknop op de rol die u wilt bijwerken, en selecteer in het contextmenu **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-135">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Solution Explorer Azure rol contextmenu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="c9d90-137">Selecteer de **configuratie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c9d90-137">Select the **Configuration** tab.</span></span>

    ![Tabblad configuratie](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. <span data-ttu-id="c9d90-139">In de **serviceconfiguratie** , selecteert u de configuratie van de service die u wilt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="c9d90-139">In the **Service Configuration** list, select the service configuration that you want to update.</span></span>
   
    ![Lijst van de configuratie van de service](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. <span data-ttu-id="c9d90-141">In de **aantal exemplaar** tekst en voer het nummer van exemplaren die u voor deze rol wilt starten.</span><span class="sxs-lookup"><span data-stu-id="c9d90-141">In the **Instance count** text box, enter the number of instances that you want to start for this role.</span></span> <span data-ttu-id="c9d90-142">Elk exemplaar wordt uitgevoerd op een afzonderlijke virtuele machine als u de cloudservice naar Azure publiceren.</span><span class="sxs-lookup"><span data-stu-id="c9d90-142">Each instance runs on a separate virtual machine when you publish the cloud service to Azure.</span></span>

    ![Bijwerken van het aantal exemplaren](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. <span data-ttu-id="c9d90-144">Vanuit de Visual Studio werkbalk, selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-144">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="manage-connection-strings-for-storage-accounts"></a><span data-ttu-id="c9d90-145">Tekenreeksen voor databaseverbindingen voor storage-accounts beheren</span><span class="sxs-lookup"><span data-stu-id="c9d90-145">Manage connection strings for storage accounts</span></span>
<span data-ttu-id="c9d90-146">U kunt toevoegen, verwijderen of wijzigen van tekenreeksen voor databaseverbindingen voor uw serviceconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="c9d90-146">You can add, remove, or modify connection strings for your service configurations.</span></span> <span data-ttu-id="c9d90-147">Bijvoorbeeld, wilt u mogelijk een lokale verbindingsreeks voor de configuratie van een lokale service die een waarde van heeft `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="c9d90-147">For example, you might want a local connection string for a local service configuration that has a value of `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="c9d90-148">U kunt ook de configuratie van een cloud-service die gebruikmaakt van een opslagaccount in Azure te configureren.</span><span class="sxs-lookup"><span data-stu-id="c9d90-148">You might also want to configure a cloud service configuration that uses a storage account in Azure.</span></span>

> [!WARNING]
> <span data-ttu-id="c9d90-149">Wanneer u de Azure storage-account-sleutelgegevens voor een verbindingsreeks voor opslag account opgeeft, wordt deze informatie lokaal opgeslagen in het configuratiebestand van de service.</span><span class="sxs-lookup"><span data-stu-id="c9d90-149">When you enter the Azure storage account key information for a storage account connection string, this information is stored locally in the service configuration file.</span></span> <span data-ttu-id="c9d90-150">Deze informatie wordt echter momenteel niet opgeslagen als gecodeerde tekst.</span><span class="sxs-lookup"><span data-stu-id="c9d90-150">However, this information is currently not stored as encrypted text.</span></span>
> 
> 

<span data-ttu-id="c9d90-151">U hebt via een andere waarde voor elke serviceconfiguratie niet voor het gebruik van verschillende verbindingsreeksen in uw cloudservice of uw code te wijzigen wanneer u uw cloudservice naar Azure publiceert.</span><span class="sxs-lookup"><span data-stu-id="c9d90-151">By using a different value for each service configuration, you do not have to use different connection strings in your cloud service or modify your code when you publish your cloud service to Azure.</span></span> <span data-ttu-id="c9d90-152">U kunt dezelfde naam voor de verbindingsreeks gebruiken in uw code en de waarde is verschillend zijn, op basis van de configuratie van de service die u selecteert wanneer u uw cloudservice maakt of wanneer u deze hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="c9d90-152">You can use the same name for the connection string in your code and the value is different, based on the service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="c9d90-153">Maak of open een Azure-cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c9d90-153">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="c9d90-154">In **Solution Explorer**, vouw het projectknooppunt.</span><span class="sxs-lookup"><span data-stu-id="c9d90-154">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="c9d90-155">Onder de **rollen** knooppunt met de rechtermuisknop op de rol die u wilt bijwerken, en selecteer in het contextmenu **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-155">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Solution Explorer Azure rol contextmenu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="c9d90-157">Selecteer de **instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c9d90-157">Select the **Settings** tab.</span></span>

    ![Tabblad instellingen](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="c9d90-159">In de **serviceconfiguratie** , selecteert u de configuratie van de service die u wilt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="c9d90-159">In the **Service Configuration** list, select the service configuration that you want to update.</span></span>

    ![Configuratie van de service](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="c9d90-161">Selecteer om een verbindingsreeks toe **instelling toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-161">To add a connection string, select **Add Setting**.</span></span>

    ![Verbindingsreeks toevoegen](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="c9d90-163">Nadat de nieuwe instelling is toegevoegd aan de lijst, worden de rij in de lijst met de benodigde informatie bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c9d90-163">Once the new setting has been added to the list, update the row in the list with the necessary information.</span></span>

    ![Nieuwe verbindingsreeks](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="c9d90-165">**Naam** -Voer de naam die u wilt gebruiken voor de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="c9d90-165">**Name** - Enter the name that you want to use for the connection string.</span></span>
    - <span data-ttu-id="c9d90-166">**Type** : Selecteer **verbindingsreeks** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="c9d90-166">**Type** - Select **Connection String** from the drop-down list.</span></span>
    - <span data-ttu-id="c9d90-167">**Waarde** -kunt u de verbindingsreeks rechtstreeks in invoeren de **waarde** cellen of Selecteer het weglatingsteken (...) om te werken in de **Create Storage Connection String** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c9d90-167">**Value** - You can either enter the connection string directly into the **Value** cell, or select the ellipsis (...) to work in the **Create Storage Connection String** dialog.</span></span>  

1. <span data-ttu-id="c9d90-168">In de **Create Storage Connection String** dialoogvenster, selecteert u een optie voor **verbinding maken via**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-168">In the **Create Storage Connection String** dialog, select an option for **Connect using**.</span></span> <span data-ttu-id="c9d90-169">Volg de instructies voor de geselecteerde optie:</span><span class="sxs-lookup"><span data-stu-id="c9d90-169">Then follow the instructions for the option you select:</span></span>

    - <span data-ttu-id="c9d90-170">**Microsoft Azure-opslagemulator** -als u deze optie selecteert, de overige instellingen in het dialoogvenster zijn uitgeschakeld, omdat ze alleen van toepassing op Azure.</span><span class="sxs-lookup"><span data-stu-id="c9d90-170">**Microsoft Azure storage emulator** - If you select this option, the remaining settings on the dialog are disabled as they apply only to Azure.</span></span> <span data-ttu-id="c9d90-171">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-171">Select **OK**.</span></span>
    - <span data-ttu-id="c9d90-172">**Uw abonnement** : als u deze optie selecteert, gebruikt u de vervolgkeuzelijst ofwel selecteren en meld u aan bij een Microsoft-account of een Microsoft-account toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c9d90-172">**Your subscription** - If you select this option, use the dropdown list to either select and sign into a Microsoft account, or add a Microsoft account.</span></span> <span data-ttu-id="c9d90-173">Selecteer een Azure-abonnement en storage-account.</span><span class="sxs-lookup"><span data-stu-id="c9d90-173">Select an Azure subscription and storage account.</span></span> <span data-ttu-id="c9d90-174">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-174">Select **OK**.</span></span>
    - <span data-ttu-id="c9d90-175">**Referenties handmatig worden ingevoerd** -naam van het opslagaccount en de primaire of tweede sleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="c9d90-175">**Manually entered credentials** - Enter the storage account name, and either the primary or second key.</span></span> <span data-ttu-id="c9d90-176">Selecteer een optie voor **verbinding** (HTTPS wordt aanbevolen voor de meeste scenario's.) Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-176">Select an option for **Connection** (HTTPS is recommended for most scenarios.) Select **OK**.</span></span>

1. <span data-ttu-id="c9d90-177">Als u wilt verwijderen een verbindingsreeks, selecteert u de verbindingsreeks en selecteer vervolgens **instelling verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-177">To delete a connection string, select the connection string, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="c9d90-178">Vanuit de Visual Studio werkbalk, selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-178">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-connection-string"></a><span data-ttu-id="c9d90-179">Programmatisch toegang verkrijgen tot een verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="c9d90-179">Programmatically access a connection string</span></span>

<span data-ttu-id="c9d90-180">De volgende stappen laten zien hoe programmatisch toegang verkrijgen tot een verbindingsreeks met C#.</span><span class="sxs-lookup"><span data-stu-id="c9d90-180">The following steps show how to programmatically access a connection string using C#.</span></span>

1. <span data-ttu-id="c9d90-181">Voeg het volgende toe met behulp van instructies naar een C#-bestand dat u gaat waar de instelling te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="c9d90-181">Add the following using directives to a C# file where you are going to use the setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="c9d90-182">De volgende code ziet u een voorbeeld van hoe u toegang tot een verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="c9d90-182">The following code illustrates an example of how to access a connection string.</span></span> <span data-ttu-id="c9d90-183">Vervang de &lt;ConnectionStringName > aanduiding voor items met de juiste waarde.</span><span class="sxs-lookup"><span data-stu-id="c9d90-183">Replace the &lt;ConnectionStringName> placeholder with the appropriate value.</span></span> 

    ```csharp
    // Setup the connection to Azure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-to-use-in-your-azure-cloud-service"></a><span data-ttu-id="c9d90-184">Toevoegen van aangepaste instellingen te gebruiken in uw Azure-cloud-service</span><span class="sxs-lookup"><span data-stu-id="c9d90-184">Add custom settings to use in your Azure cloud service</span></span>
<span data-ttu-id="c9d90-185">Aangepaste instellingen in het configuratiebestand van de service kunt u een naam en waarde voor een tekenreeks op voor de configuratie van een specifieke service toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c9d90-185">Custom settings in the service configuration file let you add a name and value for a string for a specific service configuration.</span></span> <span data-ttu-id="c9d90-186">U kunt deze instelling te gebruiken voor het configureren van een functie in uw cloudservice door te lezen van de waarde van de instelling en deze waarde om te bepalen van de logica in uw code.</span><span class="sxs-lookup"><span data-stu-id="c9d90-186">You might choose to use this setting to configure a feature in your cloud service by reading the value of the setting and using this value to control the logic in your code.</span></span> <span data-ttu-id="c9d90-187">U kunt de configuratiewaarden van deze service wijzigen zonder opnieuw opbouwen van het servicepakket of wanneer uw cloudservice wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9d90-187">You can change these service configuration values without having to rebuild your service package or when your cloud service is running.</span></span> <span data-ttu-id="c9d90-188">Uw code kunt meldingen van controleren wanneer een instelling wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c9d90-188">Your code can check for notifications of when a setting changes.</span></span> <span data-ttu-id="c9d90-189">Zie [RoleEnvironment.Changing gebeurtenis](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9d90-189">See [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span></span>

<span data-ttu-id="c9d90-190">U kunt toevoegen, verwijderen of wijzigen van de aangepaste instellingen voor uw serviceconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="c9d90-190">You can add, remove, or modify custom settings for your service configurations.</span></span> <span data-ttu-id="c9d90-191">Wilt u mogelijk verschillende waarden voor deze tekenreeksen voor verschillende configuraties.</span><span class="sxs-lookup"><span data-stu-id="c9d90-191">You might want different values for these strings for different service configurations.</span></span>

<span data-ttu-id="c9d90-192">U hebt via een andere waarde voor elke serviceconfiguratie niet voor het gebruik van verschillende tekenreeksen in uw cloudservice of uw code te wijzigen wanneer u uw cloudservice naar Azure publiceert.</span><span class="sxs-lookup"><span data-stu-id="c9d90-192">By using a different value for each service configuration, you do not have to use different strings in your cloud service or modify your code when you publish your cloud service to Azure.</span></span> <span data-ttu-id="c9d90-193">U kunt dezelfde naam voor de tekenreeks in uw code en de waarde is verschillend zijn, op basis van de configuratie van de service die u selecteert wanneer u uw cloudservice maakt of wanneer u deze hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="c9d90-193">You can use the same name for the string in your code and the value is different, based on the service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="c9d90-194">Maak of open een Azure-cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c9d90-194">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="c9d90-195">In **Solution Explorer**, vouw het projectknooppunt.</span><span class="sxs-lookup"><span data-stu-id="c9d90-195">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="c9d90-196">Onder de **rollen** knooppunt met de rechtermuisknop op de rol die u wilt bijwerken, en selecteer in het contextmenu **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-196">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Solution Explorer Azure rol contextmenu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="c9d90-198">Selecteer de **instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c9d90-198">Select the **Settings** tab.</span></span>

    ![Tabblad instellingen](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="c9d90-200">In de **serviceconfiguratie** , selecteert u de configuratie van de service die u wilt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="c9d90-200">In the **Service Configuration** list, select the service configuration that you want to update.</span></span>

    ![Lijst van de configuratie van de service](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="c9d90-202">Selecteer om een aangepaste instelling toe **instelling toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-202">To add a custom setting, select **Add Setting**.</span></span>

    ![Aangepaste instelling toevoegen](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="c9d90-204">Nadat de nieuwe instelling is toegevoegd aan de lijst, worden de rij in de lijst met de benodigde informatie bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c9d90-204">Once the new setting has been added to the list, update the row in the list with the necessary information.</span></span>

    ![Nieuwe aangepaste instelling](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="c9d90-206">**Naam** -Voer de naam van de instelling.</span><span class="sxs-lookup"><span data-stu-id="c9d90-206">**Name** - Enter the name of the setting.</span></span>
    - <span data-ttu-id="c9d90-207">**Type** : Selecteer **tekenreeks** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="c9d90-207">**Type** - Select **String** from the drop-down list.</span></span>
    - <span data-ttu-id="c9d90-208">**Waarde** -Voer de waarde van de instelling.</span><span class="sxs-lookup"><span data-stu-id="c9d90-208">**Value** - Enter the value of the setting.</span></span> <span data-ttu-id="c9d90-209">U kunt de waarde rechtstreeks in invoeren de **waarde** cellen of Selecteer het weglatingsteken (...) de waarde in te voeren in de **tekenreeks bewerken** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c9d90-209">You can either enter the value directly into the **Value** cell, or select the ellipsis (...) to enter the value in the **Edit String** dialog.</span></span>  

1. <span data-ttu-id="c9d90-210">Selecteer de instelling voor het verwijderen van een aangepaste instelling en selecteer vervolgens **instelling verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-210">To delete a custom setting, select the setting, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="c9d90-211">Vanuit de Visual Studio werkbalk, selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-211">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-custom-settings-value"></a><span data-ttu-id="c9d90-212">Programmatisch toegang biedt tot de waarde van een aangepaste instelling</span><span class="sxs-lookup"><span data-stu-id="c9d90-212">Programmatically access a custom setting's value</span></span>
 
<span data-ttu-id="c9d90-213">De volgende stappen laten zien hoe programmatisch toegang verkrijgen tot een aangepaste met C#-instelling.</span><span class="sxs-lookup"><span data-stu-id="c9d90-213">The following steps show how to programmatically access a custom setting using C#.</span></span>

1. <span data-ttu-id="c9d90-214">Voeg het volgende toe met behulp van instructies naar een C#-bestand dat u gaat waar de instelling te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="c9d90-214">Add the following using directives to a C# file where you are going to use the setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="c9d90-215">De volgende code ziet u een voorbeeld van hoe u een aangepaste instelling.</span><span class="sxs-lookup"><span data-stu-id="c9d90-215">The following code illustrates an example of how to access a custom setting.</span></span> <span data-ttu-id="c9d90-216">Vervang de &lt;Instellingsnaam > aanduiding voor items met de juiste waarde.</span><span class="sxs-lookup"><span data-stu-id="c9d90-216">Replace the &lt;SettingName> placeholder with the appropriate value.</span></span> 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a><span data-ttu-id="c9d90-217">Lokale opslag voor elk rolexemplaar beheren</span><span class="sxs-lookup"><span data-stu-id="c9d90-217">Manage local storage for each role instance</span></span>
<span data-ttu-id="c9d90-218">U kunt de lokale system-bestandsopslag voor elk exemplaar van een rol toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c9d90-218">You can add local file system storage for each instance of a role.</span></span> <span data-ttu-id="c9d90-219">De gegevens die zijn opgeslagen in de betreffende opslag is niet toegankelijk door andere exemplaren van de rol voor de gegevens worden opgeslagen of door andere rollen.</span><span class="sxs-lookup"><span data-stu-id="c9d90-219">The data stored in that storage is not accessible by other instances of the role for which the data is stored, or by other roles.</span></span>  

1. <span data-ttu-id="c9d90-220">Maak of open een Azure-cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c9d90-220">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="c9d90-221">In **Solution Explorer**, vouw het projectknooppunt.</span><span class="sxs-lookup"><span data-stu-id="c9d90-221">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="c9d90-222">Onder de **rollen** knooppunt met de rechtermuisknop op de rol die u wilt bijwerken, en selecteer in het contextmenu **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-222">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Solution Explorer Azure rol contextmenu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="c9d90-224">Selecteer de **lokale opslag** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c9d90-224">Select the **Local Storage** tab.</span></span>

    ![Tabblad lokale opslag](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. <span data-ttu-id="c9d90-226">In de **serviceconfiguratie** lijst **alle configuraties** is geselecteerd als de instellingen van lokale opslag van toepassing op alle serviceconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="c9d90-226">In the **Service Configuration** list, ensure that **All Configurations** is selected as the local storage settings apply to all service configurations.</span></span> <span data-ttu-id="c9d90-227">Een andere waarde resulteert in de invoer velden op de pagina wordt uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c9d90-227">Any other value results in all the input fields on the page being disabled.</span></span> 

    ![Lijst van de configuratie van de service](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. <span data-ttu-id="c9d90-229">Selecteer om de vermelding voor een lokale opslag toe **lokale opslag toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-229">To add a local storage entry, select **Add Local Storage**.</span></span>

    ![Lokale opslag toevoegen](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. <span data-ttu-id="c9d90-231">Nadat de nieuwe invoer van de lokale opslag is toegevoegd aan de lijst, worden de rij in de lijst met de benodigde informatie bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c9d90-231">Once the new local storage entry has been added to the list, update the row in the list with the necessary information.</span></span>

    ![Nieuw item voor lokale opslag](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - <span data-ttu-id="c9d90-233">**Naam** -Voer de naam die u wilt gebruiken voor het nieuwe lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="c9d90-233">**Name** - Enter the name that you want to use for the new local storage.</span></span>
    - <span data-ttu-id="c9d90-234">**Grootte (MB)** -Geef de grootte in MB, die u nodig hebt voor het nieuwe lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="c9d90-234">**Size (MB)** - Enter the size in MB that you need for the new local storage.</span></span>
    - <span data-ttu-id="c9d90-235">**Schoon op functie Prullenbak** -Selecteer deze optie om de gegevens in de nieuwe lokale opslag verwijderen wanneer de virtuele machine voor de rol gerecycled wordt.</span><span class="sxs-lookup"><span data-stu-id="c9d90-235">**Clean on role recycle** - Select this option to remove the data in the new local storage when the virtual machine for the role is recycled.</span></span>

1. <span data-ttu-id="c9d90-236">Selecteer de vermelding voor het verwijderen van een vermelding voor lokale opslag, en selecteer vervolgens **lokale opslag verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-236">To delete a local storage entry, select the entry, and then select **Remove Local Storage**.</span></span>

1. <span data-ttu-id="c9d90-237">Vanuit de Visual Studio werkbalk, selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-237">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-accessing-local-storage"></a><span data-ttu-id="c9d90-238">Programmatisch toegang tot lokale opslag</span><span class="sxs-lookup"><span data-stu-id="c9d90-238">Programmatically accessing local storage</span></span>

<span data-ttu-id="c9d90-239">Deze sectie ziet u hoe u programmatisch toegang verkrijgen tot lokale opslag met C# met het schrijven van een Testtekstbestand `MyLocalStorageTest.txt`.</span><span class="sxs-lookup"><span data-stu-id="c9d90-239">This section illustrates how to programmatically access local storage using C# by writing a test text file `MyLocalStorageTest.txt`.</span></span>  

### <a name="write-a-text-file-to-local-storage"></a><span data-ttu-id="c9d90-240">Een tekstbestand schrijven naar de lokale opslag</span><span class="sxs-lookup"><span data-stu-id="c9d90-240">Write a text file to local storage</span></span>

<span data-ttu-id="c9d90-241">De volgende code toont een voorbeeld van hoe een tekstbestand schrijven naar de lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="c9d90-241">The following code shows an example of how to write a text file to local storage.</span></span> <span data-ttu-id="c9d90-242">Vervang de &lt;LocalStorageName > aanduiding voor items met de juiste waarde.</span><span class="sxs-lookup"><span data-stu-id="c9d90-242">Replace the &lt;LocalStorageName> placeholder with the appropriate value.</span></span> 

    ```csharp
    // Retrieve an object that points to the local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define the file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-to-local-storage"></a><span data-ttu-id="c9d90-243">Zoeken naar een bestand dat is geschreven naar de lokale opslag</span><span class="sxs-lookup"><span data-stu-id="c9d90-243">Find a file written to local storage</span></span>

<span data-ttu-id="c9d90-244">Als u wilt weergeven van het bestand gemaakt door de code in de vorige sectie, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c9d90-244">To view the file created by the code in the previous section, follow these steps:</span></span>
    
1.  <span data-ttu-id="c9d90-245">In de Windows-systeemvak met de rechtermuisknop op het pictogram voor Azure en, in het contextmenu Selecteer **weergeven Compute-Emulator UI**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-245">In the Windows notification area, right-click the Azure icon, and, from the context menu, select **Show Compute Emulator UI**.</span></span> 

    ![Azure-rekenemulator weergeven](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. <span data-ttu-id="c9d90-247">Selecteer de Webrol.</span><span class="sxs-lookup"><span data-stu-id="c9d90-247">Select the web role.</span></span>

    ![Azure-rekenemulator](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. <span data-ttu-id="c9d90-249">Op de **Microsoft Azure Compute-Emulator** selecteert u **extra** > **Open lokale archief**.</span><span class="sxs-lookup"><span data-stu-id="c9d90-249">On the **Microsoft Azure Compute Emulator** menu, select **Tools** > **Open local store**.</span></span>

    ![Open lokale archief menu-item](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. <span data-ttu-id="c9d90-251">Wanneer de Windows Verkenner-venster wordt geopend, typt u ' MyLocalStorageTest.txt'' in de **Search** tekstvak in en selecteer **Enter** wilt beginnen met zoeken.</span><span class="sxs-lookup"><span data-stu-id="c9d90-251">When the Windows Explorer window opens, enter `MyLocalStorageTest.txt`\` into the **Search** text box, and select **Enter** to start the search.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c9d90-252">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c9d90-252">Next steps</span></span>
<span data-ttu-id="c9d90-253">Meer informatie over Azure projecten in Visual Studio door te lezen [configureren van een Azure-Project](vs-azure-tools-configuring-an-azure-project.md).</span><span class="sxs-lookup"><span data-stu-id="c9d90-253">Learn more about Azure projects in Visual Studio by reading [Configuring an Azure Project](vs-azure-tools-configuring-an-azure-project.md).</span></span> <span data-ttu-id="c9d90-254">Meer informatie over het schema van cloud-service door te lezen [schemaverwijzing](https://msdn.microsoft.com/library/azure/dd179398).</span><span class="sxs-lookup"><span data-stu-id="c9d90-254">Learn more about the cloud service schema by reading [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span></span>

