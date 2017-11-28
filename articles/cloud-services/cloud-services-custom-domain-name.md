---
title: een aangepaste domeinnaam in Cloudservices aaaConfigure | Microsoft Docs
description: Meer informatie over hoe tooexpose uw Azure-toepassing of de gegevens op een aangepast domein door DNS-instellingen configureren.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 6a62c2b7-ea47-4cce-9d6a-0cca38357f42
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 71e553a73b40a8d0512b4d40173500561841772c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="3adc3-103">Een aangepaste domeinnaam voor een Azure-cloud-service configureren</span><span class="sxs-lookup"><span data-stu-id="3adc3-103">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3adc3-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3adc3-104">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="3adc3-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3adc3-105">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="3adc3-106">Wanneer u een Cloudservice maakt, kent Azure tooa subdomein van cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="3adc3-106">When you create a Cloud Service, Azure assigns it tooa subdomain of cloudapp.net.</span></span> <span data-ttu-id="3adc3-107">Bijvoorbeeld, als uw Cloudservice met de naam 'contoso', uw gebruikers zullen kunnen tooaccess worden uw toepassing op een URL als http://contoso.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="3adc3-107">For example, if your Cloud Service is named "contoso", your users will be able tooaccess your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="3adc3-108">Azure wordt ook een virtueel IP-adres toegewezen.</span><span class="sxs-lookup"><span data-stu-id="3adc3-108">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="3adc3-109">U kunt echter ook uw toepassing weergegeven op uw eigen domeinnaam bijvoorbeeld contoso.com. Dit artikel wordt uitgelegd hoe tooreserve of een aangepaste domeinnaam configureren voor Cloud Service-web-rollen.</span><span class="sxs-lookup"><span data-stu-id="3adc3-109">However, you can also expose your application on your own domain name, such as contoso.com. This article explains how tooreserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="3adc3-110">U al begrijpen wat CNAME en A-records zijn?</span><span class="sxs-lookup"><span data-stu-id="3adc3-110">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="3adc3-111">[Korte inleiding voorbij Hallo uitleg](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="3adc3-111">[Jump past hello explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="3adc3-112">U gaat sneller!</span><span class="sxs-lookup"><span data-stu-id="3adc3-112">Get going faster!</span></span> <span data-ttu-id="3adc3-113">Gebruik hello Azure [scenario begeleide](http://support.microsoft.com/kb/2990804).</span><span class="sxs-lookup"><span data-stu-id="3adc3-113">Use hello Azure [guided walkthrough](http://support.microsoft.com/kb/2990804).</span></span> <span data-ttu-id="3adc3-114">Het maakt koppelen van een aangepaste domeinnaam en het beveiligen van communicatie (SSL) met Azure Cloud Services of Azure Websites een module.</span><span class="sxs-lookup"><span data-stu-id="3adc3-114">It makes associating a custom domain name and securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

<p/>

> [!NOTE]
> <span data-ttu-id="3adc3-115">Hallo procedures in deze taak toepassing tooAzure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="3adc3-115">hello procedures in this task apply tooAzure Cloud Services.</span></span> <span data-ttu-id="3adc3-116">Zie voor App-Services, [dit](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="3adc3-116">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="3adc3-117">Zie voor storage-accounts [dit](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="3adc3-117">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="3adc3-118">Records CNAME en A begrijpen</span><span class="sxs-lookup"><span data-stu-id="3adc3-118">Understand CNAME and A records</span></span>
<span data-ttu-id="3adc3-119">CNAME (of aliasrecords) en een records zowel kunnen u een domeinnaam met een specifieke server tooassociate (of service in dit geval) echter ze anders werken.</span><span class="sxs-lookup"><span data-stu-id="3adc3-119">CNAME (or alias records) and A records both allow you tooassociate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="3adc3-120">Er zijn ook enkele specifieke overwegingen bij het gebruik van A-records met Azure-Cloud-services die u overwegen moet voordat u besluit welke toouse.</span><span class="sxs-lookup"><span data-stu-id="3adc3-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which toouse.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="3adc3-121">CNAME- of Alias-record</span><span class="sxs-lookup"><span data-stu-id="3adc3-121">CNAME or Alias record</span></span>
<span data-ttu-id="3adc3-122">Een CNAME-record verwijst een *specifieke* domein, zoals **contoso.com** of **www.contoso.com**, tooa canonieke domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="3adc3-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, tooa canonical domain name.</span></span> <span data-ttu-id="3adc3-123">In dit geval de canonieke domeinnaam Hallo Hallo is **[myapp] .cloudapp .net** domeinnaam van uw Azure gehoste toepassing.</span><span class="sxs-lookup"><span data-stu-id="3adc3-123">In this case, hello canonical domain name is hello **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="3adc3-124">Zodra gemaakt, Hallo CNAME maakt een alias voor Hallo **[myapp] .cloudapp .net**.</span><span class="sxs-lookup"><span data-stu-id="3adc3-124">Once created, hello CNAME creates an alias for hello **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="3adc3-125">Hallo CNAME-vermelding wordt opgelost toohello IP-adres van uw **[myapp] .cloudapp .net** service automatisch als Hallo IP-adres van de cloudservice Hallo verandert, u hoeft dus niet tootake geen actie.</span><span class="sxs-lookup"><span data-stu-id="3adc3-125">hello CNAME entry will resolve toohello IP address of your **[myapp].cloudapp.net** service automatically, so if hello IP address of hello cloud service changes, you do not have tootake any action.</span></span>

> [!NOTE]
> <span data-ttu-id="3adc3-126">Sommige registrars domein alleen kunnen u toomap subdomeinen wanneer u een CNAME-record, bijvoorbeeld www.contoso.com en geen basis-namen, zoals contoso.com. Zie voor meer informatie over CNAME-records Hallo documentatie bij uw registrar [Hallo vermelding Wikipedia (Engelstalig) op de CNAME-record](http://en.wikipedia.org/wiki/CNAME_record), of Hallo [IETF domeinnamen - implementatie en specificatie](http://tools.ietf.org/html/rfc1035) document.</span><span class="sxs-lookup"><span data-stu-id="3adc3-126">Some domain registrars only allow you toomap subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see hello documentation provided by your registrar, [hello Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or hello [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="3adc3-127">een record</span><span class="sxs-lookup"><span data-stu-id="3adc3-127">A record</span></span>
<span data-ttu-id="3adc3-128">Een A-record wordt een domein, zoals toegewezen **contoso.com** of **www.contoso.com**, *of een jokertekendomein* zoals  **\*. contoso.com**, tooan IP-adres.</span><span class="sxs-lookup"><span data-stu-id="3adc3-128">An A record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, tooan IP address.</span></span> <span data-ttu-id="3adc3-129">In geval van een Azure Cloud Service Hallo Hallo virtueel IP-adres van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="3adc3-129">In hello case of an Azure Cloud Service, hello virtual IP of hello service.</span></span> <span data-ttu-id="3adc3-130">Dus Hallo belangrijkste voordeel van een A-record via een CNAME-record is dat u kunt een vermelding die gebruikmaakt van een jokerteken, zoals \* **. contoso.com**, die zou staat aanvragen verwerken voor meerdere subdomeinen zoals  **mail.contoso.com**, **login.contoso.com**, of **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="3adc3-130">So hello main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="3adc3-131">Omdat een A-record is toegewezen tooa statische IP-adres, het automatisch wijzigingen toohello IP-adres van uw Cloud-Service kan niet worden omgezet.</span><span class="sxs-lookup"><span data-stu-id="3adc3-131">Since an A record is mapped tooa static IP address, it cannot automatically resolve changes toohello IP address of your Cloud Service.</span></span> <span data-ttu-id="3adc3-132">Hallo IP-adres wordt gebruikt door uw Cloud-Service is toegewezen Hallo eerste keer dat u implementeert tooan lege sleuf (productie of staging.) Als u Hallo-implementatie voor Hallo sleuf verwijdert, Hallo IP-adres is vrijgegeven door Azure en alle toekomstige implementaties toohello sleuf kan een nieuw IP-adres worden gegeven.</span><span class="sxs-lookup"><span data-stu-id="3adc3-132">hello IP address used by your Cloud Service is allocated hello first time you deploy tooan empty slot (either production or staging.) If you delete hello deployment for hello slot, hello IP address is released by Azure and any future deployments toohello slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="3adc3-133">Hallo IP-adres van een opgegeven implementatiesleuf (productie of staging) is gemakkelijk persistent bij het wisselen tussen fasering en productie-implementaties of het uitvoeren van een in-place upgrade van een bestaande implementatie.</span><span class="sxs-lookup"><span data-stu-id="3adc3-133">Conveniently, hello IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="3adc3-134">Zie voor meer informatie over het uitvoeren van deze acties [hoe toomanage cloudservices](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="3adc3-134">For more information on performing these actions, see [How toomanage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="3adc3-135">Voeg een CNAME-record voor uw aangepaste domein</span><span class="sxs-lookup"><span data-stu-id="3adc3-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="3adc3-136">toocreate een CNAME-record, moet u een nieuwe vermelding toevoegen in Hallo DNS-tabel voor uw aangepaste domein met behulp van Hallo-hulpprogramma's van uw registrar.</span><span class="sxs-lookup"><span data-stu-id="3adc3-136">toocreate a CNAME record, you must add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="3adc3-137">Elke registrar heeft een methode vergelijkbaar maar enigszins verschillen van het opgeven van een CNAME-record, maar de concepten Hallo Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="3adc3-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="3adc3-138">Gebruik een van deze methoden toofind hello **. cloudapp.net** domeinnaam tooyour cloudservice toegewezen.</span><span class="sxs-lookup"><span data-stu-id="3adc3-138">Use one of these methods toofind hello **.cloudapp.net** domain name assigned tooyour cloud service.</span></span>
   
   * <span data-ttu-id="3adc3-139">Aanmelding toohello [klassieke Azure-portal], selecteer uw cloudservice, selecteert u **Dashboard**, en gaat u naar Hallo **Site-URL** vermelding in Hallo **snelle weergave**  sectie.</span><span class="sxs-lookup"><span data-stu-id="3adc3-139">Login toohello [Azure classic portal], select your cloud service, select **Dashboard**, and then find hello **Site URL** entry in hello **quick glance** section.</span></span>
     
       ![snelle weergave sectie Hallo site-URL wordt weergegeven][csurl]
     
       <span data-ttu-id="3adc3-141">**OR**</span><span class="sxs-lookup"><span data-stu-id="3adc3-141">**OR**</span></span>  
   * <span data-ttu-id="3adc3-142">Installeer en configureer [Azure Powershell](/powershell/azure/overview), en vervolgens gebruik Hallo opdracht:</span><span class="sxs-lookup"><span data-stu-id="3adc3-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="3adc3-143">Hallo-domeinnaam die is gebruikt in Hallo-URL die wordt geretourneerd door een van de methoden, zoals u deze hebt bij het maken van een CNAME-record opslaan.</span><span class="sxs-lookup"><span data-stu-id="3adc3-143">Save hello domain name used in hello URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="3adc3-144">Meld u op de website van tooyour DNS-registratieservice en ga toohello pagina voor het beheren van DNS.</span><span class="sxs-lookup"><span data-stu-id="3adc3-144">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="3adc3-145">Zoek naar koppelingen of gebieden van Hallo site met het label **domeinnaam**, **DNS**, of **naam Serverbeheer**.</span><span class="sxs-lookup"><span data-stu-id="3adc3-145">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="3adc3-146">Nu kunt u selecteren of invoeren van CNAME zoeken.</span><span class="sxs-lookup"><span data-stu-id="3adc3-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="3adc3-147">Mogelijk hebt u tooselect Hallo record uit een vervolgkeuzelijst, of Ga tooan geavanceerde voor instellingenpagina.</span><span class="sxs-lookup"><span data-stu-id="3adc3-147">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span> <span data-ttu-id="3adc3-148">Zoek naar Hallo woorden **CNAME**, **Alias**, of **subdomeinen**.</span><span class="sxs-lookup"><span data-stu-id="3adc3-148">You should look for hello words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="3adc3-149">U moet ook opgeven Hallo domein of subdomein alias voor Hallo CNAME, zoals **www** als u een alias voor toocreate wilt **www.customdomain.com**. Als u toocreate een alias voor het hoofddomein hello wilt, kan dit worden vermeld als Hallo '**@**' symbool in DNS-hulpprogramma's van uw registrar.</span><span class="sxs-lookup"><span data-stu-id="3adc3-149">You must also provide hello domain or subdomain alias for hello CNAME, such as **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate an alias for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="3adc3-150">Vervolgens moet u een canonieke hostnaam, uw toepassing is opgeven **cloudapp.net** domein in dit geval.</span><span class="sxs-lookup"><span data-stu-id="3adc3-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="3adc3-151">Bijvoorbeeld, Hallo volgt CNAME-record al het verkeer van stuurt **www.contoso.com** te**contoso.cloudapp.net**, Hallo aangepaste domeinnaam van uw geïmplementeerde toepassing:</span><span class="sxs-lookup"><span data-stu-id="3adc3-151">For example, hello following CNAME record forwards all traffic from **www.contoso.com** too**contoso.cloudapp.net**, hello custom domain name of your deployed application:</span></span>

| <span data-ttu-id="3adc3-152">Alias/Host-naam/subdomein</span><span class="sxs-lookup"><span data-stu-id="3adc3-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="3adc3-153">Canonieke domein</span><span class="sxs-lookup"><span data-stu-id="3adc3-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="3adc3-154">www</span><span class="sxs-lookup"><span data-stu-id="3adc3-154">www</span></span> |<span data-ttu-id="3adc3-155">Contoso.cloudapp.NET</span><span class="sxs-lookup"><span data-stu-id="3adc3-155">contoso.cloudapp.net</span></span> |

<span data-ttu-id="3adc3-156">Een bezoeker van **www.contoso.com** Zie nooit Hallo true host (contoso.cloudapp.net), zodat Hallo doorstuurproces onzichtbaar toothe eindgebruiker.</span><span class="sxs-lookup"><span data-stu-id="3adc3-156">A visitor of **www.contoso.com** will never see hello true host (contoso.cloudapp.net), so hello forwarding process is invisible toothe end user.</span></span>

> [!NOTE]
> <span data-ttu-id="3adc3-157">Hallo in bovenstaand voorbeeld is alleen van toepassing tootraffic op Hallo **www** subdomein.</span><span class="sxs-lookup"><span data-stu-id="3adc3-157">hello example above only applies tootraffic at hello **www** subdomain.</span></span> <span data-ttu-id="3adc3-158">Aangezien u kunt geen jokertekens CNAME-records gebruiken, moet u een CNAME voor elk domein/subdomein maken.</span><span class="sxs-lookup"><span data-stu-id="3adc3-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="3adc3-159">Als u wilt dat toodirect verkeer van subdomeinen, zoals \*. contoso.com, tooyour cloudapp.net adres, kunt u een **Omleidings-URL** of **URL doorsturen** vermelding in uw DNS-instellingen, of Maak een A-record.</span><span class="sxs-lookup"><span data-stu-id="3adc3-159">If you want toodirect  traffic from subdomains, such as \*.contoso.com, tooyour cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="3adc3-160">Een A-record voor uw aangepaste domein toevoegen</span><span class="sxs-lookup"><span data-stu-id="3adc3-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="3adc3-161">toocreate een A-record, moet u eerst Hallo virtueel IP-adres van uw cloudservice zoeken.</span><span class="sxs-lookup"><span data-stu-id="3adc3-161">toocreate an A record, you must first find hello virtual IP address of your cloud service.</span></span> <span data-ttu-id="3adc3-162">Vervolgens voegt een nieuwe vermelding in Hallo DNS-tabel voor uw aangepaste domein met Hallo-hulpprogramma's van uw registrar.</span><span class="sxs-lookup"><span data-stu-id="3adc3-162">Then add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="3adc3-163">Elke registrar heeft een methode vergelijkbaar maar enigszins verschillen van het opgeven van een A-record, maar de concepten Hallo Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="3adc3-163">Each registrar has a similar but slightly different method of specifying an A record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="3adc3-164">Gebruik een van de volgende methoden tooget Hallo IP-adres van uw cloudservice Hallo.</span><span class="sxs-lookup"><span data-stu-id="3adc3-164">Use one of hello following methods tooget hello IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="3adc3-165">aanmelding toohello [klassieke Azure-portal], selecteer uw cloudservice, selecteert u **Dashboard**, en gaat u naar Hallo **adres van de openbare virtuele IP-adres (VIP)** vermelding in Hallo **snelle weergave** sectie.</span><span class="sxs-lookup"><span data-stu-id="3adc3-165">login toohello [Azure classic portal], select your cloud service, select **Dashboard**, and then find hello **Public Virtual IP (VIP) address** entry in hello **quick glance** section.</span></span>
     
       ![snelle weergave sectie Hallo VIP wordt weergegeven][vip]
     
       <span data-ttu-id="3adc3-167">**OR**</span><span class="sxs-lookup"><span data-stu-id="3adc3-167">**OR**</span></span>  
   * <span data-ttu-id="3adc3-168">Installeer en configureer [Azure Powershell](/powershell/azure/overview), en vervolgens gebruik Hallo opdracht:</span><span class="sxs-lookup"><span data-stu-id="3adc3-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="3adc3-169">Als u meerdere eindpunten die zijn gekoppeld aan uw cloudservice hebt, ontvangt u meerdere regels met Hallo IP-adres, maar alle moet worden weergegeven in dezelfde Hallo adres.</span><span class="sxs-lookup"><span data-stu-id="3adc3-169">If you have multiple endpoints associated with your cloud service, you will receive multiple lines containing hello IP address, but all should display hello same address.</span></span>
     
     <span data-ttu-id="3adc3-170">Hallo IP-adres niet opslaan omdat u deze hebt bij het maken van een A-record.</span><span class="sxs-lookup"><span data-stu-id="3adc3-170">Save hello IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="3adc3-171">Meld u op de website van tooyour DNS-registratieservice en ga toohello pagina voor het beheren van DNS.</span><span class="sxs-lookup"><span data-stu-id="3adc3-171">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="3adc3-172">Zoek naar koppelingen of gebieden van Hallo site met het label **domeinnaam**, **DNS**, of **naam Serverbeheer**.</span><span class="sxs-lookup"><span data-stu-id="3adc3-172">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="3adc3-173">Nu kunt u selecteren of invoeren van de record zoeken.</span><span class="sxs-lookup"><span data-stu-id="3adc3-173">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="3adc3-174">Mogelijk hebt u tooselect Hallo record uit een vervolgkeuzelijst, of Ga tooan geavanceerde voor instellingenpagina.</span><span class="sxs-lookup"><span data-stu-id="3adc3-174">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span>
4. <span data-ttu-id="3adc3-175">Selecteer of typ Hallo domein of subdomein die door deze A-record wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3adc3-175">Select or enter hello domain or subdomain that will use this A record.</span></span> <span data-ttu-id="3adc3-176">Selecteer bijvoorbeeld **www** als u een alias voor toocreate wilt **www.customdomain.com**. Als u wilt dat toocreate een vermelding jokerteken voor alle subdomeinen, voert u '__*__'.</span><span class="sxs-lookup"><span data-stu-id="3adc3-176">For example, select **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate a wildcard entry for all subdomains, enter '__*__'.</span></span> <span data-ttu-id="3adc3-177">Hierin vindt u alle subdomeinen zoals **mail.customdomain.com**, **login.customdomain.com**, en **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="3adc3-177">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="3adc3-178">Als u toocreate een A-record voor het hoofddomein hello wilt, kan dit worden vermeld als Hallo '**@**' symbool in DNS-hulpprogramma's van uw registrar.</span><span class="sxs-lookup"><span data-stu-id="3adc3-178">If you want toocreate an A record for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="3adc3-179">Voer Hallo IP-adres van de cloudservice in Hallo opgegeven veld.</span><span class="sxs-lookup"><span data-stu-id="3adc3-179">Enter hello IP address of your cloud service in hello provided field.</span></span> <span data-ttu-id="3adc3-180">Dit koppelt Hallo domein vermelding in het Hallo-A-record met Hallo IP-adres van uw cloud service-implementatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3adc3-180">This associates hello domain entry used in hello A record with hello IP address of your cloud service deployment.</span></span>

<span data-ttu-id="3adc3-181">Bijvoorbeeld, een record na Hallo al het verkeer van stuurt **contoso.com** te**137.135.70.239**, IP-adres van de geïmplementeerde toepassing hello:</span><span class="sxs-lookup"><span data-stu-id="3adc3-181">For example, hello following A record forwards all traffic from **contoso.com** too**137.135.70.239**, hello IP address of your deployed application:</span></span>

| <span data-ttu-id="3adc3-182">Host-naam/subdomein</span><span class="sxs-lookup"><span data-stu-id="3adc3-182">Host name/Subdomain</span></span> | <span data-ttu-id="3adc3-183">IP-adres</span><span class="sxs-lookup"><span data-stu-id="3adc3-183">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="3adc3-184">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="3adc3-184">137.135.70.239</span></span> |

<span data-ttu-id="3adc3-185">Dit voorbeeld wordt een A-record voor het hoofddomein Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="3adc3-185">This example demonstrates creating an A record for hello root domain.</span></span> <span data-ttu-id="3adc3-186">Als u een jokerteken vermelding toocover toocreate wenst alle subdomeinen, voert u '__*__' als Hallo subdomein.</span><span class="sxs-lookup"><span data-stu-id="3adc3-186">If you wish toocreate a wildcard entry toocover all subdomains, you would enter '__*__' as hello subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="3adc3-187">IP-adressen in Azure zijn standaard dynamisch.</span><span class="sxs-lookup"><span data-stu-id="3adc3-187">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="3adc3-188">Wilt u waarschijnlijk toouse een [gereserveerd IP-adres](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure dat uw IP-adres niet verandert.</span><span class="sxs-lookup"><span data-stu-id="3adc3-188">You will probably want toouse a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3adc3-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3adc3-189">Next steps</span></span>
* [<span data-ttu-id="3adc3-190">Hoe tooManage Cloud-Services</span><span class="sxs-lookup"><span data-stu-id="3adc3-190">How tooManage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="3adc3-191">Hoe tooMap CDN inhoud tooa aangepaste domeinen</span><span class="sxs-lookup"><span data-stu-id="3adc3-191">How tooMap CDN Content tooa Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="3adc3-192">[Algemene configuratie van uw cloudservice](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="3adc3-192">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="3adc3-193">Meer informatie over hoe te[implementeren van een cloudservice](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3adc3-193">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="3adc3-194">Configureer [ssl-certificaten](cloud-services-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="3adc3-194">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[klassieke Azure-portal]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
