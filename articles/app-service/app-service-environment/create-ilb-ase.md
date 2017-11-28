---
title: aaaCreate en het gebruik van een interne load balancer met een Azure App Service-omgeving
description: "Meer informatie over het toocreate en gebruik van een geïsoleerd van internet Azure App Service-omgeving"
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
ms.openlocfilehash: d019ca6f231c3acfdab4cd380db375a076802f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="61d81-103">Maken en gebruiken van een interne load balancer met een App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="61d81-103">Create and use an internal load balancer with an App Service environment</span></span> #

 <span data-ttu-id="61d81-104">Azure App Service-omgeving is een implementatie van Azure App Service in een subnet in een Azure-netwerk (VNet).</span><span class="sxs-lookup"><span data-stu-id="61d81-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="61d81-105">Er zijn twee manieren toodeploy een App Service-omgeving (as-omgeving):</span><span class="sxs-lookup"><span data-stu-id="61d81-105">There are two ways toodeploy an App Service environment (ASE):</span></span> 

- <span data-ttu-id="61d81-106">Een VIP-adres op een externe IP-adres, vaak aangeduid als een externe as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="61d81-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="61d81-107">Een VIP-adres op een interne IP-adres, vaak genoemd, een ILB-as-omgeving omdat Hallo interne eindpunt, een interne load balancer (ILB is).</span><span class="sxs-lookup"><span data-stu-id="61d81-107">With a VIP on an internal IP address, often called an ILB ASE because hello internal endpoint is an internal load balancer (ILB).</span></span> 

<span data-ttu-id="61d81-108">Dit artikel ziet u hoe toocreate een ILB-as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="61d81-108">This article shows you how toocreate an ILB ASE.</span></span> <span data-ttu-id="61d81-109">Zie voor een overzicht op Hallo as-omgeving [inleiding tooApp Service-omgevingen][Intro].</span><span class="sxs-lookup"><span data-stu-id="61d81-109">For an overview on hello ASE, see [Introduction tooApp Service environments][Intro].</span></span> <span data-ttu-id="61d81-110">hoe toocreate een externe as-omgeving, Zie toolearn [maken van een externe as-omgeving][MakeExternalASE].</span><span class="sxs-lookup"><span data-stu-id="61d81-110">toolearn how toocreate an External ASE, see [Create an External ASE][MakeExternalASE].</span></span>

## <a name="overview"></a><span data-ttu-id="61d81-111">Overzicht</span><span class="sxs-lookup"><span data-stu-id="61d81-111">Overview</span></span> ##

<span data-ttu-id="61d81-112">U kunt een as-omgeving met een internet toegankelijke eindpunt of met een IP-adres implementeren in uw VNet.</span><span class="sxs-lookup"><span data-stu-id="61d81-112">You can deploy an ASE with an internet-accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="61d81-113">tooset hello IP-adressen tooa VNet-adres, Hallo as-omgeving moet worden geïmplementeerd met een ILB.</span><span class="sxs-lookup"><span data-stu-id="61d81-113">tooset hello IP address tooa VNet address, hello ASE must be deployed with an ILB.</span></span> <span data-ttu-id="61d81-114">Wanneer u uw as-omgeving met een ILB implementeert, moet u het volgende opgeven:</span><span class="sxs-lookup"><span data-stu-id="61d81-114">When you deploy your ASE with an ILB, you must provide:</span></span>

-   <span data-ttu-id="61d81-115">Uw eigen domein dat u bij het maken van uw apps.</span><span class="sxs-lookup"><span data-stu-id="61d81-115">Your own domain that you use when you create your apps.</span></span>
-   <span data-ttu-id="61d81-116">Hallo-certificaat gebruikt voor HTTPS.</span><span class="sxs-lookup"><span data-stu-id="61d81-116">hello certificate used for HTTPS.</span></span>
-   <span data-ttu-id="61d81-117">DNS-beheer voor uw domein.</span><span class="sxs-lookup"><span data-stu-id="61d81-117">DNS management for your domain.</span></span>

<span data-ttu-id="61d81-118">Tegenprestatie kunt u doen, zoals:</span><span class="sxs-lookup"><span data-stu-id="61d81-118">In return, you can do things such as:</span></span>

-   <span data-ttu-id="61d81-119">Intranet-hosttoepassingen veilig in Hallo cloud, die u via een site-naar-site of Azure ExpressRoute VPN-toegang.</span><span class="sxs-lookup"><span data-stu-id="61d81-119">Host intranet applications securely in hello cloud, which you access through a site-to-site or Azure ExpressRoute VPN.</span></span>
-   <span data-ttu-id="61d81-120">Host-apps in Hallo cloud die niet zijn opgenomen in de openbare DNS-servers.</span><span class="sxs-lookup"><span data-stu-id="61d81-120">Host apps in hello cloud that aren't listed in public DNS servers.</span></span>
-   <span data-ttu-id="61d81-121">Internet geïsoleerd back-end-apps, die uw front-apps kunnen veilig worden geïntegreerd met maken.</span><span class="sxs-lookup"><span data-stu-id="61d81-121">Create internet-isolated back-end apps, which your front-end apps can securely integrate with.</span></span>

### <a name="disabled-functionality"></a><span data-ttu-id="61d81-122">Uitgeschakelde functionaliteit</span><span class="sxs-lookup"><span data-stu-id="61d81-122">Disabled functionality</span></span> ###

<span data-ttu-id="61d81-123">Er zijn een aantal zaken die u niet mogelijk wanneer u een ILB-as-omgeving:</span><span class="sxs-lookup"><span data-stu-id="61d81-123">There are some things that you can't do when you use an ILB ASE:</span></span>

-   <span data-ttu-id="61d81-124">IP-gebaseerde SSL wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="61d81-124">Use IP-based SSL.</span></span>
-   <span data-ttu-id="61d81-125">IP-adressen toewijzen toospecific apps.</span><span class="sxs-lookup"><span data-stu-id="61d81-125">Assign IP addresses toospecific apps.</span></span>
-   <span data-ttu-id="61d81-126">Koop en een certificaat met een app via hello Azure-portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="61d81-126">Buy and use a certificate with an app through hello Azure portal.</span></span> <span data-ttu-id="61d81-127">U kunt certificaten rechtstreeks vanuit een certificeringsinstantie verkrijgen en ze gebruiken met uw apps.</span><span class="sxs-lookup"><span data-stu-id="61d81-127">You can obtain certificates directly from a certificate authority and use them with your apps.</span></span> <span data-ttu-id="61d81-128">U kunt deze kan niet verkrijgen via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="61d81-128">You can't obtain them through hello Azure portal.</span></span>

## <a name="create-an-ilb-ase"></a><span data-ttu-id="61d81-129">Een as ILB-omgeving maken</span><span class="sxs-lookup"><span data-stu-id="61d81-129">Create an ILB ASE</span></span> ##

<span data-ttu-id="61d81-130">toocreate een ILB-as-omgeving:</span><span class="sxs-lookup"><span data-stu-id="61d81-130">toocreate an ILB ASE:</span></span>

1. <span data-ttu-id="61d81-131">Selecteer in de Azure-portal hello, **nieuw** > **Web en mobiel** > **App Service-omgeving**.</span><span class="sxs-lookup"><span data-stu-id="61d81-131">In hello Azure portal, select **New** > **Web + Mobile** > **App Service Environment**.</span></span>

2. <span data-ttu-id="61d81-132">Selecteer uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="61d81-132">Select your subscription.</span></span>

3. <span data-ttu-id="61d81-133">Selecteer of maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="61d81-133">Select or create a resource group.</span></span>

4. <span data-ttu-id="61d81-134">Selecteer of maak een VNet.</span><span class="sxs-lookup"><span data-stu-id="61d81-134">Select or create a VNet.</span></span>

5. <span data-ttu-id="61d81-135">Als u een bestaande VNet selecteert, moet u toocreate een subnet toohold Hallo as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="61d81-135">If you select an existing VNet, you need toocreate a subnet toohold hello ASE.</span></span> <span data-ttu-id="61d81-136">Zorg ervoor dat eventuele toekomstige groei van uw as-omgeving voor grootte groot genoeg tooaccommodate tooset een subnet.</span><span class="sxs-lookup"><span data-stu-id="61d81-136">Make sure tooset a subnet size large enough tooaccommodate any future growth of your ASE.</span></span> <span data-ttu-id="61d81-137">Een grootte van het is raadzaam `/25`, waardoor 128 adressen heeft en een maximale grootte as-omgeving kan verwerken.</span><span class="sxs-lookup"><span data-stu-id="61d81-137">We recommend a size of `/25`, which has 128 addresses and can handle a maximum-sized ASE.</span></span> <span data-ttu-id="61d81-138">is de minimale grootte Hallo kunt u een `/28`.</span><span class="sxs-lookup"><span data-stu-id="61d81-138">hello minimum size you can select is a `/28`.</span></span> <span data-ttu-id="61d81-139">Nadat de infrastructuur nodig heeft, kan de grootte van deze geschaalde tooa maximaal 11 exemplaren zijn.</span><span class="sxs-lookup"><span data-stu-id="61d81-139">After infrastructure needs, this size can be scaled tooa maximum of 11 instances.</span></span>

    * <span data-ttu-id="61d81-140">Verder dan Hallo standaardaantal van maximaal 100 exemplaren in uw App Service-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="61d81-140">Go beyond hello default maximum of 100 instances in your App Service plans.</span></span>

    * <span data-ttu-id="61d81-141">In de buurt van 100, maar met meer snelle front-schaling schalen.</span><span class="sxs-lookup"><span data-stu-id="61d81-141">Scale near 100 but with more rapid front-end scaling.</span></span>

6. <span data-ttu-id="61d81-142">Selecteer **virtuele netwerklocatie** > **virtuele netwerkconfiguratie**.</span><span class="sxs-lookup"><span data-stu-id="61d81-142">Select **Virtual Network/Location** > **Virtual Network Configuration**.</span></span> <span data-ttu-id="61d81-143">Set Hallo **VIP Type** te**intern**.</span><span class="sxs-lookup"><span data-stu-id="61d81-143">Set hello **VIP Type** too**Internal**.</span></span>

7. <span data-ttu-id="61d81-144">Voer de domeinnaam van een.</span><span class="sxs-lookup"><span data-stu-id="61d81-144">Enter a domain name.</span></span> <span data-ttu-id="61d81-145">Dit domein is Hallo gebruikt voor apps die zijn gemaakt in deze as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="61d81-145">This domain is hello one used for apps created in this ASE.</span></span> <span data-ttu-id="61d81-146">Er zijn enkele beperkingen.</span><span class="sxs-lookup"><span data-stu-id="61d81-146">There are some restrictions.</span></span> <span data-ttu-id="61d81-147">Kan niet worden:</span><span class="sxs-lookup"><span data-stu-id="61d81-147">It can't be:</span></span>

    * <span data-ttu-id="61d81-148">NET</span><span class="sxs-lookup"><span data-stu-id="61d81-148">net</span></span>   

    * <span data-ttu-id="61d81-149">azurewebsites.NET</span><span class="sxs-lookup"><span data-stu-id="61d81-149">azurewebsites.net</span></span>

    * <span data-ttu-id="61d81-150">p.azurewebsites.NET</span><span class="sxs-lookup"><span data-stu-id="61d81-150">p.azurewebsites.net</span></span>

    * <span data-ttu-id="61d81-151">&lt;asename&gt;. p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="61d81-151">&lt;asename&gt;.p.azurewebsites.net</span></span>

   <span data-ttu-id="61d81-152">de aangepaste domeinnaam Hallo gebruikt voor apps en Hallo-domeinnaam die wordt gebruikt door uw as-omgeving kunnen elkaar niet overlappen.</span><span class="sxs-lookup"><span data-stu-id="61d81-152">hello custom domain name used for apps and hello domain name used by your ASE can't overlap.</span></span> <span data-ttu-id="61d81-153">Voor een as ILB-omgeving met de domeinnaam Hallo _contoso.com_, u kunt aangepaste domeinnamen voor uw apps zoals niet gebruiken:</span><span class="sxs-lookup"><span data-stu-id="61d81-153">For an ILB ASE with hello domain name _contoso.com_, you can't use custom domain names for your apps like:</span></span>

    * <span data-ttu-id="61d81-154">www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="61d81-154">www.contoso.com</span></span>

    * <span data-ttu-id="61d81-155">ABCD.def.contoso.com</span><span class="sxs-lookup"><span data-stu-id="61d81-155">abcd.def.contoso.com</span></span>

    * <span data-ttu-id="61d81-156">ABCD.contoso.com</span><span class="sxs-lookup"><span data-stu-id="61d81-156">abcd.contoso.com</span></span>

   <span data-ttu-id="61d81-157">Als u Hallo aangepaste domeinnamen voor uw apps weet, kiest u een domein voor Hallo as-ILB omgeving die u geen een conflict met deze aangepaste domeinnamen hebt.</span><span class="sxs-lookup"><span data-stu-id="61d81-157">If you know hello custom domain names for your apps, choose a domain for hello ILB ASE that won’t have a conflict with those custom domain names.</span></span> <span data-ttu-id="61d81-158">In dit voorbeeld kunt u ongeveer *contoso internal.com* voor Hallo domein van uw as-omgeving omdat dat geen met aangepaste domeinnamen die eindigen conflicten op *. contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="61d81-158">In this example, you can use something like *contoso-internal.com* for hello domain of your ASE because that won't conflict with custom domain names that end in *.contoso.com*.</span></span>

8. <span data-ttu-id="61d81-159">Selecteer **OK**, en selecteer vervolgens **maken**.</span><span class="sxs-lookup"><span data-stu-id="61d81-159">Select **OK**, and then select **Create**.</span></span>

    ![ASE maken][1]

<span data-ttu-id="61d81-161">Op Hallo **virtueel netwerk** blade, er is een **virtuele netwerkconfiguratie** optie.</span><span class="sxs-lookup"><span data-stu-id="61d81-161">On hello **Virtual Network** blade, there is a **Virtual Network Configuration** option.</span></span> <span data-ttu-id="61d81-162">U kunt deze gebruiken tooselect een externe VIP of een interne VIP.</span><span class="sxs-lookup"><span data-stu-id="61d81-162">You can use it tooselect an External VIP or an Internal VIP.</span></span> <span data-ttu-id="61d81-163">Hallo standaardwaarde is **externe**.</span><span class="sxs-lookup"><span data-stu-id="61d81-163">hello default is **External**.</span></span> <span data-ttu-id="61d81-164">Als u selecteert **externe**, uw as-omgeving maakt gebruik van een internet toegankelijke VIP.</span><span class="sxs-lookup"><span data-stu-id="61d81-164">If you select **External**, your ASE uses an internet-accessible VIP.</span></span> <span data-ttu-id="61d81-165">Als u selecteert **intern**, uw as-omgeving is geconfigureerd met een ILB op een IP-adres binnen uw VNet.</span><span class="sxs-lookup"><span data-stu-id="61d81-165">If you select **Internal**, your ASE is configured with an ILB on an IP address within your VNet.</span></span>

<span data-ttu-id="61d81-166">Nadat u hebt geselecteerd **intern**, Hallo mogelijkheid tooadd meer IP-adressen tooyour as-omgeving wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="61d81-166">After you select **Internal**, hello ability tooadd more IP addresses tooyour ASE is removed.</span></span> <span data-ttu-id="61d81-167">In plaats daarvan moet u tooprovide Hallo domein Hallo as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="61d81-167">Instead, you need tooprovide hello domain of hello ASE.</span></span> <span data-ttu-id="61d81-168">In een as met een externe VIP-omgeving, wordt hello naam van het Hallo-as-omgeving gebruikt in Hallo domein voor apps die zijn gemaakt in die as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="61d81-168">In an ASE with an External VIP, hello name of hello ASE is used in hello domain for apps created in that ASE.</span></span>

<span data-ttu-id="61d81-169">Als u instelt **VIP Type** te**intern**, de naam van uw as-omgeving wordt niet gebruikt in Hallo domein voor Hallo as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="61d81-169">If you set **VIP Type** too**Internal**, your ASE name is not used in hello domain for hello ASE.</span></span> <span data-ttu-id="61d81-170">U opgeven expliciet Hallo domein.</span><span class="sxs-lookup"><span data-stu-id="61d81-170">You specify hello domain explicitly.</span></span> <span data-ttu-id="61d81-171">Als uw domein *contoso.corp.net* en u een app maken in de betreffende as-omgeving met de naam *timereporting*, Hallo URL voor die app timereporting.contoso.corp.net is.</span><span class="sxs-lookup"><span data-stu-id="61d81-171">If your domain is *contoso.corp.net* and you create an app in that ASE named *timereporting*, hello URL for that app is timereporting.contoso.corp.net.</span></span>


## <a name="create-an-app-in-an-ilb-ase"></a><span data-ttu-id="61d81-172">Een app maken in een ILB-as-omgeving</span><span class="sxs-lookup"><span data-stu-id="61d81-172">Create an app in an ILB ASE</span></span> ##

<span data-ttu-id="61d81-173">U een app maken in een ILB-as-omgeving in Hallo dezelfde manier waarop u een app in een as-omgeving normaal.</span><span class="sxs-lookup"><span data-stu-id="61d81-173">You create an app in an ILB ASE in hello same way that you create an app in an ASE normally.</span></span>

1. <span data-ttu-id="61d81-174">Selecteer in de Azure-portal hello, **nieuw** > **Web en mobiel** > **Web** of **Mobile** of  **API-App**.</span><span class="sxs-lookup"><span data-stu-id="61d81-174">In hello Azure portal, select **New** > **Web + Mobile** > **Web** or **Mobile** or **API App**.</span></span>

2. <span data-ttu-id="61d81-175">Voer de naam Hallo van Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="61d81-175">Enter hello name of hello app.</span></span>

3. <span data-ttu-id="61d81-176">Hallo-abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="61d81-176">Select hello subscription.</span></span>

4. <span data-ttu-id="61d81-177">Selecteer of maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="61d81-177">Select or create a resource group.</span></span>

5. <span data-ttu-id="61d81-178">Selecteer of maak een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="61d81-178">Select or create an App Service plan.</span></span> <span data-ttu-id="61d81-179">Als u een nieuw App Service-plan toocreate wilt, selecteert u uw as-omgeving als Hallo locatie.</span><span class="sxs-lookup"><span data-stu-id="61d81-179">If you want toocreate a new App Service plan, select your ASE as hello location.</span></span> <span data-ttu-id="61d81-180">Selecteer Hallo werknemersgroep waar u uw App Service-plan toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="61d81-180">Select hello worker pool where you want your App Service plan toobe created.</span></span> <span data-ttu-id="61d81-181">Wanneer u Hallo App Service-abonnement hebt gemaakt, selecteert u uw as-omgeving als Hallo locatie en Hallo werknemersgroep.</span><span class="sxs-lookup"><span data-stu-id="61d81-181">When you create hello App Service plan, select your ASE as hello location and hello worker pool.</span></span> <span data-ttu-id="61d81-182">Wanneer u Hallo-naam van Hallo app opgeeft, is Hallo domein onder de appnaam van uw vervangen door Hallo domein voor uw as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="61d81-182">When you specify hello name of hello app, hello domain under your app name is replaced by hello domain for your ASE.</span></span>

6. <span data-ttu-id="61d81-183">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="61d81-183">Select **Create**.</span></span> <span data-ttu-id="61d81-184">Als u Hallo app tooappear op uw dashboard, selecteert de **pincode toodashboard** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="61d81-184">If you want hello app tooappear on your dashboard, select the **Pin toodashboard** check box.</span></span>

    ![App Service-abonnement maken][2]

    <span data-ttu-id="61d81-186">Onder **appnaam**, Hallo domeinnaam is bijgewerkte tooreflect Hallo domein van uw as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="61d81-186">Under **App name**, hello domain name is updated tooreflect hello domain of your ASE.</span></span>

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="61d81-187">Validatie van post ILB as-omgeving maken</span><span class="sxs-lookup"><span data-stu-id="61d81-187">Post-ILB ASE creation validation</span></span> ##

<span data-ttu-id="61d81-188">Er is een ILB-as-omgeving iets anders dan Hallo niet - ILB as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="61d81-188">An ILB ASE is slightly different than hello non-ILB ASE.</span></span> <span data-ttu-id="61d81-189">Als al hebt genoteerd moet u toomanage uw eigen DNS.</span><span class="sxs-lookup"><span data-stu-id="61d81-189">As already noted, you need toomanage your own DNS.</span></span> <span data-ttu-id="61d81-190">Hebt u ook tooprovide uw eigen certificaat voor HTTPS-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="61d81-190">You also have tooprovide your own certificate for HTTPS connections.</span></span>

<span data-ttu-id="61d81-191">Nadat u uw as-omgeving hebt gemaakt, toont domeinnaam Hallo Hallo door u opgegeven domein.</span><span class="sxs-lookup"><span data-stu-id="61d81-191">After you create your ASE, hello domain name shows hello domain you specified.</span></span> <span data-ttu-id="61d81-192">Een nieuw item wordt weergegeven in de **instelling** menu aangeroepen **ILB certificaat**.</span><span class="sxs-lookup"><span data-stu-id="61d81-192">A new item appears in the **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="61d81-193">Hallo as-omgeving wordt gemaakt met een certificaat dat niet Hallo ILB as-omgeving domein opgeven.</span><span class="sxs-lookup"><span data-stu-id="61d81-193">hello ASE is created with a certificate that doesn't specify hello ILB ASE domain.</span></span> <span data-ttu-id="61d81-194">Als u Hallo as-omgeving met dat certificaat gebruikt, wordt uw browser aangegeven dat het is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="61d81-194">If you use hello ASE with that certificate, your browser tells you that it's invalid.</span></span> <span data-ttu-id="61d81-195">Dit certificaat maakt het eenvoudiger tootest HTTPS, maar u moet tooupload uw eigen certificaat dat is gebonden tooyour ILB as-omgeving domein.</span><span class="sxs-lookup"><span data-stu-id="61d81-195">This certificate makes it easier tootest HTTPS, but you need tooupload your own certificate that's tied tooyour ILB ASE domain.</span></span> <span data-ttu-id="61d81-196">Deze stap is nodig, ongeacht of het certificaat is zelfondertekend of verkregen via een certificeringsinstantie.</span><span class="sxs-lookup"><span data-stu-id="61d81-196">This step is necessary regardless of whether your certificate is self-signed or acquired from a certificate authority.</span></span>

![De domeinnaam ILB as-omgeving][3]

<span data-ttu-id="61d81-198">Uw as ILB-omgeving moet een geldig SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="61d81-198">Your ILB ASE needs a valid SSL certificate.</span></span> <span data-ttu-id="61d81-199">Interne CA's gebruiken, een certificaat kopen bij een externe verlener of een zelfondertekend certificaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="61d81-199">Use internal certificate authorities, purchase a certificate from an external issuer, or use a self-signed certificate.</span></span> <span data-ttu-id="61d81-200">Ongeacht Hallo bron van het SSL-certificaat hello moeten hello volgende kenmerken van het certificaat toobe correct is geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="61d81-200">Regardless of hello source of hello SSL certificate, hello following certificate attributes need toobe configured properly:</span></span>

* <span data-ttu-id="61d81-201">**Onderwerp**: dit kenmerk too*.your, root, domein, hier moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="61d81-201">**Subject**: This attribute must be set too*.your-root-domain-here.</span></span>
* <span data-ttu-id="61d81-202">**Alternatieve onderwerpnaam**: dit kenmerk moet bevatten beide **.your, root, domein, hier* en **.scm.your-hoofdmap-domain-hier*.</span><span class="sxs-lookup"><span data-stu-id="61d81-202">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here* and **.scm.your-root-domain-here*.</span></span> <span data-ttu-id="61d81-203">SSL-verbindingen toohello SCM/Kudu site die is gekoppeld aan elke app gebruiken een adres van het formulier Hallo *your-app-name.scm.your-root-domain-here*.</span><span class="sxs-lookup"><span data-stu-id="61d81-203">SSL connections toohello SCM/Kudu site associated with each app use an address of hello form *your-app-name.scm.your-root-domain-here*.</span></span>

<span data-ttu-id="61d81-204">Hallo SSL-certificaat, converteren/opslaan als een .pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="61d81-204">Convert/save hello SSL certificate as a .pfx file.</span></span> <span data-ttu-id="61d81-205">Hallo pfx-bestand moet alle tussenliggende bevatten en de hoofd-certificaten.</span><span class="sxs-lookup"><span data-stu-id="61d81-205">hello .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="61d81-206">Beveilig deze met een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="61d81-206">Secure it with a password.</span></span>

<span data-ttu-id="61d81-207">Als u een zelfondertekend certificaat toocreate wilt, kunt u hier Hallo PowerShell-opdrachten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="61d81-207">If you want toocreate a self-signed certificate, you can use hello PowerShell commands here.</span></span> <span data-ttu-id="61d81-208">Worden toouse ervoor dat de domeinnaam van uw ILB as-omgeving in plaats van *internal.contoso.com*:</span><span class="sxs-lookup"><span data-stu-id="61d81-208">Be sure toouse your ILB ASE domain name instead of *internal.contoso.com*:</span></span> 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

<span data-ttu-id="61d81-209">Hallo-certificaat dat u deze PowerShell-opdrachten genereren is gemarkeerd door browsers omdat Hallo-certificaat is niet gemaakt door een certificeringsinstantie die in de vertrouwensketen van uw browser.</span><span class="sxs-lookup"><span data-stu-id="61d81-209">hello certificate that these PowerShell commands generate is flagged by browsers because hello certificate wasn't created by a certificate authority that's in your browser's chain of trust.</span></span> <span data-ttu-id="61d81-210">tooget een certificaat dat door uw browser vertrouwt, schaft u deze via een commerciële certificeringsinstantie in de vertrouwensketen van uw browser.</span><span class="sxs-lookup"><span data-stu-id="61d81-210">tooget a certificate that your browser trusts, procure it from a commercial certificate authority in your browser's chain of trust.</span></span> 

![Set ILB certificaat][4]

<span data-ttu-id="61d81-212">tooupload uw eigen certificaten en toegang testen:</span><span class="sxs-lookup"><span data-stu-id="61d81-212">tooupload your own certificates and test access:</span></span>

1. <span data-ttu-id="61d81-213">Nadat het Hallo-as-omgeving is gemaakt, gaat u toohello UI as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="61d81-213">After hello ASE is created, go toohello ASE UI.</span></span> <span data-ttu-id="61d81-214">Selecteer **as-omgeving** > **instellingen** > **ILB certificaat**.</span><span class="sxs-lookup"><span data-stu-id="61d81-214">Select **ASE** > **Settings** > **ILB Certificate**.</span></span>

2. <span data-ttu-id="61d81-215">tooset hello ILB certificaat Hallo certificate pfx-bestand selecteren en Hallo wachtwoord invoeren.</span><span class="sxs-lookup"><span data-stu-id="61d81-215">tooset hello ILB certificate, select hello certificate .pfx file and enter hello password.</span></span> <span data-ttu-id="61d81-216">Deze stap duurt enkele tooprocess tijd.</span><span class="sxs-lookup"><span data-stu-id="61d81-216">This step takes some time tooprocess.</span></span> <span data-ttu-id="61d81-217">Er verschijnt een bericht dat een uploadbewerking uitgevoerd wordt.</span><span class="sxs-lookup"><span data-stu-id="61d81-217">A message appears stating that an upload operation is in progress.</span></span>

3. <span data-ttu-id="61d81-218">Hallo ILB adres ophalen voor uw as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="61d81-218">Get hello ILB address for your ASE.</span></span> <span data-ttu-id="61d81-219">Selecteer **as-omgeving** > **eigenschappen** > **virtueel IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="61d81-219">Select **ASE** > **Properties** > **Virtual IP Address**.</span></span>

4. <span data-ttu-id="61d81-220">Een web-app maken in uw as-omgeving nadat Hallo as-omgeving is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="61d81-220">Create a web app in your ASE after hello ASE is created.</span></span>

5. <span data-ttu-id="61d81-221">Een virtuele machine maken als u niet in dit VNet hebt.</span><span class="sxs-lookup"><span data-stu-id="61d81-221">Create a VM if you don't have one in that VNet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="61d81-222">Probeer niet toocreate deze virtuele machine in hetzelfde subnet Hallo zoals Hallo as-omgeving, omdat deze wordt niet uitgevoerd of problemen veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="61d81-222">Don't try toocreate this VM in hello same subnet as hello ASE because it will fail or cause problems.</span></span>
    >
    >

6. <span data-ttu-id="61d81-223">Hallo DNS voor uw domein as-omgeving instellen.</span><span class="sxs-lookup"><span data-stu-id="61d81-223">Set hello DNS for your ASE domain.</span></span> <span data-ttu-id="61d81-224">U kunt een jokerteken gebruiken met uw domein in uw DNS.</span><span class="sxs-lookup"><span data-stu-id="61d81-224">You can use a wildcard with your domain in your DNS.</span></span> <span data-ttu-id="61d81-225">toodo enkele eenvoudige tests, Hallo hosts-bestand op uw VM tooset Hallo web app name toohello VIP IP-adres bewerken:</span><span class="sxs-lookup"><span data-stu-id="61d81-225">toodo some simple tests, edit hello hosts file on your VM tooset hello web app name toohello VIP IP address:</span></span>

    <span data-ttu-id="61d81-226">a.</span><span class="sxs-lookup"><span data-stu-id="61d81-226">a.</span></span> <span data-ttu-id="61d81-227">Als uw as-omgeving Hallo domeinnaam heeft _. ilbase.com_ en maken van Hallo web-app met de naam _mytestapp_, het gericht op _mytestapp.ilbase.com_. Vervolgens stelt u _mytestapp.ilbase.com_ tooresolve toohello ILB adres.</span><span class="sxs-lookup"><span data-stu-id="61d81-227">If your ASE has hello domain name _.ilbase.com_ and you create hello web app named _mytestapp_, it's addressed at _mytestapp.ilbase.com_. You then set _mytestapp.ilbase.com_ tooresolve toohello ILB address.</span></span> <span data-ttu-id="61d81-228">(Op Windows hello hostbestand loopt _C:\Windows\System32\drivers\etc\_.)</span><span class="sxs-lookup"><span data-stu-id="61d81-228">(On Windows, hello hosts file is at _C:\Windows\System32\drivers\etc\_.)</span></span>

    <span data-ttu-id="61d81-229">b.</span><span class="sxs-lookup"><span data-stu-id="61d81-229">b.</span></span> <span data-ttu-id="61d81-230">tootest web deployment publishing of toegang toohello, geavanceerde console, maakt u een record voor _mytestapp.scm.ilbase.com_.</span><span class="sxs-lookup"><span data-stu-id="61d81-230">tootest web deployment publishing or access toohello advanced console, create a record for _mytestapp.scm.ilbase.com_.</span></span>

7. <span data-ttu-id="61d81-231">Een browser gebruiken die op deze virtuele machine en Ga naar http://mytestapp.ilbase.com. (Of de naam van uw web-app met uw domein is toowhatever gaat.)</span><span class="sxs-lookup"><span data-stu-id="61d81-231">Use a browser on that VM and go to http://mytestapp.ilbase.com. (Or go toowhatever your web app name is with your domain.)</span></span>

8. <span data-ttu-id="61d81-232">Een browser gebruiken die op deze virtuele machine en Ga naar https://mytestapp.ilbase.com. Als u een zelfondertekend certificaat gebruikt, accepteert u Hallo gebrek aan beveiliging.</span><span class="sxs-lookup"><span data-stu-id="61d81-232">Use a browser on that VM and go to https://mytestapp.ilbase.com. If you use a self-signed certificate, accept hello lack of security.</span></span>

    <span data-ttu-id="61d81-233">Hallo IP-adres voor de ILB wordt vermeld onder **IP-adressen**.</span><span class="sxs-lookup"><span data-stu-id="61d81-233">hello IP address for your ILB is listed under **IP addresses**.</span></span> <span data-ttu-id="61d81-234">Deze lijst heeft ook Hallo IP-adressen die door externe VIP Hallo en voor binnenkomende beheer van verkeer.</span><span class="sxs-lookup"><span data-stu-id="61d81-234">This list also has hello IP addresses used by hello external VIP and for inbound management traffic.</span></span>

    ![ILB IP-adres][5]

### <a name="web-jobs-functions-and-hello-ilb-ase"></a><span data-ttu-id="61d81-236">Web-taken, functies en Hallo ILB as-omgeving</span><span class="sxs-lookup"><span data-stu-id="61d81-236">Web jobs, Functions and hello ILB ASE</span></span>

<span data-ttu-id="61d81-237">Zowel functies en webtaken worden ondersteund op een as ILB-omgeving, maar voor Hallo portal toowork met hen, moet u toegang toohello SCM netwerksite hebben.</span><span class="sxs-lookup"><span data-stu-id="61d81-237">Both Functions and web jobs are supported on an ILB ASE but for hello portal toowork with them, you must have network access toohello SCM site.</span></span>  <span data-ttu-id="61d81-238">Dit betekent dat de browser moet op een host die zich in of toohello virtueel netwerk is verbonden.</span><span class="sxs-lookup"><span data-stu-id="61d81-238">This means your browser must either be on a host that is either in or connected toohello virtual network.</span></span>  

<span data-ttu-id="61d81-239">Als u Azure Functions op een as ILB-omgeving gebruikt, krijgt u mogelijk een foutbericht weergegeven waarin wordt gemeld 'We kunnen niet kunnen tooretrieve momenteel door uw functies.</span><span class="sxs-lookup"><span data-stu-id="61d81-239">When you use Azure Functions on an ILB ASE, you might get an error message that says "We are not able tooretrieve your functions right now.</span></span> <span data-ttu-id="61d81-240">Probeer het later opnieuw."</span><span class="sxs-lookup"><span data-stu-id="61d81-240">Please try again later."</span></span> <span data-ttu-id="61d81-241">Deze fout treedt op omdat Hallo functies UI maakt gebruik van Hallo SCM site via HTTPS en het Hallo-basiscertificaat niet in Hallo browser vertrouwensketen wordt.</span><span class="sxs-lookup"><span data-stu-id="61d81-241">This error occurs because hello Functions UI leverages hello SCM site over HTTPS and hello root certificate is not in hello browser chain of trust.</span></span> <span data-ttu-id="61d81-242">Webtaken heeft een soortgelijk probleem.</span><span class="sxs-lookup"><span data-stu-id="61d81-242">Web jobs has a similar problem.</span></span> <span data-ttu-id="61d81-243">tooavoid dit probleem kunt u een van de volgende Hallo doen:</span><span class="sxs-lookup"><span data-stu-id="61d81-243">tooavoid this problem you can do one of hello following:</span></span>

- <span data-ttu-id="61d81-244">Hallo certificaat tooyour vertrouwde certificaatarchief toevoegen.</span><span class="sxs-lookup"><span data-stu-id="61d81-244">Add hello certificate tooyour trusted certificate store.</span></span> <span data-ttu-id="61d81-245">Dit blokkering opgeheven rand en Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="61d81-245">This unblocks Edge and Internet Explorer.</span></span>
- <span data-ttu-id="61d81-246">Chrome gebruiken en ga toohello SCM eerst, niet-vertrouwd certificaat Hallo accepteren en gaat u toohello-portal.</span><span class="sxs-lookup"><span data-stu-id="61d81-246">Use Chrome and go toohello SCM site first, accept hello untrusted certificate and then go toohello portal.</span></span>
- <span data-ttu-id="61d81-247">Een commerciële certificaat in uw browser vertrouwensketen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="61d81-247">Use a commercial certificate that is in your browser chain of trust.</span></span>  <span data-ttu-id="61d81-248">Dit is de beste optie Hallo.</span><span class="sxs-lookup"><span data-stu-id="61d81-248">This is hello best option.</span></span>  

## <a name="dns-configuration"></a><span data-ttu-id="61d81-249">DNS-configuratie</span><span class="sxs-lookup"><span data-stu-id="61d81-249">DNS configuration</span></span> ##

<span data-ttu-id="61d81-250">Wanneer u een externe VIP gebruikt, wordt door Azure DNS Hallo beheerd.</span><span class="sxs-lookup"><span data-stu-id="61d81-250">When you use an External VIP, hello DNS is managed by Azure.</span></span> <span data-ttu-id="61d81-251">Elke app gemaakt in uw as-omgeving automatisch toegevoegd tooAzure DNS, dit is een openbare DNS-server.</span><span class="sxs-lookup"><span data-stu-id="61d81-251">Any app created in your ASE is automatically added tooAzure DNS, which is a public DNS.</span></span> <span data-ttu-id="61d81-252">In een ILB as-omgeving, moet u uw eigen DNS beheren.</span><span class="sxs-lookup"><span data-stu-id="61d81-252">In an ILB ASE, you must manage your own DNS.</span></span> <span data-ttu-id="61d81-253">Voor een bepaald domein, zoals _contoso.net_, moet u toocreate DNS A-records in DNS dat punt tooyour ILB-adres voor:</span><span class="sxs-lookup"><span data-stu-id="61d81-253">For a given domain such as _contoso.net_, you need toocreate DNS A records in your DNS that point tooyour ILB address for:</span></span>

- <span data-ttu-id="61d81-254">*. contoso.net</span><span class="sxs-lookup"><span data-stu-id="61d81-254">*.contoso.net</span></span>
- <span data-ttu-id="61d81-255">*. scm.contoso.net</span><span class="sxs-lookup"><span data-stu-id="61d81-255">*.scm.contoso.net</span></span>

<span data-ttu-id="61d81-256">Als uw domein ILB as-omgeving wordt gebruikt voor meerdere dingen buiten deze as-omgeving, moet u mogelijk toomanage DNS op basis van de per-app-naam.</span><span class="sxs-lookup"><span data-stu-id="61d81-256">If your ILB ASE domain is used for multiple things outside this ASE, you might need toomanage DNS on a per-app-name basis.</span></span> <span data-ttu-id="61d81-257">Deze methode is lastig omdat u nodig tooadd elke nieuwe appnaam in uw DNS hebt wanneer u deze maakt.</span><span class="sxs-lookup"><span data-stu-id="61d81-257">This method is challenging because you need tooadd each new app name into your DNS when you create it.</span></span> <span data-ttu-id="61d81-258">Daarom is het raadzaam dat u een speciale domein.</span><span class="sxs-lookup"><span data-stu-id="61d81-258">For this reason, we recommend that you use a dedicated domain.</span></span>

## <a name="publish-with-an-ilb-ase"></a><span data-ttu-id="61d81-259">Publiceren met een ILB-as-omgeving</span><span class="sxs-lookup"><span data-stu-id="61d81-259">Publish with an ILB ASE</span></span> ##

<span data-ttu-id="61d81-260">Voor elke app die gemaakt, zijn er twee eindpunten.</span><span class="sxs-lookup"><span data-stu-id="61d81-260">For every app that's created, there are two endpoints.</span></span> <span data-ttu-id="61d81-261">In een ILB as-omgeving, hebt u  *&lt;app-naam >.&lt; ILB as-omgeving Domain >* en  *&lt;app-naam > .scm.&lt; ILB as-omgeving Domain >*.</span><span class="sxs-lookup"><span data-stu-id="61d81-261">In an ILB ASE, you have *&lt;app name>.&lt;ILB ASE Domain>* and *&lt;app name>.scm.&lt;ILB ASE Domain>*.</span></span> 

<span data-ttu-id="61d81-262">Hallo SCM-sitenaam gaat u verder toohello Kudu-console, aangeroepen Hallo **geavanceerde portal**in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="61d81-262">hello SCM site name takes you toohello Kudu console, called hello **Advanced portal**, within hello Azure portal.</span></span> <span data-ttu-id="61d81-263">Hallo Kudu-console kunt u omgevingsvariabelen weergeven, Hallo schijf verkennen, gebruikt u een console, en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="61d81-263">hello Kudu console lets you view environment variables, explore hello disk, use a console, and much more.</span></span> <span data-ttu-id="61d81-264">Zie voor meer informatie [Kudu-console voor Azure App Service][Kudu].</span><span class="sxs-lookup"><span data-stu-id="61d81-264">For more information, see [Kudu console for Azure App Service][Kudu].</span></span> 

<span data-ttu-id="61d81-265">Er is eenmalige aanmelding tussen hello Azure-portal en Hallo Kudu-console in Hallo multitenant-App Service en in een externe as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="61d81-265">In hello multitenant App Service and in an External ASE, there's single sign-on between hello Azure portal and hello Kudu console.</span></span> <span data-ttu-id="61d81-266">Voor Hallo ILB as-omgeving, maar moet u toouse uw publishing referenties toosign in Hallo Kudu-console.</span><span class="sxs-lookup"><span data-stu-id="61d81-266">For hello ILB ASE, however, you need toouse your publishing credentials toosign into hello Kudu console.</span></span>

<span data-ttu-id="61d81-267">Internetgebaseerde CI systemen, zoals GitHub en Visual Studio Team Services, werkt niet met een ILB-as-omgeving omdat publishing Hallo-eindpunt niet toegankelijk internet.</span><span class="sxs-lookup"><span data-stu-id="61d81-267">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because hello publishing endpoint isn't internet accessible.</span></span> <span data-ttu-id="61d81-268">In plaats daarvan moet u een CI-besturingssysteem dat gebruikmaakt van een pull-model, zoals Dropbox toouse.</span><span class="sxs-lookup"><span data-stu-id="61d81-268">Instead, you need toouse a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="61d81-269">Hallo publishing eindpunten voor apps in een ILB-as-omgeving gebruik Hallo domein dat Hallo die ILB as-omgeving is gemaakt met.</span><span class="sxs-lookup"><span data-stu-id="61d81-269">hello publishing endpoints for apps in an ILB ASE use hello domain that hello ILB ASE was created with.</span></span> <span data-ttu-id="61d81-270">Dit domein wordt weergegeven in het publicatieprofiel Hallo-app en op de portalblade van Hallo app (**overzicht** > **Essentials** en ook **eigenschappen**).</span><span class="sxs-lookup"><span data-stu-id="61d81-270">This domain appears in hello app's publishing profile and in hello app's portal blade (**Overview** > **Essentials** and also **Properties**).</span></span> <span data-ttu-id="61d81-271">Als u een ILB-as-omgeving met Hallo subdomein hebt *contoso.net* en een app met de naam *mytest*, gebruik *mytest.contoso.net* voor FTP en *mytest.scm.contoso.net*  voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="61d81-271">If you have an ILB ASE with hello subdomain *contoso.net* and an app named *mytest*, use *mytest.contoso.net* for FTP and *mytest.scm.contoso.net* for web deployment.</span></span>

## <a name="couple-an-ilb-ase-with-a-waf-device"></a><span data-ttu-id="61d81-272">Combineer een ILB-as-omgeving met een WAF-apparaat</span><span class="sxs-lookup"><span data-stu-id="61d81-272">Couple an ILB ASE with a WAF device</span></span> ##

<span data-ttu-id="61d81-273">Azure App Service biedt veel beveiligingsfuncties die Hallo systeem te beschermen.</span><span class="sxs-lookup"><span data-stu-id="61d81-273">Azure App Service provides many security measures that protect hello system.</span></span> <span data-ttu-id="61d81-274">Ze helpen ook toodetermine of een app gehackte is.</span><span class="sxs-lookup"><span data-stu-id="61d81-274">They also help toodetermine whether an app was hacked.</span></span> <span data-ttu-id="61d81-275">Hallo beste beveiliging voor een webtoepassing is toocouple een host-platform, zoals Azure App Service met een web application firewall (WAF).</span><span class="sxs-lookup"><span data-stu-id="61d81-275">hello best protection for a web application is toocouple a hosting platform, such as Azure App Service, with a web application firewall (WAF).</span></span> <span data-ttu-id="61d81-276">Omdat Hallo ILB as-omgeving een toepassingseindpunt netwerk geïsoleerd van heeft, is het geschikt is voor dit gebruik.</span><span class="sxs-lookup"><span data-stu-id="61d81-276">Because hello ILB ASE has a network-isolated application endpoint, it's appropriate for such a use.</span></span>

<span data-ttu-id="61d81-277">meer informatie over hoe tooconfigure uw as ILB-omgeving met een apparaat WAF zien toolearn [web application firewall configureren met uw App-serviceomgeving][ASEWAF].</span><span class="sxs-lookup"><span data-stu-id="61d81-277">toolearn more about how tooconfigure your ILB ASE with a WAF device, see [Configure a web application firewall with your App Service environment][ASEWAF].</span></span> <span data-ttu-id="61d81-278">Dit artikel laat zien hoe toouse een virtueel apparaat Barracuda met uw as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="61d81-278">This article shows how toouse a Barracuda virtual appliance with your ASE.</span></span> <span data-ttu-id="61d81-279">Een andere optie is toouse Azure Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="61d81-279">Another option is toouse Azure Application Gateway.</span></span> <span data-ttu-id="61d81-280">Toepassingsgateway maakt gebruik van Hallo OWASP core regels toosecure toepassingen erachter geplaatst.</span><span class="sxs-lookup"><span data-stu-id="61d81-280">Application Gateway uses hello OWASP core rules toosecure any applications placed behind it.</span></span> <span data-ttu-id="61d81-281">Zie voor meer informatie over Application Gateway [inleiding toohello Azure-web application firewall][AppGW].</span><span class="sxs-lookup"><span data-stu-id="61d81-281">For more information about Application Gateway, see [Introduction toohello Azure web application firewall][AppGW].</span></span>

## <a name="get-started"></a><span data-ttu-id="61d81-282">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="61d81-282">Get started</span></span> ##

<span data-ttu-id="61d81-283">Alle artikelen en hoe-tooinstructions voor ASEs zijn beschikbaar in de [Leesmij-bestand voor App Service-omgevingen][ASEReadme].</span><span class="sxs-lookup"><span data-stu-id="61d81-283">All articles and how-tooinstructions for ASEs are available in the [README for App Service environments][ASEReadme].</span></span>

* <span data-ttu-id="61d81-284">tooget gestart met ASEs, Zie [inleiding tooApp Service-omgevingen][Intro].</span><span class="sxs-lookup"><span data-stu-id="61d81-284">tooget started with ASEs, see [Introduction tooApp Service environments][Intro].</span></span>
* <span data-ttu-id="61d81-285">Zie voor meer informatie over hello Azure App Service-platform, [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span><span class="sxs-lookup"><span data-stu-id="61d81-285">For more information about hello Azure App Service platform, see [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span></span>
 
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
