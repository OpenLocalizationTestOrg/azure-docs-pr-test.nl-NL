---
title: aaaIssuer naam en sleutel van verlener in BizTalk Services | Microsoft Docs
description: Meer informatie over hoe tooretrieve verlener naam en sleutel van verlener voor Service Bus of Access Control (ACS) in BizTalk Services. MABS, WABS
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
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="25b96-104">BizTalk Services: naam en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="25b96-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="25b96-105">Azure BizTalk Services maakt gebruik van Hallo naam van Service Bus verlener en sleutel van verlener en Hallo Access Control certificaatverlener en sleutel van verlener.</span><span class="sxs-lookup"><span data-stu-id="25b96-105">Azure BizTalk Services uses hello Service Bus Issuer Name and Issuer Key, and hello Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="25b96-106">Specifiek:</span><span class="sxs-lookup"><span data-stu-id="25b96-106">Specifically:</span></span>

| <span data-ttu-id="25b96-107">Taak</span><span class="sxs-lookup"><span data-stu-id="25b96-107">Task</span></span> | <span data-ttu-id="25b96-108">Welke naam van verlener en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="25b96-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="25b96-109">Implementeren van uw toepassing vanuit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="25b96-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="25b96-110">Toegang tot de naam van de certificaatverlener besturingselement en de sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="25b96-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="25b96-111">Hello Azure BizTalk Services-Portal configureren</span><span class="sxs-lookup"><span data-stu-id="25b96-111">Configuring hello Azure BizTalk Services Portal</span></span> |<span data-ttu-id="25b96-112">Toegang tot de naam van de certificaatverlener besturingselement en de sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="25b96-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="25b96-113">LOB-Relays maken Hello BizTalk Adapter Services in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="25b96-113">Creating LOB Relays with hello BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="25b96-114">Naam van Service Bus verlener en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="25b96-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="25b96-115">In dit onderwerp bevat Hallo stappen tooretrieve Hallo naam van verlener en sleutel van verlener.</span><span class="sxs-lookup"><span data-stu-id="25b96-115">This topic lists hello steps tooretrieve hello Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="25b96-116">Toegang tot de naam van de certificaatverlener besturingselement en de sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="25b96-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="25b96-117">Hallo Access Control verlener naam en sleutel van verlener worden gebruikt door de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="25b96-117">hello Access Control Issuer Name and Issuer Key are used by hello following:</span></span>

* <span data-ttu-id="25b96-118">Uw Azure BizTalk Service-toepassing in Visual Studio gemaakt: toosuccessfully uw BizTalk Service-toepassing in Visual Studio tooAzure implementeert, kunt u Hallo Access Control verlener naam en sleutel van verlener invoeren.</span><span class="sxs-lookup"><span data-stu-id="25b96-118">Your Azure BizTalk Service application created in Visual Studio: toosuccessfully deploy your BizTalk Service application in Visual Studio tooAzure, you enter hello Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="25b96-119">Hello Azure BizTalk Services-Portal: als u een BizTalk Service maakt en geopend Hallo BizTalk Services-Portal, de naam van uw Access Control verlener en sleutel van verlener worden automatisch geregistreerd voor uw implementaties met Hallo dezelfde Access Control-waarden.</span><span class="sxs-lookup"><span data-stu-id="25b96-119">hello Azure BizTalk Services  Portal: When you create a BizTalk Service and open hello BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with hello same Access Control values.</span></span>

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="25b96-120">Ophalen van Hallo Access Control verlener naam en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="25b96-120">Get hello Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="25b96-121">toouse ACS voor verificatie en get Hallo waarden voor naam van de verlener en sleutel van verlener, hello algemene stappen omvatten:</span><span class="sxs-lookup"><span data-stu-id="25b96-121">toouse ACS for authentication, and get hello Issuer Name and Issuer Key values, hello overall steps include:</span></span>

1. <span data-ttu-id="25b96-122">Hallo installeren [Azure Powershell-cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="25b96-122">Install hello [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="25b96-123">Uw Azure-account toevoegen:`Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="25b96-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="25b96-124">Retourneert de abonnementsnaam van uw:`get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="25b96-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="25b96-125">Selecteer uw abonnement:`select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="25b96-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="25b96-126">Maak een nieuwe naamruimte:`new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="25b96-126">Create a new namespace: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="25b96-127">Voorbeeld:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="25b96-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="25b96-128">Wanneer Hallo nieuwe ACS-naamruimte wordt gemaakt (dit kan enkele minuten duren), vindt u in verbindingsreeks Hallo Hallo-naam van verlener en sleutel van verlener waarden:</span><span class="sxs-lookup"><span data-stu-id="25b96-128">When hello new ACS namespace is created (which can take several minutes), hello Issuer Name and Issuer Key values are listed in hello connection string:</span></span> 

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

<span data-ttu-id="25b96-129">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="25b96-129">toosummarize:</span></span>  
<span data-ttu-id="25b96-130">De naam van certificaatverlener SharedSecretIssuer =</span><span class="sxs-lookup"><span data-stu-id="25b96-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="25b96-131">Sleutel van verlener SharedSecretKey =</span><span class="sxs-lookup"><span data-stu-id="25b96-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="25b96-132">Meer informatie over Hallo [nieuw AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25b96-132">More on hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="25b96-133">Naam van Service Bus verlener en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="25b96-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="25b96-134">Naam van Service Bus verlener en sleutel van verlener worden gebruikt door de BizTalk Adapter Services.</span><span class="sxs-lookup"><span data-stu-id="25b96-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="25b96-135">In uw BizTalk Services-project in Visual Studio gebruikt u Hallo BizTalk Adapter Services tooconnect tooan on-premises Line-of-Business (LOB)-systeem.</span><span class="sxs-lookup"><span data-stu-id="25b96-135">In your BizTalk Services project in Visual Studio, you use hello BizTalk Adapter Services tooconnect tooan on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="25b96-136">tooconnect, u Hallo Relay LOB maken en voer de details van uw LOB-systeem.</span><span class="sxs-lookup"><span data-stu-id="25b96-136">tooconnect, you create hello LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="25b96-137">Wanneer u dit doet, Voer u ook Hallo naam van Service Bus verlener en sleutel van verlener.</span><span class="sxs-lookup"><span data-stu-id="25b96-137">When doing this, you also enter hello Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="25b96-138">tooretrieve hello naam van Service Bus verlener en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="25b96-138">tooretrieve hello Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="25b96-139">Meld u aan toohello [klassieke Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="25b96-139">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="25b96-140">Selecteer in de Hallo navigatiedeelvenster links **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="25b96-140">In hello left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="25b96-141">Selecteer de naamruimte.</span><span class="sxs-lookup"><span data-stu-id="25b96-141">Select your namespace.</span></span> <span data-ttu-id="25b96-142">Selecteer in de taakbalk Hallo **verbindingsgegevens**.</span><span class="sxs-lookup"><span data-stu-id="25b96-142">In hello task bar, select **Connection Information**.</span></span> <span data-ttu-id="25b96-143">Hallo ziet **standaard verlener** (naam van de certificaatverlener) en **standaard sleutel** (sleutel van verlener).</span><span class="sxs-lookup"><span data-stu-id="25b96-143">This displays hello **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="25b96-144">De waarden kunnen worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="25b96-144">Their values can be copied.</span></span>  

<span data-ttu-id="25b96-145">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="25b96-145">toosummarize:</span></span>  
<span data-ttu-id="25b96-146">De naam van certificaatverlener = standaard certificaatverlener</span><span class="sxs-lookup"><span data-stu-id="25b96-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="25b96-147">Sleutel van verlener standaardsleutel =</span><span class="sxs-lookup"><span data-stu-id="25b96-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="25b96-148">Volgende</span><span class="sxs-lookup"><span data-stu-id="25b96-148">Next</span></span>
<span data-ttu-id="25b96-149">Aanvullende onderwerpen voor Azure BizTalk Services:</span><span class="sxs-lookup"><span data-stu-id="25b96-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="25b96-150">Hello Azure BizTalk Services SDK installeren</span><span class="sxs-lookup"><span data-stu-id="25b96-150">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="25b96-151">Zelfstudies: Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="25b96-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="25b96-152">Hoe gaan gebruiken Azure BizTalk Services SDK Hallo</span><span class="sxs-lookup"><span data-stu-id="25b96-152">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="25b96-153">Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="25b96-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="25b96-154">Zie ook</span><span class="sxs-lookup"><span data-stu-id="25b96-154">See Also</span></span>
* [<span data-ttu-id="25b96-155">Hoe: gebruik ACS-Management-Service tooConfigure Service-identiteiten</span><span class="sxs-lookup"><span data-stu-id="25b96-155">How to: Use ACS Management Service tooConfigure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="25b96-156">BizTalk Services: Developer, Basic, Standard en Premium-edities grafiek</span><span class="sxs-lookup"><span data-stu-id="25b96-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="25b96-157">BizTalk Services: Inrichten met behulp van Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="25b96-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="25b96-158">BizTalk Services: statusgrafiek voor de inrichting</span><span class="sxs-lookup"><span data-stu-id="25b96-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="25b96-159">BizTalk Services: de tabbladen Dashboard, Bewaken en Schalen</span><span class="sxs-lookup"><span data-stu-id="25b96-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="25b96-160">BizTalk Services: back-ups maken en herstellen</span><span class="sxs-lookup"><span data-stu-id="25b96-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="25b96-161">BizTalk Services: beperking</span><span class="sxs-lookup"><span data-stu-id="25b96-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

