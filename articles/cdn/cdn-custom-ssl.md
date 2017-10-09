---
title: aaa "HTTPS op een aangepaste Azure CDN-domein inschakelen | Microsoft Docs'
description: Meer informatie over hoe tooenable HTTPS op uw Azure CDN-eindpunt met een aangepast domein.
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="1686d-103">HTTPS op een aangepast domein van Azure CDN inschakelen</span><span class="sxs-lookup"><span data-stu-id="1686d-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="1686d-104">HTTPS-ondersteuning voor Azure CDN aangepaste domeinen kan toodeliver beveiligde inhoud met behulp van uw eigen domein naam tooimprove Hallo beveiliging van gegevens die onderweg SSL-beveiliging.</span><span class="sxs-lookup"><span data-stu-id="1686d-104">HTTPS support for Azure CDN custom domains enables you toodeliver secure content via SSL using your own domain name tooimprove hello security of data while in transit.</span></span> <span data-ttu-id="1686d-105">Hallo end-to-end werkstroom tooenable HTTPS voor uw aangepaste domein wordt vereenvoudigd, via één klik inschakelen, complete certificaatbeheer en alle met zonder extra kosten.</span><span class="sxs-lookup"><span data-stu-id="1686d-105">hello end-to-end workflow tooenable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="1686d-106">Kritieke tooensure Hallo privacy en integriteit van gegevens van al uw web-toepassingen gevoelige gegevens die onderweg is.</span><span class="sxs-lookup"><span data-stu-id="1686d-106">It's critical tooensure hello privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="1686d-107">Met behulp van HTTPS-protocol zorgt ervoor dat uw vertrouwelijke gegevens worden versleuteld wanneer deze wordt verzonden via Hallo Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="1686d-107">Using hello HTTPS protocol ensures that your sensitive data is encrypted when it is sent across hello internet.</span></span> <span data-ttu-id="1686d-108">Het biedt vertrouwt, verificatie en uw webtoepassingen worden beschermd tegen aanvallen.</span><span class="sxs-lookup"><span data-stu-id="1686d-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="1686d-109">Op dit moment ondersteunt Azure CDN HTTPS op een CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="1686d-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="1686d-110">Als u een CDN-eindpunt vanaf Azure CDN (bijvoorbeeld https://contoso.azureedge.net) maakt, wordt HTTPS bijvoorbeeld standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1686d-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="1686d-111">Nu met het aangepaste domein HTTPS kunt u beveiligde levering voor een aangepast domein (bijvoorbeeld https://www.contoso.com) ook.</span><span class="sxs-lookup"><span data-stu-id="1686d-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="1686d-112">Enkele belangrijke kenmerken van de functie HTTPS Hallo zijn:</span><span class="sxs-lookup"><span data-stu-id="1686d-112">Some of hello key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="1686d-113">Kan zonder extra kosten: Er zijn geen kosten voor het verkrijgen van het certificaat of vernieuwen en zonder extra kosten voor HTTPS-verkeer.</span><span class="sxs-lookup"><span data-stu-id="1686d-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="1686d-114">U betaalt alleen voor uitgaande van Hallo CDN GB.</span><span class="sxs-lookup"><span data-stu-id="1686d-114">You just pay for GB egress from hello CDN.</span></span>

- <span data-ttu-id="1686d-115">Eenvoudige activering: één klik inrichting is beschikbaar via Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1686d-115">Simple enablement: One click provisioning is available from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1686d-116">U kunt ook de REST-API of andere onderdeel developer tools tooenable hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1686d-116">You can also use REST API or other developer tools tooenable hello feature.</span></span>

- <span data-ttu-id="1686d-117">Voltooien van Certificaatbeheer: alle aanschaf van het certificaat en u wordt beheerd.</span><span class="sxs-lookup"><span data-stu-id="1686d-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="1686d-118">Certificaten automatisch worden ingericht en eerdere tooexpiration vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="1686d-118">Certificates are automatically provisioned and renewed prior tooexpiration.</span></span> <span data-ttu-id="1686d-119">Hiermee verwijdert u volledig Hallo risico's van de service wordt onderbroken als gevolg van een certificaat verloopt.</span><span class="sxs-lookup"><span data-stu-id="1686d-119">This completely removes hello risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="1686d-120">Eerdere tooenabling HTTPS ondersteunen, u moet al hebt vastgesteld een [aangepaste Azure CDN-domein](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="1686d-120">Prior tooenabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-hello-feature"></a><span data-ttu-id="1686d-121">Stap 1: Het inschakelen van Hallo-functie</span><span class="sxs-lookup"><span data-stu-id="1686d-121">Step 1: Enabling hello feature</span></span> 

1. <span data-ttu-id="1686d-122">In Hallo [Azure-portal](https://portal.azure.com), bladeren tooyour Verizon standard of premium CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="1686d-122">In hello [Azure portal](https://portal.azure.com), browse tooyour Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="1686d-123">Klik op Hallo-eindpunt met uw aangepaste domein in Hallo lijst met eindpunten.</span><span class="sxs-lookup"><span data-stu-id="1686d-123">In hello list of endpoints, click hello endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="1686d-124">Klik op Hallo aangepast domein waarvoor u tooenable HTTPS wilt.</span><span class="sxs-lookup"><span data-stu-id="1686d-124">Click hello custom domain for which you want tooenable HTTPS.</span></span>

    ![De blade een eindpunt](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="1686d-126">Klik op **op** tooenable HTTPS en Hallo wijziging op te slaan.</span><span class="sxs-lookup"><span data-stu-id="1686d-126">Click **On** tooenable HTTPS and save hello change.</span></span>

    ![Dialoogvenster voor aangepaste HTTPS](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="1686d-128">Stap 2: Validatie van domein</span><span class="sxs-lookup"><span data-stu-id="1686d-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="1686d-129">U moet domeinvalidatie voltooien voordat HTTPS actief op uw aangepaste domein zijn.</span><span class="sxs-lookup"><span data-stu-id="1686d-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="1686d-130">U hebt 6 business dagen tooapprove Hallo-domein.</span><span class="sxs-lookup"><span data-stu-id="1686d-130">You have 6 business days tooapprove hello domain.</span></span> <span data-ttu-id="1686d-131">Aanvraag worden met geen goedkeuring binnen 6 werkdagen geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="1686d-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="1686d-132">Nadat HTTPS op uw aangepaste domein is ingeschakeld, valideert onze certificaatprovider HTTPS DigiCert eigendom van uw domein contact opnemen met de Hallo registrant voor uw domein, op basis van WHOIS registrant informatie via e-mail (standaard) of telefoon.</span><span class="sxs-lookup"><span data-stu-id="1686d-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting hello registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="1686d-133">DigiCert verzonden hello verificatie e toohello hieronder adressen ook.</span><span class="sxs-lookup"><span data-stu-id="1686d-133">DigiCert will also send hello verification email toohello below addresses.</span></span> <span data-ttu-id="1686d-134">Als WHOIS registrant informatie persoonlijke, zorg er dan voor dat u rechtstreeks vanuit een van deze adressen kan goedkeuren.</span><span class="sxs-lookup"><span data-stu-id="1686d-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="1686d-135">beheerder @ beheerder < uw-domain-name.com > @< uw-domain-name.com ></span><span class="sxs-lookup"><span data-stu-id="1686d-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="1686d-136">webbeheerder @< uw-domain-name.com ></span><span class="sxs-lookup"><span data-stu-id="1686d-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="1686d-137">hostmaster @< uw-domain-name.com ></span><span class="sxs-lookup"><span data-stu-id="1686d-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="1686d-138">postbeheerder @< uw-domain-name.com ></span><span class="sxs-lookup"><span data-stu-id="1686d-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="1686d-139">Bij ontvangst Hallo e-mail, hebt u twee opties voor verificatie:</span><span class="sxs-lookup"><span data-stu-id="1686d-139">Upon receiving hello email, you have two verification options:</span></span>

1. <span data-ttu-id="1686d-140">U kunt alle toekomstige orders geplaatst via Hallo dezelfde account voor Hallo goedkeuren dezelfde hoofddomein, bijvoorbeeld consoto.com. Dit is een aanbevolen benadering als u van plan bent tooadd aanvullende aangepaste domeinen in toekomstige voor Hallo Hallo dezelfde hoofddomein.</span><span class="sxs-lookup"><span data-stu-id="1686d-140">You can approve all future orders placed through hello same account for hello same root domain, e.g. consoto.com. This is a recommended approach if you are planning tooadd additional custom domains in hello future for hello same root domain.</span></span>
 
2. <span data-ttu-id="1686d-141">U kunt alleen Hallo specifieke hostnaam die wordt gebruikt in deze aanvraag goedkeuren.</span><span class="sxs-lookup"><span data-stu-id="1686d-141">You can just approve hello specific host name used in this request.</span></span> <span data-ttu-id="1686d-142">Aanvullende goedkeuring is vereist voor de volgende aanvragen.</span><span class="sxs-lookup"><span data-stu-id="1686d-142">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="1686d-143">Voorbeeld e-mailadres:</span><span class="sxs-lookup"><span data-stu-id="1686d-143">Example email:</span></span>
    
    ![Dialoogvenster voor aangepaste HTTPS](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="1686d-145">Na goedkeuring, wordt DigiCert uw aangepaste domein naam toohello SAN-certificaat toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1686d-145">After approval, DigiCert will add your custom domain name toohello SAN certificate.</span></span> <span data-ttu-id="1686d-146">Hallo-certificaat wordt één jaar geldig zijn en wordt automatisch vernieuwd voordat deze is verlopen.</span><span class="sxs-lookup"><span data-stu-id="1686d-146">hello certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a><span data-ttu-id="1686d-147">Stap 3: Wachten op Hallo doorgeven en start met behulp van de functie</span><span class="sxs-lookup"><span data-stu-id="1686d-147">Step 3: Wait for hello propagation then start using your feature</span></span>

<span data-ttu-id="1686d-148">Nadat de domeinnaam Hallo is gevalideerd wordt het Hallo aangepast domein HTTPS functie toobe active too6 8 uur duren.</span><span class="sxs-lookup"><span data-stu-id="1686d-148">After hello domain name is validated it will take up too6-8 hours for hello custom domain HTTPS feature toobe active.</span></span> <span data-ttu-id="1686d-149">Nadat het Hallo-proces is voltooid, wordt Hallo 'aangepaste HTTPS'-status in hello Azure-portal te 'Enabled' worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1686d-149">After hello process is complete, hello "custom HTTPS" status in hello Azure portal will be set too"Enabled".</span></span> <span data-ttu-id="1686d-150">HTTPS met uw aangepaste domein is nu gereed voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="1686d-150">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="1686d-151">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="1686d-151">Frequently asked questions</span></span>

1. <span data-ttu-id="1686d-152">*Wie is Hallo certificaatprovider en type van het certificaat dat wordt gebruikt?*</span><span class="sxs-lookup"><span data-stu-id="1686d-152">*Who is hello certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="1686d-153">We gebruiken namen met alternatieve onderwerp (SAN)-certificaat opgegeven door DigiCert.</span><span class="sxs-lookup"><span data-stu-id="1686d-153">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="1686d-154">Een SAN-certificaat kan meerdere FQDN-namen met één certificaat kunt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="1686d-154">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="1686d-155">*Kan ik mijn speciaal certificaatarchief gebruiken?*</span><span class="sxs-lookup"><span data-stu-id="1686d-155">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="1686d-156">Momenteel niet, maar de op Hallo roadmap.</span><span class="sxs-lookup"><span data-stu-id="1686d-156">Not currently, but it's on hello roadmap.</span></span>

3. <span data-ttu-id="1686d-157">*Wat gebeurt er als ik ontvang geen Hallo domein bevestigingsmail van DigiCert?*</span><span class="sxs-lookup"><span data-stu-id="1686d-157">*What if I don't receive hello domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="1686d-158">Neem contact op met Microsoft als u een e-mailbericht niet binnen 24 uur ontvangt.</span><span class="sxs-lookup"><span data-stu-id="1686d-158">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="1686d-159">*Maakt gebruik van een SAN-certificaat minder veilig dan een speciaal certificaatarchief?*</span><span class="sxs-lookup"><span data-stu-id="1686d-159">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="1686d-160">Een SAN-certificaat volgt Hallo dezelfde codering en beveiliging normen als een certificaat dat is toegewezen. Alle uitgegeven certificaten voor SSL gebruikt SHA-256 voor uitgebreide beveiliging.</span><span class="sxs-lookup"><span data-stu-id="1686d-160">A SAN cert follows hello same encryption and security standards as a dedicated cert. All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="1686d-161">*Kan ik het aangepaste domein HTTPS gebruiken met Azure CDN van Akamai?*</span><span class="sxs-lookup"><span data-stu-id="1686d-161">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="1686d-162">Deze functie is momenteel alleen beschikbaar met Azure CDN van Verizon.</span><span class="sxs-lookup"><span data-stu-id="1686d-162">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="1686d-163">We werken aan deze functie met Azure CDN van Akamai ondersteunende in de komende maanden Hallo.</span><span class="sxs-lookup"><span data-stu-id="1686d-163">We are working on supporting this feature with Azure CDN from Akamai in hello coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1686d-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1686d-164">Next steps</span></span>

- <span data-ttu-id="1686d-165">Meer informatie over hoe tooset van een [aangepast domein op uw Azure CDN-eindpunt](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="1686d-165">Learn how tooset up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


