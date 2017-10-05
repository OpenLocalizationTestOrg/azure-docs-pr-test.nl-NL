---
title: Data Management Gateway voor Data Factory | Microsoft Docs
description: Stel een gegevensgateway in om gegevens te verplaatsen tussen on-premises en de cloud. Gebruik Data Management Gateway in Azure Data Factory om uw gegevens te verplaatsen.
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 9e40eba285aeb1cce6b77311d1b69a6b96967a0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="data-management-gateway"></a><span data-ttu-id="8337f-104">Gegevensbeheergateway</span><span class="sxs-lookup"><span data-stu-id="8337f-104">Data Management Gateway</span></span>
<span data-ttu-id="8337f-105">Data management gateway is een clientagent waarmee u in uw on-premises omgeving installeren moet kopiëren van gegevens tussen cloud en on-premises gegevensopslagexemplaren.</span><span class="sxs-lookup"><span data-stu-id="8337f-105">The Data management gateway is a client agent that you must install in your on-premises environment to copy data between cloud and on-premises data stores.</span></span> <span data-ttu-id="8337f-106">De on-premises gegevens opslaat die worden ondersteund door Data Factory worden vermeld in de [ondersteunde gegevensbronnen](data-factory-data-movement-activities.md#supported-data-stores-and-formats) sectie.</span><span class="sxs-lookup"><span data-stu-id="8337f-106">The on-premises data stores supported by Data Factory are listed in the [Supported data sources](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.</span></span>

<span data-ttu-id="8337f-107">In dit artikel is een aanvulling op de procedures in de [gegevens verplaatsen tussen on-premises en cloud gegevensarchieven](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="8337f-107">This article complements the walkthrough in the [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="8337f-108">In de procedure maakt u een pijplijn die de gateway gebruikt om gegevens te verplaatsen van een on-premises SQL Server database naar een Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="8337f-108">In the walkthrough, you create a pipeline that uses the gateway to move data from an on-premises SQL Server database to an Azure blob.</span></span> <span data-ttu-id="8337f-109">Dit artikel bevat gedetailleerde informatie over het data management gateway.</span><span class="sxs-lookup"><span data-stu-id="8337f-109">This article provides detailed in-depth information about the data management gateway.</span></span> 

<span data-ttu-id="8337f-110">U kunt een data management gateway uitbreiden door meerdere lokale computers koppelen aan de gateway.</span><span class="sxs-lookup"><span data-stu-id="8337f-110">You can scale out a data management gateway by associating multiple on-premises machines with the gateway.</span></span> <span data-ttu-id="8337f-111">U kunt schalen omhoog door het aantal data movement taken die kunnen tegelijkertijd worden uitgevoerd op een knooppunt te verhogen.</span><span class="sxs-lookup"><span data-stu-id="8337f-111">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="8337f-112">Deze functie is ook beschikbaar voor een logische gateway met één knooppunt.</span><span class="sxs-lookup"><span data-stu-id="8337f-112">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="8337f-113">Zie [schaal data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8337f-113">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>

> [!NOTE]
> <span data-ttu-id="8337f-114">Gateway ondersteunt momenteel alleen de kopieeractiviteit en de activiteit opgeslagen procedure in de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8337f-114">Currently, gateway supports only the copy activity and stored procedure activity in Data Factory.</span></span> <span data-ttu-id="8337f-115">Het is niet mogelijk is op de gateway van een aangepaste activiteit voor toegang tot on-premises gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="8337f-115">It is not possible to use the gateway from a custom activity to access on-premises data sources.</span></span>      

## <a name="overview"></a><span data-ttu-id="8337f-116">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8337f-116">Overview</span></span>
### <a name="capabilities-of-data-management-gateway"></a><span data-ttu-id="8337f-117">Mogelijkheden van data management gateway</span><span class="sxs-lookup"><span data-stu-id="8337f-117">Capabilities of data management gateway</span></span>
<span data-ttu-id="8337f-118">Data management gateway biedt de volgende mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="8337f-118">Data management gateway provides the following capabilities:</span></span>

* <span data-ttu-id="8337f-119">On-premises gegevensbronnen model en cloud gegevensbronnen binnen de dezelfde gegevensfactory en gegevens te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="8337f-119">Model on-premises data sources and cloud data sources within the same data factory and move data.</span></span>
* <span data-ttu-id="8337f-120">Een door één venster voor bewaking en beheer inzicht in de gateway de status van de Data Factory-pagina hebben.</span><span class="sxs-lookup"><span data-stu-id="8337f-120">Have a single pane of glass for monitoring and management with visibility into gateway status from the Data Factory page.</span></span>
* <span data-ttu-id="8337f-121">Toegang tot on-premises gegevensbronnen veilig beheren.</span><span class="sxs-lookup"><span data-stu-id="8337f-121">Manage access to on-premises data sources securely.</span></span>
  * <span data-ttu-id="8337f-122">Er zijn geen wijzigingen vereist voor de firewall van het bedrijf.</span><span class="sxs-lookup"><span data-stu-id="8337f-122">No changes required to corporate firewall.</span></span> <span data-ttu-id="8337f-123">Gateway alleen uitgaande HTTP-gebaseerde verbindingen maakt met internet te openen.</span><span class="sxs-lookup"><span data-stu-id="8337f-123">Gateway only makes outbound HTTP-based connections to open internet.</span></span>
  * <span data-ttu-id="8337f-124">Referenties voor uw on-premises gegevensopslagexemplaren met uw certificaat niet versleutelen.</span><span class="sxs-lookup"><span data-stu-id="8337f-124">Encrypt credentials for your on-premises data stores with your certificate.</span></span>
* <span data-ttu-id="8337f-125">Gegevens efficiënt te verplaatsen: de gegevens worden overgedragen parallel flexibel omgaan met onregelmatige netwerkproblemen met automatisch Pogingslogica.</span><span class="sxs-lookup"><span data-stu-id="8337f-125">Move data efficiently – data is transferred in parallel, resilient to intermittent network issues with auto retry logic.</span></span>

### <a name="command-flow-and-data-flow"></a><span data-ttu-id="8337f-126">Opdracht stroom en de gegevensstroom</span><span class="sxs-lookup"><span data-stu-id="8337f-126">Command flow and data flow</span></span>
<span data-ttu-id="8337f-127">Wanneer u een kopieeractiviteit om gegevens tussen on-premises en cloud te kopiëren, de activiteit maakt gebruik van een gateway voor gegevensoverdracht van on-premises gegevensbron naar de cloud en vice versa.</span><span class="sxs-lookup"><span data-stu-id="8337f-127">When you use a copy activity to copy data between on-premises and cloud, the activity uses a gateway to transfer data from on-premises data source to cloud and vice versa.</span></span>

<span data-ttu-id="8337f-128">Hier is de gegevensstroom op hoog niveau voor en overzicht van stappen voor het kopiëren met gegevensgateway: ![gegevensstroom met gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span><span class="sxs-lookup"><span data-stu-id="8337f-128">Here is the high-level data flow for and summary of steps for copy with data gateway: ![Data flow using gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span></span>

1. <span data-ttu-id="8337f-129">Gegevens ontwikkelaars een gateway maakt voor een Azure Data Factory met behulp van de [Azure-portal](https://portal.azure.com) of [PowerShell-Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).</span><span class="sxs-lookup"><span data-stu-id="8337f-129">Data developer creates a gateway for an Azure Data Factory using either the [Azure portal](https://portal.azure.com) or [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).</span></span>
2. <span data-ttu-id="8337f-130">Een gekoppelde service voor een on-premises gegevensopslag gegevens developer gemaakt door te geven van de gateway.</span><span class="sxs-lookup"><span data-stu-id="8337f-130">Data developer creates a linked service for an on-premises data store by specifying the gateway.</span></span> <span data-ttu-id="8337f-131">Als onderdeel van het instellen van de gekoppelde service gebruikt gegevens ontwikkelaar de instelling referenties toepassing verificatietypen en referenties op te geven.</span><span class="sxs-lookup"><span data-stu-id="8337f-131">As part of setting up the linked service, data developer uses the Setting Credentials application to specify authentication types and credentials.</span></span>  <span data-ttu-id="8337f-132">Het dialoogvenster instelling referenties toepassing communiceert met de gegevensopslag voor het testen van verbinding en de gateway naar de referenties op te slaan.</span><span class="sxs-lookup"><span data-stu-id="8337f-132">The Setting Credentials application dialog communicates with the data store to test connection and the gateway to save credentials.</span></span>
3. <span data-ttu-id="8337f-133">Gateway versleutelt de referenties met het certificaat dat is gekoppeld aan de gateway (opgegeven door de ontwikkelaar gegevens), voordat de referenties worden opgeslagen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="8337f-133">Gateway encrypts the credentials with the certificate associated with the gateway (supplied by data developer), before saving the credentials in the cloud.</span></span>
4. <span data-ttu-id="8337f-134">Data Factory-service communiceert met de gateway voor planning en beheer van taken via een besturingskanaal die gebruikmaakt van een gedeelde Azure service bus-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="8337f-134">Data Factory service communicates with the gateway for scheduling & management of jobs via a control channel that uses a shared Azure service bus queue.</span></span> <span data-ttu-id="8337f-135">Wanneer een taak kopiëren activiteit worden gestart moet, wachtrijen Data Factory de aanvraag samen met de referentie-informatie.</span><span class="sxs-lookup"><span data-stu-id="8337f-135">When a copy activity job needs to be kicked off, Data Factory queues the request along with credential information.</span></span> <span data-ttu-id="8337f-136">Gateway is serversysteemstatus van de taak na polling van de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="8337f-136">Gateway kicks off the job after polling the queue.</span></span>
5. <span data-ttu-id="8337f-137">De gateway, ontsleutelt de referenties met hetzelfde certificaat en maakt vervolgens verbinding met het lokale gegevensarchief met de juiste authenticatietype en referenties.</span><span class="sxs-lookup"><span data-stu-id="8337f-137">The gateway decrypts the credentials with the same certificate and then connects to the on-premises data store with proper authentication type and credentials.</span></span>
6. <span data-ttu-id="8337f-138">De gateway kopiëren bij een winkel lokale gegevens naar een cloudopslag of omgekeerd, afhankelijk van hoe de kopieerbewerking is geconfigureerd in de pijplijn gegevens.</span><span class="sxs-lookup"><span data-stu-id="8337f-138">The gateway copies data from an on-premises store to a cloud storage, or vice versa depending on how the Copy Activity is configured in the data pipeline.</span></span> <span data-ttu-id="8337f-139">Voor deze stap worden de gateway rechtstreeks communiceert met de opslag op basis van een cloud-services zoals Azure Blob Storage via een beveiligd kanaal voor (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="8337f-139">For this step, the gateway directly communicates with cloud-based storage services such as Azure Blob Storage over a secure (HTTPS) channel.</span></span>

### <a name="considerations-for-using-gateway"></a><span data-ttu-id="8337f-140">Overwegingen voor het gebruik van gateway</span><span class="sxs-lookup"><span data-stu-id="8337f-140">Considerations for using gateway</span></span>
* <span data-ttu-id="8337f-141">Één exemplaar van data management gateway kan worden gebruikt voor meerdere on-premises-gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="8337f-141">A single instance of data management gateway can be used for multiple on-premises data sources.</span></span> <span data-ttu-id="8337f-142">Echter, **één gatewayexemplaar is gekoppeld aan slechts één Azure data factory** en kan niet worden gedeeld met een andere data factory.</span><span class="sxs-lookup"><span data-stu-id="8337f-142">However, **a single gateway instance is tied to only one Azure data factory** and cannot be shared with another data factory.</span></span>
* <span data-ttu-id="8337f-143">U kunt hebben **slechts één exemplaar van data management gateway** geïnstalleerd op een enkele computer.</span><span class="sxs-lookup"><span data-stu-id="8337f-143">You can have **only one instance of data management gateway** installed on a single machine.</span></span> <span data-ttu-id="8337f-144">Stel dat u hebt twee gegevensfactory's die toegang moeten krijgen tot on-premises gegevensbronnen, moet u om gateways te installeren op twee lokale computers.</span><span class="sxs-lookup"><span data-stu-id="8337f-144">Suppose, you have two data factories that need to access on-premises data sources, you need to install gateways on two on-premises computers.</span></span> <span data-ttu-id="8337f-145">Met andere woorden, is een gateway gekoppeld aan een specifieke gegevensfactory</span><span class="sxs-lookup"><span data-stu-id="8337f-145">In other words, a gateway is tied to a specific data factory</span></span>
* <span data-ttu-id="8337f-146">De **gateway niet hoeft te worden op dezelfde computer als de gegevensbron**.</span><span class="sxs-lookup"><span data-stu-id="8337f-146">The **gateway does not need to be on the same machine as the data source**.</span></span> <span data-ttu-id="8337f-147">Echter minder dichter gateway met de gegevensbron met tijd voor de gateway verbinding maken met de gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="8337f-147">However, having gateway closer to the data source reduces the time for the gateway to connect to the data source.</span></span> <span data-ttu-id="8337f-148">Het is raadzaam dat u de gateway installeren op een machine die verschilt van de naam die als host fungeert voor on-premises gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="8337f-148">We recommend that you install the gateway on a machine that is different from the one that hosts on-premises data source.</span></span> <span data-ttu-id="8337f-149">Wanneer de gateway en de gegevensbron zich op verschillende computers bevinden, de gateway niet zou concurreren voor bronnen met de gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="8337f-149">When the gateway and data source are on different machines, the gateway does not compete for resources with data source.</span></span>
* <span data-ttu-id="8337f-150">U kunt hebben **meerdere gateways op verschillende computers verbinding maken met dezelfde lokale gegevensbron**.</span><span class="sxs-lookup"><span data-stu-id="8337f-150">You can have **multiple gateways on different machines connecting to the same on-premises data source**.</span></span> <span data-ttu-id="8337f-151">Bijvoorbeeld wellicht hebt u twee gateways voor de twee data Factory, maar dezelfde lokale gegevensbron is geregistreerd bij de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="8337f-151">For example, you may have two gateways serving two data factories but the same on-premises data source is registered with both the data factories.</span></span>
* <span data-ttu-id="8337f-152">Als u al een gateway geïnstalleerd op uw computer voor een **Power BI** scenario installeert een **afzonderlijke gateway voor Azure Data Factory** op een andere computer.</span><span class="sxs-lookup"><span data-stu-id="8337f-152">If you already have a gateway installed on your computer serving a **Power BI** scenario, install a **separate gateway for Azure Data Factory** on another machine.</span></span>
* <span data-ttu-id="8337f-153">Gateway moet worden gebruikt, zelfs wanneer u **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="8337f-153">Gateway must be used even when you use **ExpressRoute**.</span></span>
* <span data-ttu-id="8337f-154">Uw gegevensbron behandelen als een lokale gegevensbron (die zich achter een firewall) zelfs als u werkt met **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="8337f-154">Treat your data source as an on-premises data source (that is behind a firewall) even when you use **ExpressRoute**.</span></span> <span data-ttu-id="8337f-155">De gateway gebruiken om verbinding tussen de service en de gegevensbron te maken.</span><span class="sxs-lookup"><span data-stu-id="8337f-155">Use the gateway to establish connectivity between the service and the data source.</span></span>
* <span data-ttu-id="8337f-156">U moet **gebruik van de gateway** zelfs als het gegevensarchief is in de cloud op een **Azure IaaS VM**.</span><span class="sxs-lookup"><span data-stu-id="8337f-156">You must **use the gateway** even if the data store is in the cloud on an **Azure IaaS VM**.</span></span>

## <a name="installation"></a><span data-ttu-id="8337f-157">Installeren</span><span class="sxs-lookup"><span data-stu-id="8337f-157">Installation</span></span>
### <a name="prerequisites"></a><span data-ttu-id="8337f-158">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8337f-158">Prerequisites</span></span>
* <span data-ttu-id="8337f-159">De ondersteunde **besturingssysteem** versies zijn Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="8337f-159">The supported **Operating System** versions are Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span></span> <span data-ttu-id="8337f-160">Installatie van data management gateway op een domeincontroller is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="8337f-160">Installation of the data management gateway on a domain controller is currently not supported.</span></span>
* <span data-ttu-id="8337f-161">.NET framework 4.5.1 of hoger is vereist.</span><span class="sxs-lookup"><span data-stu-id="8337f-161">.NET Framework 4.5.1 or above is required.</span></span> <span data-ttu-id="8337f-162">Als u gateway op een computer met Windows 7 installeert, installeert u .NET Framework 4.5 of hoger.</span><span class="sxs-lookup"><span data-stu-id="8337f-162">If you are installing gateway on a Windows 7 machine, install .NET Framework 4.5 or later.</span></span> <span data-ttu-id="8337f-163">Zie [.NET Framework-systeemvereisten](https://msdn.microsoft.com/library/8z6watww.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8337f-163">See [.NET Framework System Requirements](https://msdn.microsoft.com/library/8z6watww.aspx) for details.</span></span>
* <span data-ttu-id="8337f-164">De aanbevolen **configuratie** voor de gateway machine ten minste 2 GHz, 4 kernen, 8 GB RAM-geheugen en schijf 80 GB is.</span><span class="sxs-lookup"><span data-stu-id="8337f-164">The recommended **configuration** for the gateway machine is at least 2 GHz, 4 cores, 8-GB RAM, and 80-GB disk.</span></span>
* <span data-ttu-id="8337f-165">Als de hostmachine in de slaapstand, reageert de gateway niet op gegevensaanvragen.</span><span class="sxs-lookup"><span data-stu-id="8337f-165">If the host machine hibernates, the gateway does not respond to data requests.</span></span> <span data-ttu-id="8337f-166">Configureer daarom een geschikte **energiebeheerschema** op de computer voordat de gateway is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8337f-166">Therefore, configure an appropriate **power plan** on the computer before installing the gateway.</span></span> <span data-ttu-id="8337f-167">Als de machine is geconfigureerd voor de sluimerstand, wordt een bericht gevraagd in de installatie van de gateway.</span><span class="sxs-lookup"><span data-stu-id="8337f-167">If the machine is configured to hibernate, the gateway installation prompts a message.</span></span>
* <span data-ttu-id="8337f-168">U moet een beheerder op de computer installeren en configureren van de data management gateway is.</span><span class="sxs-lookup"><span data-stu-id="8337f-168">You must be an administrator on the machine to install and configure the data management gateway successfully.</span></span> <span data-ttu-id="8337f-169">U kunt extra gebruikers toevoegen aan de **data management gateway gebruikers** lokale Windows-groep.</span><span class="sxs-lookup"><span data-stu-id="8337f-169">You can add additional users to the **data management gateway Users** local Windows group.</span></span> <span data-ttu-id="8337f-170">De leden van deze groep kunnen gebruiken om zich de **Data Management Gateway Configuration Manager** hulpprogramma om de gateway te configureren.</span><span class="sxs-lookup"><span data-stu-id="8337f-170">The members of this group are able to use the **Data Management Gateway Configuration Manager** tool to configure the gateway.</span></span>

<span data-ttu-id="8337f-171">Als kopie activiteiten bij uitvoering op een specifieke frequentie gebeuren, volgt het brongebruik (CPU, geheugen) op de machine ook hetzelfde patroon met piek- en niet-actieve tijd.</span><span class="sxs-lookup"><span data-stu-id="8337f-171">As copy activity runs happen on a specific frequency, the resource usage (CPU, memory) on the machine also follows the same pattern with peak and idle times.</span></span> <span data-ttu-id="8337f-172">Resourcegebruik ook afhankelijk van geheugenlatentie de hoeveelheid gegevens worden verplaatst.</span><span class="sxs-lookup"><span data-stu-id="8337f-172">Resource utilization also depends heavily on the amount of data being moved.</span></span> <span data-ttu-id="8337f-173">Als meerdere kopie taken uitgevoerd worden, ziet u Resourcegebruik tijdens piektijden omhoog gaan.</span><span class="sxs-lookup"><span data-stu-id="8337f-173">When multiple copy jobs are in progress, you see resource usage go up during peak times.</span></span>

### <a name="installation-options"></a><span data-ttu-id="8337f-174">Opties voor de installatie</span><span class="sxs-lookup"><span data-stu-id="8337f-174">Installation options</span></span>
<span data-ttu-id="8337f-175">Data management gateway kan worden geïnstalleerd op de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="8337f-175">Data management gateway can be installed in the following ways:</span></span>

* <span data-ttu-id="8337f-176">Downloaden van een MSI-installatiepakket van de [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="8337f-176">By downloading an MSI setup package from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>  <span data-ttu-id="8337f-177">Het MSI-bestand kan ook worden gebruikt om te upgraden van bestaande data management gateway naar de nieuwste versie met alle instellingen behouden.</span><span class="sxs-lookup"><span data-stu-id="8337f-177">The MSI can also be used to upgrade existing data management gateway to the latest version, with all settings preserved.</span></span>
* <span data-ttu-id="8337f-178">Door te klikken op **downloaden en installeren van de gegevensgateway** koppeling onder handmatige installatie of **rechtstreeks op deze computer installeren** onder snelle installatie.</span><span class="sxs-lookup"><span data-stu-id="8337f-178">By clicking **Download and install data gateway** link under MANUAL SETUP or **Install directly on this computer** under EXPRESS SETUP.</span></span> <span data-ttu-id="8337f-179">Zie [gegevens verplaatsen tussen on-premises en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies over het gebruik van de snelle installatie.</span><span class="sxs-lookup"><span data-stu-id="8337f-179">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on using express setup.</span></span> <span data-ttu-id="8337f-180">De handmatige stap gaat u naar het download center.</span><span class="sxs-lookup"><span data-stu-id="8337f-180">The manual step takes you to the download center.</span></span>  <span data-ttu-id="8337f-181">De instructies voor het downloaden en installeren van de gateway van Downloadcentrum zijn in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="8337f-181">The instructions for downloading and installing the gateway from download center are in the next section.</span></span>

### <a name="installation-best-practices"></a><span data-ttu-id="8337f-182">Best practices voor installatie:</span><span class="sxs-lookup"><span data-stu-id="8337f-182">Installation best practices:</span></span>
1. <span data-ttu-id="8337f-183">Energiebeheerschema op de hostcomputer voor de gateway zodanig configureren dat de machine sluimerstand niet.</span><span class="sxs-lookup"><span data-stu-id="8337f-183">Configure power plan on the host machine for the gateway so that the machine does not hibernate.</span></span> <span data-ttu-id="8337f-184">Als de hostmachine in de slaapstand, reageert de gateway niet op gegevensaanvragen.</span><span class="sxs-lookup"><span data-stu-id="8337f-184">If the host machine hibernates, the gateway does not respond to data requests.</span></span>
2. <span data-ttu-id="8337f-185">Back-up van het certificaat dat hoort bij de gateway.</span><span class="sxs-lookup"><span data-stu-id="8337f-185">Back up the certificate associated with the gateway.</span></span>

### <a name="install-the-gateway-from-download-center"></a><span data-ttu-id="8337f-186">Installeer de gateway van Downloadcentrum</span><span class="sxs-lookup"><span data-stu-id="8337f-186">Install the gateway from download center</span></span>
1. <span data-ttu-id="8337f-187">Navigeer naar [Microsoft Data Management Gateway-downloadpagina](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="8337f-187">Navigate to [Microsoft Data Management Gateway download page](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>
2. <span data-ttu-id="8337f-188">Klik op **downloaden**, selecteer de juiste versie (**32-bits** vs. **64-bits**), en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8337f-188">Click **Download**, select the appropriate version (**32-bit** vs. **64-bit**), and click **Next**.</span></span>
3. <span data-ttu-id="8337f-189">Voer de **MSI** rechtstreeks of sla het op uw harde schijf en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8337f-189">Run the **MSI** directly or save it to your hard disk and run.</span></span>
4. <span data-ttu-id="8337f-190">Op de **Welkom** pagina een **taal** klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8337f-190">On the **Welcome** page, select a **language** click **Next**.</span></span>
5. <span data-ttu-id="8337f-191">**Accepteer** de gebruiksrechtovereenkomst en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8337f-191">**Accept** the End-User License Agreement and click **Next**.</span></span>
6. <span data-ttu-id="8337f-192">Selecteer **map** installeren van de gateway en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8337f-192">Select **folder** to install the gateway and click **Next**.</span></span>
7. <span data-ttu-id="8337f-193">Op de **gereed voor installatie** pagina, klikt u op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="8337f-193">On the **Ready to install** page, click **Install**.</span></span>
8. <span data-ttu-id="8337f-194">Klik op **voltooien** om installatie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="8337f-194">Click **Finish** to complete installation.</span></span>
9. <span data-ttu-id="8337f-195">De sleutel ophalen van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8337f-195">Get the key from the Azure portal.</span></span> <span data-ttu-id="8337f-196">Zie de volgende sectie voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="8337f-196">See the next section for step-by-step instructions.</span></span>
10. <span data-ttu-id="8337f-197">Op de **gateway registreren** pagina van **Data Management Gateway Configuration Manager** op uw computer de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8337f-197">On the **Register gateway** page of **Data Management Gateway Configuration Manager** running on your machine, do the following steps:</span></span>
    1. <span data-ttu-id="8337f-198">De sleutel in de tekst te plakken.</span><span class="sxs-lookup"><span data-stu-id="8337f-198">Paste the key in the text.</span></span>
    2. <span data-ttu-id="8337f-199">Klik desgewenst op **gatewaycode weergeven** om te zien van de belangrijkste tekst.</span><span class="sxs-lookup"><span data-stu-id="8337f-199">Optionally, click **Show gateway key** to see the key text.</span></span>
    3. <span data-ttu-id="8337f-200">Klik op **registreren**.</span><span class="sxs-lookup"><span data-stu-id="8337f-200">Click **Register**.</span></span>

### <a name="register-gateway-using-key"></a><span data-ttu-id="8337f-201">Registreer gateway met sleutel</span><span class="sxs-lookup"><span data-stu-id="8337f-201">Register gateway using key</span></span>
#### <a name="if-you-havent-already-created-a-logical-gateway-in-the-portal"></a><span data-ttu-id="8337f-202">Als u een logische gateway al hebt gemaakt in de portal</span><span class="sxs-lookup"><span data-stu-id="8337f-202">If you haven't already created a logical gateway in the portal</span></span>
<span data-ttu-id="8337f-203">Als u wilt maken van een gateway in de portal en de sleutel van de **configureren** pagina, volg de stappen van de procedures in de [gegevens verplaatsen tussen on-premises en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="8337f-203">To create a gateway in the portal and get the key from the **Configure** page, Follow steps from walkthrough in the [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>    

#### <a name="if-you-have-already-created-the-logical-gateway-in-the-portal"></a><span data-ttu-id="8337f-204">Als u de logische gateway al hebt gemaakt in de portal</span><span class="sxs-lookup"><span data-stu-id="8337f-204">If you have already created the logical gateway in the portal</span></span>
1. <span data-ttu-id="8337f-205">Navigeer in Azure portal naar de **Data Factory** pagina en klik op **gekoppelde Services** tegel.</span><span class="sxs-lookup"><span data-stu-id="8337f-205">In Azure portal, navigate to the **Data Factory** page, and click **Linked Services** tile.</span></span>

    ![Data Factory-pagina](media/data-factory-data-management-gateway/data-factory-blade.png)
2. <span data-ttu-id="8337f-207">In de **gekoppelde Services** pagina, selecteert u de logische **gateway** in de portal worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8337f-207">In the **Linked Services** page, select the logical **gateway** you created in the portal.</span></span>

    ![logische gateway](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. <span data-ttu-id="8337f-209">In de **Data Gateway** pagina, klikt u op **downloaden en installeren van de gegevensgateway**.</span><span class="sxs-lookup"><span data-stu-id="8337f-209">In the **Data Gateway** page, click **Download and install data gateway**.</span></span>

    ![Download de koppeling in de portal](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. <span data-ttu-id="8337f-211">In de **configureren** pagina, klikt u op **Maak sleutel**.</span><span class="sxs-lookup"><span data-stu-id="8337f-211">In the **Configure** page, click **Recreate key**.</span></span> <span data-ttu-id="8337f-212">Klik op Ja in het waarschuwingsbericht staan aangegeven na het lezen van deze zorgvuldig.</span><span class="sxs-lookup"><span data-stu-id="8337f-212">Click Yes on the warning message after reading it carefully.</span></span>

    ![Sleutel opnieuw maken](media/data-factory-data-management-gateway/recreate-key-button.png)
5. <span data-ttu-id="8337f-214">Klik op de knop kopiëren naast de sleutel.</span><span class="sxs-lookup"><span data-stu-id="8337f-214">Click Copy button next to the key.</span></span> <span data-ttu-id="8337f-215">De sleutel wordt gekopieerd naar het Klembord.</span><span class="sxs-lookup"><span data-stu-id="8337f-215">The key is copied to the clipboard.</span></span>

    ![Kopieer sleutel](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a><span data-ttu-id="8337f-217">Pictogrammen in systeemvak / meldingen</span><span class="sxs-lookup"><span data-stu-id="8337f-217">System tray icons/ notifications</span></span>
<span data-ttu-id="8337f-218">De volgende afbeelding ziet u enkele van de pictogrammen in systeemvak die u ziet.</span><span class="sxs-lookup"><span data-stu-id="8337f-218">The following image shows some of the tray icons that you see.</span></span>

![pictogrammen in systeemvak](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

<span data-ttu-id="8337f-220">Als u de cursor op het systeem/Meldingsbericht voor een pictogram systeemvak plaatst, ziet u details over de status van de gateway updatebewerking in een pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="8337f-220">If you move cursor over the system tray icon/notification message, you see details about the state of the gateway/update operation in a popup window.</span></span>

### <a name="ports-and-firewall"></a><span data-ttu-id="8337f-221">Poorten en firewall</span><span class="sxs-lookup"><span data-stu-id="8337f-221">Ports and firewall</span></span>
<span data-ttu-id="8337f-222">Er zijn twee firewalls, moet u rekening houden: **bedrijfsfirewall** uitgevoerd op de centrale router van de organisatie en **Windows firewall** geconfigureerd als een daemon op de lokale computer waarop de gateway is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8337f-222">There are two firewalls you need to consider: **corporate firewall** running on the central router of the organization, and **Windows firewall** configured as a daemon on the local machine where the gateway is installed.</span></span>  

![firewalls](./media/data-factory-data-management-gateway/firewalls2.png)

<span data-ttu-id="8337f-224">Op het niveau van de firewall van het bedrijf, moet u de volgende domeinen en uitgaande poorten configureren:</span><span class="sxs-lookup"><span data-stu-id="8337f-224">At corporate firewall level, you need configure the following domains and outbound ports:</span></span>

| <span data-ttu-id="8337f-225">Domeinnamen</span><span class="sxs-lookup"><span data-stu-id="8337f-225">Domain names</span></span> | <span data-ttu-id="8337f-226">Poorten</span><span class="sxs-lookup"><span data-stu-id="8337f-226">Ports</span></span> | <span data-ttu-id="8337f-227">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8337f-227">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8337f-228">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="8337f-228">*.servicebus.windows.net</span></span> |<span data-ttu-id="8337f-229">443, 80</span><span class="sxs-lookup"><span data-stu-id="8337f-229">443, 80</span></span> |<span data-ttu-id="8337f-230">Gebruikt voor communicatie met Data Movement Service back-end</span><span class="sxs-lookup"><span data-stu-id="8337f-230">Used for communication with Data Movement Service backend</span></span> |
| <span data-ttu-id="8337f-231">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="8337f-231">*.core.windows.net</span></span> |<span data-ttu-id="8337f-232">443</span><span class="sxs-lookup"><span data-stu-id="8337f-232">443</span></span> |<span data-ttu-id="8337f-233">Gebruikt voor de tijdelijke kopie met behulp van Azure-Blob (indien geconfigureerd)</span><span class="sxs-lookup"><span data-stu-id="8337f-233">Used for Staged copy using Azure Blob (if configured)</span></span>|
| <span data-ttu-id="8337f-234">*. frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="8337f-234">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="8337f-235">443</span><span class="sxs-lookup"><span data-stu-id="8337f-235">443</span></span> |<span data-ttu-id="8337f-236">Gebruikt voor communicatie met Data Movement Service back-end</span><span class="sxs-lookup"><span data-stu-id="8337f-236">Used for communication with Data Movement Service backend</span></span> |


<span data-ttu-id="8337f-237">Deze uitgaande poorten zijn normaal gesproken op niveau van Windows firewall is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8337f-237">At Windows firewall level, these outbound ports are normally enabled.</span></span> <span data-ttu-id="8337f-238">Als u niet het geval is, kunt u de domeinen en poorten dienovereenkomstig op gateway-apparaat.</span><span class="sxs-lookup"><span data-stu-id="8337f-238">If not, you can configure the domains and ports accordingly on gateway machine.</span></span>

> [!NOTE]
> 1. <span data-ttu-id="8337f-239">Op basis van de bron / put u wellicht aanvullende domeinen van goedgekeurde IP-adressen en uitgaande poorten in uw zakelijke/Windows firewall.</span><span class="sxs-lookup"><span data-stu-id="8337f-239">Based on your source/ sinks, you may have to whitelist additional domains and outbound ports in your corporate/Windows firewall.</span></span>
> 2. <span data-ttu-id="8337f-240">Voor sommige Databases van de Cloud (bijvoorbeeld: [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), enzovoort), mogelijk moet u geaccepteerde IP-adres van de computer met de Gateway op de firewallconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="8337f-240">For some Cloud Databases (For example: [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), you may need to whitelist IP address of Gateway machine on their firewall configuration.</span></span>
>
>


#### <a name="copy-data-from-a-source-data-store-to-a-sink-data-store"></a><span data-ttu-id="8337f-241">Gegevens kopiëren van een brongegevensarchief naar een gegevensarchief sink</span><span class="sxs-lookup"><span data-stu-id="8337f-241">Copy data from a source data store to a sink data store</span></span>
<span data-ttu-id="8337f-242">Zorg ervoor dat de firewallregels correct zijn ingeschakeld op de firewall van het bedrijf, Windows firewall op de gatewaycomputer en opslaan van de gegevens zelf.</span><span class="sxs-lookup"><span data-stu-id="8337f-242">Ensure that the firewall rules are enabled properly on the corporate firewall, Windows firewall on the gateway machine, and the data store itself.</span></span> <span data-ttu-id="8337f-243">Inschakelen van deze regels kunt de gateway verbinding maken met zowel bron en sink is.</span><span class="sxs-lookup"><span data-stu-id="8337f-243">Enabling these rules allows the gateway to connect to both source and sink successfully.</span></span> <span data-ttu-id="8337f-244">Schakel regels voor elke gegevensopslag die bij de kopieerbewerking betrokken is.</span><span class="sxs-lookup"><span data-stu-id="8337f-244">Enable rules for each data store that is involved in the copy operation.</span></span>

<span data-ttu-id="8337f-245">Bijvoorbeeld: voor het kopiëren van **een on-premises gegevensopslag een sink Azure SQL Database of een Azure SQL Data Warehouse sink**, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8337f-245">For example, to copy from **an on-premises data store to an Azure SQL Database sink or an Azure SQL Data Warehouse sink**, do the following steps:</span></span>

* <span data-ttu-id="8337f-246">Uitgaand verkeer toestaan **TCP** -communicatie op poort **1433** voor Windows firewall- en firewall van het bedrijf.</span><span class="sxs-lookup"><span data-stu-id="8337f-246">Allow outbound **TCP** communication on port **1433** for both Windows firewall and corporate firewall.</span></span>
* <span data-ttu-id="8337f-247">Configureer de firewallinstellingen van Azure SQL-server om toe te voegen van de IP-adres van het gateway-apparaat aan de lijst met toegestane IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="8337f-247">Configure the firewall settings of Azure SQL server to add the IP address of the gateway machine to the list of allowed IP addresses.</span></span>

> [!NOTE]
> <span data-ttu-id="8337f-248">Als uw firewall kan geen uitgaande poort 1433, Gateway kan niet rechtstreeks toegang hebben tot Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="8337f-248">If your firewall does not allow outbound port 1433, Gateway can't access Azure SQL directly.</span></span> <span data-ttu-id="8337f-249">U kunt in dit geval [kopie gefaseerde](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) naar Azure SQL Database / SQL Azure DW.</span><span class="sxs-lookup"><span data-stu-id="8337f-249">In this case, you may use [Staged Copy](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) to SQL Azure Database/ SQL Azure DW.</span></span> <span data-ttu-id="8337f-250">In dit scenario zou u alleen HTTPS (poort 443) nodig voor de verplaatsing van gegevens.</span><span class="sxs-lookup"><span data-stu-id="8337f-250">In this scenario, you would only require HTTPS (port 443) for the data movement.</span></span>
>
>


### <a name="proxy-server-considerations"></a><span data-ttu-id="8337f-251">Overwegingen voor proxy-server</span><span class="sxs-lookup"><span data-stu-id="8337f-251">Proxy server considerations</span></span>
<span data-ttu-id="8337f-252">Als uw zakelijke netwerkomgeving een proxyserver gebruikt voor toegang tot het internet, configureert u de data management gateway voor het gebruik van de juiste proxy-instellingen.</span><span class="sxs-lookup"><span data-stu-id="8337f-252">If your corporate network environment uses a proxy server to access the internet, configure data management gateway to use appropriate proxy settings.</span></span> <span data-ttu-id="8337f-253">U kunt de proxy instellen tijdens de registratie van de eerste fase.</span><span class="sxs-lookup"><span data-stu-id="8337f-253">You can set the proxy during the initial registration phase.</span></span>

![Set-proxy tijdens de registratie](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

<span data-ttu-id="8337f-255">De proxyserver gateway gebruikt om verbinding met de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="8337f-255">Gateway uses the proxy server to connect to the cloud service.</span></span> <span data-ttu-id="8337f-256">Klik op **wijziging** koppeling tijdens de eerste configuratie.</span><span class="sxs-lookup"><span data-stu-id="8337f-256">Click **Change** link during initial setup.</span></span> <span data-ttu-id="8337f-257">U ziet de **proxyinstelling** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8337f-257">You see the **proxy setting** dialog.</span></span>

![Set-proxy met Configuratiebeheer](media/data-factory-data-management-gateway/SetProxySettings.png)

<span data-ttu-id="8337f-259">Er zijn drie opties:</span><span class="sxs-lookup"><span data-stu-id="8337f-259">There are three configuration options:</span></span>

* <span data-ttu-id="8337f-260">**Gebruik geen proxy**: Gateway expliciet gebruikt geen elke proxy verbinding maken met cloudservices.</span><span class="sxs-lookup"><span data-stu-id="8337f-260">**Do not use proxy**: Gateway does not explicitly use any proxy to connect to cloud services.</span></span>
* <span data-ttu-id="8337f-261">**Gebruik system proxy**: Gateway maakt gebruik van de proxy-instelling is geconfigureerd in diahost.exe.config en diawp.exe.config.  Als geen proxy is geconfigureerd in diahost.exe.config en diawp.exe.config, gateway wordt verbonden met cloudservice rechtstreeks zonder gebruik te maken via proxy.</span><span class="sxs-lookup"><span data-stu-id="8337f-261">**Use system proxy**: Gateway uses the proxy setting that is configured in diahost.exe.config and diawp.exe.config.  If no proxy is configured in diahost.exe.config and diawp.exe.config, gateway connects to cloud service directly without going through proxy.</span></span>
* <span data-ttu-id="8337f-262">**Aangepaste proxy gebruikt**: de HTTP-proxy-instellingen te gebruiken voor de gateway in plaats van configuraties in diahost.exe.config en diawp.exe.config configureren.  Adres en poort zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="8337f-262">**Use custom proxy**: Configure the HTTP proxy setting to use for gateway, instead of using configurations in diahost.exe.config and diawp.exe.config.  Address and Port are required.</span></span>  <span data-ttu-id="8337f-263">Gebruikersnaam en wachtwoord zijn optioneel, afhankelijk van uw proxyserver verificatie-instelling.</span><span class="sxs-lookup"><span data-stu-id="8337f-263">User Name and Password are optional depending on your proxy’s authentication setting.</span></span>  <span data-ttu-id="8337f-264">Alle instellingen zijn versleuteld met de referenties van het certificaat van de gateway en die lokaal zijn opgeslagen op de hostcomputer van de gateway.</span><span class="sxs-lookup"><span data-stu-id="8337f-264">All settings are encrypted with the credential certificate of the gateway and stored locally on the gateway host machine.</span></span>

<span data-ttu-id="8337f-265">Data management gateway Host Service wordt automatisch opnieuw opgestart nadat u de bijgewerkte proxy-instellingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="8337f-265">The data management gateway Host Service restarts automatically after you save the updated proxy settings.</span></span>

<span data-ttu-id="8337f-266">Nadat de gateway is geregistreerd, als u wilt weergeven of bijwerken van proxy-instellingen, gebruikt u Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="8337f-266">After gateway has been successfully registered, if you want to view or update proxy settings, use Data Management Gateway Configuration Manager.</span></span>

1. <span data-ttu-id="8337f-267">Start **Data Management Gateway Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="8337f-267">Launch **Data Management Gateway Configuration Manager**.</span></span>
2. <span data-ttu-id="8337f-268">Overschakelen naar de **instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="8337f-268">Switch to the **Settings** tab.</span></span>
3. <span data-ttu-id="8337f-269">Klik op **wijziging** koppelen **HTTP-Proxy** sectie starten de **Set HTTP-Proxy** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8337f-269">Click **Change** link in **HTTP Proxy** section to launch the **Set HTTP Proxy** dialog.</span></span>  
4. <span data-ttu-id="8337f-270">Nadat u op de **volgende** knop klikt, ziet u een waarschuwingsdialoogvenster waarin wordt gevraagd uw toestemming voor het opslaan van de proxy-instelling en start de Gateway-hostservice opnieuw op.</span><span class="sxs-lookup"><span data-stu-id="8337f-270">After you click the **Next** button, you see a warning dialog asking for your permission to save the proxy setting and restart the Gateway Host Service.</span></span>

<span data-ttu-id="8337f-271">U kunt weergeven en bijwerken van HTTP-proxy met behulp van Configuration Manager-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="8337f-271">You can view and update HTTP proxy by using Configuration Manager tool.</span></span>

![Set-proxy met Configuratiebeheer](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> <span data-ttu-id="8337f-273">Als u een proxyserver met NTLM-verificatie hebt ingesteld, is Gateway Host Service wordt uitgevoerd onder het domeinaccount.</span><span class="sxs-lookup"><span data-stu-id="8337f-273">If you set up a proxy server with NTLM authentication, Gateway Host Service runs under the domain account.</span></span> <span data-ttu-id="8337f-274">Als u het wachtwoord voor het domeinaccount later wijzigt, moet u configuratie-instellingen voor de service bijwerken en dienovereenkomstig aan het programma opnieuw.</span><span class="sxs-lookup"><span data-stu-id="8337f-274">If you change the password for the domain account later, remember to update configuration settings for the service and restart it accordingly.</span></span> <span data-ttu-id="8337f-275">Vanwege deze vereiste raden we dat u een specifiek domeinaccount gebruiken voor toegang tot de proxyserver die vereist niet dat u het wachtwoord regelmatig bijwerken.</span><span class="sxs-lookup"><span data-stu-id="8337f-275">Due to this requirement, we suggest you use a dedicated domain account to access the proxy server that does not require you to update the password frequently.</span></span>
>
>

### <a name="configure-proxy-server-settings"></a><span data-ttu-id="8337f-276">Proxyserverinstellingen configureren</span><span class="sxs-lookup"><span data-stu-id="8337f-276">Configure proxy server settings</span></span>
<span data-ttu-id="8337f-277">Als u selecteert **system proxy gebruiken** instellen voor de HTTP-proxy, gateway maakt gebruik van de proxy-instelling in diahost.exe.config en diawp.exe.config.  Als er geen proxyserver is opgegeven in diahost.exe.config en diawp.exe.config, gateway wordt verbonden met cloudservice rechtstreeks zonder gebruik te maken via proxy.</span><span class="sxs-lookup"><span data-stu-id="8337f-277">If you select **Use system proxy** setting for the HTTP proxy, gateway uses the proxy setting in diahost.exe.config and diawp.exe.config.  If no proxy is specified in diahost.exe.config and diawp.exe.config, gateway connects to cloud service directly without going through proxy.</span></span> <span data-ttu-id="8337f-278">De volgende procedure bevat instructies voor het bijwerken van het bestand diahost.exe.config.</span><span class="sxs-lookup"><span data-stu-id="8337f-278">The following procedure provides instructions for updating the diahost.exe.config file.</span></span>  

1. <span data-ttu-id="8337f-279">Maak een veilige kopie van C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config back-up van het oorspronkelijke bestand in Verkenner.</span><span class="sxs-lookup"><span data-stu-id="8337f-279">In File Explorer, make a safe copy of C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config to back up the original file.</span></span>
2. <span data-ttu-id="8337f-280">Starten van Notepad.exe uitgevoerd als administrator en open tekstbestand "C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. U kunt het standaardlabel voor system.net vinden zoals weergegeven in de volgende code:</span><span class="sxs-lookup"><span data-stu-id="8337f-280">Launch Notepad.exe running as administrator, and open text file “C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. You find the default tag for system.net as shown in the following code:</span></span>

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   <span data-ttu-id="8337f-281">Vervolgens kunt u proxy-servergegevens toevoegen, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8337f-281">You can then add proxy server details as shown in the following example:</span></span>

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   <span data-ttu-id="8337f-282">Aanvullende eigenschappen zijn toegestaan in de tag proxy om op te geven van de vereiste instellingen zoals scriptLocation.</span><span class="sxs-lookup"><span data-stu-id="8337f-282">Additional properties are allowed inside the proxy tag to specify the required settings like scriptLocation.</span></span> <span data-ttu-id="8337f-283">Raadpleeg [proxy Element (netwerkinstellingen)](https://msdn.microsoft.com/library/sa91de1e.aspx) op syntaxis.</span><span class="sxs-lookup"><span data-stu-id="8337f-283">Refer to [proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on syntax.</span></span>

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. <span data-ttu-id="8337f-284">Start de Data Management Gateway Host service, die de wijzigingen neemt vervolgens het configuratiebestand in de oorspronkelijke locatie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="8337f-284">Save the configuration file into the original location, then restart the Data Management Gateway Host service, which picks up the changes.</span></span> <span data-ttu-id="8337f-285">De service te starten: Gebruik de applet services in het Configuratiescherm, of vanuit de **Data Management Gateway Configuration Manager** > Klik op de **Service stoppen** knop en klik vervolgens op de **Service starten**.</span><span class="sxs-lookup"><span data-stu-id="8337f-285">To restart the service: use services applet from the control panel, or from the **Data Management Gateway Configuration Manager** > click the **Stop Service** button, then click the **Start Service**.</span></span> <span data-ttu-id="8337f-286">Als de service niet wordt gestart, is het waarschijnlijk dat er een onjuiste syntaxis van de XML-label is toegevoegd in het toepassingsconfiguratiebestand die is bewerkt.</span><span class="sxs-lookup"><span data-stu-id="8337f-286">If the service does not start, it is likely that an incorrect XML tag syntax has been added into the application configuration file that was edited.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8337f-287">Vergeet niet om bij te werken **beide** diahost.exe.config en diawp.exe.config.</span><span class="sxs-lookup"><span data-stu-id="8337f-287">Do not forget to update **both** diahost.exe.config and diawp.exe.config.</span></span>  


<span data-ttu-id="8337f-288">Naast deze punten moet u ook om te controleren of Microsoft Azure in goedgekeurde lijst van uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="8337f-288">In addition to these points, you also need to make sure Microsoft Azure is in your company’s whitelist.</span></span> <span data-ttu-id="8337f-289">De lijst met geldige Microsoft Azure-IP-adressen kan worden gedownload vanuit de [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="8337f-289">The list of valid Microsoft Azure IP addresses can be downloaded from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a><span data-ttu-id="8337f-290">Mogelijke problemen voor firewall en proxy server-problemen</span><span class="sxs-lookup"><span data-stu-id="8337f-290">Possible symptoms for firewall and proxy server-related issues</span></span>
<span data-ttu-id="8337f-291">Als u fouten overeen met de volgende procedures optreden, is het waarschijnlijk door onjuiste configuratie van de firewall of proxyserver server gateway verbinding maken met de Data Factory blokkeert zichzelf verifiëren.</span><span class="sxs-lookup"><span data-stu-id="8337f-291">If you encounter errors similar to the following ones, it is likely due to improper configuration of the firewall or proxy server, which blocks gateway from connecting to Data Factory to authenticate itself.</span></span> <span data-ttu-id="8337f-292">Raadpleeg de vorige sectie om te controleren of uw firewall en proxy-server correct zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8337f-292">Refer to previous section to ensure your firewall and proxy server are properly configured.</span></span>

1. <span data-ttu-id="8337f-293">Wanneer u probeert om de gateway te registreren, wordt de volgende fout: 'kan niet de gatewaycode registreren.</span><span class="sxs-lookup"><span data-stu-id="8337f-293">When you try to register the gateway, you receive the following error: "Failed to register the gateway key.</span></span> <span data-ttu-id="8337f-294">Voordat u probeert de gatewaycode opnieuw registreren, Controleer of de data management gateway verbonden is en Data Management Gateway Host Service wordt gestart."</span><span class="sxs-lookup"><span data-stu-id="8337f-294">Before trying to register the gateway key again, confirm that the data management gateway is in a connected state and the Data Management Gateway Host Service is Started."</span></span>
2. <span data-ttu-id="8337f-295">Wanneer u Configuration Manager opent, ziet u status als 'Verbinding verbroken' of "Verbinden."</span><span class="sxs-lookup"><span data-stu-id="8337f-295">When you open Configuration Manager, you see status as “Disconnected” or “Connecting.”</span></span> <span data-ttu-id="8337f-296">Tijdens het weergeven van Windows-gebeurtenislogboeken onder 'Logboeken' > 'Toepassingen en Services Logs' > 'Data Management Gateway', ziet u foutberichten, zoals de volgende fout:`Unable to connect to the remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span><span class="sxs-lookup"><span data-stu-id="8337f-296">When viewing Windows event logs, under “Event Viewer” > “Application and Services Logs” > “Data Management Gateway”, you see error messages such as the following error: `Unable to connect to the remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span></span>

### <a name="open-port-8050-for-credential-encryption"></a><span data-ttu-id="8337f-297">Open poort 8050 voor referentieversleuteling.</span><span class="sxs-lookup"><span data-stu-id="8337f-297">Open port 8050 for credential encryption</span></span>
<span data-ttu-id="8337f-298">De **instelling referenties** toepassing gebruikmaakt van de binnenkomende poort **8050** relay referenties naar de gateway bij het instellen van een lokaal gekoppelde service in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8337f-298">The **Setting Credentials** application uses the inbound port **8050** to relay credentials to the gateway when you set up an on-premises linked service in the Azure portal.</span></span> <span data-ttu-id="8337f-299">Tijdens de installatie van de gateway wordt standaard de installatie van de gateway geopend op de gateway-apparaat.</span><span class="sxs-lookup"><span data-stu-id="8337f-299">During gateway setup, by default, the gateway installation opens it on the gateway machine.</span></span>

<span data-ttu-id="8337f-300">Als u een firewall van derden gebruikt, kunt u handmatig de poort 8050 openen.</span><span class="sxs-lookup"><span data-stu-id="8337f-300">If you are using a third-party firewall, you can manually open the port 8050.</span></span> <span data-ttu-id="8337f-301">Als u in de firewallprobleem tijdens de gatewayinstallatie uitvoert, kunt u proberen met de volgende opdracht voor het installeren van de gateway zonder het configureren van de firewall.</span><span class="sxs-lookup"><span data-stu-id="8337f-301">If you run into firewall issue during gateway setup, you can try using the following command to install the gateway without configuring the firewall.</span></span>

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

<span data-ttu-id="8337f-302">Als u niet de poort te openen 8050 op de gatewaycomputer, gebruikgemaakt van mechanismen dan met behulp van de **instelling referenties** toepassing voor het configureren van referenties voor gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="8337f-302">If you choose not to open the port 8050 on the gateway machine, use mechanisms other than using the **Setting Credentials** application to configure data store credentials.</span></span> <span data-ttu-id="8337f-303">U kunt bijvoorbeeld [nieuw AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8337f-303">For example, you could use [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="8337f-304">Zie [instelling referenties en beveiliging](#set-credentials-and-securityy) sectie op hoe de referenties voor het opslaan van gegevens kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8337f-304">See [Setting Credentials and Security](#set-credentials-and-securityy) section on how data store credentials can be set.</span></span>

## <a name="update"></a><span data-ttu-id="8337f-305">Update</span><span class="sxs-lookup"><span data-stu-id="8337f-305">Update</span></span>
<span data-ttu-id="8337f-306">Data management gateway wordt standaard automatisch bijgewerkt wanneer een nieuwere versie van de gateway beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="8337f-306">By default, data management gateway is automatically updated when a newer version of the gateway is available.</span></span> <span data-ttu-id="8337f-307">De gateway is niet bijgewerkt tot de geplande taken kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8337f-307">The gateway is not updated until all the scheduled tasks are done.</span></span> <span data-ttu-id="8337f-308">Geen verdere taken worden verwerkt door de gateway, totdat de updatebewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="8337f-308">No further tasks are processed by the gateway until the update operation is completed.</span></span> <span data-ttu-id="8337f-309">Als de update is mislukt, is gateway teruggedraaid naar de oude versie.</span><span class="sxs-lookup"><span data-stu-id="8337f-309">If the update fails, gateway is rolled back to the old version.</span></span>

<span data-ttu-id="8337f-310">De geplande updatetijd ziet u in de volgende locaties:</span><span class="sxs-lookup"><span data-stu-id="8337f-310">You see the scheduled update time in the following places:</span></span>

* <span data-ttu-id="8337f-311">De eigenschappenpagina van de gateway in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8337f-311">The gateway properties page in the Azure portal.</span></span>
* <span data-ttu-id="8337f-312">Startpagina van de Data Management Gateway Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="8337f-312">Home page of the Data Management Gateway Configuration Manager</span></span>
* <span data-ttu-id="8337f-313">Melding voor systeem-systeemvak.</span><span class="sxs-lookup"><span data-stu-id="8337f-313">System tray notification message.</span></span>

<span data-ttu-id="8337f-314">Het tabblad Start van de Data Management Gateway Configuration Manager geeft de updateplanning en de laatste keer dat de gateway is geïnstalleerd/bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="8337f-314">The Home tab of the Data Management Gateway Configuration Manager displays the update schedule and the last time the gateway was installed/updated.</span></span>

![Updates plannen](media/data-factory-data-management-gateway/UpdateSection.png)

<span data-ttu-id="8337f-316">U kunt de update onmiddellijk te installeren of wacht u totdat de gateway worden automatisch bijgewerkt op het geplande tijdstip.</span><span class="sxs-lookup"><span data-stu-id="8337f-316">You can install the update right away or wait for the gateway to be automatically updated at the scheduled time.</span></span> <span data-ttu-id="8337f-317">Bijvoorbeeld de volgende afbeelding ziet u de melding wordt weergegeven in de Gateway Configuration Manager samen met de knop bijwerken waarop u klikken kunt om onmiddellijk te installeren.</span><span class="sxs-lookup"><span data-stu-id="8337f-317">For example, the following image shows you the notification message shown in the Gateway Configuration Manager along with the Update button that you can click to install it immediately.</span></span>

![Update in DMG Configuration Manager](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

<span data-ttu-id="8337f-319">Het meldingsbericht in het systeemvak eruit zoals weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="8337f-319">The notification message in the system tray would look as shown in the following image:</span></span>

![Systeemvak systeembericht](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

<span data-ttu-id="8337f-321">U ziet de status van updatebewerking (handmatig of automatisch) in het systeemvak.</span><span class="sxs-lookup"><span data-stu-id="8337f-321">You see the status of update operation (manual or automatic) in the system tray.</span></span> <span data-ttu-id="8337f-322">Als u Gateway Configuration Manager volgende keer start, ziet u een bericht op de meldingsbalk dat samen met een koppeling naar de gateway is bijgewerkt [wat is er nieuw onderwerp](data-factory-gateway-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="8337f-322">When you launch Gateway Configuration Manager next time, you see a message on the notification bar that the gateway has been updated along with a link to [what's new topic](data-factory-gateway-release-notes.md).</span></span>

### <a name="to-disableenable-auto-update-feature"></a><span data-ttu-id="8337f-323">Aan de functie voor automatisch bijwerken inschakelen/uitschakelen</span><span class="sxs-lookup"><span data-stu-id="8337f-323">To disable/enable auto-update feature</span></span>
<span data-ttu-id="8337f-324">U kunt inschakelen/uitschakelen de functie voor automatisch bijwerken door de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="8337f-324">You can disable/enable the auto-update feature by doing the following steps:</span></span>

<span data-ttu-id="8337f-325">[Voor één knooppunt gateway]</span><span class="sxs-lookup"><span data-stu-id="8337f-325">[For single node gateway]</span></span>
1. <span data-ttu-id="8337f-326">Start Windows PowerShell op de gateway-apparaat.</span><span class="sxs-lookup"><span data-stu-id="8337f-326">Launch Windows PowerShell on the gateway machine.</span></span>
2. <span data-ttu-id="8337f-327">Ga naar de map C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript.</span><span class="sxs-lookup"><span data-stu-id="8337f-327">Switch to the C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="8337f-328">Voer de volgende opdracht om de automatische updates inschakelen functie uit te schakelen.</span><span class="sxs-lookup"><span data-stu-id="8337f-328">Run the following command to turn the auto-update feature OFF (disable).</span></span>   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. <span data-ttu-id="8337f-329">Aan deze weer inschakelen:</span><span class="sxs-lookup"><span data-stu-id="8337f-329">To turn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
<span data-ttu-id="8337f-330">[[Voor meerdere knooppunten maximaal beschikbare en schaalbare gateway (preview)](data-factory-data-management-gateway-high-availability-scalability.md)]</span><span class="sxs-lookup"><span data-stu-id="8337f-330">[[For multi-node highly available and scalable gateway (preview)](data-factory-data-management-gateway-high-availability-scalability.md)]</span></span>
1. <span data-ttu-id="8337f-331">Start Windows PowerShell op de gateway-apparaat.</span><span class="sxs-lookup"><span data-stu-id="8337f-331">Launch Windows PowerShell on the gateway machine.</span></span>
2. <span data-ttu-id="8337f-332">Ga naar de map C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript.</span><span class="sxs-lookup"><span data-stu-id="8337f-332">Switch to the C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="8337f-333">Voer de volgende opdracht om de automatische updates inschakelen functie uit te schakelen.</span><span class="sxs-lookup"><span data-stu-id="8337f-333">Run the following command to turn the auto-update feature OFF (disable).</span></span>   

    <span data-ttu-id="8337f-334">Een extra AuthKey param is vereist voor de gateway met hoge beschikbaarheid-functie (preview).</span><span class="sxs-lookup"><span data-stu-id="8337f-334">For gateway with high availability feature (preview), an extra AuthKey param is required.</span></span>
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. <span data-ttu-id="8337f-335">Aan deze weer inschakelen:</span><span class="sxs-lookup"><span data-stu-id="8337f-335">To turn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install the gateway, you can launch Data Management Gateway Configuration Manager in one of the following ways:

1. In the **Search** window, type **Data Management Gateway** to access this utility.
2. Run the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
The Home page allows you to do the following actions:

* View status of the gateway (connected to the cloud service etc.).
* **Register** using a key from the portal.
* **Stop** and start the **Data Management Gateway Host service** on the gateway machine.
* **Schedule updates** at a specific time of the days.
* View the date when the gateway was **last updated**.

### Settings page
The Settings page allows you to do the following actions:

* View, change, and export **certificate** used by the gateway. This certificate is used to encrypt data source credentials.
* Change **HTTPS port** for the endpoint. The gateway opens a port for setting the data source credentials.
* **Status** of the endpoint
* View **SSL certificate** is used for SSL communication between portal and the gateway to set credentials for data sources.  

### Diagnostics page
The Diagnostics page allows you to do the following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs to Microsoft if there was a failure.
* **Test connection** to a data source.  

### Help page
The Help page displays the following information:  

* Brief description of the gateway
* Version number
* Links to online help, privacy statement, and license agreement.  

## Monitor gateway in the portal
In the Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate to the home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select the **gateway** in the **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In the **Gateway** page, you can see the memory and CPU usage of the gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** to see more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

The following table provides descriptions of columns in the **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of the logical gateway and nodes associated with the gateway. Node is an on-premises Windows machine that has the gateway installed on it. For information on having more than one node (up to four nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of the logical gateway and the gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows the version of the logical gateway and each gateway node. The version of the logical gateway is determined based on version of majority of nodes in the group. If there are nodes with different versions in the logical gateway setup, only the nodes with the same version number as the logical gateway function properly. Others are in the limited mode and need to be manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies the maximum concurrent jobs for each node. This value is defined based on the machine size. You can increase the limit to scale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when the scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used to execute jobs. There is only one dispatcher node, which is used to pull tasks/jobs from cloud services and dispatch them to different worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in the gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
The following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected to Data Factory service.
Offline | Node is offline.
Upgrading | The node is being auto-updated.
Limited | Due to Connectivity issue. May be due to HTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from the configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect to other nodes. 


The following table provides possible statuses of a **logical gateway**. The gateway status depends on statuses of the gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered to this logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due to credential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure the number of **concurrent data movement jobs** that can run on a node to scale up the capability of moving data between on-premises and cloud data stores. 

When the available memory and CPU are not utilized well, but the idle capacity is 0, you should scale up by increasing the number of concurrent jobs that can run on a node. You may also want to scale up when activities are timing out because the gateway is overloaded. In the advanced settings of a gateway node, you can increase the maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using the data management gateway.  

## Move gateway from one machine to another
This section provides steps for moving gateway client from one machine to another machine.

1. In the portal, navigate to the **Data Factory home page**, and click the **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in the **DATA GATEWAYS** section of the **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In the **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In the **Configure** page, click **Download and install data gateway**, and follow instructions to install the data gateway on the machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep the **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In the **Configure** page in the portal, click **Recreate key** on the command bar, and click **Yes** for the warning message. Click **copy button** next to key text that copies the key to the clipboard. The gateway on the old machine stops functioning as soon you recreate the key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste the **key** into text box in the **Register Gateway** page of the **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box to see the key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** to register the gateway with the cloud service.
9. On the **Settings** tab, click **Change** to select the same certificate that was used with the old gateway, enter the **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from the old gateway by doing the following steps: launch Data Management Gateway Configuration Manager on the old machine, switch to the **Certificate** tab, click **Export** button and follow the instructions.
10. After successful registration of the gateway, you should see the **Registration** set to **Registered** and **Status** set to **Started** on the Home page of the Gateway Configuration Manager.

## Encrypting credentials
To encrypt credentials in the Data Factory Editor, do the following steps:

1. Launch web browser on the **gateway machine**, navigate to [Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in the **DATA FACTORY** page and then click **Author & Deploy** to launch Data Factory Editor.   
2. Click an existing **linked service** in the tree view to see its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In the JSON editor, for the **gatewayName** property, enter the name of the gateway.
4. Enter server name for the **Data Source** property in the **connectionString**.
5. Enter database name for the **Initial Catalog** property in the **connectionString**.    
6. Click **Encrypt** button on the command bar that launches the click-once **Credential Manager** application. You should see the **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In the **Setting Credentials** dialog box, do the following steps:
   1. Select **authentication** that you want the Data Factory service to use to connect to the database.
   2. Enter name of the user who has access to the database for the **USERNAME** setting.
   3. Enter password for the user for the **PASSWORD** setting.  
   4. Click **OK** to encrypt credentials and close the dialog box.
8. You should see a **encryptedCredential** property in the **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
<span data-ttu-id="8337f-336">Als u de portal vanaf een machine die verschilt van het gateway-apparaat openen, moet u ervoor zorgen dat de toepassing Referentiebeheer verbinding met de gateway-machine maken kan.</span><span class="sxs-lookup"><span data-stu-id="8337f-336">If you access the portal from a machine that is different from the gateway machine, you must make sure that the Credentials Manager application can connect to the gateway machine.</span></span> <span data-ttu-id="8337f-337">Als de toepassing niet kan van het gateway-apparaat bereiken, kunt niet u referenties voor de gegevensbron in te stellen en om verbinding met de gegevensbron te testen.</span><span class="sxs-lookup"><span data-stu-id="8337f-337">If the application cannot reach the gateway machine, it does not allow you to set credentials for the data source and to test connection to the data source.</span></span>  

<span data-ttu-id="8337f-338">Wanneer u gebruikt de **instelling referenties** toepassing, de portal versleutelt de referenties met het certificaat dat is opgegeven in de **certificaat** tabblad van de **Gateway Configuration Manager** op de gateway-apparaat.</span><span class="sxs-lookup"><span data-stu-id="8337f-338">When you use the **Setting Credentials** application, the portal encrypts the credentials with the certificate specified in the **Certificate** tab of the **Gateway Configuration Manager** on the gateway machine.</span></span>

<span data-ttu-id="8337f-339">Als u voor een API-gebaseerde methode voor het versleutelen van de referenties op zoek bent, kunt u de [nieuw AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell-cmdlet om referenties te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="8337f-339">If you are looking for an API-based approach for encrypting the credentials, you can use the [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet to encrypt credentials.</span></span> <span data-ttu-id="8337f-340">Het certificaat wordt gebruikt door de cmdlet die gateway is geconfigureerd om te gebruiken om de referenties te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="8337f-340">The cmdlet uses the certificate that gateway is configured to use to encrypt the credentials.</span></span> <span data-ttu-id="8337f-341">Toevoegen van versleutelde referenties voor de **EncryptedCredential** element van de **connectionString** in de JSON.</span><span class="sxs-lookup"><span data-stu-id="8337f-341">You add encrypted credentials to the **EncryptedCredential** element of the **connectionString** in the JSON.</span></span> <span data-ttu-id="8337f-342">U gebruikt de JSON met de [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet of in de Data Factory-Editor.</span><span class="sxs-lookup"><span data-stu-id="8337f-342">You use the JSON with the [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet or in the Data Factory Editor.</span></span>

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

<span data-ttu-id="8337f-343">Er is een meer aanpak voor het instellen van referenties met behulp van de Data Factory-Editor.</span><span class="sxs-lookup"><span data-stu-id="8337f-343">There is one more approach for setting credentials using Data Factory Editor.</span></span> <span data-ttu-id="8337f-344">Als u een SQL Server gekoppelde service maken met behulp van de editor en u referenties als tekst zonder opmaak invoeren, kan de referenties zijn versleuteld met behulp van een Data Factory-service-certificaat.</span><span class="sxs-lookup"><span data-stu-id="8337f-344">If you create a SQL Server linked service by using the editor and you enter credentials in plain text, the credentials are encrypted using a certificate that the Data Factory service owns.</span></span> <span data-ttu-id="8337f-345">Gebruikt het certificaat niet dat gateway is geconfigureerd voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="8337f-345">It does NOT use the certificate that gateway is configured to use.</span></span> <span data-ttu-id="8337f-346">Tijdens deze benadering is mogelijk iets sneller in sommige gevallen, is het minder veilig.</span><span class="sxs-lookup"><span data-stu-id="8337f-346">While this approach might be a little faster in some cases, it is less secure.</span></span> <span data-ttu-id="8337f-347">Daarom raden we aan dat u deze methode alleen voor ontwikkeling/testdoeleinden volgt.</span><span class="sxs-lookup"><span data-stu-id="8337f-347">Therefore, we recommend that you follow this approach only for development/testing purposes.</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="8337f-348">PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="8337f-348">PowerShell cmdlets</span></span>
<span data-ttu-id="8337f-349">Deze sectie beschrijft het maken en registreren van een gateway met behulp van Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8337f-349">This section describes how to create and register a gateway using Azure PowerShell cmdlets.</span></span>

1. <span data-ttu-id="8337f-350">Start **Azure PowerShell** in de beheerdersmodus.</span><span class="sxs-lookup"><span data-stu-id="8337f-350">Launch **Azure PowerShell** in administrator mode.</span></span>
2. <span data-ttu-id="8337f-351">Meld u aan bij uw Azure-account door de volgende opdracht uit te voeren en uw Azure-referenties in te voeren.</span><span class="sxs-lookup"><span data-stu-id="8337f-351">Log in to your Azure account by running the following command and entering your Azure credentials.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="8337f-352">Gebruik de **nieuw AzureRmDataFactoryGateway** cmdlet voor het maken van een logische gateway als volgt:</span><span class="sxs-lookup"><span data-stu-id="8337f-352">Use the **New-AzureRmDataFactoryGateway** cmdlet to create a logical gateway as follows:</span></span>

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    <span data-ttu-id="8337f-353">**Van de voorbeeldopdracht en uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="8337f-353">**Example command and output**:</span></span>

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. <span data-ttu-id="8337f-354">Ga naar de map in Azure PowerShell: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span><span class="sxs-lookup"><span data-stu-id="8337f-354">In Azure PowerShell, switch to the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span></span> <span data-ttu-id="8337f-355">Voer **RegisterGateway.ps1** die zijn gekoppeld aan de lokale variabele **$Key** zoals weergegeven in de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="8337f-355">Run **RegisterGateway.ps1** associated with the local variable **$Key** as shown in the following command.</span></span> <span data-ttu-id="8337f-356">Dit script registreert de clientagent is geïnstalleerd op uw computer met de logische gateway die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8337f-356">This script registers the client agent installed on your machine with the logical gateway you create earlier.</span></span>

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    <span data-ttu-id="8337f-357">U kunt de gateway op een externe computer met de parameter IsRegisterOnRemoteMachine registreren.</span><span class="sxs-lookup"><span data-stu-id="8337f-357">You can register the gateway on a remote machine by using the IsRegisterOnRemoteMachine parameter.</span></span> <span data-ttu-id="8337f-358">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8337f-358">Example:</span></span>

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. <span data-ttu-id="8337f-359">U kunt de **Get-AzureRmDataFactoryGateway** cmdlet om de lijst met Gateways in uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="8337f-359">You can use the **Get-AzureRmDataFactoryGateway** cmdlet to get the list of Gateways in your data factory.</span></span> <span data-ttu-id="8337f-360">Wanneer de **Status** toont **online**, betekent dit uw gateway is klaar voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="8337f-360">When the **Status** shows **online**, it means your gateway is ready to use.</span></span>

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
<span data-ttu-id="8337f-361">Kunt u een gateway met de **verwijderen AzureRmDataFactoryGateway** cmdlet en update beschrijving voor een gateway met de **Set AzureRmDataFactoryGateway** cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8337f-361">You can remove a gateway using the **Remove-AzureRmDataFactoryGateway** cmdlet and update description for a gateway using the **Set-AzureRmDataFactoryGateway** cmdlets.</span></span> <span data-ttu-id="8337f-362">Zie voor de syntaxis en andere details over deze cmdlets Data Factory Cmdlet Reference.</span><span class="sxs-lookup"><span data-stu-id="8337f-362">For syntax and other details about these cmdlets, see Data Factory Cmdlet Reference.</span></span>  

### <a name="list-gateways-using-powershell"></a><span data-ttu-id="8337f-363">Lijst met gateways met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="8337f-363">List gateways using PowerShell</span></span>

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a><span data-ttu-id="8337f-364">Verwijderen van de gateway met PowerShell</span><span class="sxs-lookup"><span data-stu-id="8337f-364">Remove gateway using PowerShell</span></span>

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a><span data-ttu-id="8337f-365">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8337f-365">Next steps</span></span>
* <span data-ttu-id="8337f-366">Zie [gegevens verplaatsen tussen on-premises en cloud gegevensarchieven](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="8337f-366">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="8337f-367">In de procedure maakt u een pijplijn die de gateway gebruikt om gegevens te verplaatsen van een on-premises SQL Server database naar een Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="8337f-367">In the walkthrough, you create a pipeline that uses the gateway to move data from an on-premises SQL Server database to an Azure blob.</span></span>  
