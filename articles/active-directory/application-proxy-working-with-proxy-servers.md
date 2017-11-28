---
title: aaaWork met bestaande on-premises proxy-servers en Azure AD | Microsoft Docs
description: Bevat informatie over hoe toowork met bestaande lokale proxyservers.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="513f5-103">Werken met bestaande lokale proxyservers</span><span class="sxs-lookup"><span data-stu-id="513f5-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="513f5-104">Dit artikel wordt uitgelegd hoe tooconfigure toepassingsproxy van Azure Active Directory (Azure AD) connectors toowork met uitgaande proxyservers.</span><span class="sxs-lookup"><span data-stu-id="513f5-104">This article explains how tooconfigure Azure Active Directory (Azure AD) Application Proxy connectors toowork with outbound proxy servers.</span></span> <span data-ttu-id="513f5-105">Het is bedoeld voor klanten met een netwerkomgevingen met bestaande proxy's.</span><span class="sxs-lookup"><span data-stu-id="513f5-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="513f5-106">We beginnen door te kijken deze belangrijkste implementatiescenario's:</span><span class="sxs-lookup"><span data-stu-id="513f5-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="513f5-107">Connectors toobypass uw lokale uitgaande proxy configureren.</span><span class="sxs-lookup"><span data-stu-id="513f5-107">Configure connectors toobypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="513f5-108">Configureer connectors toouse een uitgaande proxyconfiguratie tooaccess Azure AD-toepassingsproxy.</span><span class="sxs-lookup"><span data-stu-id="513f5-108">Configure connectors toouse an outbound proxy tooaccess Azure AD Application Proxy.</span></span>

<span data-ttu-id="513f5-109">Zie voor meer informatie over hoe connectors werken [inzicht in Azure AD-toepassingsproxy connectors](application-proxy-understand-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="513f5-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-hello-outbound-proxy"></a><span data-ttu-id="513f5-110">Hallo uitgaande proxy configureren</span><span class="sxs-lookup"><span data-stu-id="513f5-110">Configure hello outbound proxy</span></span>

<span data-ttu-id="513f5-111">Als u een uitgaande proxyconfiguratie in uw omgeving hebt, kunt u een account gebruiken met de juiste machtigingen tooconfigure Hallo uitgaande proxyconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="513f5-111">If you have an outbound proxy in your environment, use an account with appropriate permissions tooconfigure hello outbound proxy.</span></span> <span data-ttu-id="513f5-112">Omdat Hallo installatieprogramma wordt uitgevoerd in de context Hallo van Hallo-gebruiker die Hallo installatie doet, kunt u Hallo-configuratie controleren met behulp van Microsoft Edge of een andere internetbrowser.</span><span class="sxs-lookup"><span data-stu-id="513f5-112">Because hello installer runs in hello context of hello user who's doing hello installation, you can check hello configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="513f5-113">tooconfigure hello proxy-instellingen in Microsoft Edge:</span><span class="sxs-lookup"><span data-stu-id="513f5-113">tooconfigure hello proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="513f5-114">Ga te**instellingen** > **weergave geavanceerde instellingen** > **Open Proxy-instellingen** > **handmatige Proxy-instellingen** .</span><span class="sxs-lookup"><span data-stu-id="513f5-114">Go too**Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="513f5-115">Stel **een proxyserver gebruiken** te**op**, selecteer Hallo **Hallo proxyserver niet gebruiken voor lokale adressen (intranet)** selectievakje en het Hallo-adres en poort tooreflect wijzigen uw lokale proxyserver.</span><span class="sxs-lookup"><span data-stu-id="513f5-115">Set **Use a proxy server** too**On**, select hello **Don’t use hello proxy server for local (intranet) addresses** check box, and then change hello address and port tooreflect your local proxy server.</span></span>
3. <span data-ttu-id="513f5-116">Vul in Hallo nodig proxy-instellingen.</span><span class="sxs-lookup"><span data-stu-id="513f5-116">Fill in hello necessary proxy settings.</span></span>

   ![In het dialoogvenster voor proxy-instellingen](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="513f5-118">Uitgaande bypass-proxy 's</span><span class="sxs-lookup"><span data-stu-id="513f5-118">Bypass outbound proxies</span></span>

<span data-ttu-id="513f5-119">Connectors hebben onderliggende besturingssysteemonderdelen die uitgaande aanvragen.</span><span class="sxs-lookup"><span data-stu-id="513f5-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="513f5-120">Deze onderdelen worden automatisch een proxyserver op Hallo netwerk toolocate geprobeerd.</span><span class="sxs-lookup"><span data-stu-id="513f5-120">These components automatically attempt toolocate a proxy server on hello network.</span></span> <span data-ttu-id="513f5-121">Ze Web Proxy Auto-Discovery (WPAD) gebruiken als deze ingeschakeld in Hallo-omgeving.</span><span class="sxs-lookup"><span data-stu-id="513f5-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in hello environment.</span></span>

<span data-ttu-id="513f5-122">Hallo besturingssysteemonderdelen proberen toolocate een proxyserver door middel van een DNS-zoekactie voor wpad.domainsuffix.</span><span class="sxs-lookup"><span data-stu-id="513f5-122">hello OS components attempt toolocate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="513f5-123">Als dit wordt omgezet in DNS, een HTTP-aanvraag vervolgens gemaakt toohello IP-adres voor wpad.dat.</span><span class="sxs-lookup"><span data-stu-id="513f5-123">If this resolves in DNS, an HTTP request is then made toohello IP address for wpad.dat.</span></span> <span data-ttu-id="513f5-124">Deze aanvraag wordt Hallo configuratiescript in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="513f5-124">This request becomes hello proxy configuration script in your environment.</span></span> <span data-ttu-id="513f5-125">Hallo-connector gebruikt dit script tooselect een uitgaande proxyserver.</span><span class="sxs-lookup"><span data-stu-id="513f5-125">hello connector uses this script tooselect an outbound proxy server.</span></span> <span data-ttu-id="513f5-126">Echter, connector verkeer mogelijk nog steeds niet via, vanwege de extra configuratie-instellingen die nodig zijn op Hallo proxy.</span><span class="sxs-lookup"><span data-stu-id="513f5-126">However, connector traffic might still not go through, because of additional configuration settings needed on hello proxy.</span></span>

<span data-ttu-id="513f5-127">U kunt configureren Hallo connector toobypass uw lokale proxy tooensure dat wordt gebruikt directe connectiviteit toohello Azure services.</span><span class="sxs-lookup"><span data-stu-id="513f5-127">You can configure hello connector toobypass your on-premises proxy tooensure that it uses direct connectivity toohello Azure services.</span></span> <span data-ttu-id="513f5-128">Het is raadzaam deze benadering (als dit het netwerkbeleid mogelijk), omdat het betekent dat u een minder configuratie toomaintain hebt.</span><span class="sxs-lookup"><span data-stu-id="513f5-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration toomaintain.</span></span>

<span data-ttu-id="513f5-129">toodisable uitgaande proxyconfiguratie gebruik voor Hallo-connector Hallo C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config bestand bewerken en toevoegen van Hallo *system.net* sectie in dit voorbeeld wordt weergegeven :</span><span class="sxs-lookup"><span data-stu-id="513f5-129">toodisable outbound proxy usage for hello connector, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
<span data-ttu-id="513f5-130">een vergelijkbare wijziging toohello ApplicationProxyConnectorUpdaterService.exe.config bestand in C:\Program Files\Microsoft AAD App Proxy Connector Updater tooensure dat Hallo Connector Updater service ook Hallo proxy, omzeilt maken</span><span class="sxs-lookup"><span data-stu-id="513f5-130">tooensure that hello Connector Updater service also bypasses hello proxy, make a similar change toohello ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="513f5-131">Worden ervoor toomake kopieën van de oorspronkelijke bestanden hello, geval u toorevert toohello standaard .config-bestanden die nodig is.</span><span class="sxs-lookup"><span data-stu-id="513f5-131">Be sure toomake copies of hello original files, in case you need toorevert toohello default .config files.</span></span>

## <a name="use-hello-outbound-proxy-server"></a><span data-ttu-id="513f5-132">Hallo uitgaande proxyserver gebruiken</span><span class="sxs-lookup"><span data-stu-id="513f5-132">Use hello outbound proxy server</span></span>

<span data-ttu-id="513f5-133">Sommige omgevingen is vereist voor alle uitgaande verkeer toogo via een uitgaande proxyconfiguratie, zonder uitzondering.</span><span class="sxs-lookup"><span data-stu-id="513f5-133">Some environments require all outbound traffic toogo through an outbound proxy, without exception.</span></span> <span data-ttu-id="513f5-134">Als gevolg hiervan kan omzeilen Hallo proxy niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="513f5-134">As a result, bypassing hello proxy is not an option.</span></span>

<span data-ttu-id="513f5-135">Hallo connector verkeer toogo via Hallo uitgaande proxyconfiguratie, kunt u configureren zoals wordt weergegeven in het volgende diagram Hallo:</span><span class="sxs-lookup"><span data-stu-id="513f5-135">You can configure hello connector traffic toogo through hello outbound proxy, as shown in hello following diagram:</span></span>

 ![Configureren van de connector verkeer toogo via een uitgaande proxyconfiguratie tooAzure AD-toepassingsproxy](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="513f5-137">Als gevolg hiervan hebben alleen uitgaand verkeer, er is geen tooconfigure moeten binnenkomende toegang via de firewalls.</span><span class="sxs-lookup"><span data-stu-id="513f5-137">As a result of having only outbound traffic, there's no need tooconfigure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a><span data-ttu-id="513f5-138">Stap 1: Hallo-connector configureren en gerelateerde services toogo via Hallo uitgaande proxyconfiguratie</span><span class="sxs-lookup"><span data-stu-id="513f5-138">Step 1: Configure hello connector and related services toogo through hello outbound proxy</span></span>

<span data-ttu-id="513f5-139">Gedekt eerder als WPAD is ingeschakeld in de omgeving Hallo en juist geconfigureerde, Hallo-connector wordt automatisch gedetecteerd door Hallo uitgaande proxyconfiguratie server uit en proberen toouse deze.</span><span class="sxs-lookup"><span data-stu-id="513f5-139">As covered earlier, if WPAD is enabled in hello environment and configured appropriately, hello connector will automatically discover hello outbound proxy server and attempt toouse it.</span></span> <span data-ttu-id="513f5-140">U kunt echter expliciet Hallo connector toogo via een uitgaande proxy configureren.</span><span class="sxs-lookup"><span data-stu-id="513f5-140">However, you can explicitly configure hello connector toogo through an outbound proxy.</span></span>

<span data-ttu-id="513f5-141">toodo dus Hallo C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config bestand bewerken en toevoegen van Hallo *system.net* sectie in dit voorbeeld wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="513f5-141">toodo so, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample.</span></span> <span data-ttu-id="513f5-142">Wijziging *proxyserver:8080* tooreflect uw lokale proxy-servernaam of IP-adres en Hallo dat deze luistert op poort.</span><span class="sxs-lookup"><span data-stu-id="513f5-142">Change *proxyserver:8080* tooreflect your local proxy server name or IP address, and hello port that it's listening on.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

<span data-ttu-id="513f5-143">Configureer vervolgens Hallo Connector Updater toouse Hallo-serviceproxy door het maken van een vergelijkbare wijziging toohello bestand in C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span><span class="sxs-lookup"><span data-stu-id="513f5-143">Next, configure hello Connector Updater service toouse hello proxy by making a similar change toohello file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a><span data-ttu-id="513f5-144">Stap 2: Hallo proxy tooallow verkeer van het Hallo-connector en verwante services tooflow via configureren</span><span class="sxs-lookup"><span data-stu-id="513f5-144">Step 2: Configure hello proxy tooallow traffic from hello connector and related services tooflow through</span></span>

<span data-ttu-id="513f5-145">Er zijn vier aspecten tooconsider op Hallo uitgaande proxyconfiguratie:</span><span class="sxs-lookup"><span data-stu-id="513f5-145">There are four aspects tooconsider at hello outbound proxy:</span></span>
* <span data-ttu-id="513f5-146">Uitgaande proxy-regels</span><span class="sxs-lookup"><span data-stu-id="513f5-146">Proxy outbound rules</span></span>
* <span data-ttu-id="513f5-147">Proxyverificatie</span><span class="sxs-lookup"><span data-stu-id="513f5-147">Proxy authentication</span></span>
* <span data-ttu-id="513f5-148">Proxy-poorten</span><span class="sxs-lookup"><span data-stu-id="513f5-148">Proxy ports</span></span>
* <span data-ttu-id="513f5-149">SSL-inspectie</span><span class="sxs-lookup"><span data-stu-id="513f5-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="513f5-150">Uitgaande proxy-regels</span><span class="sxs-lookup"><span data-stu-id="513f5-150">Proxy outbound rules</span></span>
<span data-ttu-id="513f5-151">Toegang toohello volgende eindpunten voor connector-Servicetoegang toestaan:</span><span class="sxs-lookup"><span data-stu-id="513f5-151">Allow access toohello following endpoints for connector service access:</span></span>

* <span data-ttu-id="513f5-152">*. msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="513f5-152">*.msappproxy.net</span></span>
* <span data-ttu-id="513f5-153">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="513f5-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="513f5-154">Voor de initiële registratie toestaan toegang toohello eindpunten te volgen:</span><span class="sxs-lookup"><span data-stu-id="513f5-154">For initial registration, allow access toohello following endpoints:</span></span>

* <span data-ttu-id="513f5-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="513f5-155">login.windows.net</span></span>
* <span data-ttu-id="513f5-156">Login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="513f5-156">login.microsoftonline.com</span></span>

<span data-ttu-id="513f5-157">Als u kan geen verbinding met FQDN-naam en moeten toospecify IP-adresbereiken in plaats daarvan gebruik deze opties:</span><span class="sxs-lookup"><span data-stu-id="513f5-157">If you can't allow connectivity by FQDN and need toospecify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="513f5-158">Hallo connector uitgaande toegang tooall bestemmingen toestaan.</span><span class="sxs-lookup"><span data-stu-id="513f5-158">Allow hello connector outbound access tooall destinations.</span></span>
* <span data-ttu-id="513f5-159">Hallo connector uitgaande toegang te verlenen[Azure datacenter IP-adresbereiken](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="513f5-159">Allow hello connector outbound access too[Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="513f5-160">Hallo uitdaging met het gebruik van Hallo lijst met Azure datacenter IP-adresbereiken is wekelijks wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="513f5-160">hello challenge with using hello list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="513f5-161">U moet tooput een proces in place tooensure uw toegangsregels worden dienovereenkomstig bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="513f5-161">You need tooput a process in place tooensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="513f5-162">Proxyverificatie</span><span class="sxs-lookup"><span data-stu-id="513f5-162">Proxy authentication</span></span>

<span data-ttu-id="513f5-163">Proxyverificatie is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="513f5-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="513f5-164">We bevelen aan huidige is tooallow Hallo connector anonieme toegang toohello Internet doelen.</span><span class="sxs-lookup"><span data-stu-id="513f5-164">Our current recommendation is tooallow hello connector anonymous access toohello Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="513f5-165">Proxy-poorten</span><span class="sxs-lookup"><span data-stu-id="513f5-165">Proxy ports</span></span>

<span data-ttu-id="513f5-166">Hallo-connector maakt uitgaande verbindingen op basis van SSL met Hallo CONNECT methode.</span><span class="sxs-lookup"><span data-stu-id="513f5-166">hello connector makes outbound SSL-based connections by using hello CONNECT method.</span></span> <span data-ttu-id="513f5-167">Deze methode wordt in wezen stelt u een tunnel via Hallo uitgaande proxyconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="513f5-167">This method essentially sets up a tunnel through hello outbound proxy.</span></span> <span data-ttu-id="513f5-168">Hallo proxy server tooallow tooports 443 en 80 tunneling configureren.</span><span class="sxs-lookup"><span data-stu-id="513f5-168">Configure hello proxy server tooallow tunneling tooports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="513f5-169">Wanneer Service Bus wordt uitgevoerd via HTTPS, poort 443 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="513f5-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="513f5-170">Echter, standaard, Service Bus probeert rechtstreekse TCP-verbindingen en valt terug tooHTTPS alleen als directe verbinding mislukt.</span><span class="sxs-lookup"><span data-stu-id="513f5-170">However, by default, Service Bus attempts direct TCP connections and falls back tooHTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="513f5-171">tooensure die Service Bus verkeer ook wordt verzonden via de uitgaande proxyserver Hallo Hallo, zorg die Hallo-connector kan niet rechtstreeks verbinding maken met toohello Azure services voor poorten 9350, 9352 en 5671.</span><span class="sxs-lookup"><span data-stu-id="513f5-171">tooensure that hello Service Bus traffic is also sent through hello outbound proxy server, ensure that hello connector cannot directly connect toohello Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="513f5-172">SSL-inspectie</span><span class="sxs-lookup"><span data-stu-id="513f5-172">SSL inspection</span></span>
<span data-ttu-id="513f5-173">Gebruik geen SSL-inspectie voor verkeer van de connector hello, omdat er problemen optreden voor Hallo connector verkeer.</span><span class="sxs-lookup"><span data-stu-id="513f5-173">Do not use SSL inspection for hello connector traffic, because it causes problems for hello connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="513f5-174">Connector-proxy problemen en service-verbindingsproblemen oplossen</span><span class="sxs-lookup"><span data-stu-id="513f5-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="513f5-175">U ziet nu al het verkeer via Hallo proxy.</span><span class="sxs-lookup"><span data-stu-id="513f5-175">Now you should see all traffic flowing through hello proxy.</span></span> <span data-ttu-id="513f5-176">Als u problemen ondervindt, kan Hallo volgende informatie over probleemoplossing helpen.</span><span class="sxs-lookup"><span data-stu-id="513f5-176">If you have problems, hello following troubleshooting information should help.</span></span>

<span data-ttu-id="513f5-177">Hallo van de beste manier tooidentify en het oplossen van de verbinding van connector problemen tootake vastleggen van een netwerk op Hallo connector-service tijdens het starten van de connectorservice Hallo is.</span><span class="sxs-lookup"><span data-stu-id="513f5-177">hello best way tooidentify and troubleshoot connector connectivity issues is tootake a network capture on hello connector service while starting hello connector service.</span></span> <span data-ttu-id="513f5-178">Dit kan geen sinecure, bekijken we snelle tips voor het vastleggen en netwerktracering filteren.</span><span class="sxs-lookup"><span data-stu-id="513f5-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="513f5-179">U kunt Hallo controlehulpprogramma van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="513f5-179">You can use hello monitoring tool of your choice.</span></span> <span data-ttu-id="513f5-180">Voor de toepassing hello van dit artikel, hebben we Microsoft Network Monitor 3.4 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="513f5-180">For hello purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="513f5-181">U kunt [downloaden vanaf Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span><span class="sxs-lookup"><span data-stu-id="513f5-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="513f5-182">Hallo-voorbeelden en filters die we gebruiken in de volgende secties Hallo zijn specifieke tooNetwork Monitor, maar Hallo beginselen analysehulpprogramma toegepaste tooany zijn.</span><span class="sxs-lookup"><span data-stu-id="513f5-182">hello examples and filters that we use in hello following sections are specific tooNetwork Monitor, but hello principles can be applied tooany analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="513f5-183">Uitvoeren van een vastleggen met behulp van Network Monitor</span><span class="sxs-lookup"><span data-stu-id="513f5-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="513f5-184">toostart opnemen:</span><span class="sxs-lookup"><span data-stu-id="513f5-184">toostart a capture:</span></span>

1. <span data-ttu-id="513f5-185">Open Netwerkmonitor en klikt u op **nieuwe vastleggen**.</span><span class="sxs-lookup"><span data-stu-id="513f5-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="513f5-186">Klik op Hallo **Start** knop.</span><span class="sxs-lookup"><span data-stu-id="513f5-186">Click hello **Start** button.</span></span>

   ![Het venster van Network Monitor](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="513f5-188">Nadat u een opname hebt voltooid, klikt u op Hallo **stoppen** knop tooend deze.</span><span class="sxs-lookup"><span data-stu-id="513f5-188">After you complete a capture, click hello **Stop** button tooend it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="513f5-189">Een maken van connector verkeer</span><span class="sxs-lookup"><span data-stu-id="513f5-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="513f5-190">Voer voor de eerste probleemoplossing Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="513f5-190">For initial troubleshooting, perform hello following steps:</span></span>

1. <span data-ttu-id="513f5-191">Van services.msc hello Azure AD-Application Proxy Connector-service niet stoppen.</span><span class="sxs-lookup"><span data-stu-id="513f5-191">From services.msc, stop hello Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="513f5-192">Hallo netwerkopname starten.</span><span class="sxs-lookup"><span data-stu-id="513f5-192">Start hello network capture.</span></span>
3. <span data-ttu-id="513f5-193">Hello Azure AD-Application Proxy Connector-service starten.</span><span class="sxs-lookup"><span data-stu-id="513f5-193">Start hello Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="513f5-194">Hallo netwerkopname stoppen.</span><span class="sxs-lookup"><span data-stu-id="513f5-194">Stop hello network capture.</span></span>

   ![Azure AD Connector voor toepassingsproxy-service in services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a><span data-ttu-id="513f5-196">Bekijkt hello aanvragen van Hallo connector toohello proxyserver</span><span class="sxs-lookup"><span data-stu-id="513f5-196">Look at hello requests from hello connector toohello proxy server</span></span>

<span data-ttu-id="513f5-197">Nu u hebt een netwerkopname, bent u klaar toofilter deze.</span><span class="sxs-lookup"><span data-stu-id="513f5-197">Now that you’ve got a network capture, you're ready toofilter it.</span></span> <span data-ttu-id="513f5-198">Hallo sleutel toolooking op Hallo trace is begrijpen hoe toofilter Hallo vastleggen.</span><span class="sxs-lookup"><span data-stu-id="513f5-198">hello key toolooking at hello trace is understanding how toofilter hello capture.</span></span>

<span data-ttu-id="513f5-199">Een filter is als volgt (waarbij 8080 Hallo service proxypoort is):</span><span class="sxs-lookup"><span data-stu-id="513f5-199">One filter is as follows (where 8080 is hello proxy service port):</span></span>

<span data-ttu-id="513f5-200">**(http. Aanvraag of http. Antwoord) en tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="513f5-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="513f5-201">Als u dit filter in Hallo **Filter weergeven** venster en selecteer **toepassen**, wordt vastgelegd Hallo-verkeer op basis van Hallo filter gefilterd.</span><span class="sxs-lookup"><span data-stu-id="513f5-201">If you enter this filter in hello **Display Filter** window and select **Apply**, it filters hello captured traffic based on hello filter.</span></span>

<span data-ttu-id="513f5-202">Hallo voorgaande filter geeft alleen Hallo HTTP-aanvragen en antwoorden van Hallo proxypoort.</span><span class="sxs-lookup"><span data-stu-id="513f5-202">hello preceding filter shows just hello HTTP requests and responses to/from hello proxy port.</span></span> <span data-ttu-id="513f5-203">Voor een connector starten waarbij Hallo connector geconfigureerde toouse een proxyserver is, zou Hallo filter ongeveer het volgende weergegeven:</span><span class="sxs-lookup"><span data-stu-id="513f5-203">For a connector startup where hello connector is configured toouse a proxy server, hello filter would show something like this:</span></span>

 ![Voorbeeld van de lijst met gefilterde HTTP-aanvragen en antwoorden](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="513f5-205">U nu zoekt specifiek Hallo die Connect aanvragen die communicatie met de proxyserver Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="513f5-205">You're now specifically looking for hello CONNECT requests that show communication with hello proxy server.</span></span> <span data-ttu-id="513f5-206">Als dit lukt krijgt u een HTTP-OK (200) antwoord.</span><span class="sxs-lookup"><span data-stu-id="513f5-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="513f5-207">Als u de overige reactiecodes zoals 407 of 502, ziet is Hallo-proxy die verificatie vereist of niet Hallo verkeer toestaat voor een andere reden.</span><span class="sxs-lookup"><span data-stu-id="513f5-207">If you see other response codes, such as 407 or 502, hello proxy is requiring authentication or not allowing hello traffic for some other reason.</span></span> <span data-ttu-id="513f5-208">Nu benaderen u het ondersteuningsteam van proxy server.</span><span class="sxs-lookup"><span data-stu-id="513f5-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="513f5-209">Identificeren van mislukte pogingen voor TCP-verbinding</span><span class="sxs-lookup"><span data-stu-id="513f5-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="513f5-210">Hallo is andere veelvoorkomende scenario dat u mogelijk geïnteresseerd in hello connector probeert tooconnect rechtstreeks, maar niet lukt.</span><span class="sxs-lookup"><span data-stu-id="513f5-210">hello other common scenario that you may be interested in is when hello connector is trying tooconnect directly, but it's failing.</span></span>

<span data-ttu-id="513f5-211">Er is een ander filter van Network Monitor waarmee u tooeasily dit probleem vast te stellen:</span><span class="sxs-lookup"><span data-stu-id="513f5-211">Another Network Monitor filter that helps you tooeasily identify this problem is:</span></span>

<span data-ttu-id="513f5-212">**de eigenschap. TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="513f5-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="513f5-213">Een SYN-pakket is het eerste pakket Hallo verzonden tooestablish een TCP-verbinding.</span><span class="sxs-lookup"><span data-stu-id="513f5-213">A SYN packet is hello first packet sent tooestablish a TCP connection.</span></span> <span data-ttu-id="513f5-214">Als dit pakket een antwoord retourneren heeft niet, wordt de Hallo SYN reattempted.</span><span class="sxs-lookup"><span data-stu-id="513f5-214">If this packet doesn’t return a response, hello SYN is reattempted.</span></span> <span data-ttu-id="513f5-215">Kunt u Hallo toosee filter vóór alle verzonden SYN.</span><span class="sxs-lookup"><span data-stu-id="513f5-215">You can use hello preceding filter toosee any retransmitted SYNs.</span></span> <span data-ttu-id="513f5-216">Vervolgens kunt u controleren of deze SYN tooany connector-verkeer overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="513f5-216">Then, you can check whether these SYNs correspond tooany connector-related traffic.</span></span>

<span data-ttu-id="513f5-217">Hallo volgende voorbeeld ziet u een mislukte verbindingspoging tooService buspoort 9352:</span><span class="sxs-lookup"><span data-stu-id="513f5-217">hello following example shows a failed connection attempt tooService Bus port 9352:</span></span>

 ![Voorbeeld van een antwoord voor een mislukte poging](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="513f5-219">Als u ongeveer Hallo vóór het antwoord ziet, probeert Hallo connector toocommunicate rechtstreeks met hello Azure Service Bus-service.</span><span class="sxs-lookup"><span data-stu-id="513f5-219">If you see something like hello preceding response, hello connector is trying toocommunicate directly with hello Azure Service Bus service.</span></span> <span data-ttu-id="513f5-220">Als u verwacht Hallo connector toomake rechtstreekse verbindingen toohello Azure dat-services, dit antwoord is een duidelijke aanwijzing is dat er een probleem met het netwerk of de firewall.</span><span class="sxs-lookup"><span data-stu-id="513f5-220">If you expect hello connector toomake direct connections toohello Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="513f5-221">Als u een proxyserver voor geconfigureerde toouse, kan deze reactie kan betekenen dat Service Bus een directe TCP-verbinding probeert voordat u de tooattempting een verbinding via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="513f5-221">If you are configured toouse a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching tooattempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="513f5-222">Analyse van netwerk-tracering is niet voor iedereen.</span><span class="sxs-lookup"><span data-stu-id="513f5-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="513f5-223">Het kan wel een waardevol hulpmiddel tooget snelle informatie over wat met uw netwerk gebeurt er.</span><span class="sxs-lookup"><span data-stu-id="513f5-223">But it can be a valuable tool tooget quick information about what's going on with your network.</span></span>

<span data-ttu-id="513f5-224">Als u toostruggle met verbindingsproblemen connector doorgaat, maakt u een ticket aan ons ondersteuningsteam.</span><span class="sxs-lookup"><span data-stu-id="513f5-224">If you continue toostruggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="513f5-225">Hallo-team kan u helpen verder op te lossen.</span><span class="sxs-lookup"><span data-stu-id="513f5-225">hello team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="513f5-226">Zie voor meer informatie over het oplossen van problemen met de Connector voor toepassingsproxy [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="513f5-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="513f5-227">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="513f5-227">Next steps</span></span>

[<span data-ttu-id="513f5-228">Azure AD-toepassingsproxy connectors begrijpen</span><span class="sxs-lookup"><span data-stu-id="513f5-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="513f5-229">
[Hoe toosilently hello Azure AD-Application Proxy Connector installeren](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="513f5-229">
[How toosilently install hello Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
