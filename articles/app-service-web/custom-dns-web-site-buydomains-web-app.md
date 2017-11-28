---
title: aaaBuy een aangepaste domeinnaam voor Azure-Web-Apps
description: Meer informatie over hoe een aangepast domein toobuy naam met een web-app in Azure App Service.
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="f4083-103">Een aangepaste domeinnaam voor Azure-Web-Apps kopen</span><span class="sxs-lookup"><span data-stu-id="f4083-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="f4083-104">App Service-domeinen (preview) zijn op het hoogste niveau van de domeinen die worden beheerd rechtstreeks in Azure.</span><span class="sxs-lookup"><span data-stu-id="f4083-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="f4083-105">Ze kunnen aangepaste domeinen eenvoudig toomanage [Azure Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4083-105">They make it easy toomanage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="f4083-106">Deze zelfstudie leert u hoe namen tooAzure Web Apps toobuy een App Service-domein en DNS toewijzen.</span><span class="sxs-lookup"><span data-stu-id="f4083-106">This tutorial shows you how toobuy an App Service domain and assign DNS names tooAzure Web Apps.</span></span>

<span data-ttu-id="f4083-107">Dit artikel is voor Azure App Service (Web-Apps, API-Apps, Mobile Apps, Logic Apps).</span><span class="sxs-lookup"><span data-stu-id="f4083-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="f4083-108">Zie voor de virtuele machine in Azure of Azure Storage, [toewijzen App Service domein tooAzure VM of Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span><span class="sxs-lookup"><span data-stu-id="f4083-108">For Azure VM or Azure Storage, see [Assign App Service domain tooAzure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="f4083-109">Zie voor Cloud-Services, [configureren van een aangepaste domeinnaam voor een Azure cloudservice](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f4083-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4083-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f4083-110">Prerequisites</span></span>

<span data-ttu-id="f4083-111">toocomplete in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="f4083-111">toocomplete this tutorial:</span></span>

* <span data-ttu-id="f4083-112">[Een App Service-app maken](/azure/app-service/), of gebruik een app die u hebt gemaakt voor een andere zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f4083-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-hello-app"></a><span data-ttu-id="f4083-113">Hallo app voorbereiden</span><span class="sxs-lookup"><span data-stu-id="f4083-113">Prepare hello app</span></span>

<span data-ttu-id="f4083-114">aangepaste domeinen in Azure Web Apps, uw web-app van toouse [App Service-abonnement](https://azure.microsoft.com/pricing/details/app-service/) moet een betaald laag (**gedeelde**, **Basic**, **standaard**, of **Premium**).</span><span class="sxs-lookup"><span data-stu-id="f4083-114">toouse custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="f4083-115">In deze stap maakt ervoor u zorgen dat Hallo web-app wordt in Hallo ondersteund prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="f4083-115">In this step, you make sure that hello web app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="f4083-116">Meld u aan tooAzure</span><span class="sxs-lookup"><span data-stu-id="f4083-116">Sign in tooAzure</span></span>

<span data-ttu-id="f4083-117">Open Hallo [Azure-portal](https://portal.azure.com) en meld u aan met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="f4083-117">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="f4083-118">Navigeer in hello Azure-portal toohello app</span><span class="sxs-lookup"><span data-stu-id="f4083-118">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="f4083-119">Selecteer in het linkermenu Hallo **App Services**, en selecteer vervolgens de naam Hallo van Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="f4083-119">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="f4083-121">U ziet de pagina voor het beheren van App Service-app Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="f4083-121">You see hello management page of hello App Service app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="f4083-122">Hallo prijscategorie controleren</span><span class="sxs-lookup"><span data-stu-id="f4083-122">Check hello pricing tier</span></span>

<span data-ttu-id="f4083-123">Schuif in Hallo linkernavigatiebalk van de pagina app hello, toohello **instellingen** sectie en selecteer **opschalen (App Service-abonnement)**.</span><span class="sxs-lookup"><span data-stu-id="f4083-123">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Omhoog schalen-menu](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="f4083-125">de huidige tier Hallo-app wordt door een rand gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="f4083-125">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="f4083-126">Controleren of die Hallo-app niet Hallo toomake **vrije** laag.</span><span class="sxs-lookup"><span data-stu-id="f4083-126">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="f4083-127">Aangepaste DNS wordt niet ondersteund in Hallo **vrije** laag.</span><span class="sxs-lookup"><span data-stu-id="f4083-127">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Controleer de prijscategorie](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="f4083-129">Hallo App Service-abonnement is niet als **vrije**, sluit Hallo **Kies uw prijscategorie** pagina en te overslaan[kopen Hallo domein](#buy-the-domain).</span><span class="sxs-lookup"><span data-stu-id="f4083-129">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Buy hello domain](#buy-the-domain).</span></span>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="f4083-130">Hallo opschalen met App Service-abonnement</span><span class="sxs-lookup"><span data-stu-id="f4083-130">Scale up hello App Service plan</span></span>

<span data-ttu-id="f4083-131">Selecteer een van de Hallo-free lagen (**gedeelde**, **Basic**, **standaard**, of **Premium**).</span><span class="sxs-lookup"><span data-stu-id="f4083-131">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="f4083-132">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="f4083-132">Click **Select**.</span></span>

![Controleer de prijscategorie](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="f4083-134">Wanneer u de volgende kennisgeving Hallo ziet, is Hallo schaalbewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f4083-134">When you see hello following notification, hello scale operation is complete.</span></span>

![Schaal bewerking bevestigen](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a><span data-ttu-id="f4083-136">Hallo domein kopen</span><span class="sxs-lookup"><span data-stu-id="f4083-136">Buy hello domain</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="f4083-137">Meld u aan tooAzure</span><span class="sxs-lookup"><span data-stu-id="f4083-137">Sign in tooAzure</span></span>
<span data-ttu-id="f4083-138">Open Hallo [Azure-portal](https://portal.azure.com/) en meld u aan met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="f4083-138">Open hello [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="f4083-139">Kopen domeinen starten</span><span class="sxs-lookup"><span data-stu-id="f4083-139">Launch Buy domains</span></span>
<span data-ttu-id="f4083-140">In Hallo **Web-Apps** en klik op Hallo-naam van uw web-app, selecteer **instellingen**, en selecteer vervolgens **aangepaste domeinen**</span><span class="sxs-lookup"><span data-stu-id="f4083-140">In hello **Web Apps** tab, click hello name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="f4083-141">In Hallo **aangepaste domeinen** pagina, klikt u op **domeinen kopen**.</span><span class="sxs-lookup"><span data-stu-id="f4083-141">In hello **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a><span data-ttu-id="f4083-142">Hallo domein aankoop configureren</span><span class="sxs-lookup"><span data-stu-id="f4083-142">Configure hello domain purchase</span></span>

<span data-ttu-id="f4083-143">In Hallo **Service toepassingsdomein** pagina in Hallo **zoeken naar domein** vak, Hallo-domeinnaam voor het type gewenste toobuy en het type `Enter`.</span><span class="sxs-lookup"><span data-stu-id="f4083-143">In hello **App Service Domain** page, in hello **Search for domain** box, type hello domain name you want toobuy and type `Enter`.</span></span> <span data-ttu-id="f4083-144">Hallo worden voorgestelde beschikbare domeinen weergegeven onder het tekstvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="f4083-144">hello suggested available domains are shown just below hello text box.</span></span> <span data-ttu-id="f4083-145">Selecteer een of meer domeinen die u wilt dat toobuy.</span><span class="sxs-lookup"><span data-stu-id="f4083-145">Select one or more domains you want toobuy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="f4083-146">Klik op Hallo **contactgegevens** en van het domein Hallo contactgegevens formulier invullen.</span><span class="sxs-lookup"><span data-stu-id="f4083-146">Click hello **Contact Information** and fill out hello domain's contact information form.</span></span> <span data-ttu-id="f4083-147">Wanneer u klaar bent, klikt u op **OK** tooreturn toohello Service toepassingsdomein pagina.</span><span class="sxs-lookup"><span data-stu-id="f4083-147">When finished, click **OK** tooreturn toohello App Service Domain page.</span></span>
   
<span data-ttu-id="f4083-148">Het is belangrijk dat u alle vereiste velden met zo nauwkeurig mogelijk invullen.</span><span class="sxs-lookup"><span data-stu-id="f4083-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="f4083-149">Onjuiste gegevens voor de contactgegevens kan resulteren in fout toopurchase domeinen.</span><span class="sxs-lookup"><span data-stu-id="f4083-149">Incorrect data for contact information can result in failure toopurchase domains.</span></span> 

<span data-ttu-id="f4083-150">Selecteer vervolgens de gewenste Hallo opties voor uw domein.</span><span class="sxs-lookup"><span data-stu-id="f4083-150">Next, select hello desired options for your domain.</span></span> <span data-ttu-id="f4083-151">Zie Hallo tabel uitleg:</span><span class="sxs-lookup"><span data-stu-id="f4083-151">See hello following table for explanations:</span></span>

| <span data-ttu-id="f4083-152">Instelling</span><span class="sxs-lookup"><span data-stu-id="f4083-152">Setting</span></span> | <span data-ttu-id="f4083-153">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="f4083-153">Suggested Value</span></span> | <span data-ttu-id="f4083-154">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f4083-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="f4083-155">Automatisch vernieuwen</span><span class="sxs-lookup"><span data-stu-id="f4083-155">Auto renew</span></span> | <span data-ttu-id="f4083-156">**Inschakelen**</span><span class="sxs-lookup"><span data-stu-id="f4083-156">**Enable**</span></span> | <span data-ttu-id="f4083-157">Hiermee vernieuwt u uw App Service-domein automatisch elk jaar.</span><span class="sxs-lookup"><span data-stu-id="f4083-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="f4083-158">Uw creditcard in rekening gebracht dezelfde aankoopbedrag Hallo op Hallo moment van verlenging.</span><span class="sxs-lookup"><span data-stu-id="f4083-158">Your credit card is charged hello same purchase price at hello time of renewal.</span></span> |
|<span data-ttu-id="f4083-159">Privacybescherming</span><span class="sxs-lookup"><span data-stu-id="f4083-159">Privacy protection</span></span> | <span data-ttu-id="f4083-160">Inschakelen</span><span class="sxs-lookup"><span data-stu-id="f4083-160">Enable</span></span> | <span data-ttu-id="f4083-161">Opt-in te 'Privacy protection', dat van het aankoopbedrag Hallo uitmaakt deel _gratis_ (met uitzondering van het hoogste niveau domeinen die het register ondersteunen geen privacybescherming, zoals _. co.in_, _. CO.uk_, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="f4083-161">Opt in too"Privacy protection", which is included in hello purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="f4083-162">Standaard hostnamen toewijzen</span><span class="sxs-lookup"><span data-stu-id="f4083-162">Assign default hostnames</span></span> | <span data-ttu-id="f4083-163">**www** en**@**</span><span class="sxs-lookup"><span data-stu-id="f4083-163">**www** and **@**</span></span> | <span data-ttu-id="f4083-164">Selecteer Hallo gewenste hostnaambindings, indien gewenst.</span><span class="sxs-lookup"><span data-stu-id="f4083-164">Select hello desired hostname bindings, if desired.</span></span> <span data-ttu-id="f4083-165">Wanneer Hallo domein aankoop voltooid is, kan uw web-app op geselecteerde Hallo hostnamen worden benaderd.</span><span class="sxs-lookup"><span data-stu-id="f4083-165">When hello domain purchase operation is complete, your web app can be accessed at hello selected hostnames.</span></span> <span data-ttu-id="f4083-166">Als de web-app Hallo zich achter [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), er geen Hallo optie tooassign Hallo-hoofddomein (@), omdat het Traffic Manager biedt geen ondersteuning voor A-records.</span><span class="sxs-lookup"><span data-stu-id="f4083-166">If hello web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see hello option tooassign hello root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="f4083-167">U kunt wijzigingen aanbrengen toohello hostnaam toewijzingen nadat Hallo domein aankoop is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f4083-167">You can make changes toohello hostname assignments after hello domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="f4083-168">Voorwaarden accepteren en kopen</span><span class="sxs-lookup"><span data-stu-id="f4083-168">Accept terms and purchase</span></span>

<span data-ttu-id="f4083-169">Klik op **juridische voorwaarden** tooreview Hallo voorwaarden en Hallo kosten, klik vervolgens op **kopen**.</span><span class="sxs-lookup"><span data-stu-id="f4083-169">Click **Legal Terms** tooreview hello terms and hello charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="f4083-170">App Service-domeinen Azure DNS toohost Hallo domeinen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f4083-170">App Service Domains use Azure DNS toohost hello domains.</span></span> <span data-ttu-id="f4083-171">Daarnaast toohello domain registration kosten gebruikskosten voor Azure DNS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f4083-171">In addition toohello domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="f4083-172">Zie voor informatie [prijzen van Azure DNS-](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="f4083-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="f4083-173">Terug in Hallo **Service toepassingsdomein** pagina, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4083-173">Back in hello **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="f4083-174">Tijdens het Hallo-bewerking wordt uitgevoerd, ziet u Hallo meldingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f4083-174">While hello operation is in progress, you see hello following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="f4083-175">Hallo hostnamen testen</span><span class="sxs-lookup"><span data-stu-id="f4083-175">Test hello hostnames</span></span>

<span data-ttu-id="f4083-176">Als u de standaard hostnamen tooyour web-app hebt toegewezen, ziet u ook een melding geslaagd voor elke geselecteerde hostnaam.</span><span class="sxs-lookup"><span data-stu-id="f4083-176">If you have assigned default hostnames tooyour web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="f4083-177">U ziet ook Hallo geselecteerd hostnamen in Hallo **aangepaste domeinen** pagina in Hallo **hostnamen** sectie.</span><span class="sxs-lookup"><span data-stu-id="f4083-177">You also see hello selected hostnames in hello **Custom domains** page, in hello **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="f4083-178">tootest hello hostnamen, navigeer hostnamen toohello vermeld in de browser Hallo.</span><span class="sxs-lookup"><span data-stu-id="f4083-178">tootest hello hostnames, navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="f4083-179">Hallo-voorbeeld in Hallo voorgaande schermafbeelding probeert in too_kontoso.net_ navigeren en _www.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="f4083-179">In hello example in hello preceding screenshot, try navigating too_kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-tooweb-app"></a><span data-ttu-id="f4083-180">Hostnamen tooweb app toewijzen</span><span class="sxs-lookup"><span data-stu-id="f4083-180">Assign hostnames tooweb app</span></span>

<span data-ttu-id="f4083-181">Als u ervoor geen tooassign een kiest of meer standaard hostnamen tooyour web-app tijdens Hallo aankoopproces, of als u een hostnaam tooassign niet moet worden weergegeven, kunt u een hostnaam op elk gewenst moment kunt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="f4083-181">If you choose not tooassign one or more default hostnames tooyour web app during hello purchase process, or if you need tooassign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="f4083-182">U kunt andere web-app ook hostnamen in Hallo App Service-domein tooany.</span><span class="sxs-lookup"><span data-stu-id="f4083-182">You can also assign hostnames in hello App Service Domain tooany other web app.</span></span> <span data-ttu-id="f4083-183">Hallo stappen afhankelijk van of Hallo App Service-domein en Hallo web-app toohello behoren hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="f4083-183">hello steps depend on whether hello App Service Domain and hello web app belong toohello same subscription.</span></span>

- <span data-ttu-id="f4083-184">Ander abonnement: aangepaste DNS-records van App Service-domein toohello web-app als een extern gekochte domein Hallo toewijzen.</span><span class="sxs-lookup"><span data-stu-id="f4083-184">Different subscription: Map custom DNS records from hello App Service Domain toohello web app like an externally purchased domain.</span></span> <span data-ttu-id="f4083-185">Zie voor informatie over het toevoegen van aangepaste DNS tooan App Service-domein namen, [aangepaste DNS-records beheren](#custom).</span><span class="sxs-lookup"><span data-stu-id="f4083-185">For information on adding custom DNS names tooan App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="f4083-186">een externe gekochte domein tooa web-app toomap Zie [toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="f4083-186">toomap an external purchased domain tooa web app, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="f4083-187">Hetzelfde abonnement: gebruik Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="f4083-187">Same subscription: Use hello following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="f4083-188">Start de hostnaam toevoegen</span><span class="sxs-lookup"><span data-stu-id="f4083-188">Launch add hostname</span></span>
<span data-ttu-id="f4083-189">In Hallo **App Services** pagina, selecteer Hallo-naam van uw web-app die u wilt dat tooassign hostnamen te selecteren **instellingen**, en selecteer vervolgens **aangepaste domeinen**.</span><span class="sxs-lookup"><span data-stu-id="f4083-189">In hello **App Services** page, select hello name of your web app that you want tooassign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="f4083-190">Controleer of uw aangeschafte domein wordt vermeld in Hallo **Service AppDomains** sectie, maar niet selecteren.</span><span class="sxs-lookup"><span data-stu-id="f4083-190">Make sure that your purchased domain is listed in hello **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="f4083-191">Alle App Service-domeinen in hetzelfde abonnement worden weergegeven in Hallo van web-app Hallo **aangepaste domeinen** pagina.</span><span class="sxs-lookup"><span data-stu-id="f4083-191">All App Service Domains in hello same subscription are shown in hello web app's **Custom domains** page.</span></span> <span data-ttu-id="f4083-192">Als uw domein in het abonnement Hallo van web-app, maar u deze niet in Hallo van web-app ziet **aangepaste domeinen** pagina, opnieuw Hallo **aangepaste domeinen** of Hallo webpagina Vernieuw deze pagina.</span><span class="sxs-lookup"><span data-stu-id="f4083-192">If your domain is in hello web app's subscription, but you cannot see it in hello web app's **Custom domains** page, try reopening hello **Custom domains** page or refresh hello webpage.</span></span> <span data-ttu-id="f4083-193">Controleer ook Hallo melding Bel bovenaan Hallo hello Azure-portal voor fouten in de voortgang of maken.</span><span class="sxs-lookup"><span data-stu-id="f4083-193">Also, check hello notification bell at hello top of hello Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="f4083-194">Selecteer **hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f4083-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="f4083-195">Hostname configureren</span><span class="sxs-lookup"><span data-stu-id="f4083-195">Configure hostname</span></span>
<span data-ttu-id="f4083-196">In Hallo **hostnaam toevoegen** dialoogvenster, type Hallo volledig gekwalificeerde domeinnaam van uw App Service-domein of elk subdomein.</span><span class="sxs-lookup"><span data-stu-id="f4083-196">In hello **Add hostname** dialog, type hello fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="f4083-197">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f4083-197">For example:</span></span>

- <span data-ttu-id="f4083-198">kontoso.NET</span><span class="sxs-lookup"><span data-stu-id="f4083-198">kontoso.net</span></span>
- <span data-ttu-id="f4083-199">www.kontoso.NET</span><span class="sxs-lookup"><span data-stu-id="f4083-199">www.kontoso.net</span></span>
- <span data-ttu-id="f4083-200">ABC.kontoso.NET</span><span class="sxs-lookup"><span data-stu-id="f4083-200">abc.kontoso.net</span></span>

<span data-ttu-id="f4083-201">Wanneer u klaar bent, selecteert u **valideren**.</span><span class="sxs-lookup"><span data-stu-id="f4083-201">When finished, select **Validate**.</span></span> <span data-ttu-id="f4083-202">Hallo hostnaam recordtype wordt automatisch geselecteerd voor u.</span><span class="sxs-lookup"><span data-stu-id="f4083-202">hello hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="f4083-203">Selecteer **hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f4083-203">Select **Add hostname**.</span></span>

<span data-ttu-id="f4083-204">Als het Hallo-bewerking is voltooid, ziet u een melding geslaagd voor Hallo hostnaam toegewezen.</span><span class="sxs-lookup"><span data-stu-id="f4083-204">When hello operation is complete, you see a success notification for hello assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="f4083-205">Sluit de hostnaam toevoegen</span><span class="sxs-lookup"><span data-stu-id="f4083-205">Close add hostname</span></span>
<span data-ttu-id="f4083-206">In Hallo **hostnaam toevoegen** pagina, een andere hostnaam tooyour web-app, desgewenst toewijzen.</span><span class="sxs-lookup"><span data-stu-id="f4083-206">In hello **Add hostname** page, assign any other hostname tooyour web app, as desired.</span></span> <span data-ttu-id="f4083-207">Wanneer u klaar bent, sluit u Hallo **hostnaam toevoegen** pagina.</span><span class="sxs-lookup"><span data-stu-id="f4083-207">When finished, close hello **Add hostname** page.</span></span>

<span data-ttu-id="f4083-208">U ziet nu Hallo zojuist toegewezen hostname(s) in uw app **aangepaste domeinen** pagina.</span><span class="sxs-lookup"><span data-stu-id="f4083-208">You should now see hello newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="f4083-209">Hallo hostnamen testen</span><span class="sxs-lookup"><span data-stu-id="f4083-209">Test hello hostnames</span></span>

<span data-ttu-id="f4083-210">Navigeer hostnamen toohello vermeld in de browser Hallo.</span><span class="sxs-lookup"><span data-stu-id="f4083-210">Navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="f4083-211">Probeer too_abc.kontoso.net_ navigeren in voorbeeld Hallo in Hallo voorgaande schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="f4083-211">In hello example in hello preceding screenshot, try navigating too_abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="f4083-212">Aangepaste DNS-records beheren</span><span class="sxs-lookup"><span data-stu-id="f4083-212">Manage custom DNS records</span></span>

<span data-ttu-id="f4083-213">In Azure, DNS-records voor een App-domein worden beheerd met [Azure DNS](https://azure.microsoft.com/services/dns/).</span><span class="sxs-lookup"><span data-stu-id="f4083-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="f4083-214">U kunt toevoegen, verwijderen, en DNS-records bijwerken, net als voor een extern gekochte domein.</span><span class="sxs-lookup"><span data-stu-id="f4083-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="f4083-215">Open-App Service-domein</span><span class="sxs-lookup"><span data-stu-id="f4083-215">Open App Service Domain</span></span>

<span data-ttu-id="f4083-216">Selecteer in de Azure-portal in het linkermenu hello, Hallo **meer Services** > **Service AppDomains**.</span><span class="sxs-lookup"><span data-stu-id="f4083-216">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="f4083-217">Selecteer Hallo domein toomanage.</span><span class="sxs-lookup"><span data-stu-id="f4083-217">Select hello domain toomanage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="f4083-218">Toegang tot DNS-zone</span><span class="sxs-lookup"><span data-stu-id="f4083-218">Access DNS zone</span></span>

<span data-ttu-id="f4083-219">Selecteer in het linkermenu Hallo-domein, **DNS-zone**.</span><span class="sxs-lookup"><span data-stu-id="f4083-219">In hello domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="f4083-220">Hiermee Hallo [DNS-zone](../dns/dns-zones-records.md) pagina van uw App Service-domein in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f4083-220">This action opens hello [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="f4083-221">Voor meer informatie over tooedit DNS-records, Zie [hoe toomanage DNS-Zones in Azure-portal Hallo](../dns/dns-operations-dnszones-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f4083-221">For information on how tooedit DNS records, see [How toomanage DNS Zones in hello Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="f4083-222">(Domein verwijderen) aankoop annuleren</span><span class="sxs-lookup"><span data-stu-id="f4083-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="f4083-223">Als u Hallo toepassingsdomein Service koopt, hebt u vijf dagen toocancel uw aankoop voor een volledige terugbetaling.</span><span class="sxs-lookup"><span data-stu-id="f4083-223">After you purchase hello App Service Domain, you have five days toocancel your purchase for a full refund.</span></span> <span data-ttu-id="f4083-224">Na vijf dagen Hallo App Service-domein kunt verwijderen, maar kan geen restitutie ontvangen.</span><span class="sxs-lookup"><span data-stu-id="f4083-224">After five days, you can delete hello App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="f4083-225">Open-App Service-domein</span><span class="sxs-lookup"><span data-stu-id="f4083-225">Open App Service Domain</span></span>

<span data-ttu-id="f4083-226">Selecteer in de Azure-portal in het linkermenu hello, Hallo **meer Services** > **Service AppDomains**.</span><span class="sxs-lookup"><span data-stu-id="f4083-226">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="f4083-227">Hallo domein tooyou wilt toocancel selecteren of te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f4083-227">Select hello domain tooyou want toocancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="f4083-228">Hostnaambindings verwijderen</span><span class="sxs-lookup"><span data-stu-id="f4083-228">Delete hostname bindings</span></span>

<span data-ttu-id="f4083-229">Selecteer in het linkermenu Hallo-domein, **hostnaambindings**.</span><span class="sxs-lookup"><span data-stu-id="f4083-229">In hello domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="f4083-230">hostnaambindings Hallo van alle Azure-services worden hier weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f4083-230">hello hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="f4083-231">U kunt Hallo App Service-domein niet verwijderen nadat alle hostnaambindings zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f4083-231">You cannot delete hello App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="f4083-232">De binding voor elke hostnaam verwijderen door het selecteren van **...**   >  **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="f4083-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="f4083-233">Nadat alle Hallo-bindingen zijn verwijderd, selecteert u **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f4083-233">After all hello bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="f4083-234">Annuleren of verwijderen</span><span class="sxs-lookup"><span data-stu-id="f4083-234">Cancel or delete</span></span>

<span data-ttu-id="f4083-235">Selecteer in het linkermenu Hallo-domein, **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="f4083-235">In hello domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="f4083-236">Als Hallo annulering periode op Hallo aangeschaft domein niet is verstreken, selecteert u **aankoop annuleren**.</span><span class="sxs-lookup"><span data-stu-id="f4083-236">If hello cancellation period on hello purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="f4083-237">Anders ziet u een **verwijderen** knop in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="f4083-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="f4083-238">toodelete hello domein zonder een restitutie, selecteer **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="f4083-238">toodelete hello domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="f4083-239">Selecteer **OK** tooconfirm Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="f4083-239">Select **OK** tooconfirm hello operation.</span></span> <span data-ttu-id="f4083-240">Als u niet dat tooproceed wilt, klikt u buiten Hallo bevestigingsvenster.</span><span class="sxs-lookup"><span data-stu-id="f4083-240">If you don't want tooproceed, click anywhere outside of hello confirmation dialog.</span></span>

<span data-ttu-id="f4083-241">Nadat het Hallo-bewerking is voltooid, Hallo domein is vrijgegeven voor uw abonnement en beschikbaar zijn voor iedereen toopurchase opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f4083-241">After hello operation is complete, hello domain is released from your subscription and available for anyone toopurchase again.</span></span> 
