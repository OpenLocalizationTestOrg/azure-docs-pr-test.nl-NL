---
title: Maken en gebruiken van een interne load balancer met een Azure App Service-omgeving
description: "Meer informatie over het maken en gebruiken van een geïsoleerd van internet Azure App Service-omgeving"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: e7f85aaf2d940f114248d5925a1e97fe0f6bda6c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="20d1e-103">Maken en gebruiken van een interne load balancer met een App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="20d1e-103">Create and use an internal load balancer with an App Service environment</span></span> #

 <span data-ttu-id="20d1e-104">Azure App Service-omgeving is een implementatie van Azure App Service in een subnet in een Azure-netwerk (VNet).</span><span class="sxs-lookup"><span data-stu-id="20d1e-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="20d1e-105">Er zijn twee manieren voor het implementeren van een App Service-omgeving (as-omgeving):</span><span class="sxs-lookup"><span data-stu-id="20d1e-105">There are two ways to deploy an App Service environment (ASE):</span></span> 

- <span data-ttu-id="20d1e-106">Een VIP-adres op een externe IP-adres, vaak aangeduid als een externe as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="20d1e-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="20d1e-107">Een VIP-adres op een interne IP-adres, vaak genoemd, een ILB-as-omgeving omdat het interne eindpunt, een interne load balancer (ILB is).</span><span class="sxs-lookup"><span data-stu-id="20d1e-107">With a VIP on an internal IP address, often called an ILB ASE because the internal endpoint is an internal load balancer (ILB).</span></span> 

<span data-ttu-id="20d1e-108">In dit artikel leest u hoe een ILB-as-omgeving te maken.</span><span class="sxs-lookup"><span data-stu-id="20d1e-108">This article shows you how to create an ILB ASE.</span></span> <span data-ttu-id="20d1e-109">Zie voor een overzicht op de as-omgeving [Inleiding tot de App Service-omgevingen][Intro].</span><span class="sxs-lookup"><span data-stu-id="20d1e-109">For an overview on the ASE, see [Introduction to App Service environments][Intro].</span></span> <span data-ttu-id="20d1e-110">Zie voor meer informatie over het maken van een externe as-omgeving, [maken van een externe as-omgeving][MakeExternalASE].</span><span class="sxs-lookup"><span data-stu-id="20d1e-110">To learn how to create an External ASE, see [Create an External ASE][MakeExternalASE].</span></span>

## <a name="overview"></a><span data-ttu-id="20d1e-111">Overzicht</span><span class="sxs-lookup"><span data-stu-id="20d1e-111">Overview</span></span> ##

<span data-ttu-id="20d1e-112">U kunt een as-omgeving met een internet toegankelijke eindpunt of met een IP-adres implementeren in uw VNet.</span><span class="sxs-lookup"><span data-stu-id="20d1e-112">You can deploy an ASE with an internet-accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="20d1e-113">Om in te stellen het IP-adres in een VNet-adres, moet de as-omgeving worden geïmplementeerd met een ILB.</span><span class="sxs-lookup"><span data-stu-id="20d1e-113">To set the IP address to a VNet address, the ASE must be deployed with an ILB.</span></span> <span data-ttu-id="20d1e-114">Wanneer u uw as-omgeving met een ILB implementeert, moet u het volgende opgeven:</span><span class="sxs-lookup"><span data-stu-id="20d1e-114">When you deploy your ASE with an ILB, you must provide:</span></span>

-   <span data-ttu-id="20d1e-115">Uw eigen domein dat u bij het maken van uw apps.</span><span class="sxs-lookup"><span data-stu-id="20d1e-115">Your own domain that you use when you create your apps.</span></span>
-   <span data-ttu-id="20d1e-116">Het certificaat dat wordt gebruikt voor HTTPS.</span><span class="sxs-lookup"><span data-stu-id="20d1e-116">The certificate used for HTTPS.</span></span>
-   <span data-ttu-id="20d1e-117">DNS-beheer voor uw domein.</span><span class="sxs-lookup"><span data-stu-id="20d1e-117">DNS management for your domain.</span></span>

<span data-ttu-id="20d1e-118">Tegenprestatie kunt u doen, zoals:</span><span class="sxs-lookup"><span data-stu-id="20d1e-118">In return, you can do things such as:</span></span>

-   <span data-ttu-id="20d1e-119">Intranet-hosttoepassingen veilig in de cloud, die u via een site-naar-site of Azure ExpressRoute VPN-toegang.</span><span class="sxs-lookup"><span data-stu-id="20d1e-119">Host intranet applications securely in the cloud, which you access through a site-to-site or Azure ExpressRoute VPN.</span></span>
-   <span data-ttu-id="20d1e-120">Host-apps in de cloud die niet zijn opgenomen in de openbare DNS-servers.</span><span class="sxs-lookup"><span data-stu-id="20d1e-120">Host apps in the cloud that aren't listed in public DNS servers.</span></span>
-   <span data-ttu-id="20d1e-121">Internet geïsoleerd back-end-apps, die uw front-apps kunnen veilig worden geïntegreerd met maken.</span><span class="sxs-lookup"><span data-stu-id="20d1e-121">Create internet-isolated back-end apps, which your front-end apps can securely integrate with.</span></span>

### <a name="disabled-functionality"></a><span data-ttu-id="20d1e-122">Uitgeschakelde functionaliteit</span><span class="sxs-lookup"><span data-stu-id="20d1e-122">Disabled functionality</span></span> ###

<span data-ttu-id="20d1e-123">Er zijn een aantal zaken die u niet mogelijk wanneer u een ILB-as-omgeving:</span><span class="sxs-lookup"><span data-stu-id="20d1e-123">There are some things that you can't do when you use an ILB ASE:</span></span>

-   <span data-ttu-id="20d1e-124">IP-gebaseerde SSL wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="20d1e-124">Use IP-based SSL.</span></span>
-   <span data-ttu-id="20d1e-125">IP-adressen toewijzen aan specifieke apps.</span><span class="sxs-lookup"><span data-stu-id="20d1e-125">Assign IP addresses to specific apps.</span></span>
-   <span data-ttu-id="20d1e-126">Koop en een certificaat met een app via de Azure portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="20d1e-126">Buy and use a certificate with an app through the Azure portal.</span></span> <span data-ttu-id="20d1e-127">U kunt certificaten rechtstreeks vanuit een certificeringsinstantie verkrijgen en ze gebruiken met uw apps.</span><span class="sxs-lookup"><span data-stu-id="20d1e-127">You can obtain certificates directly from a certificate authority and use them with your apps.</span></span> <span data-ttu-id="20d1e-128">U kunt deze kan niet verkrijgen via de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="20d1e-128">You can't obtain them through the Azure portal.</span></span>

## <a name="create-an-ilb-ase"></a><span data-ttu-id="20d1e-129">Een as ILB-omgeving maken</span><span class="sxs-lookup"><span data-stu-id="20d1e-129">Create an ILB ASE</span></span> ##

<span data-ttu-id="20d1e-130">Een as ILB-omgeving maken:</span><span class="sxs-lookup"><span data-stu-id="20d1e-130">To create an ILB ASE:</span></span>

1. <span data-ttu-id="20d1e-131">Selecteer in de Azure-portal **nieuw** > **Web en mobiel** > **App Service-omgeving**.</span><span class="sxs-lookup"><span data-stu-id="20d1e-131">In the Azure portal, select **New** > **Web + Mobile** > **App Service Environment**.</span></span>

2. <span data-ttu-id="20d1e-132">Selecteer uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="20d1e-132">Select your subscription.</span></span>

3. <span data-ttu-id="20d1e-133">Selecteer of maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="20d1e-133">Select or create a resource group.</span></span>

4. <span data-ttu-id="20d1e-134">Selecteer of maak een VNet.</span><span class="sxs-lookup"><span data-stu-id="20d1e-134">Select or create a VNet.</span></span>

5. <span data-ttu-id="20d1e-135">Als u een bestaande VNet selecteert, moet u een subnet voor het opslaan van de as-omgeving maken.</span><span class="sxs-lookup"><span data-stu-id="20d1e-135">If you select an existing VNet, you need to create a subnet to hold the ASE.</span></span> <span data-ttu-id="20d1e-136">Zorg ervoor dat een subnetgrootte die groot genoeg voor een eventuele toekomstige groei van uw as-omgeving instellen.</span><span class="sxs-lookup"><span data-stu-id="20d1e-136">Make sure to set a subnet size large enough to accommodate any future growth of your ASE.</span></span> <span data-ttu-id="20d1e-137">Een grootte van het is raadzaam `/25`, waardoor 128 adressen heeft en een maximale grootte as-omgeving kan verwerken.</span><span class="sxs-lookup"><span data-stu-id="20d1e-137">We recommend a size of `/25`, which has 128 addresses and can handle a maximum-sized ASE.</span></span> <span data-ttu-id="20d1e-138">De minimale grootte die u kunt selecteren is een `/28`.</span><span class="sxs-lookup"><span data-stu-id="20d1e-138">The minimum size you can select is a `/28`.</span></span> <span data-ttu-id="20d1e-139">Nadat de infrastructuur nodig heeft, kan de grootte van deze tot maximaal 11 exemplaren worden uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="20d1e-139">After infrastructure needs, this size can be scaled to a maximum of 11 instances.</span></span>

    * <span data-ttu-id="20d1e-140">Verder dan het maximumaantal 100 exemplaren in uw App Service-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="20d1e-140">Go beyond the default maximum of 100 instances in your App Service plans.</span></span>

    * <span data-ttu-id="20d1e-141">In de buurt van 100, maar met meer snelle front-schaling schalen.</span><span class="sxs-lookup"><span data-stu-id="20d1e-141">Scale near 100 but with more rapid front-end scaling.</span></span>

6. <span data-ttu-id="20d1e-142">Selecteer **virtuele netwerklocatie** > **virtuele netwerkconfiguratie**.</span><span class="sxs-lookup"><span data-stu-id="20d1e-142">Select **Virtual Network/Location** > **Virtual Network Configuration**.</span></span> <span data-ttu-id="20d1e-143">Stel de **VIP Type** naar **interne**.</span><span class="sxs-lookup"><span data-stu-id="20d1e-143">Set the **VIP Type** to **Internal**.</span></span>

7. <span data-ttu-id="20d1e-144">Voer de domeinnaam van een.</span><span class="sxs-lookup"><span data-stu-id="20d1e-144">Enter a domain name.</span></span> <span data-ttu-id="20d1e-145">Dit domein wordt gebruikt voor apps die zijn gemaakt in deze as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="20d1e-145">This domain is the one used for apps created in this ASE.</span></span> <span data-ttu-id="20d1e-146">Er zijn enkele beperkingen.</span><span class="sxs-lookup"><span data-stu-id="20d1e-146">There are some restrictions.</span></span> <span data-ttu-id="20d1e-147">Kan niet worden:</span><span class="sxs-lookup"><span data-stu-id="20d1e-147">It can't be:</span></span>

    * <span data-ttu-id="20d1e-148">NET</span><span class="sxs-lookup"><span data-stu-id="20d1e-148">net</span></span>   

    * <span data-ttu-id="20d1e-149">azurewebsites.NET</span><span class="sxs-lookup"><span data-stu-id="20d1e-149">azurewebsites.net</span></span>

    * <span data-ttu-id="20d1e-150">p.azurewebsites.NET</span><span class="sxs-lookup"><span data-stu-id="20d1e-150">p.azurewebsites.net</span></span>

    * <span data-ttu-id="20d1e-151">&lt;asename&gt;. p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="20d1e-151">&lt;asename&gt;.p.azurewebsites.net</span></span>

   <span data-ttu-id="20d1e-152">De aangepaste domeinnaam gebruikt voor apps en de domeinnaam die wordt gebruikt door uw as-omgeving kunnen elkaar niet overlappen.</span><span class="sxs-lookup"><span data-stu-id="20d1e-152">The custom domain name used for apps and the domain name used by your ASE can't overlap.</span></span> <span data-ttu-id="20d1e-153">Voor een as ILB-omgeving met de domeinnaam _contoso.com_, u kunt aangepaste domeinnamen voor uw apps zoals niet gebruiken:</span><span class="sxs-lookup"><span data-stu-id="20d1e-153">For an ILB ASE with the domain name _contoso.com_, you can't use custom domain names for your apps like:</span></span>

    * <span data-ttu-id="20d1e-154">www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="20d1e-154">www.contoso.com</span></span>

    * <span data-ttu-id="20d1e-155">ABCD.def.contoso.com</span><span class="sxs-lookup"><span data-stu-id="20d1e-155">abcd.def.contoso.com</span></span>

    * <span data-ttu-id="20d1e-156">ABCD.contoso.com</span><span class="sxs-lookup"><span data-stu-id="20d1e-156">abcd.contoso.com</span></span>

   <span data-ttu-id="20d1e-157">Als u weet dat de aangepaste domeinnamen voor uw apps, kiest u een domein voor de as ILB-omgeving die u geen een conflict met deze aangepaste domeinnamen hebt.</span><span class="sxs-lookup"><span data-stu-id="20d1e-157">If you know the custom domain names for your apps, choose a domain for the ILB ASE that won’t have a conflict with those custom domain names.</span></span> <span data-ttu-id="20d1e-158">In dit voorbeeld kunt u ongeveer *contoso internal.com* voor het domein van uw as-omgeving omdat dat geen met aangepaste domeinnamen die eindigen conflicten op *. contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="20d1e-158">In this example, you can use something like *contoso-internal.com* for the domain of your ASE because that won't conflict with custom domain names that end in *.contoso.com*.</span></span>

8. <span data-ttu-id="20d1e-159">Selecteer **OK**, en selecteer vervolgens **maken**.</span><span class="sxs-lookup"><span data-stu-id="20d1e-159">Select **OK**, and then select **Create**.</span></span>

    ![ASE maken][1]

<span data-ttu-id="20d1e-161">Op de **virtueel netwerk** blade, er is een **virtuele netwerkconfiguratie** optie.</span><span class="sxs-lookup"><span data-stu-id="20d1e-161">On the **Virtual Network** blade, there is a **Virtual Network Configuration** option.</span></span> <span data-ttu-id="20d1e-162">U kunt deze gebruiken om een externe VIP of een interne VIP te selecteren.</span><span class="sxs-lookup"><span data-stu-id="20d1e-162">You can use it to select an External VIP or an Internal VIP.</span></span> <span data-ttu-id="20d1e-163">De standaardwaarde is **externe**.</span><span class="sxs-lookup"><span data-stu-id="20d1e-163">The default is **External**.</span></span> <span data-ttu-id="20d1e-164">Als u selecteert **externe**, uw as-omgeving maakt gebruik van een internet toegankelijke VIP.</span><span class="sxs-lookup"><span data-stu-id="20d1e-164">If you select **External**, your ASE uses an internet-accessible VIP.</span></span> <span data-ttu-id="20d1e-165">Als u selecteert **intern**, uw as-omgeving is geconfigureerd met een ILB op een IP-adres binnen uw VNet.</span><span class="sxs-lookup"><span data-stu-id="20d1e-165">If you select **Internal**, your ASE is configured with an ILB on an IP address within your VNet.</span></span>

<span data-ttu-id="20d1e-166">Nadat u hebt geselecteerd **intern**, de mogelijkheid meer IP-adressen toevoegen aan uw as-omgeving wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="20d1e-166">After you select **Internal**, the ability to add more IP addresses to your ASE is removed.</span></span> <span data-ttu-id="20d1e-167">In plaats daarvan moet u het domein van de as-omgeving te bieden.</span><span class="sxs-lookup"><span data-stu-id="20d1e-167">Instead, you need to provide the domain of the ASE.</span></span> <span data-ttu-id="20d1e-168">In een as met een externe VIP-omgeving, wordt de naam van de as-omgeving in het domein gebruikt voor apps die zijn gemaakt in die as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="20d1e-168">In an ASE with an External VIP, the name of the ASE is used in the domain for apps created in that ASE.</span></span>

<span data-ttu-id="20d1e-169">Als u instelt **VIP Type** naar **intern**, de naam van uw as-omgeving wordt niet gebruikt in het domein voor de as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="20d1e-169">If you set **VIP Type** to **Internal**, your ASE name is not used in the domain for the ASE.</span></span> <span data-ttu-id="20d1e-170">U Geef expliciet het domein.</span><span class="sxs-lookup"><span data-stu-id="20d1e-170">You specify the domain explicitly.</span></span> <span data-ttu-id="20d1e-171">Als uw domein *contoso.corp.net* en u een app maken in de betreffende as-omgeving met de naam *timereporting*, de URL voor die app timereporting.contoso.corp.net is.</span><span class="sxs-lookup"><span data-stu-id="20d1e-171">If your domain is *contoso.corp.net* and you create an app in that ASE named *timereporting*, the URL for that app is timereporting.contoso.corp.net.</span></span>


## <a name="create-an-app-in-an-ilb-ase"></a><span data-ttu-id="20d1e-172">Een app maken in een ILB-as-omgeving</span><span class="sxs-lookup"><span data-stu-id="20d1e-172">Create an app in an ILB ASE</span></span> ##

<span data-ttu-id="20d1e-173">U kunt een app maken in een ILB-as-omgeving op dezelfde manier als u een app in een as-omgeving normaal maken.</span><span class="sxs-lookup"><span data-stu-id="20d1e-173">You create an app in an ILB ASE in the same way that you create an app in an ASE normally.</span></span>

1. <span data-ttu-id="20d1e-174">Selecteer in de Azure-portal **nieuw** > **Web en mobiel** > **Web** of **Mobile** of **API-App**.</span><span class="sxs-lookup"><span data-stu-id="20d1e-174">In the Azure portal, select **New** > **Web + Mobile** > **Web** or **Mobile** or **API App**.</span></span>

2. <span data-ttu-id="20d1e-175">Voer de naam van de app.</span><span class="sxs-lookup"><span data-stu-id="20d1e-175">Enter the name of the app.</span></span>

3. <span data-ttu-id="20d1e-176">Selecteer het abonnement.</span><span class="sxs-lookup"><span data-stu-id="20d1e-176">Select the subscription.</span></span>

4. <span data-ttu-id="20d1e-177">Selecteer of maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="20d1e-177">Select or create a resource group.</span></span>

5. <span data-ttu-id="20d1e-178">Selecteer of maak een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="20d1e-178">Select or create an App Service plan.</span></span> <span data-ttu-id="20d1e-179">Als u maken van een nieuw App Service-plan wilt, selecteert u uw as-omgeving als de locatie.</span><span class="sxs-lookup"><span data-stu-id="20d1e-179">If you want to create a new App Service plan, select your ASE as the location.</span></span> <span data-ttu-id="20d1e-180">Selecteer de worker-groep waar u uw App Service-abonnement worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="20d1e-180">Select the worker pool where you want your App Service plan to be created.</span></span> <span data-ttu-id="20d1e-181">Wanneer u de App Service-abonnement hebt gemaakt, selecteert u uw as-omgeving als de locatie en de worker-groep.</span><span class="sxs-lookup"><span data-stu-id="20d1e-181">When you create the App Service plan, select your ASE as the location and the worker pool.</span></span> <span data-ttu-id="20d1e-182">Wanneer u de naam van de app opgeeft, wordt het domein onder de appnaam van uw vervangen door het domein voor uw as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="20d1e-182">When you specify the name of the app, the domain under your app name is replaced by the domain for your ASE.</span></span>

6. <span data-ttu-id="20d1e-183">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="20d1e-183">Select **Create**.</span></span> <span data-ttu-id="20d1e-184">Als u wilt dat de app op uw dashboard wilt weergeven, selecteert u de **vastmaken aan dashboard** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="20d1e-184">If you want the app to appear on your dashboard, select the **Pin to dashboard** check box.</span></span>

    ![App Service-abonnement maken][2]

    <span data-ttu-id="20d1e-186">Onder **appnaam**, de domeinnaam wordt bijgewerkt met het domein van uw as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="20d1e-186">Under **App name**, the domain name is updated to reflect the domain of your ASE.</span></span>

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="20d1e-187">Validatie van post ILB as-omgeving maken</span><span class="sxs-lookup"><span data-stu-id="20d1e-187">Post-ILB ASE creation validation</span></span> ##

<span data-ttu-id="20d1e-188">Er is een ILB-as-omgeving iets anders dan de niet - ILB as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="20d1e-188">An ILB ASE is slightly different than the non-ILB ASE.</span></span> <span data-ttu-id="20d1e-189">Als al hebt genoteerd moet u uw eigen DNS beheren.</span><span class="sxs-lookup"><span data-stu-id="20d1e-189">As already noted, you need to manage your own DNS.</span></span> <span data-ttu-id="20d1e-190">U moet ook uw eigen certificaat voor HTTPS-verbindingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="20d1e-190">You also have to provide your own certificate for HTTPS connections.</span></span>

<span data-ttu-id="20d1e-191">Nadat u uw as-omgeving hebt gemaakt, ziet u de domeinnaam in het opgegeven domein.</span><span class="sxs-lookup"><span data-stu-id="20d1e-191">After you create your ASE, the domain name shows the domain you specified.</span></span> <span data-ttu-id="20d1e-192">Een nieuw item wordt weergegeven in de **instelling** menu aangeroepen **ILB certificaat**.</span><span class="sxs-lookup"><span data-stu-id="20d1e-192">A new item appears in the **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="20d1e-193">De as-omgeving wordt gemaakt met een certificaat dat niet Geef het domein ILB as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="20d1e-193">The ASE is created with a certificate that doesn't specify the ILB ASE domain.</span></span> <span data-ttu-id="20d1e-194">Als u het as-omgeving met dat certificaat gebruikt, ziet uw browser u dat het is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="20d1e-194">If you use the ASE with that certificate, your browser tells you that it's invalid.</span></span> <span data-ttu-id="20d1e-195">Dit certificaat vereenvoudigt het testen van HTTPS, maar u moet voor het uploaden van uw eigen certificaat dat gekoppeld aan uw domein ILB as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="20d1e-195">This certificate makes it easier to test HTTPS, but you need to upload your own certificate that's tied to your ILB ASE domain.</span></span> <span data-ttu-id="20d1e-196">Deze stap is nodig, ongeacht of het certificaat is zelfondertekend of verkregen via een certificeringsinstantie.</span><span class="sxs-lookup"><span data-stu-id="20d1e-196">This step is necessary regardless of whether your certificate is self-signed or acquired from a certificate authority.</span></span>

![De domeinnaam ILB as-omgeving][3]

<span data-ttu-id="20d1e-198">Uw as ILB-omgeving moet een geldig SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="20d1e-198">Your ILB ASE needs a valid SSL certificate.</span></span> <span data-ttu-id="20d1e-199">Interne CA's gebruiken, een certificaat kopen bij een externe verlener of een zelfondertekend certificaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="20d1e-199">Use internal certificate authorities, purchase a certificate from an external issuer, or use a self-signed certificate.</span></span> <span data-ttu-id="20d1e-200">Ongeacht de bron van het SSL-certificaat moeten de volgende kenmerken van de certificaten correct worden geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="20d1e-200">Regardless of the source of the SSL certificate, the following certificate attributes need to be configured properly:</span></span>

* <span data-ttu-id="20d1e-201">**Onderwerp**: dit kenmerk moet worden ingesteld op *.your, root, domein, hier.</span><span class="sxs-lookup"><span data-stu-id="20d1e-201">**Subject**: This attribute must be set to *.your-root-domain-here.</span></span>
* <span data-ttu-id="20d1e-202">**Alternatieve onderwerpnaam**: dit kenmerk moet bevatten beide **.your, root, domein, hier* en **.scm.your-hoofdmap-domain-hier*.</span><span class="sxs-lookup"><span data-stu-id="20d1e-202">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here* and **.scm.your-root-domain-here*.</span></span> <span data-ttu-id="20d1e-203">SSL-verbindingen met de SCM/Kudu-site die is gekoppeld aan elke app een adres van het formulier gebruiken *your-app-name.scm.your-root-domain-here*.</span><span class="sxs-lookup"><span data-stu-id="20d1e-203">SSL connections to the SCM/Kudu site associated with each app use an address of the form *your-app-name.scm.your-root-domain-here*.</span></span>

<span data-ttu-id="20d1e-204">Het SSL-certificaat, converteren/opslaan als een .pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="20d1e-204">Convert/save the SSL certificate as a .pfx file.</span></span> <span data-ttu-id="20d1e-205">Het pfx-bestand moet alle tussenliggende bevatten en de hoofd-certificaten.</span><span class="sxs-lookup"><span data-stu-id="20d1e-205">The .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="20d1e-206">Beveilig deze met een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="20d1e-206">Secure it with a password.</span></span>

<span data-ttu-id="20d1e-207">Als u maken van een zelfondertekend certificaat wilt, kunt u hier de PowerShell-opdrachten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="20d1e-207">If you want to create a self-signed certificate, you can use the PowerShell commands here.</span></span> <span data-ttu-id="20d1e-208">Zorg ervoor dat u uw domeinnaam ILB as-omgeving in plaats van *internal.contoso.com*:</span><span class="sxs-lookup"><span data-stu-id="20d1e-208">Be sure to use your ILB ASE domain name instead of *internal.contoso.com*:</span></span> 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

<span data-ttu-id="20d1e-209">Het certificaat dat u deze PowerShell-opdrachten genereren is door browsers gemarkeerd, omdat het certificaat is niet gemaakt door een certificeringsinstantie die in de vertrouwensketen van uw browser.</span><span class="sxs-lookup"><span data-stu-id="20d1e-209">The certificate that these PowerShell commands generate is flagged by browsers because the certificate wasn't created by a certificate authority that's in your browser's chain of trust.</span></span> <span data-ttu-id="20d1e-210">Als u een certificaat dat uw browser vertrouwt, kunt u het aanschaffen van een commerciële certificeringsinstantie in uw browser vertrouwensketen.</span><span class="sxs-lookup"><span data-stu-id="20d1e-210">To get a certificate that your browser trusts, procure it from a commercial certificate authority in your browser's chain of trust.</span></span> 

![Set ILB certificaat][4]

<span data-ttu-id="20d1e-212">Uw eigen certificaten uploaden en toegang testen:</span><span class="sxs-lookup"><span data-stu-id="20d1e-212">To upload your own certificates and test access:</span></span>

1. <span data-ttu-id="20d1e-213">Nadat de as-omgeving is gemaakt, gaat u naar de gebruikersinterface van de as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="20d1e-213">After the ASE is created, go to the ASE UI.</span></span> <span data-ttu-id="20d1e-214">Selecteer **as-omgeving** > **instellingen** > **ILB certificaat**.</span><span class="sxs-lookup"><span data-stu-id="20d1e-214">Select **ASE** > **Settings** > **ILB Certificate**.</span></span>

2. <span data-ttu-id="20d1e-215">Het certificaat ILB instellen, selecteert u het PFX-certificaatbestand en voer het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="20d1e-215">To set the ILB certificate, select the certificate .pfx file and enter the password.</span></span> <span data-ttu-id="20d1e-216">Deze stap duurt enige tijd om te verwerken.</span><span class="sxs-lookup"><span data-stu-id="20d1e-216">This step takes some time to process.</span></span> <span data-ttu-id="20d1e-217">Er verschijnt een bericht dat een uploadbewerking uitgevoerd wordt.</span><span class="sxs-lookup"><span data-stu-id="20d1e-217">A message appears stating that an upload operation is in progress.</span></span>

3. <span data-ttu-id="20d1e-218">Haal de ILB-adres voor uw as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="20d1e-218">Get the ILB address for your ASE.</span></span> <span data-ttu-id="20d1e-219">Selecteer **as-omgeving** > **eigenschappen** > **virtueel IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="20d1e-219">Select **ASE** > **Properties** > **Virtual IP Address**.</span></span>

4. <span data-ttu-id="20d1e-220">Een web-app maken in uw as-omgeving, nadat de as-omgeving is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="20d1e-220">Create a web app in your ASE after the ASE is created.</span></span>

5. <span data-ttu-id="20d1e-221">Een virtuele machine maken als u niet in dit VNet hebt.</span><span class="sxs-lookup"><span data-stu-id="20d1e-221">Create a VM if you don't have one in that VNet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="20d1e-222">Niet probeert te maken van deze virtuele machine in hetzelfde subnet als de as-omgeving, omdat deze wordt niet uitgevoerd of problemen veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="20d1e-222">Don't try to create this VM in the same subnet as the ASE because it will fail or cause problems.</span></span>
    >
    >

6. <span data-ttu-id="20d1e-223">Stel de DNS-server voor uw domein as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="20d1e-223">Set the DNS for your ASE domain.</span></span> <span data-ttu-id="20d1e-224">U kunt een jokerteken gebruiken met uw domein in uw DNS.</span><span class="sxs-lookup"><span data-stu-id="20d1e-224">You can use a wildcard with your domain in your DNS.</span></span> <span data-ttu-id="20d1e-225">Bewerk het bestand hosts op de virtuele machine de naam van de web-app instellen op het VIP-IP-adres hiervoor enkele eenvoudige tests uit:</span><span class="sxs-lookup"><span data-stu-id="20d1e-225">To do some simple tests, edit the hosts file on your VM to set the web app name to the VIP IP address:</span></span>

    <span data-ttu-id="20d1e-226">a.</span><span class="sxs-lookup"><span data-stu-id="20d1e-226">a.</span></span> <span data-ttu-id="20d1e-227">Als uw as-omgeving de domeinnaam heeft _. ilbase.com_ en maken van de web-app met de naam _mytestapp_, het gericht op _mytestapp.ilbase.com_. Vervolgens stelt u _mytestapp.ilbase.com_ omzetten naar het adres van de ILB.</span><span class="sxs-lookup"><span data-stu-id="20d1e-227">If your ASE has the domain name _.ilbase.com_ and you create the web app named _mytestapp_, it's addressed at _mytestapp.ilbase.com_. You then set _mytestapp.ilbase.com_ to resolve to the ILB address.</span></span> <span data-ttu-id="20d1e-228">(Het hosts-bestand in vensters is _C:\Windows\System32\drivers\etc\_.)</span><span class="sxs-lookup"><span data-stu-id="20d1e-228">(On Windows, the hosts file is at _C:\Windows\System32\drivers\etc\_.)</span></span>

    <span data-ttu-id="20d1e-229">b.</span><span class="sxs-lookup"><span data-stu-id="20d1e-229">b.</span></span> <span data-ttu-id="20d1e-230">Als u wilt testen webpublicaties implementatie of toegang tot de geavanceerde console, maakt u een record voor _mytestapp.scm.ilbase.com_.</span><span class="sxs-lookup"><span data-stu-id="20d1e-230">To test web deployment publishing or access to the advanced console, create a record for _mytestapp.scm.ilbase.com_.</span></span>

7. <span data-ttu-id="20d1e-231">Een browser gebruiken die op deze virtuele machine en Ga naar http://mytestapp.ilbase.com. (Of Ga naar wat de naam van uw web-app met uw domein is.)</span><span class="sxs-lookup"><span data-stu-id="20d1e-231">Use a browser on that VM and go to http://mytestapp.ilbase.com. (Or go to whatever your web app name is with your domain.)</span></span>

8. <span data-ttu-id="20d1e-232">Een browser gebruiken die op deze virtuele machine en Ga naar https://mytestapp.ilbase.com. Als u een zelfondertekend certificaat gebruikt, accepteert u het gebrek aan beveiliging.</span><span class="sxs-lookup"><span data-stu-id="20d1e-232">Use a browser on that VM and go to https://mytestapp.ilbase.com. If you use a self-signed certificate, accept the lack of security.</span></span>

    <span data-ttu-id="20d1e-233">Het IP-adres voor de ILB wordt vermeld onder **IP-adressen**.</span><span class="sxs-lookup"><span data-stu-id="20d1e-233">The IP address for your ILB is listed under **IP addresses**.</span></span> <span data-ttu-id="20d1e-234">Deze lijst heeft ook de IP-adressen die door het externe VIP en voor binnenkomende beheer van verkeer.</span><span class="sxs-lookup"><span data-stu-id="20d1e-234">This list also has the IP addresses used by the external VIP and for inbound management traffic.</span></span>

    ![ILB IP-adres][5]

### <a name="web-jobs-functions-and-the-ilb-ase"></a><span data-ttu-id="20d1e-236">Webtaken, functies en de as ILB-omgeving</span><span class="sxs-lookup"><span data-stu-id="20d1e-236">Web jobs, Functions and the ILB ASE</span></span>

<span data-ttu-id="20d1e-237">Zowel functies en webtaken worden ondersteund op een as ILB-omgeving, maar voor de portal om hiermee te werken, moet u toegang tot het netwerk hebben tot de SCM-site.</span><span class="sxs-lookup"><span data-stu-id="20d1e-237">Both Functions and web jobs are supported on an ILB ASE but for the portal to work with them, you must have network access to the SCM site.</span></span>  <span data-ttu-id="20d1e-238">Dit betekent dat de browser moet op een host die is in- of verbonden met het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="20d1e-238">This means your browser must either be on a host that is either in or connected to the virtual network.</span></span>  

<span data-ttu-id="20d1e-239">Als u Azure Functions op een as ILB-omgeving gebruikt, krijgt u mogelijk een foutbericht weergegeven waarin wordt gemeld 'We kunnen geen uw functies nu ophalen.</span><span class="sxs-lookup"><span data-stu-id="20d1e-239">When you use Azure Functions on an ILB ASE, you might get an error message that says "We are not able to retrieve your functions right now.</span></span> <span data-ttu-id="20d1e-240">Probeer het later opnieuw."</span><span class="sxs-lookup"><span data-stu-id="20d1e-240">Please try again later."</span></span> <span data-ttu-id="20d1e-241">Deze fout treedt op omdat de gebruikersinterface van de functies maakt gebruik van de site SCM via HTTPS en het basiscertificaat niet in de vertrouwensketen browser is.</span><span class="sxs-lookup"><span data-stu-id="20d1e-241">This error occurs because the Functions UI leverages the SCM site over HTTPS and the root certificate is not in the browser chain of trust.</span></span> <span data-ttu-id="20d1e-242">Webtaken heeft een soortgelijk probleem.</span><span class="sxs-lookup"><span data-stu-id="20d1e-242">Web jobs has a similar problem.</span></span> <span data-ttu-id="20d1e-243">U kunt het volgende doen om dit probleem te voorkomen:</span><span class="sxs-lookup"><span data-stu-id="20d1e-243">To avoid this problem you can do one of the following:</span></span>

- <span data-ttu-id="20d1e-244">Het certificaat toevoegen aan uw vertrouwde certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="20d1e-244">Add the certificate to your trusted certificate store.</span></span> <span data-ttu-id="20d1e-245">Dit blokkering opgeheven rand en Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="20d1e-245">This unblocks Edge and Internet Explorer.</span></span>
- <span data-ttu-id="20d1e-246">Chrome gebruiken en gaat u naar de site SCM eerst, niet-vertrouwd certificaat te accepteren en gaat u naar de portal.</span><span class="sxs-lookup"><span data-stu-id="20d1e-246">Use Chrome and go to the SCM site first, accept the untrusted certificate and then go to the portal.</span></span>
- <span data-ttu-id="20d1e-247">Een commerciële certificaat in uw browser vertrouwensketen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="20d1e-247">Use a commercial certificate that is in your browser chain of trust.</span></span>  <span data-ttu-id="20d1e-248">Dit is de beste optie.</span><span class="sxs-lookup"><span data-stu-id="20d1e-248">This is the best option.</span></span>  

## <a name="dns-configuration"></a><span data-ttu-id="20d1e-249">DNS-configuratie</span><span class="sxs-lookup"><span data-stu-id="20d1e-249">DNS configuration</span></span> ##

<span data-ttu-id="20d1e-250">Wanneer u een externe VIP gebruikt, wordt de DNS-server wordt beheerd door Azure.</span><span class="sxs-lookup"><span data-stu-id="20d1e-250">When you use an External VIP, the DNS is managed by Azure.</span></span> <span data-ttu-id="20d1e-251">Elke app gemaakt in uw as-omgeving wordt automatisch toegevoegd aan Azure DNS, die een openbare DNS-server is.</span><span class="sxs-lookup"><span data-stu-id="20d1e-251">Any app created in your ASE is automatically added to Azure DNS, which is a public DNS.</span></span> <span data-ttu-id="20d1e-252">In een ILB as-omgeving, moet u uw eigen DNS beheren.</span><span class="sxs-lookup"><span data-stu-id="20d1e-252">In an ILB ASE, you must manage your own DNS.</span></span> <span data-ttu-id="20d1e-253">Voor een bepaald domein, zoals _contoso.net_, moet u DNS A-records in DNS die verwijzen naar uw adres ILB voor maken:</span><span class="sxs-lookup"><span data-stu-id="20d1e-253">For a given domain such as _contoso.net_, you need to create DNS A records in your DNS that point to your ILB address for:</span></span>

- <span data-ttu-id="20d1e-254">*. contoso.net</span><span class="sxs-lookup"><span data-stu-id="20d1e-254">*.contoso.net</span></span>
- <span data-ttu-id="20d1e-255">*. scm.contoso.net</span><span class="sxs-lookup"><span data-stu-id="20d1e-255">*.scm.contoso.net</span></span>

<span data-ttu-id="20d1e-256">Als uw domein ILB as-omgeving wordt gebruikt voor meerdere dingen buiten deze as-omgeving, moet u mogelijk DNS beheren op basis van de per-app-naam.</span><span class="sxs-lookup"><span data-stu-id="20d1e-256">If your ILB ASE domain is used for multiple things outside this ASE, you might need to manage DNS on a per-app-name basis.</span></span> <span data-ttu-id="20d1e-257">Deze methode is lastig omdat u de appnaam van elke nieuwe toevoegen in uw DNS moet wanneer u deze maakt.</span><span class="sxs-lookup"><span data-stu-id="20d1e-257">This method is challenging because you need to add each new app name into your DNS when you create it.</span></span> <span data-ttu-id="20d1e-258">Daarom is het raadzaam dat u een speciale domein.</span><span class="sxs-lookup"><span data-stu-id="20d1e-258">For this reason, we recommend that you use a dedicated domain.</span></span>

## <a name="publish-with-an-ilb-ase"></a><span data-ttu-id="20d1e-259">Publiceren met een ILB-as-omgeving</span><span class="sxs-lookup"><span data-stu-id="20d1e-259">Publish with an ILB ASE</span></span> ##

<span data-ttu-id="20d1e-260">Voor elke app die gemaakt, zijn er twee eindpunten.</span><span class="sxs-lookup"><span data-stu-id="20d1e-260">For every app that's created, there are two endpoints.</span></span> <span data-ttu-id="20d1e-261">In een ILB as-omgeving, hebt u  *&lt;app-naam >.&lt; ILB as-omgeving Domain >* en  *&lt;app-naam > .scm.&lt; ILB as-omgeving Domain >*.</span><span class="sxs-lookup"><span data-stu-id="20d1e-261">In an ILB ASE, you have *&lt;app name>.&lt;ILB ASE Domain>* and *&lt;app name>.scm.&lt;ILB ASE Domain>*.</span></span> 

<span data-ttu-id="20d1e-262">De sitenaam SCM Hiermee gaat u naar de Kudu-console, genaamd de **geavanceerde portal**, binnen de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="20d1e-262">The SCM site name takes you to the Kudu console, called the **Advanced portal**, within the Azure portal.</span></span> <span data-ttu-id="20d1e-263">De Kudu-console kunt u omgevingsvariabelen weergeven, de schijf verkennen, gebruikt u een console, en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="20d1e-263">The Kudu console lets you view environment variables, explore the disk, use a console, and much more.</span></span> <span data-ttu-id="20d1e-264">Zie voor meer informatie [Kudu-console voor Azure App Service][Kudu].</span><span class="sxs-lookup"><span data-stu-id="20d1e-264">For more information, see [Kudu console for Azure App Service][Kudu].</span></span> 

<span data-ttu-id="20d1e-265">Er is eenmalige aanmelding tussen de Azure-portal en de Kudu-console in de multitenant-App Service en in een externe as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="20d1e-265">In the multitenant App Service and in an External ASE, there's single sign-on between the Azure portal and the Kudu console.</span></span> <span data-ttu-id="20d1e-266">Voor de ILB as-omgeving, echter, moet u uw publishing referenties gebruiken om aan te melden bij de Kudu-console.</span><span class="sxs-lookup"><span data-stu-id="20d1e-266">For the ILB ASE, however, you need to use your publishing credentials to sign into the Kudu console.</span></span>

<span data-ttu-id="20d1e-267">Internetgebaseerde CI systemen, zoals GitHub en Visual Studio Team Services, werkt niet met een ILB-as-omgeving omdat het publishing eindpunt niet toegankelijk internet.</span><span class="sxs-lookup"><span data-stu-id="20d1e-267">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because the publishing endpoint isn't internet accessible.</span></span> <span data-ttu-id="20d1e-268">In plaats daarvan moet u een CI-besturingssysteem dat gebruikmaakt van een pull-model, zoals Dropbox gebruiken.</span><span class="sxs-lookup"><span data-stu-id="20d1e-268">Instead, you need to use a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="20d1e-269">Het domein dat de as ILB-omgeving is gemaakt met de publicatie eindpunten voor apps in een ILB-as-omgeving gebruiken</span><span class="sxs-lookup"><span data-stu-id="20d1e-269">The publishing endpoints for apps in an ILB ASE use the domain that the ILB ASE was created with.</span></span> <span data-ttu-id="20d1e-270">Dit domein wordt weergegeven in het profiel voor het publiceren van de app en de portalblade van de app (**overzicht** > **Essentials** en ook **eigenschappen**).</span><span class="sxs-lookup"><span data-stu-id="20d1e-270">This domain appears in the app's publishing profile and in the app's portal blade (**Overview** > **Essentials** and also **Properties**).</span></span> <span data-ttu-id="20d1e-271">Als u een ILB-as-omgeving met het subdomein hebt *contoso.net* en een app met de naam *mytest*, gebruik *mytest.contoso.net* voor FTP en *mytest.scm.contoso.net* voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="20d1e-271">If you have an ILB ASE with the subdomain *contoso.net* and an app named *mytest*, use *mytest.contoso.net* for FTP and *mytest.scm.contoso.net* for web deployment.</span></span>

## <a name="couple-an-ilb-ase-with-a-waf-device"></a><span data-ttu-id="20d1e-272">Combineer een ILB-as-omgeving met een WAF-apparaat</span><span class="sxs-lookup"><span data-stu-id="20d1e-272">Couple an ILB ASE with a WAF device</span></span> ##

<span data-ttu-id="20d1e-273">Azure App Service biedt veel beveiligingsfuncties die beschermen van het systeem.</span><span class="sxs-lookup"><span data-stu-id="20d1e-273">Azure App Service provides many security measures that protect the system.</span></span> <span data-ttu-id="20d1e-274">Ze helpen ook om te bepalen of een app is gehackte.</span><span class="sxs-lookup"><span data-stu-id="20d1e-274">They also help to determine whether an app was hacked.</span></span> <span data-ttu-id="20d1e-275">De beste beveiliging voor een webtoepassing is het een host-platform, zoals Azure App Service, Combineer met web application firewall (WAF).</span><span class="sxs-lookup"><span data-stu-id="20d1e-275">The best protection for a web application is to couple a hosting platform, such as Azure App Service, with a web application firewall (WAF).</span></span> <span data-ttu-id="20d1e-276">Omdat de as ILB-omgeving een toepassingseindpunt netwerk geïsoleerd van heeft, is het geschikt is voor dit gebruik.</span><span class="sxs-lookup"><span data-stu-id="20d1e-276">Because the ILB ASE has a network-isolated application endpoint, it's appropriate for such a use.</span></span>

<span data-ttu-id="20d1e-277">Zie voor meer informatie over het configureren van de as ILB-omgeving met een apparaat WAF, [web application firewall configureren met uw App-serviceomgeving][ASEWAF].</span><span class="sxs-lookup"><span data-stu-id="20d1e-277">To learn more about how to configure your ILB ASE with a WAF device, see [Configure a web application firewall with your App Service environment][ASEWAF].</span></span> <span data-ttu-id="20d1e-278">Dit artikel laat zien hoe u een virtueel apparaat Barracuda met uw as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="20d1e-278">This article shows how to use a Barracuda virtual appliance with your ASE.</span></span> <span data-ttu-id="20d1e-279">Een andere optie is het gebruik van Azure Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="20d1e-279">Another option is to use Azure Application Gateway.</span></span> <span data-ttu-id="20d1e-280">Toepassingsgateway gebruikt de OWASP core-regels voor het beveiligen van alle toepassingen erachter geplaatst.</span><span class="sxs-lookup"><span data-stu-id="20d1e-280">Application Gateway uses the OWASP core rules to secure any applications placed behind it.</span></span> <span data-ttu-id="20d1e-281">Zie voor meer informatie over Application Gateway [Inleiding tot de Azure-web application firewall][AppGW].</span><span class="sxs-lookup"><span data-stu-id="20d1e-281">For more information about Application Gateway, see [Introduction to the Azure web application firewall][AppGW].</span></span>

## <a name="get-started"></a><span data-ttu-id="20d1e-282">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="20d1e-282">Get started</span></span> ##

<span data-ttu-id="20d1e-283">Alle artikelen en instructies voor ASEs zijn beschikbaar in de [Leesmij-bestand voor App Service-omgevingen][ASEReadme].</span><span class="sxs-lookup"><span data-stu-id="20d1e-283">All articles and how-to instructions for ASEs are available in the [README for App Service environments][ASEReadme].</span></span>

* <span data-ttu-id="20d1e-284">Als u wilt beginnen met ASEs, Zie [Inleiding tot de App Service-omgevingen][Intro].</span><span class="sxs-lookup"><span data-stu-id="20d1e-284">To get started with ASEs, see [Introduction to App Service environments][Intro].</span></span>
* <span data-ttu-id="20d1e-285">Zie [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/) voor meer informatie over het Azure App Service-platform.</span><span class="sxs-lookup"><span data-stu-id="20d1e-285">For more information about the Azure App Service platform, see [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span></span>
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
