---
title: Meerdere sites met Azure Application Gateway | Microsoft Docs
description: Deze pagina bevat instructies voor het configureren van een bestaande Azure application gateway voor het hosten van meerdere webtoepassingen op dezelfde gateway met de Azure-portal.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 84bd62ae17b7f7ba4cd815ef1f9880679607ebce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="f9e59-103">Een bestaande toepassingsgateway voor het hosten van meerdere webtoepassingen configureren</span><span class="sxs-lookup"><span data-stu-id="f9e59-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f9e59-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f9e59-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="f9e59-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9e59-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="f9e59-106">Meerdere hosting-site, kunt u meer dan een webtoepassing op dezelfde toepassingsgateway implementeren.</span><span class="sxs-lookup"><span data-stu-id="f9e59-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="f9e59-107">Is afhankelijk van de aanwezigheid van de host-header in de binnenkomende HTTP-aanvraag om te bepalen welke listener verkeer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="f9e59-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="f9e59-108">De listener stuurt vervolgens verkeer naar de juiste back-endpool zoals geconfigureerd in de definitie van de gateway.</span><span class="sxs-lookup"><span data-stu-id="f9e59-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="f9e59-109">In webtoepassingen SSL is ingeschakeld, is de toepassingsgateway afhankelijk van de Server de naam van vermelding (SNI)-extensie voor kiest u de juiste listener voor internetverkeer.</span><span class="sxs-lookup"><span data-stu-id="f9e59-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="f9e59-110">Vaak gebruikt voor het hosten van meerdere site is van aanvragen verdelen over voor verschillende webdomeinen op verschillende back-endserver opslaggroepen.</span><span class="sxs-lookup"><span data-stu-id="f9e59-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="f9e59-111">Op dezelfde manier kunnen meerdere subdomeinen van het hoofddomein dezelfde ook worden gehost op dezelfde toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="f9e59-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="f9e59-112">Scenario</span><span class="sxs-lookup"><span data-stu-id="f9e59-112">Scenario</span></span>

<span data-ttu-id="f9e59-113">In het volgende voorbeeld toepassingsgateway verkeer voor contoso.com en fabrikam.com bedient met twee back-endserver van toepassingen: contoso-servergroep en fabrikam-servergroep.</span><span class="sxs-lookup"><span data-stu-id="f9e59-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="f9e59-114">Vergelijkbare setup kan worden gebruikt voor de host subdomeinen zoals app.contoso.com en blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="f9e59-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![scenario voor meerdere locaties][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="f9e59-116">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="f9e59-116">Before you begin</span></span>

<span data-ttu-id="f9e59-117">Dit scenario voegt ondersteuning voor meerdere locaties aan een bestaande toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="f9e59-117">This scenario adds multi-site support to an existing application gateway.</span></span> <span data-ttu-id="f9e59-118">Als u dit scenario, moet een bestaande toepassingsgateway beschikbaar om te configureren.</span><span class="sxs-lookup"><span data-stu-id="f9e59-118">To complete this scenario, an existing application gateway needs to be available to configure.</span></span> <span data-ttu-id="f9e59-119">Ga naar [een toepassingsgateway maken met behulp van de portal](application-gateway-create-gateway-portal.md) voor informatie over het maken van een basic-toepassingsgateway in de portal.</span><span class="sxs-lookup"><span data-stu-id="f9e59-119">Visit [Create an application gateway by using the portal](application-gateway-create-gateway-portal.md) to learn how to create a basic application gateway in the portal.</span></span>

<span data-ttu-id="f9e59-120">Hier volgen de stappen die nodig is om de toepassingsgateway:</span><span class="sxs-lookup"><span data-stu-id="f9e59-120">The following are the steps needed to update the application gateway:</span></span>

1. <span data-ttu-id="f9e59-121">Maak back-end-adresgroepen wilt gebruiken voor elke site.</span><span class="sxs-lookup"><span data-stu-id="f9e59-121">Create back-end pools to use for each site.</span></span>
2. <span data-ttu-id="f9e59-122">Maak een listener voor elke site toepassingsgateway ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="f9e59-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="f9e59-123">Maak regels om toe te wijzen elke listener met de juiste back-end.</span><span class="sxs-lookup"><span data-stu-id="f9e59-123">Create rules to map each listener with the appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="f9e59-124">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f9e59-124">Requirements</span></span>

* <span data-ttu-id="f9e59-125">**Back-endserverpool:** de lijst met IP-adressen van de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="f9e59-125">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="f9e59-126">De IP-adressen moeten ofwel deel uitmaken van het subnet van het virtuele netwerk, ofwel openbare IP-/VIP-adressen zijn.</span><span class="sxs-lookup"><span data-stu-id="f9e59-126">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="f9e59-127">FQDN-naam kan ook worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f9e59-127">FQDN can also be used.</span></span>
* <span data-ttu-id="f9e59-128">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="f9e59-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="f9e59-129">Deze instellingen zijn gekoppeld aan een pool en worden toegepast op alle servers in de pool.</span><span class="sxs-lookup"><span data-stu-id="f9e59-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="f9e59-130">**Front-endpoort:** dit is de openbare poort die in de toepassingsgateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f9e59-130">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="f9e59-131">Het verkeer komt binnen via deze poort en wordt vervolgens omgeleid naar een van de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="f9e59-131">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="f9e59-132">**Listener:** de listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig) en de SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="f9e59-132">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="f9e59-133">Voor meerdere locaties ingeschakeld Toepassingsgateways, hostnaam en SNI indicatoren ook worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f9e59-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="f9e59-134">**Regel:** de regel verbindt de listener met de back-end-servergroep, en definieert naar welke back-endserverpool het verkeer moet worden omgeleid wanneer dit bij een bepaalde listener aankomt.</span><span class="sxs-lookup"><span data-stu-id="f9e59-134">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="f9e59-135">Regels worden verwerkt in de volgorde die ze worden weergegeven en verkeer wordt doorgestuurd via de eerste regel die overeenkomt met ongeacht specifieke karakter.</span><span class="sxs-lookup"><span data-stu-id="f9e59-135">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="f9e59-136">Bijvoorbeeld, als u een regel met behulp van een basic-listener en een regel met meerdere sites listener beide op dezelfde poort hebt, kan de regel met de listener voor meerdere locaties moet worden vermeld voordat u de regel met de basic-listener in volgorde voor de regel voor meerdere locaties werken zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="f9e59-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span> 
* <span data-ttu-id="f9e59-137">**Certificaten:** elke listener vereist een uniek certificaat, in dit voorbeeld 2 listeners worden gemaakt voor meerdere locaties.</span><span class="sxs-lookup"><span data-stu-id="f9e59-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="f9e59-138">Twee pfx-certificaten en de wachtwoorden voor deze moeten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f9e59-138">Two .pfx certificates and the passwords for them need to be created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="f9e59-139">Back-end-adresgroepen voor elke site maken</span><span class="sxs-lookup"><span data-stu-id="f9e59-139">Create back-end pools for each site</span></span>

<span data-ttu-id="f9e59-140">Een back-end van toepassingen voor elke site of toepassing gateway ondersteunt is vereist, in dit geval 2 worden gemaakt voor contoso11.com en één voor fabrikam11.com.</span><span class="sxs-lookup"><span data-stu-id="f9e59-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="f9e59-141">Stap 1</span><span class="sxs-lookup"><span data-stu-id="f9e59-141">Step 1</span></span>

<span data-ttu-id="f9e59-142">Navigeer naar een bestaande toepassingsgateway in de Azure portal (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f9e59-142">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="f9e59-143">Selecteer **back-endpools** en klik op **toevoegen**</span><span class="sxs-lookup"><span data-stu-id="f9e59-143">Select **Backend pools** and click **Add**</span></span>

![back-endpools toevoegen][7]

### <a name="step-2"></a><span data-ttu-id="f9e59-145">Stap 2</span><span class="sxs-lookup"><span data-stu-id="f9e59-145">Step 2</span></span>

<span data-ttu-id="f9e59-146">Vul de gegevens voor de back-end-pool **pool1**, het toevoegen van de IP-adressen of de FQDN-namen voor de back-endservers en klikt u op **OK**</span><span class="sxs-lookup"><span data-stu-id="f9e59-146">Fill in the information for the back-end pool **pool1**, adding the ip addresses or FQDNs for the back-end servers and click **OK**</span></span>

![back-end-groepsinstellingen pool1][8]

### <a name="step-3"></a><span data-ttu-id="f9e59-148">Stap 3</span><span class="sxs-lookup"><span data-stu-id="f9e59-148">Step 3</span></span>

<span data-ttu-id="f9e59-149">Klik op de blade back-end-adresgroepen **toevoegen** toevoegen van een aanvullende back-end-adresgroep **pool2**, het toevoegen van de IP-adressen of de FQDN-namen voor de back-endservers en klikt u op **OK**</span><span class="sxs-lookup"><span data-stu-id="f9e59-149">On the backend-pools blade click **Add** to add an additional back-end pool **pool2**, adding the ip addresses or FQDNS for the back-end servers and click **OK**</span></span>

![back-end pool2 groepsinstellingen][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="f9e59-151">Listeners voor elke back-end maken</span><span class="sxs-lookup"><span data-stu-id="f9e59-151">Create listeners for each back-end</span></span>

<span data-ttu-id="f9e59-152">Application Gateway maakt gebruik van HTTP 1.1-hostheaders voor het hosten van meer dan één website op hetzelfde openbare IP-adres en dezelfde poort.</span><span class="sxs-lookup"><span data-stu-id="f9e59-152">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="f9e59-153">De basis-listener gemaakt in de portal bevat deze eigenschap niet.</span><span class="sxs-lookup"><span data-stu-id="f9e59-153">The basic listener created in the portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="f9e59-154">Stap 1</span><span class="sxs-lookup"><span data-stu-id="f9e59-154">Step 1</span></span>

<span data-ttu-id="f9e59-155">Klik op **Listeners** op de bestaande toepassingsgateway en op **multi-site** om toe te voegen van de eerste listener.</span><span class="sxs-lookup"><span data-stu-id="f9e59-155">Click **Listeners** on the existing application gateway and click **Multi-site** to add the first listener.</span></span>

![overzichtsblade listeners][1]

### <a name="step-2"></a><span data-ttu-id="f9e59-157">Stap 2</span><span class="sxs-lookup"><span data-stu-id="f9e59-157">Step 2</span></span>

<span data-ttu-id="f9e59-158">Vul de informatie voor de listener.</span><span class="sxs-lookup"><span data-stu-id="f9e59-158">Fill out the information for the listener.</span></span> <span data-ttu-id="f9e59-159">In dit voorbeeld SSL beëindiging is geconfigureerd, maakt u een nieuwe frontend-poort.</span><span class="sxs-lookup"><span data-stu-id="f9e59-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="f9e59-160">Upload het pfx-certificaat moet worden gebruikt voor SSL-beëindiging.</span><span class="sxs-lookup"><span data-stu-id="f9e59-160">Upload the .pfx certificate to be used for SSL termination.</span></span> <span data-ttu-id="f9e59-161">Het enige verschil op deze blade vergeleken met de standaard basic listener-blade is de hostnaam.</span><span class="sxs-lookup"><span data-stu-id="f9e59-161">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span>

![listener eigenschappenblade][2]

### <a name="step-3"></a><span data-ttu-id="f9e59-163">Stap 3</span><span class="sxs-lookup"><span data-stu-id="f9e59-163">Step 3</span></span>

<span data-ttu-id="f9e59-164">Klik op **multi-site** en een ander listener te maken, zoals beschreven in de vorige stap voor de tweede site.</span><span class="sxs-lookup"><span data-stu-id="f9e59-164">Click **Multi-site** and create another listener as described in the previous step for the second site.</span></span> <span data-ttu-id="f9e59-165">Zorg ervoor dat u een ander certificaat gebruikt voor de tweede listener.</span><span class="sxs-lookup"><span data-stu-id="f9e59-165">Make sure to use a different certificate for the second listener.</span></span> <span data-ttu-id="f9e59-166">Het enige verschil op deze blade vergeleken met de standaard basic listener-blade is de hostnaam.</span><span class="sxs-lookup"><span data-stu-id="f9e59-166">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span> <span data-ttu-id="f9e59-167">Vul de informatie voor de listener en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9e59-167">Fill out the information for the listener and click **OK**.</span></span>

![listener eigenschappenblade][3]

> [!NOTE]
> <span data-ttu-id="f9e59-169">Maken van luisteraars in de Azure-portal voor application gateway is een langlopende taak op. Dit kan enige tijd voor het maken van de twee listeners in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="f9e59-169">Creation of listeners in the Azure portal for application gateway is a long running task, it may take some time to create the two listeners in this scenario.</span></span> <span data-ttu-id="f9e59-170">Wanneer u klaar de listeners weergeven in de portal, zoals in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="f9e59-170">When complete the listeners show in the portal as seen in the following image:</span></span>

![overzicht van de listener][4]

## <a name="create-rules-to-map-listeners-to-backend-pools"></a><span data-ttu-id="f9e59-172">Maak regels om te listeners worden toegewezen aan back-endpools</span><span class="sxs-lookup"><span data-stu-id="f9e59-172">Create rules to map listeners to backend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="f9e59-173">Stap 1</span><span class="sxs-lookup"><span data-stu-id="f9e59-173">Step 1</span></span>

<span data-ttu-id="f9e59-174">Navigeer naar een bestaande toepassingsgateway in de Azure portal (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f9e59-174">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="f9e59-175">Selecteer **regels** en kiest u de bestaande standaardregel **rule1** en klik op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="f9e59-175">Select **Rules** and choose the existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="f9e59-176">Stap 2</span><span class="sxs-lookup"><span data-stu-id="f9e59-176">Step 2</span></span>

<span data-ttu-id="f9e59-177">Vul de blade regels zoals te zien is in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="f9e59-177">Fill out the rules blade as seen in the following image.</span></span> <span data-ttu-id="f9e59-178">De eerste listener en de eerste groep en te klikken op **opslaan** wanneer u klaar.</span><span class="sxs-lookup"><span data-stu-id="f9e59-178">Choosing the first listener and first pool and clicking **Save** when complete.</span></span>

![Bewerk de bestaande regel][6]

### <a name="step-3"></a><span data-ttu-id="f9e59-180">Stap 3</span><span class="sxs-lookup"><span data-stu-id="f9e59-180">Step 3</span></span>

<span data-ttu-id="f9e59-181">Klik op **Basic regel** om de tweede regel te maken.</span><span class="sxs-lookup"><span data-stu-id="f9e59-181">Click **Basic rule** to create the second rule.</span></span> <span data-ttu-id="f9e59-182">Vul het formulier met de tweede listener en tweede back-endpool en op **OK** om op te slaan.</span><span class="sxs-lookup"><span data-stu-id="f9e59-182">Fill out the form with the second listener and second backend pool and click **OK** to save.</span></span>

![blade basic regel toevoegen][10]

<span data-ttu-id="f9e59-184">Dit scenario is voltooid op een bestaande toepassingsgateway configureren met ondersteuning voor meerdere locaties via de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f9e59-184">This scenario completes configuring an existing application gateway with multi-site support through the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9e59-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f9e59-185">Next steps</span></span>

<span data-ttu-id="f9e59-186">Informatie over het beveiligen van uw websites met [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f9e59-186">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
