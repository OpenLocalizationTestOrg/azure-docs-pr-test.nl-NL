---
title: de gegevensgateway aaaOn-premises | Microsoft Docs
description: Een On-premises gateway is nodig als uw Analysis Services-server in Azure maakt verbinding met tooon-premises gegevensbronnen.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: fc7b9c69e6f81b41deb7a5d6d963225593845d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-tooon-premises-data-sources-with-azure-on-premises-data-gateway"></a><span data-ttu-id="3a065-103">Tooon-premises gegevensbronnen verbinden met Azure On-premises Data Gateway</span><span class="sxs-lookup"><span data-stu-id="3a065-103">Connecting tooon-premises data sources with Azure On-premises Data Gateway</span></span>
<span data-ttu-id="3a065-104">Hallo lokale gegevensgateway fungeert als een brug, bieden veilige gegevensoverdracht tussen uw Azure Analysis Services-servers in Hallo cloud en on-premises gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="3a065-104">hello on-premises data gateway acts as a bridge, providing secure data transfer between on-premises data sources and your Azure Analysis Services servers in hello cloud.</span></span> <span data-ttu-id="3a065-105">Toevoeging tooworking met meerdere Azure Analysis Services-servers in Hallo werkt dezelfde regio, de meest recente versie van gateway Hallo Hallo ook met Azure Logic Apps, Power BI, Power-Apps en Microsoft-Flow.</span><span class="sxs-lookup"><span data-stu-id="3a065-105">In addition tooworking with multiple Azure Analysis Services servers in hello same region, hello latest version of hello gateway also works with Azure Logic Apps, Power BI, Power Apps, and Microsoft Flow.</span></span> <span data-ttu-id="3a065-106">U kunt meerdere services in Hallo koppelen dezelfde regio met een enkele gateway.</span><span class="sxs-lookup"><span data-stu-id="3a065-106">You can associate multiple services in hello same region with a single gateway.</span></span> 

 <span data-ttu-id="3a065-107">Azure Analysis Services is een gateway-bron in Hallo vereist dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="3a065-107">Azure Analysis Services requires a gateway resource in hello same region.</span></span> <span data-ttu-id="3a065-108">Als u Azure Analysis Services-servers in de regio VS-Oost 2 Hallo hebt, moet u bijvoorbeeld een gateway-bron in de regio VS-Oost 2 Hallo.</span><span class="sxs-lookup"><span data-stu-id="3a065-108">For example, if you have Azure Analysis Services servers in hello East US 2 region, you need a gateway resource in hello East US 2 region.</span></span> <span data-ttu-id="3a065-109">Meerdere servers in VS-Oost 2 Hallo kunnen gebruiken dezelfde gateway.</span><span class="sxs-lookup"><span data-stu-id="3a065-109">Multiple servers in East US 2 can use hello same gateway.</span></span>

<span data-ttu-id="3a065-110">Uitvoeren van setup Hallo gateway Hello eerst is een vierdelige proces:</span><span class="sxs-lookup"><span data-stu-id="3a065-110">Getting setup with hello gateway hello first time is a four-part process:</span></span>

- <span data-ttu-id="3a065-111">**Downloaden en uitvoeren van setup** -deze stap installeert u een gatewayservice op een computer in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="3a065-111">**Download and run setup** - This step installs a gateway service on a computer in your organization.</span></span>

- <span data-ttu-id="3a065-112">**Registreren van uw gateway** - In deze stap maakt u een naam opgeven en herstel van belangrijke voor uw gateway, en selecteer een regio, uw gateway registreren met Hallo Gateway-Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="3a065-112">**Register your gateway** - In this step, you specify a name and recovery key for your gateway, and select a region, registering your gateway with hello Gateway Cloud Service.</span></span>

- <span data-ttu-id="3a065-113">**Een gateway-resource maken in Azure** -In deze stap maakt u een gateway-bron in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3a065-113">**Create a gateway resource in Azure** - In this step, you create a gateway resource in your Azure subscription.</span></span>

- <span data-ttu-id="3a065-114">**Verbinding maken met uw servers tooyour gateway resource** -zodra u een gateway-bron in uw abonnement hebt, kunt u beginnen uw tooit servers verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="3a065-114">**Connect your servers tooyour gateway resource** - Once you have a gateway resource in your subscription, you can begin connecting your servers tooit.</span></span>

<span data-ttu-id="3a065-115">Zodra u een resource gateway is geconfigureerd voor uw abonnement hebt, kunt u meerdere servers en andere services tooit.</span><span class="sxs-lookup"><span data-stu-id="3a065-115">Once you have a gateway resource configured for your subscription, you can connect multiple servers, and other services tooit.</span></span> <span data-ttu-id="3a065-116">U alleen een andere gateway tooinstall nodig hebt en aanvullende gatewayresources maken als u servers of andere services in een andere regio.</span><span class="sxs-lookup"><span data-stu-id="3a065-116">You only need tooinstall a different gateway and create additional gateway resources if you have servers or other services in a different region.</span></span>

<span data-ttu-id="3a065-117">Zie tooget meteen gestart [installeren en configureren van lokale gegevensgateway](analysis-services-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="3a065-117">tooget started right away, see [Install and configure on-premises data gateway](analysis-services-gateway-install.md).</span></span>

## <span data-ttu-id="3a065-118"><a name="how-it-works"></a>Hoe het werkt</span><span class="sxs-lookup"><span data-stu-id="3a065-118"><a name="how-it-works"> </a>How it works</span></span>
<span data-ttu-id="3a065-119">Hallo-gateway die u op een computer in uw organisatie installeert wordt uitgevoerd als een Windows-service **On-premises gegevensgateway**.</span><span class="sxs-lookup"><span data-stu-id="3a065-119">hello gateway you install on a computer in your organization runs as a Windows service, **On-premises data gateway**.</span></span> <span data-ttu-id="3a065-120">Deze lokale service is geregistreerd bij Hallo Gateway Cloud Service via Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3a065-120">This local service is registered with hello Gateway Cloud Service through Azure Service Bus.</span></span> <span data-ttu-id="3a065-121">Vervolgens maakt u een gateway resource Gateway-Cloudservice voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3a065-121">You then create a gateway resource Gateway Cloud Service for your Azure subscription.</span></span> <span data-ttu-id="3a065-122">Uw Azure analyseservices-servers zijn vervolgens verbonden tooyour gateway resource.</span><span class="sxs-lookup"><span data-stu-id="3a065-122">Your Azure Analysis Services servers are then connected tooyour gateway resource.</span></span> <span data-ttu-id="3a065-123">Wanneer modellen op uw server nodig tooconnect tooyour on-premises gegevensbronnen voor query's of verwerking wordt een query's en stroom traverses Hallo gateway resource, Azure Service Bus Hallo gatewayservice voor lokale lokale gegevens en uw gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="3a065-123">When models on your server need tooconnect tooyour on-premises data sources for queries or processing, a query and data flow traverses hello gateway resource, Azure Service Bus, hello local on-premises data gateway service, and your data sources.</span></span> 

![Hoe werkt het?](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

<span data-ttu-id="3a065-125">Query's en gegevensstroom:</span><span class="sxs-lookup"><span data-stu-id="3a065-125">Queries and data flow:</span></span>

1. <span data-ttu-id="3a065-126">Een query is gemaakt door Hallo-cloudservice met de Hallo versleuteld referenties voor Hallo on-premises gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="3a065-126">A query is created by hello cloud service with hello encrypted credentials for hello on-premises data source.</span></span> <span data-ttu-id="3a065-127">Deze heeft vervolgens tooa wachtrij voor Hallo gateway tooprocess verzonden.</span><span class="sxs-lookup"><span data-stu-id="3a065-127">It's then sent tooa queue for hello gateway tooprocess.</span></span>
2. <span data-ttu-id="3a065-128">Hallo gateway-cloudservice Hallo query analyseert en duwt Hallo aanvraag toohello [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="3a065-128">hello gateway cloud service analyzes hello query and pushes hello request toohello [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span></span>
3. <span data-ttu-id="3a065-129">Hallo lokale gegevensgateway hello Azure Service Bus voor aanvragen in behandeling worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="3a065-129">hello on-premises data gateway polls hello Azure Service Bus for pending requests.</span></span>
4. <span data-ttu-id="3a065-130">Hallo gateway Hallo query opgehaald, ontsleutelt Hallo referenties en gegevensbronnen toohello is verbonden met deze referenties.</span><span class="sxs-lookup"><span data-stu-id="3a065-130">hello gateway gets hello query, decrypts hello credentials, and connects toohello data sources with those credentials.</span></span>
5. <span data-ttu-id="3a065-131">Hallo gateway verzendt Hallo toohello querygegevensbron voor uitvoering.</span><span class="sxs-lookup"><span data-stu-id="3a065-131">hello gateway sends hello query toohello data source for execution.</span></span>
6. <span data-ttu-id="3a065-132">Hallo resultaten worden verzonden in gegevensbron hello, toohello back-gateway, en klik vervolgens op het Hallo-cloudservice en de server.</span><span class="sxs-lookup"><span data-stu-id="3a065-132">hello results are sent from hello data source, back toohello gateway, and then onto hello cloud service and your server.</span></span>

## <span data-ttu-id="3a065-133"><a name="windows-service-account"></a>Windows-serviceaccount</span><span class="sxs-lookup"><span data-stu-id="3a065-133"><a name="windows-service-account"> </a>Windows Service account</span></span>
<span data-ttu-id="3a065-134">Hallo lokale gegevensgateway is geconfigureerde toouse *NT SERVICE\PBIEgwService* voor de aanmeldingsreferenties voor Hallo Windows-service.</span><span class="sxs-lookup"><span data-stu-id="3a065-134">hello on-premises data gateway is configured toouse *NT SERVICE\PBIEgwService* for hello Windows service logon credential.</span></span> <span data-ttu-id="3a065-135">Deze heeft standaard Hallo rechts aanmelden als service; in de context van de Hallo van Hallo-machine die u installeert Hallo-gateway op.</span><span class="sxs-lookup"><span data-stu-id="3a065-135">By default, it has hello right of Logon as a service; in hello context of hello machine that you are installing hello gateway on.</span></span> <span data-ttu-id="3a065-136">Deze referentie wordt niet Hallo dezelfde account die wordt gebruikt tooconnect tooon-premises gegevensbronnen of uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="3a065-136">This credential is not hello same account used tooconnect tooon-premises data sources or your Azure account.</span></span>  

<span data-ttu-id="3a065-137">Als u problemen met de proxyserver vanwege ondervindt tooauthentication, kunt u toochange Windows hello service account tooa domeingebruiker of beheerd serviceaccount.</span><span class="sxs-lookup"><span data-stu-id="3a065-137">If you encounter issues with your proxy server due tooauthentication, you may want toochange hello Windows service account tooa domain user or managed service account.</span></span>

## <span data-ttu-id="3a065-138"><a name="ports"></a>Poorten</span><span class="sxs-lookup"><span data-stu-id="3a065-138"><a name="ports"> </a>Ports</span></span>
<span data-ttu-id="3a065-139">Hallo-gateway maakt een uitgaande verbinding tooAzure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3a065-139">hello gateway creates an outbound connection tooAzure Service Bus.</span></span> <span data-ttu-id="3a065-140">Deze communiceert op uitgaande poorten: TCP 443 (standaard), 5671, 5672, 9350 via 9354.</span><span class="sxs-lookup"><span data-stu-id="3a065-140">It communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span>  <span data-ttu-id="3a065-141">Hallo-gateway vereist geen poorten voor inkomend verkeer.</span><span class="sxs-lookup"><span data-stu-id="3a065-141">hello gateway does not require inbound ports.</span></span>

<span data-ttu-id="3a065-142">We raden u geaccepteerde Hallo IP-adressen voor de regio van uw gegevens in uw firewall.</span><span class="sxs-lookup"><span data-stu-id="3a065-142">We recommend you whitelist hello IP addresses for your data region in your firewall.</span></span> <span data-ttu-id="3a065-143">U kunt downloaden Hallo [lijst met Microsoft Azure Datacenter IP](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="3a065-143">You can download hello [Microsoft Azure Datacenter IP list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="3a065-144">Deze lijst is wekelijks bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="3a065-144">This list is updated weekly.</span></span>

> [!NOTE]
> <span data-ttu-id="3a065-145">Hallo IP-adressen die worden vermeld in de lijst met hello Azure Datacenter IP zijn in CIDR-notatie.</span><span class="sxs-lookup"><span data-stu-id="3a065-145">hello IP Addresses listed in hello Azure Datacenter IP list are in CIDR notation.</span></span> <span data-ttu-id="3a065-146">10.0.0.0/24 betekent bijvoorbeeld niet 10.0.0.0 via 10.0.0.24.</span><span class="sxs-lookup"><span data-stu-id="3a065-146">For example, 10.0.0.0/24 does not mean 10.0.0.0 through 10.0.0.24.</span></span> <span data-ttu-id="3a065-147">Meer informatie over Hallo [CIDR-notatie](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="3a065-147">Learn more about hello [CIDR notation](http://whatismyipaddress.com/cidr).</span></span>
>
>

<span data-ttu-id="3a065-148">Hallo volgen Hallo volledig gekwalificeerde domeinnamen gebruikt door Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="3a065-148">hello following are hello fully qualified domain names used by hello gateway.</span></span>

| <span data-ttu-id="3a065-149">Domeinnamen</span><span class="sxs-lookup"><span data-stu-id="3a065-149">Domain names</span></span> | <span data-ttu-id="3a065-150">Uitgaande poorten</span><span class="sxs-lookup"><span data-stu-id="3a065-150">Outbound ports</span></span> | <span data-ttu-id="3a065-151">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3a065-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a065-152">*. powerbi.com</span><span class="sxs-lookup"><span data-stu-id="3a065-152">*.powerbi.com</span></span> |<span data-ttu-id="3a065-153">80</span><span class="sxs-lookup"><span data-stu-id="3a065-153">80</span></span> |<span data-ttu-id="3a065-154">HTTP gebruikt toodownload Hallo installatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="3a065-154">HTTP used toodownload hello installer.</span></span> |
| <span data-ttu-id="3a065-155">*. powerbi.com</span><span class="sxs-lookup"><span data-stu-id="3a065-155">*.powerbi.com</span></span> |<span data-ttu-id="3a065-156">443</span><span class="sxs-lookup"><span data-stu-id="3a065-156">443</span></span> |<span data-ttu-id="3a065-157">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3a065-157">HTTPS</span></span> |
| <span data-ttu-id="3a065-158">*. analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="3a065-158">*.analysis.windows.net</span></span> |<span data-ttu-id="3a065-159">443</span><span class="sxs-lookup"><span data-stu-id="3a065-159">443</span></span> |<span data-ttu-id="3a065-160">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3a065-160">HTTPS</span></span> |
| <span data-ttu-id="3a065-161">*. login.windows.net</span><span class="sxs-lookup"><span data-stu-id="3a065-161">*.login.windows.net</span></span> |<span data-ttu-id="3a065-162">443</span><span class="sxs-lookup"><span data-stu-id="3a065-162">443</span></span> |<span data-ttu-id="3a065-163">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3a065-163">HTTPS</span></span> |
| <span data-ttu-id="3a065-164">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="3a065-164">*.servicebus.windows.net</span></span> |<span data-ttu-id="3a065-165">5671-5672</span><span class="sxs-lookup"><span data-stu-id="3a065-165">5671-5672</span></span> |<span data-ttu-id="3a065-166">Geavanceerde Message Queuing-Protocol (AMQP)</span><span class="sxs-lookup"><span data-stu-id="3a065-166">Advanced Message Queuing Protocol (AMQP)</span></span> |
| <span data-ttu-id="3a065-167">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="3a065-167">*.servicebus.windows.net</span></span> |<span data-ttu-id="3a065-168">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="3a065-168">443, 9350-9354</span></span> |<span data-ttu-id="3a065-169">Listeners op Service Bus Relay via TCP (443 voor toegangsbeheer token aanschaf vereist)</span><span class="sxs-lookup"><span data-stu-id="3a065-169">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> |
| <span data-ttu-id="3a065-170">*. frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="3a065-170">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="3a065-171">443</span><span class="sxs-lookup"><span data-stu-id="3a065-171">443</span></span> |<span data-ttu-id="3a065-172">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3a065-172">HTTPS</span></span> |
| <span data-ttu-id="3a065-173">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="3a065-173">*.core.windows.net</span></span> |<span data-ttu-id="3a065-174">443</span><span class="sxs-lookup"><span data-stu-id="3a065-174">443</span></span> |<span data-ttu-id="3a065-175">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3a065-175">HTTPS</span></span> |
| <span data-ttu-id="3a065-176">Login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="3a065-176">login.microsoftonline.com</span></span> |<span data-ttu-id="3a065-177">443</span><span class="sxs-lookup"><span data-stu-id="3a065-177">443</span></span> |<span data-ttu-id="3a065-178">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3a065-178">HTTPS</span></span> |
| <span data-ttu-id="3a065-179">*. msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="3a065-179">*.msftncsi.com</span></span> |<span data-ttu-id="3a065-180">443</span><span class="sxs-lookup"><span data-stu-id="3a065-180">443</span></span> |<span data-ttu-id="3a065-181">Verbinding met internet tootest gebruikt als Hallo-gateway onbereikbaar via Hallo Power BI-service is.</span><span class="sxs-lookup"><span data-stu-id="3a065-181">Used tootest internet connectivity if hello gateway is unreachable by hello Power BI service.</span></span> |
| <span data-ttu-id="3a065-182">*.microsoftonline p.com</span><span class="sxs-lookup"><span data-stu-id="3a065-182">*.microsoftonline-p.com</span></span> |<span data-ttu-id="3a065-183">443</span><span class="sxs-lookup"><span data-stu-id="3a065-183">443</span></span> |<span data-ttu-id="3a065-184">Gebruikt voor verificatie, afhankelijk van de configuratie.</span><span class="sxs-lookup"><span data-stu-id="3a065-184">Used for authentication depending on configuration.</span></span> |

### <span data-ttu-id="3a065-185"><a name="force-https"></a>HTTPS-communicatie met Azure Service Bus forceren</span><span class="sxs-lookup"><span data-stu-id="3a065-185"><a name="force-https"></a>Forcing HTTPS communication with Azure Service Bus</span></span>
<span data-ttu-id="3a065-186">U kunt Hallo gateway toocommunicate met Azure Service Bus afdwingen met behulp van HTTPS in plaats van rechtstreekse TCP; echter, doen dus aanzienlijk vermindert de prestaties.</span><span class="sxs-lookup"><span data-stu-id="3a065-186">You can force hello gateway toocommunicate with Azure Service Bus by using HTTPS instead of direct TCP; however, doing so can greatly reduce performance.</span></span> <span data-ttu-id="3a065-187">U kunt wijzigen Hallo *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* bestand door het wijzigen van de waarde op Hallo van `AutoDetect` te`Https`.</span><span class="sxs-lookup"><span data-stu-id="3a065-187">You can modify hello *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file by changing hello value from `AutoDetect` too`Https`.</span></span> <span data-ttu-id="3a065-188">Dit bestand bevindt zich doorgaans in *C:\Program Files\On-premises gegevensgateway*.</span><span class="sxs-lookup"><span data-stu-id="3a065-188">This file is typically located at *C:\Program Files\On-premises data gateway*.</span></span>

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <span data-ttu-id="3a065-189"><a name="faq"></a>Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="3a065-189"><a name="faq"></a>Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="3a065-190">Algemeen</span><span class="sxs-lookup"><span data-stu-id="3a065-190">General</span></span>

<span data-ttu-id="3a065-191">**Q**: moet ik een gateway voor gegevensbronnen in de cloud hello, zoals Azure SQL Database?</span><span class="sxs-lookup"><span data-stu-id="3a065-191">**Q**: Do I need a gateway for data sources in hello cloud, such as Azure SQL Database?</span></span> <br/><span data-ttu-id="3a065-192">
**Een**: Nee.</span><span class="sxs-lookup"><span data-stu-id="3a065-192">
**A**: No.</span></span> <span data-ttu-id="3a065-193">Een gateway maakt verbinding alleen tooon-premises gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="3a065-193">A gateway connects tooon-premises data sources only.</span></span>

<span data-ttu-id="3a065-194">**Q**: heeft Hallo gateway geïnstalleerd op dezelfde computer als de gegevensbron Hallo Hallo toobe?</span><span class="sxs-lookup"><span data-stu-id="3a065-194">**Q**: Does hello gateway have toobe installed on hello same machine as hello data source?</span></span> <br/><span data-ttu-id="3a065-195">
**Een**: Nee.</span><span class="sxs-lookup"><span data-stu-id="3a065-195">
**A**: No.</span></span> <span data-ttu-id="3a065-196">Hallo-gateway wordt verbonden toohello-gegevensbron Hallo verbindingsgegevens die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3a065-196">hello gateway connects toohello data source using hello connection information that was provided.</span></span> <span data-ttu-id="3a065-197">Hallo gateway beschouwen als een client-toepassing in deze zin.</span><span class="sxs-lookup"><span data-stu-id="3a065-197">Consider hello gateway as a client application in this sense.</span></span> <span data-ttu-id="3a065-198">Hallo gateway alleen moet Hallo mogelijkheid tooconnect toohello servernaam die is opgegeven, doorgaans op Hallo hetzelfde netwerk.</span><span class="sxs-lookup"><span data-stu-id="3a065-198">hello gateway just needs hello capability tooconnect toohello server name that was provided, typically on hello same network.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="3a065-199">**Q**: Waarom moet toouse werk of school account toosign in ik?</span><span class="sxs-lookup"><span data-stu-id="3a065-199">**Q**: Why do I need toouse a work or school account toosign in?</span></span> <br/><span data-ttu-id="3a065-200">
**Een**: U kunt alleen een Azure werk- of schoolaccount wanneer u Hallo lokale gegevensgateway installeert.</span><span class="sxs-lookup"><span data-stu-id="3a065-200">
**A**: You can only use an Azure work or school account when you install hello on-premises data gateway.</span></span> <span data-ttu-id="3a065-201">Uw account wordt opgeslagen in een tenant die wordt beheerd door Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a065-201">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="3a065-202">Uw Azure AD-account UPN (user Principal name) normaal gesproken komt overeen met Hallo e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="3a065-202">Usually, your Azure AD account's user principal name (UPN) matches hello email address.</span></span>

<span data-ttu-id="3a065-203">**Q**: waar mijn referenties worden opgeslagen?</span><span class="sxs-lookup"><span data-stu-id="3a065-203">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="3a065-204">
**Een**: Hallo-referenties die u voor een gegevensbron opgeeft zijn versleuteld en opgeslagen in Hallo Gateway-Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="3a065-204">
**A**: hello credentials that you enter for a data source are encrypted and stored in hello Gateway Cloud Service.</span></span> <span data-ttu-id="3a065-205">Hallo-referenties worden op Hallo lokale gegevensgateway ontsleuteld.</span><span class="sxs-lookup"><span data-stu-id="3a065-205">hello credentials are decrypted at hello on-premises data gateway.</span></span>

<span data-ttu-id="3a065-206">**Q**: zijn er vereisten voor de bandbreedte van het netwerk?</span><span class="sxs-lookup"><span data-stu-id="3a065-206">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="3a065-207">
**Een**: dit is uw netwerk het beste verbinding bevat goede doorvoer.</span><span class="sxs-lookup"><span data-stu-id="3a065-207">
**A**: It's recommend your network connection has good throughput.</span></span> <span data-ttu-id="3a065-208">Elke omgeving is verschillend en Hallo hoeveelheid verzonden gegevens heeft op Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="3a065-208">Every environment is different, and hello amount of data being sent affects hello results.</span></span> <span data-ttu-id="3a065-209">Met behulp van ExpressRoute kan helpen bij het tooguarantee een mate van doorvoer tussen on-premises en hello Azure-datacenters.</span><span class="sxs-lookup"><span data-stu-id="3a065-209">Using ExpressRoute could help tooguarantee a level of throughput between on-premises and hello Azure datacenters.</span></span>
<span data-ttu-id="3a065-210">U kunt uw doorvoer Hallo hulpprogramma van derden Azure snelheid testen app toohelp meter.</span><span class="sxs-lookup"><span data-stu-id="3a065-210">You can use hello third-party tool Azure Speed Test app toohelp gauge your throughput.</span></span>

<span data-ttu-id="3a065-211">**Q**: Wat is er Hallo latentie voor actieve query's tooa gegevensbron van Hallo gateway?</span><span class="sxs-lookup"><span data-stu-id="3a065-211">**Q**: What is hello latency for running queries tooa data source from hello gateway?</span></span> <span data-ttu-id="3a065-212">Wat is de beste architectuur Hallo?</span><span class="sxs-lookup"><span data-stu-id="3a065-212">What is hello best architecture?</span></span> <br/><span data-ttu-id="3a065-213">
**Een**: tooreduce netwerklatentie, Hallo-gateway installeren als de gegevensbron sluiten toohello mogelijk.</span><span class="sxs-lookup"><span data-stu-id="3a065-213">
**A**: tooreduce network latency, install hello gateway as close toohello data source as possible.</span></span> <span data-ttu-id="3a065-214">Als u Hallo gateway op de werkelijke gegevensbron hello installeren kunt, minimaliseert deze nabijheid Hallo latentie geïntroduceerd.</span><span class="sxs-lookup"><span data-stu-id="3a065-214">If you can install hello gateway on hello actual data source, this proximity minimizes hello latency introduced.</span></span> <span data-ttu-id="3a065-215">Hallo datacenters te overwegen.</span><span class="sxs-lookup"><span data-stu-id="3a065-215">Consider hello datacenters too.</span></span> <span data-ttu-id="3a065-216">Bijvoorbeeld, als Hallo VS-West datacenter maakt gebruik van uw service en u SQL Server gehost in een virtuele machine in Azure hebt, moet uw virtuele Azure-machine Hallo VS-West te.</span><span class="sxs-lookup"><span data-stu-id="3a065-216">For example, if your service uses hello West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in hello West US too.</span></span> <span data-ttu-id="3a065-217">Deze nabijheid minimaliseert latentie en vermijdt u kosten voor uitgaande op Hallo Azure VM.</span><span class="sxs-lookup"><span data-stu-id="3a065-217">This proximity minimizes latency and avoids egress charges on hello Azure VM.</span></span>

<span data-ttu-id="3a065-218">**Q**: hoe worden resultaten verzonden back toohello cloud?</span><span class="sxs-lookup"><span data-stu-id="3a065-218">**Q**: How are results sent back toohello cloud?</span></span> <br/><span data-ttu-id="3a065-219">
**Een**: resultaten worden verzonden via hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3a065-219">
**A**: Results are sent through hello Azure Service Bus.</span></span>

<span data-ttu-id="3a065-220">**Q**: zijn er inkomende verbindingen toohello gateway vanuit de cloud Hallo?</span><span class="sxs-lookup"><span data-stu-id="3a065-220">**Q**: Are there any inbound connections toohello gateway from hello cloud?</span></span> <br/><span data-ttu-id="3a065-221">
**Een**: Nee.</span><span class="sxs-lookup"><span data-stu-id="3a065-221">
**A**: No.</span></span> <span data-ttu-id="3a065-222">Hallo-gateway gebruikt uitgaande verbindingen tooAzure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3a065-222">hello gateway uses outbound connections tooAzure Service Bus.</span></span>

<span data-ttu-id="3a065-223">**Q**: Wat gebeurt er als ik uitgaande verbindingen blokkeren?</span><span class="sxs-lookup"><span data-stu-id="3a065-223">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="3a065-224">Wat kan ik tooopen nodig?</span><span class="sxs-lookup"><span data-stu-id="3a065-224">What do I need tooopen?</span></span> <br/><span data-ttu-id="3a065-225">
**Een**: Zie Hallo poorten en hosts die Hallo gateway gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3a065-225">
**A**: See hello ports and hosts that hello gateway uses.</span></span>

<span data-ttu-id="3a065-226">**Q**: de werkelijke Windows-service Hallo zogenaamd?</span><span class="sxs-lookup"><span data-stu-id="3a065-226">**Q**: What is hello actual Windows service called?</span></span><br/><span data-ttu-id="3a065-227">
**Een**: In de Services Hallo gateway gatewayservice voor On-premises gegevens wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="3a065-227">
**A**: In Services, hello gateway is called On-premises data gateway service.</span></span>

<span data-ttu-id="3a065-228">**Q**: kunt Hallo gateway Windows-service uitvoert met een Azure Active Directory-account?</span><span class="sxs-lookup"><span data-stu-id="3a065-228">**Q**: Can hello gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="3a065-229">
**Een**: Nee.</span><span class="sxs-lookup"><span data-stu-id="3a065-229">
**A**: No.</span></span> <span data-ttu-id="3a065-230">Hallo Windows-service moet een geldige Windows-account hebben.</span><span class="sxs-lookup"><span data-stu-id="3a065-230">hello Windows service must have a valid Windows account.</span></span> <span data-ttu-id="3a065-231">Standaard is Hallo-service wordt uitgevoerd met Hallo Service-SID NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="3a065-231">By default, hello service runs with hello Service SID, NT SERVICE\PBIEgwService.</span></span>

### <span data-ttu-id="3a065-232"><a name="high-availability"></a>Hoge beschikbaarheid en herstel na noodgevallen</span><span class="sxs-lookup"><span data-stu-id="3a065-232"><a name="high-availability"></a>High availability and disaster recovery</span></span>

<span data-ttu-id="3a065-233">**Q**: welke opties zijn beschikbaar voor herstel na noodgevallen?</span><span class="sxs-lookup"><span data-stu-id="3a065-233">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="3a065-234">
**Een**: U kunt gebruiken Hallo herstel sleutel toorestore of verplaatsen van een gateway.</span><span class="sxs-lookup"><span data-stu-id="3a065-234">
**A**: You can use hello recovery key toorestore or move a gateway.</span></span> <span data-ttu-id="3a065-235">Wanneer u Hallo-gateway installeert, geef Hallo herstelsleutel.</span><span class="sxs-lookup"><span data-stu-id="3a065-235">When you install hello gateway, specify hello recovery key.</span></span>

<span data-ttu-id="3a065-236">**Q**: Wat is Hallo voordeel van de herstelsleutel Hallo?</span><span class="sxs-lookup"><span data-stu-id="3a065-236">**Q**: What is hello benefit of hello recovery key?</span></span> <br/><span data-ttu-id="3a065-237">
**Een**: Hallo herstelsleutel biedt een manier toomigrate of de gateway-instellingen herstellen na een noodgeval.</span><span class="sxs-lookup"><span data-stu-id="3a065-237">
**A**: hello recovery key provides a way toomigrate or recover your gateway settings after a disaster.</span></span>

## <span data-ttu-id="3a065-238"><a name="troubleshooting"></a>Probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="3a065-238"><a name="troubleshooting"> </a>Troubleshooting</span></span>

<span data-ttu-id="3a065-239">**Q**: hoe kan ik zien welke query toohello on-premises gegevensbron worden verzonden?</span><span class="sxs-lookup"><span data-stu-id="3a065-239">**Q**: How can I see what queries are being sent toohello on-premises data source?</span></span> <br/><span data-ttu-id="3a065-240">
**Een**: U kunt inschakelen querytracering, waaronder het Hallo-query's die worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="3a065-240">
**A**: You can enable query tracing, which includes hello queries that are sent.</span></span> <span data-ttu-id="3a065-241">Houd er rekening mee toochange query tracering van de oorspronkelijke waarde toohello gedaan bij het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="3a065-241">Remember toochange query tracing back toohello original value when done troubleshooting.</span></span> <span data-ttu-id="3a065-242">Querytracering ingeschakeld verlaten maakt grotere Logboeken.</span><span class="sxs-lookup"><span data-stu-id="3a065-242">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="3a065-243">U kunt ook hulpprogramma's die de gegevensbron voor tracering van query's heeft bekijken.</span><span class="sxs-lookup"><span data-stu-id="3a065-243">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="3a065-244">U kunt bijvoorbeeld de Extended Events of SQL Profiler gebruiken voor SQL Server en Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="3a065-244">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="3a065-245">**Q**: waar zich de gateway-logboeken Hallo?</span><span class="sxs-lookup"><span data-stu-id="3a065-245">**Q**: Where are hello gateway logs?</span></span> <br/><span data-ttu-id="3a065-246">
**Een**: Zie de logboeken verderop in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="3a065-246">
**A**: See Logs later in this topic.</span></span>

### <span data-ttu-id="3a065-247"><a name="update"></a>Meest recente versie van de update toohello</span><span class="sxs-lookup"><span data-stu-id="3a065-247"><a name="update"></a>Update toohello latest version</span></span>

<span data-ttu-id="3a065-248">Veel problemen kunnen surface wanneer Hallo gatewayversie verouderd.</span><span class="sxs-lookup"><span data-stu-id="3a065-248">Many issues can surface when hello gateway version becomes outdated.</span></span> <span data-ttu-id="3a065-249">Zorg ervoor dat u met de meest recente versie Hallo als goed over het algemeen.</span><span class="sxs-lookup"><span data-stu-id="3a065-249">As good general practice, make sure that you use hello latest version.</span></span> <span data-ttu-id="3a065-250">Als u dit nog niet hebt Hallo gateway voor een maand of langer bijgewerkt, kunt u Overweeg de installatie van de meest recente versie van gateway Hallo Hallo en zien als u Hallo probleem kan reproduceren.</span><span class="sxs-lookup"><span data-stu-id="3a065-250">If you haven't updated hello gateway for a month or longer, you might consider installing hello latest version of hello gateway, and see if you can reproduce hello issue.</span></span>

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="3a065-251">Fout: Kan tooadd gebruiker toogroup.</span><span class="sxs-lookup"><span data-stu-id="3a065-251">Error: Failed tooadd user toogroup.</span></span> <span data-ttu-id="3a065-252">(-2147463168 PBIEgwService Prestatielogboekgebruikers)</span><span class="sxs-lookup"><span data-stu-id="3a065-252">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="3a065-253">U kunt deze fout kan ophalen, als u probeert tooinstall Hallo gateway op een domeincontroller wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="3a065-253">You might get this error if you try tooinstall hello gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="3a065-254">Zorg ervoor dat u Hallo-gateway op een computer die een domeincontroller niet implementeert.</span><span class="sxs-lookup"><span data-stu-id="3a065-254">Make sure that you deploy hello gateway on a machine that isn't a domain controller.</span></span>

## <span data-ttu-id="3a065-255"><a name="logs"></a>Logboeken</span><span class="sxs-lookup"><span data-stu-id="3a065-255"><a name="logs"></a>Logs</span></span>

<span data-ttu-id="3a065-256">Logboekbestanden zijn een belangrijke bron wanneer het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="3a065-256">Log files are an important resource when troubleshooting.</span></span>

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="3a065-257">Enterprise gateway-service-Logboeken</span><span class="sxs-lookup"><span data-stu-id="3a065-257">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a><span data-ttu-id="3a065-258">Configuratielogboeken</span><span class="sxs-lookup"><span data-stu-id="3a065-258">Configuration logs</span></span>

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a><span data-ttu-id="3a065-259">Gebeurtenislogboeken</span><span class="sxs-lookup"><span data-stu-id="3a065-259">Event logs</span></span>

<span data-ttu-id="3a065-260">U vindt Hallo Data Management Gateway en PowerBIGateway Logboeken onder **servicelogboeken voor toepassingen en**.</span><span class="sxs-lookup"><span data-stu-id="3a065-260">You can find hello Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>


## <span data-ttu-id="3a065-261"><a name="telemetry"></a>Telemetrie</span><span class="sxs-lookup"><span data-stu-id="3a065-261"><a name="telemetry"></a>Telemetry</span></span>
<span data-ttu-id="3a065-262">Telemetrie kan worden gebruikt voor bewaking en probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="3a065-262">Telemetry can be used for monitoring and troubleshooting.</span></span> <span data-ttu-id="3a065-263">Standaard</span><span class="sxs-lookup"><span data-stu-id="3a065-263">By default</span></span>

<span data-ttu-id="3a065-264">**tooturn telemetrie**</span><span class="sxs-lookup"><span data-stu-id="3a065-264">**tooturn on telemetry**</span></span>

1.  <span data-ttu-id="3a065-265">Controleer Hallo On-premises gateway client gegevensmap op Hallo-computer.</span><span class="sxs-lookup"><span data-stu-id="3a065-265">Check hello On-premises data gateway client directory on hello computer.</span></span> <span data-ttu-id="3a065-266">Dit is meestal **%systemdrive%\Program Files\On-premises gegevensgateway**.</span><span class="sxs-lookup"><span data-stu-id="3a065-266">Typically, it is **%systemdrive%\Program Files\On-premises data gateway**.</span></span> <span data-ttu-id="3a065-267">Of u kunt een servicesconsole opent en controleer of Hallo pad tooexecutable: een eigenschap van Hallo On-premises data gateway-service.</span><span class="sxs-lookup"><span data-stu-id="3a065-267">Or, you can open a Services console and check hello Path tooexecutable: A property of hello On-premises data gateway service.</span></span>
2.  <span data-ttu-id="3a065-268">In de Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config-bestand Hallo van client-directory.</span><span class="sxs-lookup"><span data-stu-id="3a065-268">In hello Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config file from client directory.</span></span> <span data-ttu-id="3a065-269">Hallo SendTelemetry instelling tootrue wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3a065-269">Change hello SendTelemetry setting tootrue.</span></span>
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  <span data-ttu-id="3a065-270">De wijzigingen opslaan en Hallo Windows-service opnieuw starten: On-premises data gateway-service.</span><span class="sxs-lookup"><span data-stu-id="3a065-270">Save your changes and restart hello Windows service: On-premises data gateway service.</span></span>




## <a name="next-steps"></a><span data-ttu-id="3a065-271">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3a065-271">Next steps</span></span>
* [<span data-ttu-id="3a065-272">Analyseservices beheren</span><span class="sxs-lookup"><span data-stu-id="3a065-272">Manage Analysis Services</span></span>](analysis-services-manage.md)
* [<span data-ttu-id="3a065-273">Gegevens ophalen uit Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="3a065-273">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
