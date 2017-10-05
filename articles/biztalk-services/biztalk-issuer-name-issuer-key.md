---
title: Naam van verlener en sleutel van verlener in BizTalk Services | Microsoft Docs
description: Informatie over het ophalen van de naam van de verlener en sleutel van verlener voor Service Bus of Access Control (ACS) in BizTalk Services. MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: b9fd985c23558596408e78eadae00dd0f95c4214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="11620-104">BizTalk Services: naam en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="11620-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="11620-105">Azure BizTalk Services maakt gebruik van de naam van de Service Bus-verlener en sleutel van verlener en de naam van de certificaatverlener Access Control en sleutel van verlener.</span><span class="sxs-lookup"><span data-stu-id="11620-105">Azure BizTalk Services uses the Service Bus Issuer Name and Issuer Key, and the Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="11620-106">Specifiek:</span><span class="sxs-lookup"><span data-stu-id="11620-106">Specifically:</span></span>

| <span data-ttu-id="11620-107">Taak</span><span class="sxs-lookup"><span data-stu-id="11620-107">Task</span></span> | <span data-ttu-id="11620-108">Welke naam van verlener en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="11620-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="11620-109">Implementeren van uw toepassing vanuit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="11620-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="11620-110">Toegang tot de naam van de certificaatverlener besturingselement en de sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="11620-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="11620-111">De Azure BizTalk Services-Portal configureren</span><span class="sxs-lookup"><span data-stu-id="11620-111">Configuring the Azure BizTalk Services Portal</span></span> |<span data-ttu-id="11620-112">Toegang tot de naam van de certificaatverlener besturingselement en de sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="11620-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="11620-113">Relays LOB maken met de BizTalk Adapter Services in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="11620-113">Creating LOB Relays with the BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="11620-114">Naam van Service Bus verlener en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="11620-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="11620-115">Dit onderwerp worden de stappen voor het ophalen van de naam van verlener en sleutel van verlener.</span><span class="sxs-lookup"><span data-stu-id="11620-115">This topic lists the steps to retrieve the Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="11620-116">Toegang tot de naam van de certificaatverlener besturingselement en de sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="11620-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="11620-117">De naam van de certificaatverlener Access Control en sleutel van verlener worden gebruikt door het volgende:</span><span class="sxs-lookup"><span data-stu-id="11620-117">The Access Control Issuer Name and Issuer Key are used by the following:</span></span>

* <span data-ttu-id="11620-118">Uw Azure BizTalk Service-toepassing in Visual Studio gemaakt: als u wilt uw BizTalk Service-toepassing in Visual Studio implementeren naar Azure, u de naam van de certificaatverlener Access Control en sleutel van verlener invoeren.</span><span class="sxs-lookup"><span data-stu-id="11620-118">Your Azure BizTalk Service application created in Visual Studio: To successfully deploy your BizTalk Service application in Visual Studio to Azure, you enter the Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="11620-119">De Azure BizTalk Services-Portal: Wanneer u een BizTalk Service maakt en de BizTalk Services-Portal te openen, uw naam van de certificaatverlener Access Control en sleutel van verlener worden automatisch geregistreerd voor uw implementaties met dezelfde Access Control-waarden.</span><span class="sxs-lookup"><span data-stu-id="11620-119">The Azure BizTalk Services  Portal: When you create a BizTalk Service and open the BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with the same Access Control values.</span></span>

### <a name="get-the-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="11620-120">De naam van de certificaatverlener Access Control en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="11620-120">Get the Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="11620-121">Om ACS gebruiken voor verificatie en krijgt u de naam van verlener en sleutel van verlener waarden, worden de algemene stappen omvatten:</span><span class="sxs-lookup"><span data-stu-id="11620-121">To use ACS for authentication, and get the Issuer Name and Issuer Key values, the overall steps include:</span></span>

1. <span data-ttu-id="11620-122">Installeer de [Azure Powershell-cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="11620-122">Install the [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="11620-123">Uw Azure-account toevoegen:`Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="11620-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="11620-124">Retourneert de abonnementsnaam van uw:`get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="11620-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="11620-125">Selecteer uw abonnement:`select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="11620-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="11620-126">Maak een nieuwe naamruimte:`new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="11620-126">Create a new namespace: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="11620-127">Voorbeeld:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="11620-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="11620-128">Wanneer de nieuwe ACS-naamruimte wordt gemaakt (dit kan enkele minuten duren), worden de naam van verlener en sleutel van verlener waarden staan in de verbindingsreeks:</span><span class="sxs-lookup"><span data-stu-id="11620-128">When the new ACS namespace is created (which can take several minutes), the Issuer Name and Issuer Key values are listed in the connection string:</span></span> 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

<span data-ttu-id="11620-129">Samengevat:</span><span class="sxs-lookup"><span data-stu-id="11620-129">To summarize:</span></span>  
<span data-ttu-id="11620-130">De naam van certificaatverlener SharedSecretIssuer =</span><span class="sxs-lookup"><span data-stu-id="11620-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="11620-131">Sleutel van verlener SharedSecretKey =</span><span class="sxs-lookup"><span data-stu-id="11620-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="11620-132">Meer op de [nieuw AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="11620-132">More on the [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="11620-133">Naam van Service Bus verlener en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="11620-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="11620-134">Naam van Service Bus verlener en sleutel van verlener worden gebruikt door de BizTalk Adapter Services.</span><span class="sxs-lookup"><span data-stu-id="11620-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="11620-135">In uw BizTalk Services-project in Visual Studio gebruikt u de BizTalk Adapter Services verbinding maken met een on-premises Line-of-Business (LOB)-systeem.</span><span class="sxs-lookup"><span data-stu-id="11620-135">In your BizTalk Services project in Visual Studio, you use the BizTalk Adapter Services to connect to an on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="11620-136">Als u wilt verbinden, de Relay LOB maken en voer de details van uw LOB-systeem.</span><span class="sxs-lookup"><span data-stu-id="11620-136">To connect, you create the LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="11620-137">Wanneer u dit doet, typt u ook de naam van Service Bus verlener en sleutel van verlener.</span><span class="sxs-lookup"><span data-stu-id="11620-137">When doing this, you also enter the Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="to-retrieve-the-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="11620-138">Voor het ophalen van de naam van Service Bus verlener en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="11620-138">To retrieve the Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="11620-139">Meld u aan bij de [klassieke Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="11620-139">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="11620-140">Selecteer in het navigatiedeelvenster links **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="11620-140">In the left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="11620-141">Selecteer de naamruimte.</span><span class="sxs-lookup"><span data-stu-id="11620-141">Select your namespace.</span></span> <span data-ttu-id="11620-142">Selecteer in de taakbalk **verbindingsgegevens**.</span><span class="sxs-lookup"><span data-stu-id="11620-142">In the task bar, select **Connection Information**.</span></span> <span data-ttu-id="11620-143">U ziet nu de **standaard verlener** (naam van de certificaatverlener) en **standaard sleutel** (sleutel van verlener).</span><span class="sxs-lookup"><span data-stu-id="11620-143">This displays the **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="11620-144">De waarden kunnen worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="11620-144">Their values can be copied.</span></span>  

<span data-ttu-id="11620-145">Samengevat:</span><span class="sxs-lookup"><span data-stu-id="11620-145">To summarize:</span></span>  
<span data-ttu-id="11620-146">De naam van certificaatverlener = standaard certificaatverlener</span><span class="sxs-lookup"><span data-stu-id="11620-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="11620-147">Sleutel van verlener standaardsleutel =</span><span class="sxs-lookup"><span data-stu-id="11620-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="11620-148">Volgende</span><span class="sxs-lookup"><span data-stu-id="11620-148">Next</span></span>
<span data-ttu-id="11620-149">Aanvullende onderwerpen voor Azure BizTalk Services:</span><span class="sxs-lookup"><span data-stu-id="11620-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="11620-150">De Azure BizTalk Services SDK installeren</span><span class="sxs-lookup"><span data-stu-id="11620-150">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="11620-151">Zelfstudies: Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="11620-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="11620-152">De Azure BizTalk Services SDK gaan gebruiken</span><span class="sxs-lookup"><span data-stu-id="11620-152">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="11620-153">Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="11620-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="11620-154">Zie ook</span><span class="sxs-lookup"><span data-stu-id="11620-154">See Also</span></span>
* [<span data-ttu-id="11620-155">How to: ACS-Management-Service gebruiken voor het configureren van de Service-identiteiten</span><span class="sxs-lookup"><span data-stu-id="11620-155">How to: Use ACS Management Service to Configure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="11620-156">BizTalk Services: Developer, Basic, Standard en Premium-edities grafiek</span><span class="sxs-lookup"><span data-stu-id="11620-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="11620-157">BizTalk Services: Inrichten met behulp van Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="11620-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="11620-158">BizTalk Services: statusgrafiek voor de inrichting</span><span class="sxs-lookup"><span data-stu-id="11620-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="11620-159">BizTalk Services: de tabbladen Dashboard, Bewaken en Schalen</span><span class="sxs-lookup"><span data-stu-id="11620-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="11620-160">BizTalk Services: back-ups maken en herstellen</span><span class="sxs-lookup"><span data-stu-id="11620-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="11620-161">BizTalk Services: beperking</span><span class="sxs-lookup"><span data-stu-id="11620-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

