---
title: aaaHost meerdere sites met Azure Application Gateway | Microsoft Docs
description: Deze pagina bevat instructies tooconfigure aan een bestaande Azure application gateway voor het hosten van meerdere webtoepassingen op Hallo dezelfde gateway Hello Azure-portal.
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
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="7e4e3-103">Een bestaande toepassingsgateway voor het hosten van meerdere webtoepassingen configureren</span><span class="sxs-lookup"><span data-stu-id="7e4e3-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7e4e3-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7e4e3-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="7e4e3-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e4e3-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="7e4e3-106">Meerdere hosting-site kunt u toodeploy meer dan één webtoepassing op Hallo dezelfde toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="7e4e3-107">Is afhankelijk van de aanwezigheid van de host-header in Hallo inkomende HTTP-aanvraag, toodetermine welke listener verkeer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="7e4e3-108">Hallo-listener stuurt vervolgens verkeer tooappropriate back-endpool zoals geconfigureerd in de definitie van de gateway Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="7e4e3-109">In webtoepassingen SSL is ingeschakeld, is de toepassingsgateway afhankelijk van Hallo indicatie voor Server-naam (SNI) extensie toochoose Hallo juist listener voor internetverkeer Hallo.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="7e4e3-110">Vaak gebruikt voor het hosten van meerdere site is van aanvragen verdelen over tooload voor verschillende web domeinen toodifferent back-end-servergroepen.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="7e4e3-111">Op dezelfde manier Hallo meerdere subdomeinen Hallo dezelfde hoofddomein kan ook worden gehost op dezelfde toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="7e4e3-112">Scenario</span><span class="sxs-lookup"><span data-stu-id="7e4e3-112">Scenario</span></span>

<span data-ttu-id="7e4e3-113">In de Hallo voorbeeld te volgen, toepassingsgateway verkeer voor contoso.com en fabrikam.com bedient met twee back-endserver van toepassingen: contoso-servergroep en fabrikam-servergroep.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="7e4e3-114">Vergelijkbare installatie wordt mogelijk gebruikt toohost subdomeinen zoals app.contoso.com en blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![scenario voor meerdere locaties][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="7e4e3-116">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="7e4e3-116">Before you begin</span></span>

<span data-ttu-id="7e4e3-117">Dit scenario voegt ondersteuning voor meerdere locaties tooan bestaande toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-117">This scenario adds multi-site support tooan existing application gateway.</span></span> <span data-ttu-id="7e4e3-118">toocomplete dit scenario wordt een bestaande toepassingsgateway moet toobe beschikbaar tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-118">toocomplete this scenario, an existing application gateway needs toobe available tooconfigure.</span></span> <span data-ttu-id="7e4e3-119">Ga naar [een toepassingsgateway maken met behulp van de portal Hallo](application-gateway-create-gateway-portal.md) toolearn hoe toocreate een basic-toepassingsgateway in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-119">Visit [Create an application gateway by using hello portal](application-gateway-create-gateway-portal.md) toolearn how toocreate a basic application gateway in hello portal.</span></span>

<span data-ttu-id="7e4e3-120">Hallo hieronder vindt u Hallo stappen nodig tooupdate Hallo toepassingsgateway:</span><span class="sxs-lookup"><span data-stu-id="7e4e3-120">hello following are hello steps needed tooupdate hello application gateway:</span></span>

1. <span data-ttu-id="7e4e3-121">Maken van back-end-adresgroepen toouse voor elke site.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-121">Create back-end pools toouse for each site.</span></span>
2. <span data-ttu-id="7e4e3-122">Maak een listener voor elke site toepassingsgateway ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="7e4e3-123">Maak regels toomap elke listener voor Hallo juiste back-end.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-123">Create rules toomap each listener with hello appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="7e4e3-124">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7e4e3-124">Requirements</span></span>

* <span data-ttu-id="7e4e3-125">**Back-endserverpool:** Hallo lijst met IP-adressen van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-125">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="7e4e3-126">Hallo IP-adressen moeten ofwel deel uitmaken toohello virtueel netwerksubnet ofwel moeten een openbare IP-/ VIP.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-126">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="7e4e3-127">FQDN-naam kan ook worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-127">FQDN can also be used.</span></span>
* <span data-ttu-id="7e4e3-128">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="7e4e3-129">Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="7e4e3-130">**Front-endpoort:** deze is Hallo openbare poort die in Hallo toepassingsgateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-130">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="7e4e3-131">Verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-131">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="7e4e3-132">**Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="7e4e3-132">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="7e4e3-133">Voor meerdere locaties ingeschakeld Toepassingsgateways, hostnaam en SNI indicatoren ook worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="7e4e3-134">**Regel:** Hallo regel verbindt Hallo listener, Hallo back-endserverpool, en definieert naar welke back-endserver groep Hallo verkeer moet gerichte toowhen dit bij een bepaalde listener aankomt.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-134">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="7e4e3-135">Regels worden verwerkt op Hallo volgorde die ze worden weergegeven en verkeer wordt omgeleid via Hallo eerste regel die overeenkomt met ongeacht specifieke karakter.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-135">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="7e4e3-136">Bijvoorbeeld, als u een regel met een basic-listener en een regel met meerdere sites listener beide op dezelfde poort, regel met Hallo Hallo hebt moet Hallo multi-site-listener worden weergegeven voordat Hallo regel met Hallo basic listener om Hallo multi-site regel toofunction als Er werd verwacht.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span> 
* <span data-ttu-id="7e4e3-137">**Certificaten:** elke listener vereist een uniek certificaat, in dit voorbeeld 2 listeners worden gemaakt voor meerdere locaties.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="7e4e3-138">Twee pfx-certificaten en wachtwoorden voor deze Hallo moeten toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-138">Two .pfx certificates and hello passwords for them need toobe created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="7e4e3-139">Back-end-adresgroepen voor elke site maken</span><span class="sxs-lookup"><span data-stu-id="7e4e3-139">Create back-end pools for each site</span></span>

<span data-ttu-id="7e4e3-140">Een back-end van toepassingen voor elke site of toepassing gateway ondersteunt is vereist, in dit geval 2 worden gemaakt voor contoso11.com en één voor fabrikam11.com.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="7e4e3-141">Stap 1</span><span class="sxs-lookup"><span data-stu-id="7e4e3-141">Step 1</span></span>

<span data-ttu-id="7e4e3-142">Navigeer tooan bestaande toepassingsgateway in hello Azure-portal (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7e4e3-142">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="7e4e3-143">Selecteer **back-endpools** en klik op **toevoegen**</span><span class="sxs-lookup"><span data-stu-id="7e4e3-143">Select **Backend pools** and click **Add**</span></span>

![back-endpools toevoegen][7]

### <a name="step-2"></a><span data-ttu-id="7e4e3-145">Stap 2</span><span class="sxs-lookup"><span data-stu-id="7e4e3-145">Step 2</span></span>

<span data-ttu-id="7e4e3-146">Vul Hallo voor back-end-pool Hallo **pool1**, Hallo IP-adressen of FQDN-namen voor Hallo back-end-servers toe te voegen en klik op **OK**</span><span class="sxs-lookup"><span data-stu-id="7e4e3-146">Fill in hello information for hello back-end pool **pool1**, adding hello ip addresses or FQDNs for hello back-end servers and click **OK**</span></span>

![back-end-groepsinstellingen pool1][8]

### <a name="step-3"></a><span data-ttu-id="7e4e3-148">Stap 3</span><span class="sxs-lookup"><span data-stu-id="7e4e3-148">Step 3</span></span>

<span data-ttu-id="7e4e3-149">Klik op Hallo back-end-adresgroepen blade **toevoegen** tooadd een aanvullende back-end-adresgroep **pool2**, Hallo IP-adressen of FQDN-namen voor Hallo back-end-servers toe te voegen en klik op **OK**</span><span class="sxs-lookup"><span data-stu-id="7e4e3-149">On hello backend-pools blade click **Add** tooadd an additional back-end pool **pool2**, adding hello ip addresses or FQDNS for hello back-end servers and click **OK**</span></span>

![back-end pool2 groepsinstellingen][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="7e4e3-151">Listeners voor elke back-end maken</span><span class="sxs-lookup"><span data-stu-id="7e4e3-151">Create listeners for each back-end</span></span>

<span data-ttu-id="7e4e3-152">Application Gateway is afhankelijk van HTTP 1.1 host headers toohost meer dan één website op Hallo hetzelfde openbare IP-adres en poort.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-152">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="7e4e3-153">basic Hallo-listener gemaakt in de portal Hallo bevat deze eigenschap niet.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-153">hello basic listener created in hello portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="7e4e3-154">Stap 1</span><span class="sxs-lookup"><span data-stu-id="7e4e3-154">Step 1</span></span>

<span data-ttu-id="7e4e3-155">Klik op **Listeners** op Hallo van bestaande application gateway en klikt u op **multi-site** tooadd Hallo eerste listener.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-155">Click **Listeners** on hello existing application gateway and click **Multi-site** tooadd hello first listener.</span></span>

![overzichtsblade listeners][1]

### <a name="step-2"></a><span data-ttu-id="7e4e3-157">Stap 2</span><span class="sxs-lookup"><span data-stu-id="7e4e3-157">Step 2</span></span>

<span data-ttu-id="7e4e3-158">Hallo-informatie voor Hallo-listener vult.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-158">Fill out hello information for hello listener.</span></span> <span data-ttu-id="7e4e3-159">In dit voorbeeld SSL beëindiging is geconfigureerd, maakt u een nieuwe frontend-poort.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="7e4e3-160">Hallo pfx-certificaat toobe gebruikt voor SSL-beëindiging uploaden.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-160">Upload hello .pfx certificate toobe used for SSL termination.</span></span> <span data-ttu-id="7e4e3-161">Hallo enige verschil op deze blade vergeleken toohello standaard basic listener-blade is Hallo hostnaam.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-161">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span>

![listener eigenschappenblade][2]

### <a name="step-3"></a><span data-ttu-id="7e4e3-163">Stap 3</span><span class="sxs-lookup"><span data-stu-id="7e4e3-163">Step 3</span></span>

<span data-ttu-id="7e4e3-164">Klik op **multi-site** en een ander listener te maken, zoals beschreven in de vorige stap voor de tweede site Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-164">Click **Multi-site** and create another listener as described in hello previous step for hello second site.</span></span> <span data-ttu-id="7e4e3-165">Zorg ervoor dat toouse een ander certificaat voor de tweede listener Hallo.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-165">Make sure toouse a different certificate for hello second listener.</span></span> <span data-ttu-id="7e4e3-166">Hallo enige verschil op deze blade vergeleken toohello standaard basic listener-blade is Hallo hostnaam.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-166">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span> <span data-ttu-id="7e4e3-167">Hallo-informatie voor Hallo-listener vult en u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-167">Fill out hello information for hello listener and click **OK**.</span></span>

![listener eigenschappenblade][3]

> [!NOTE]
> <span data-ttu-id="7e4e3-169">Maken van luisteraars in hello Azure-portal voor application gateway is een langlopende taak op. Dit kan enige tijd toocreate Hallo twee listeners in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-169">Creation of listeners in hello Azure portal for application gateway is a long running task, it may take some time toocreate hello two listeners in this scenario.</span></span> <span data-ttu-id="7e4e3-170">Wanneer volledige Hallo listeners in Hallo portal weergeven zoals gezien in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e4e3-170">When complete hello listeners show in hello portal as seen in hello following image:</span></span>

![overzicht van de listener][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a><span data-ttu-id="7e4e3-172">Regels toomap listeners toobackend groepen maken</span><span class="sxs-lookup"><span data-stu-id="7e4e3-172">Create rules toomap listeners toobackend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="7e4e3-173">Stap 1</span><span class="sxs-lookup"><span data-stu-id="7e4e3-173">Step 1</span></span>

<span data-ttu-id="7e4e3-174">Navigeer tooan bestaande toepassingsgateway in hello Azure-portal (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7e4e3-174">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="7e4e3-175">Selecteer **regels** en kiest u de bestaande standaardregel Hallo **rule1** en klik op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-175">Select **Rules** and choose hello existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="7e4e3-176">Stap 2</span><span class="sxs-lookup"><span data-stu-id="7e4e3-176">Step 2</span></span>

<span data-ttu-id="7e4e3-177">Hallo regels blade invullen zoals gezien in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-177">Fill out hello rules blade as seen in hello following image.</span></span> <span data-ttu-id="7e4e3-178">Eerste Hallo-listener en eerste groep kiezen en te klikken op **opslaan** wanneer u klaar.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-178">Choosing hello first listener and first pool and clicking **Save** when complete.</span></span>

![Bewerk de bestaande regel][6]

### <a name="step-3"></a><span data-ttu-id="7e4e3-180">Stap 3</span><span class="sxs-lookup"><span data-stu-id="7e4e3-180">Step 3</span></span>

<span data-ttu-id="7e4e3-181">Klik op **Basic regel** toocreate Hallo tweede regel.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-181">Click **Basic rule** toocreate hello second rule.</span></span> <span data-ttu-id="7e4e3-182">Hallo-formulier met Hallo tweede listener en tweede back-endpool invullen en klik op **OK** toosave.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-182">Fill out hello form with hello second listener and second backend pool and click **OK** toosave.</span></span>

![blade basic regel toevoegen][10]

<span data-ttu-id="7e4e3-184">Dit scenario is voltooid op een bestaande toepassingsgateway configureren met ondersteuning voor meerdere locaties via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7e4e3-184">This scenario completes configuring an existing application gateway with multi-site support through hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e4e3-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7e4e3-185">Next steps</span></span>

<span data-ttu-id="7e4e3-186">Meer informatie over hoe tooprotect uw websites met [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7e4e3-186">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

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
