---
title: Werken met bestaande on-premises proxy-servers en Azure AD | Microsoft Docs
description: Bevat informatie over het werken met bestaande lokale proxyservers.
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
ms.openlocfilehash: bdca442755507c4ffe8d43692c5b7f2aa3a746f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="4ac0c-103">Werken met bestaande lokale proxyservers</span><span class="sxs-lookup"><span data-stu-id="4ac0c-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="4ac0c-104">In dit artikel wordt uitgelegd hoe connectors werken met uitgaande proxyservers toepassingsproxy van Azure Active Directory (Azure AD) configureren.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-104">This article explains how to configure Azure Active Directory (Azure AD) Application Proxy connectors to work with outbound proxy servers.</span></span> <span data-ttu-id="4ac0c-105">Het is bedoeld voor klanten met een netwerkomgevingen met bestaande proxy's.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="4ac0c-106">We beginnen door te kijken deze belangrijkste implementatiescenario's:</span><span class="sxs-lookup"><span data-stu-id="4ac0c-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="4ac0c-107">Connectors configureren voor uw lokale uitgaande proxy overslaan.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-107">Configure connectors to bypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="4ac0c-108">Connectors configureren voor een uitgaande proxyconfiguratie gebruiken voor toegang tot Azure AD-toepassingsproxy.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-108">Configure connectors to use an outbound proxy to access Azure AD Application Proxy.</span></span>

<span data-ttu-id="4ac0c-109">Zie voor meer informatie over hoe connectors werken [inzicht in Azure AD-toepassingsproxy connectors](application-proxy-understand-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="4ac0c-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-the-outbound-proxy"></a><span data-ttu-id="4ac0c-110">De uitgaande proxy configureren</span><span class="sxs-lookup"><span data-stu-id="4ac0c-110">Configure the outbound proxy</span></span>

<span data-ttu-id="4ac0c-111">Als u een uitgaande proxyconfiguratie in uw omgeving hebt, gebruik een account met de juiste machtigingen voor het configureren van de uitgaande proxyconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-111">If you have an outbound proxy in your environment, use an account with appropriate permissions to configure the outbound proxy.</span></span> <span data-ttu-id="4ac0c-112">Omdat het installatieprogramma wordt uitgevoerd in de context van de gebruiker die de installatie uitvoert, kunt u de configuratie controleren met behulp van Microsoft Edge of een andere internetbrowser.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-112">Because the installer runs in the context of the user who's doing the installation, you can check the configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="4ac0c-113">De proxy-instellingen in Microsoft Edge configureren:</span><span class="sxs-lookup"><span data-stu-id="4ac0c-113">To configure the proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="4ac0c-114">Ga naar **instellingen** > **weergave geavanceerde instellingen** > **Proxy-instellingen openen** > **installatie handmatige Proxy**.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-114">Go to **Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="4ac0c-115">Stel **een proxyserver gebruiken** naar **op**, selecteer de **de proxyserver niet gebruiken voor lokale adressen (intranet)** selectievakje en wijzig vervolgens het adres en poort in overeenstemming met uw lokale proxyserver.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-115">Set **Use a proxy server** to **On**, select the **Don’t use the proxy server for local (intranet) addresses** check box, and then change the address and port to reflect your local proxy server.</span></span>
3. <span data-ttu-id="4ac0c-116">Vul de benodigde proxy-instellingen.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-116">Fill in the necessary proxy settings.</span></span>

   ![In het dialoogvenster voor proxy-instellingen](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="4ac0c-118">Uitgaande bypass-proxy 's</span><span class="sxs-lookup"><span data-stu-id="4ac0c-118">Bypass outbound proxies</span></span>

<span data-ttu-id="4ac0c-119">Connectors hebben onderliggende besturingssysteemonderdelen die uitgaande aanvragen.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="4ac0c-120">Deze onderdelen wordt automatisch geprobeerd het vinden van een proxyserver op het netwerk.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-120">These components automatically attempt to locate a proxy server on the network.</span></span> <span data-ttu-id="4ac0c-121">Ze Web Proxy Auto-Discovery (WPAD) gebruiken als deze ingeschakeld in de omgeving.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in the environment.</span></span>

<span data-ttu-id="4ac0c-122">De OS-componenten probeert te vinden van een proxyserver door middel van een DNS-zoekactie voor wpad.domainsuffix.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-122">The OS components attempt to locate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="4ac0c-123">Als dit wordt omgezet in DNS, wordt vervolgens een HTTP-aanvraag naar de IP-adres voor wpad.dat gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-123">If this resolves in DNS, an HTTP request is then made to the IP address for wpad.dat.</span></span> <span data-ttu-id="4ac0c-124">Deze aanvraag wordt het configuratiescript in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-124">This request becomes the proxy configuration script in your environment.</span></span> <span data-ttu-id="4ac0c-125">De connector gebruikt dit script te selecteren van een server voor uitgaande proxyconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-125">The connector uses this script to select an outbound proxy server.</span></span> <span data-ttu-id="4ac0c-126">Echter, connector verkeer mogelijk nog steeds niet via, vanwege de extra configuratie-instellingen op de proxy nodig.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-126">However, connector traffic might still not go through, because of additional configuration settings needed on the proxy.</span></span>

<span data-ttu-id="4ac0c-127">U kunt de connector voor het overslaan van de lokale proxy om ervoor te zorgen dat deze gebruikmaakt van directe verbinding met de Azure-services configureren.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-127">You can configure the connector to bypass your on-premises proxy to ensure that it uses direct connectivity to the Azure services.</span></span> <span data-ttu-id="4ac0c-128">Het is raadzaam deze benadering (als dit het netwerkbeleid mogelijk), omdat het betekent dat u één minder configuratie hebt te onderhouden.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration to maintain.</span></span>

<span data-ttu-id="4ac0c-129">Bewerk het bestand C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config als wilt uitschakelen uitgaande proxyconfiguratie gebruik voor de connector, en voeg de *system.net* sectie in dit voorbeeld wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4ac0c-129">To disable outbound proxy usage for the connector, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample:</span></span>

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
<span data-ttu-id="4ac0c-130">Om ervoor te zorgen dat de service-Connector Updater ook de proxy omzeilt, moet u een vergelijkbare wijziging aanbrengt in het bestand ApplicationProxyConnectorUpdaterService.exe.config in C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-130">To ensure that the Connector Updater service also bypasses the proxy, make a similar change to the ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="4ac0c-131">Zorg kopieën van de originele bestanden te maken als u wilt terugkeren naar de standaard .config-bestanden.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-131">Be sure to make copies of the original files, in case you need to revert to the default .config files.</span></span>

## <a name="use-the-outbound-proxy-server"></a><span data-ttu-id="4ac0c-132">Uitgaande proxyserver gebruiken</span><span class="sxs-lookup"><span data-stu-id="4ac0c-132">Use the outbound proxy server</span></span>

<span data-ttu-id="4ac0c-133">Sommige omgevingen vereisen al het uitgaande verkeer door een uitgaande proxyconfiguratie, zonder uitzondering gaan.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-133">Some environments require all outbound traffic to go through an outbound proxy, without exception.</span></span> <span data-ttu-id="4ac0c-134">Als gevolg hiervan kan omzeilen van de proxy niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-134">As a result, bypassing the proxy is not an option.</span></span>

<span data-ttu-id="4ac0c-135">U kunt de connector-verkeer via de uitgaande proxyconfiguratie kunt configureren, zoals wordt weergegeven in het volgende diagram:</span><span class="sxs-lookup"><span data-stu-id="4ac0c-135">You can configure the connector traffic to go through the outbound proxy, as shown in the following diagram:</span></span>

 ![Connector-verkeer naar Azure AD-toepassingsproxy via een uitgaande proxy configureren](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="4ac0c-137">Als gevolg van gelet alleen uitgaand verkeer, is er niet nodig om binnenkomende toegang via de firewall te configureren.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-137">As a result of having only outbound traffic, there's no need to configure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-the-connector-and-related-services-to-go-through-the-outbound-proxy"></a><span data-ttu-id="4ac0c-138">Stap 1: De connector en verwante services via de uitgaande proxy configureren</span><span class="sxs-lookup"><span data-stu-id="4ac0c-138">Step 1: Configure the connector and related services to go through the outbound proxy</span></span>

<span data-ttu-id="4ac0c-139">Gedekt eerder als WPAD is ingeschakeld in de omgeving en op de juiste wijze geconfigureerd, wordt de connector automatisch detecteren van de uitgaande proxyserver en probeert te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-139">As covered earlier, if WPAD is enabled in the environment and configured appropriately, the connector will automatically discover the outbound proxy server and attempt to use it.</span></span> <span data-ttu-id="4ac0c-140">U kunt echter expliciet de connector te doorlopen een uitgaande proxyconfiguratie configureren.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-140">However, you can explicitly configure the connector to go through an outbound proxy.</span></span>

<span data-ttu-id="4ac0c-141">Om dit te doen, bewerk het bestand C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config en voeg de *system.net* sectie in dit voorbeeld wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-141">To do so, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample.</span></span> <span data-ttu-id="4ac0c-142">Wijziging *proxyserver:8080* in overeenstemming met uw lokale proxy-servernaam of IP-adres en de poort die deze luistert op.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-142">Change *proxyserver:8080* to reflect your local proxy server name or IP address, and the port that it's listening on.</span></span>

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

<span data-ttu-id="4ac0c-143">Configureer vervolgens de service-Connector Updater voor het gebruik van de proxy door een vergelijkbare wijziging aan het bestand in C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-143">Next, configure the Connector Updater service to use the proxy by making a similar change to the file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-the-proxy-to-allow-traffic-from-the-connector-and-related-services-to-flow-through"></a><span data-ttu-id="4ac0c-144">Stap 2: Configureer de proxy voor verkeer van de connector en verwante services kunnen stromen</span><span class="sxs-lookup"><span data-stu-id="4ac0c-144">Step 2: Configure the proxy to allow traffic from the connector and related services to flow through</span></span>

<span data-ttu-id="4ac0c-145">Er zijn vier aspecten rekening moet houden bij de uitgaande proxy:</span><span class="sxs-lookup"><span data-stu-id="4ac0c-145">There are four aspects to consider at the outbound proxy:</span></span>
* <span data-ttu-id="4ac0c-146">Uitgaande proxy-regels</span><span class="sxs-lookup"><span data-stu-id="4ac0c-146">Proxy outbound rules</span></span>
* <span data-ttu-id="4ac0c-147">Proxyverificatie</span><span class="sxs-lookup"><span data-stu-id="4ac0c-147">Proxy authentication</span></span>
* <span data-ttu-id="4ac0c-148">Proxy-poorten</span><span class="sxs-lookup"><span data-stu-id="4ac0c-148">Proxy ports</span></span>
* <span data-ttu-id="4ac0c-149">SSL-inspectie</span><span class="sxs-lookup"><span data-stu-id="4ac0c-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="4ac0c-150">Uitgaande proxy-regels</span><span class="sxs-lookup"><span data-stu-id="4ac0c-150">Proxy outbound rules</span></span>
<span data-ttu-id="4ac0c-151">Toegang tot de volgende eindpunten voor connector-Servicetoegang toestaan:</span><span class="sxs-lookup"><span data-stu-id="4ac0c-151">Allow access to the following endpoints for connector service access:</span></span>

* <span data-ttu-id="4ac0c-152">*. msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="4ac0c-152">*.msappproxy.net</span></span>
* <span data-ttu-id="4ac0c-153">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="4ac0c-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="4ac0c-154">Voor de initiële registratie, moet u toegang tot de volgende eindpunten toestaan:</span><span class="sxs-lookup"><span data-stu-id="4ac0c-154">For initial registration, allow access to the following endpoints:</span></span>

* <span data-ttu-id="4ac0c-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="4ac0c-155">login.windows.net</span></span>
* <span data-ttu-id="4ac0c-156">Login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="4ac0c-156">login.microsoftonline.com</span></span>

<span data-ttu-id="4ac0c-157">Als u niet kan verbinding met FQDN-naam maken en moet in plaats daarvan IP-adresbereiken opgeven, gebruikt u deze opties:</span><span class="sxs-lookup"><span data-stu-id="4ac0c-157">If you can't allow connectivity by FQDN and need to specify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="4ac0c-158">De connector uitgaande toegang tot alle bestemmingen toestaan.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-158">Allow the connector outbound access to all destinations.</span></span>
* <span data-ttu-id="4ac0c-159">De connector uitgaande toegang tot [Azure datacenter IP-adresbereiken](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="4ac0c-159">Allow the connector outbound access to [Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="4ac0c-160">De uitdaging met behulp van de lijst met Azure datacenter IP-adresbereiken is wekelijks wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-160">The challenge with using the list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="4ac0c-161">U moet het plaatsen van een proces implementeren dat ervoor zorgt dat uw toegangsregels dienovereenkomstig worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-161">You need to put a process in place to ensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="4ac0c-162">Proxyverificatie</span><span class="sxs-lookup"><span data-stu-id="4ac0c-162">Proxy authentication</span></span>

<span data-ttu-id="4ac0c-163">Proxyverificatie is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="4ac0c-164">We bevelen aan huidige is dat de connector anonieme toegang tot de Internet-doelen.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-164">Our current recommendation is to allow the connector anonymous access to the Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="4ac0c-165">Proxy-poorten</span><span class="sxs-lookup"><span data-stu-id="4ac0c-165">Proxy ports</span></span>

<span data-ttu-id="4ac0c-166">De connector maakt uitgaande SSL-verbindingen met de methode CONNECT.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-166">The connector makes outbound SSL-based connections by using the CONNECT method.</span></span> <span data-ttu-id="4ac0c-167">Deze methode wordt in wezen stelt u een tunnel via de uitgaande proxyconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-167">This method essentially sets up a tunnel through the outbound proxy.</span></span> <span data-ttu-id="4ac0c-168">De proxyserver zodat de poorten 443 en 80 tunneling configureren.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-168">Configure the proxy server to allow tunneling to ports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="4ac0c-169">Wanneer Service Bus wordt uitgevoerd via HTTPS, poort 443 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="4ac0c-170">Echter, standaard, Service Bus probeert rechtstreekse TCP-verbindingen en terugvalt op HTTPS alleen als directe verbinding mislukt.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-170">However, by default, Service Bus attempts direct TCP connections and falls back to HTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="4ac0c-171">Zorg ervoor dat de connector rechtstreeks kan geen verbinding met de Azure-services voor poorten 9350, 9352 en 5671, om te zorgen dat de Service Bus-verkeer ook wordt verzonden via de uitgaande proxyserver.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-171">To ensure that the Service Bus traffic is also sent through the outbound proxy server, ensure that the connector cannot directly connect to the Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="4ac0c-172">SSL-inspectie</span><span class="sxs-lookup"><span data-stu-id="4ac0c-172">SSL inspection</span></span>
<span data-ttu-id="4ac0c-173">Gebruik geen SSL-inspectie voor het verkeer van de connector, omdat er problemen optreden voor het verkeer van de connector.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-173">Do not use SSL inspection for the connector traffic, because it causes problems for the connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="4ac0c-174">Connector-proxy problemen en service-verbindingsproblemen oplossen</span><span class="sxs-lookup"><span data-stu-id="4ac0c-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="4ac0c-175">U ziet nu al het verkeer via de proxy.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-175">Now you should see all traffic flowing through the proxy.</span></span> <span data-ttu-id="4ac0c-176">Als u problemen hebt, moet de volgende informatie voor probleemoplossing helpen.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-176">If you have problems, the following troubleshooting information should help.</span></span>

<span data-ttu-id="4ac0c-177">De beste manier om te identificeren en oplossen van problemen met de netwerkverbinding van de connector is het nemen van een netwerkopname op de connector-service tijdens het starten van de connector-service.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-177">The best way to identify and troubleshoot connector connectivity issues is to take a network capture on the connector service while starting the connector service.</span></span> <span data-ttu-id="4ac0c-178">Dit kan geen sinecure, bekijken we snelle tips voor het vastleggen en netwerktracering filteren.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="4ac0c-179">U kunt het programma voor bewaking van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-179">You can use the monitoring tool of your choice.</span></span> <span data-ttu-id="4ac0c-180">Voor de doeleinden van dit artikel hebben we Microsoft Network Monitor 3.4 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-180">For the purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="4ac0c-181">U kunt [downloaden vanaf Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span><span class="sxs-lookup"><span data-stu-id="4ac0c-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="4ac0c-182">De voorbeelden en filters die we in de volgende secties gebruiken zijn specifiek voor Netwerkcontrole, maar de beginselen kunnen worden toegepast op alle analysehulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-182">The examples and filters that we use in the following sections are specific to Network Monitor, but the principles can be applied to any analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="4ac0c-183">Uitvoeren van een vastleggen met behulp van Network Monitor</span><span class="sxs-lookup"><span data-stu-id="4ac0c-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="4ac0c-184">Een vastleggen starten:</span><span class="sxs-lookup"><span data-stu-id="4ac0c-184">To start a capture:</span></span>

1. <span data-ttu-id="4ac0c-185">Open Netwerkmonitor en klikt u op **nieuwe vastleggen**.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="4ac0c-186">Klik op de **Start** knop.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-186">Click the **Start** button.</span></span>

   ![Het venster van Network Monitor](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="4ac0c-188">Nadat u een opname hebt voltooid, klikt u op de **stoppen** knop om te beëindigen.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-188">After you complete a capture, click the **Stop** button to end it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="4ac0c-189">Een maken van connector verkeer</span><span class="sxs-lookup"><span data-stu-id="4ac0c-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="4ac0c-190">Voer de volgende stappen uit voor de eerste probleemoplossing:</span><span class="sxs-lookup"><span data-stu-id="4ac0c-190">For initial troubleshooting, perform the following steps:</span></span>

1. <span data-ttu-id="4ac0c-191">Stop de service Azure AD-Application Proxy Connector van services.msc.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-191">From services.msc, stop the Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="4ac0c-192">Start het vastleggen van het netwerk.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-192">Start the network capture.</span></span>
3. <span data-ttu-id="4ac0c-193">Start de service Azure AD-Application Proxy Connector.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-193">Start the Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="4ac0c-194">Stop de netwerkopname.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-194">Stop the network capture.</span></span>

   ![Azure AD Connector voor toepassingsproxy-service in services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-the-requests-from-the-connector-to-the-proxy-server"></a><span data-ttu-id="4ac0c-196">Bekijk de aanvragen van de connector met de proxyserver</span><span class="sxs-lookup"><span data-stu-id="4ac0c-196">Look at the requests from the connector to the proxy server</span></span>

<span data-ttu-id="4ac0c-197">Nu u hebt een netwerkopname, bent u klaar om te filteren.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-197">Now that you’ve got a network capture, you're ready to filter it.</span></span> <span data-ttu-id="4ac0c-198">De sleutel te kijken naar de tracering is het registreren van het vastleggen te filteren.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-198">The key to looking at the trace is understanding how to filter the capture.</span></span>

<span data-ttu-id="4ac0c-199">Een filter is als volgt (8080 is de poort van de proxy-service):</span><span class="sxs-lookup"><span data-stu-id="4ac0c-199">One filter is as follows (where 8080 is the proxy service port):</span></span>

<span data-ttu-id="4ac0c-200">**(http. Aanvraag of http. Antwoord) en tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="4ac0c-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="4ac0c-201">Als u dit filter in de **Filter weergeven** venster en selecteer **toepassen**, wordt de vastgelegde verkeer op basis van het filter gefilterd.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-201">If you enter this filter in the **Display Filter** window and select **Apply**, it filters the captured traffic based on the filter.</span></span>

<span data-ttu-id="4ac0c-202">Het voorgaande filter geeft alleen de HTTP-aanvragen en antwoorden van de proxypoort.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-202">The preceding filter shows just the HTTP requests and responses to/from the proxy port.</span></span> <span data-ttu-id="4ac0c-203">Voor een connector starten waarin de connector is geconfigureerd voor gebruik van een proxyserver, het filter, ziet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="4ac0c-203">For a connector startup where the connector is configured to use a proxy server, the filter would show something like this:</span></span>

 ![Voorbeeld van de lijst met gefilterde HTTP-aanvragen en antwoorden](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="4ac0c-205">U nu zoekt specifiek de CONNECT-aanvragen die communicatie met de proxyserver weergeven.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-205">You're now specifically looking for the CONNECT requests that show communication with the proxy server.</span></span> <span data-ttu-id="4ac0c-206">Als dit lukt krijgt u een HTTP-OK (200) antwoord.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="4ac0c-207">Als u overige reactiecodes zoals 407 of 502, wordt de proxy die verificatie vereist of niet de verkeer toestaat voor een andere reden.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-207">If you see other response codes, such as 407 or 502, the proxy is requiring authentication or not allowing the traffic for some other reason.</span></span> <span data-ttu-id="4ac0c-208">Nu benaderen u het ondersteuningsteam van proxy server.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="4ac0c-209">Identificeren van mislukte pogingen voor TCP-verbinding</span><span class="sxs-lookup"><span data-stu-id="4ac0c-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="4ac0c-210">Het andere gangbare scenario die u mogelijk geïnteresseerd in is de connector probeert rechtstreeks verbinding te maken, maar niet lukt.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-210">The other common scenario that you may be interested in is when the connector is trying to connect directly, but it's failing.</span></span>

<span data-ttu-id="4ac0c-211">Een ander filter van Network Monitor die u helpt bij het herkennen van dit probleem is:</span><span class="sxs-lookup"><span data-stu-id="4ac0c-211">Another Network Monitor filter that helps you to easily identify this problem is:</span></span>

<span data-ttu-id="4ac0c-212">**de eigenschap. TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="4ac0c-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="4ac0c-213">Een pakket SYN is het eerste pakket verzonden naar TCP-verbinding wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-213">A SYN packet is the first packet sent to establish a TCP connection.</span></span> <span data-ttu-id="4ac0c-214">Als dit pakket een antwoord retourneren heeft niet, wordt de SYN reattempted.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-214">If this packet doesn’t return a response, the SYN is reattempted.</span></span> <span data-ttu-id="4ac0c-215">De voorgaande filter kunt u eventuele verzonden SYN Zie.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-215">You can use the preceding filter to see any retransmitted SYNs.</span></span> <span data-ttu-id="4ac0c-216">Vervolgens kunt u controleren of deze SYN komen met een connector-verkeer overeen.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-216">Then, you can check whether these SYNs correspond to any connector-related traffic.</span></span>

<span data-ttu-id="4ac0c-217">Het volgende voorbeeld ziet u een mislukte verbindingspoging met Service Bus-poort 9352:</span><span class="sxs-lookup"><span data-stu-id="4ac0c-217">The following example shows a failed connection attempt to Service Bus port 9352:</span></span>

 ![Voorbeeld van een antwoord voor een mislukte poging](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="4ac0c-219">Als u dat lijkt op het vorige antwoord ziet, wordt de connector probeert te communiceren rechtstreeks met de Azure Service Bus-service.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-219">If you see something like the preceding response, the connector is trying to communicate directly with the Azure Service Bus service.</span></span> <span data-ttu-id="4ac0c-220">Als u verwacht de connector dat voor het rechtstreeks verbinding maken met de Azure-services, is dit antwoord een duidelijke aanwijzing dat er een probleem met het netwerk of de firewall.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-220">If you expect the connector to make direct connections to the Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="4ac0c-221">Als u zijn geconfigureerd voor een proxyserver gebruiken, kan deze reactie kan betekenen dat Service Bus een directe TCP-verbinding probeert voordat u probeert een verbinding via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-221">If you are configured to use a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching to attempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="4ac0c-222">Analyse van netwerk-tracering is niet voor iedereen.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="4ac0c-223">Het kan wel een waardevol hulpmiddel voor snelle informatie over wat met uw netwerk gebeurt er.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-223">But it can be a valuable tool to get quick information about what's going on with your network.</span></span>

<span data-ttu-id="4ac0c-224">Als u met problemen met de netwerkverbinding van de connector is het moeilijk doorgaat, maakt u een ticket aan ons ondersteuningsteam.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-224">If you continue to struggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="4ac0c-225">Het team kan u helpen bij problemen op te lossen.</span><span class="sxs-lookup"><span data-stu-id="4ac0c-225">The team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="4ac0c-226">Zie voor meer informatie over het oplossen van problemen met de Connector voor toepassingsproxy [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="4ac0c-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ac0c-227">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4ac0c-227">Next steps</span></span>

[<span data-ttu-id="4ac0c-228">Azure AD-toepassingsproxy connectors begrijpen</span><span class="sxs-lookup"><span data-stu-id="4ac0c-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="4ac0c-229">
[Het installeren van de Azure AD Application Proxy Connector achtergrond](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="4ac0c-229">
[How to silently install the Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
