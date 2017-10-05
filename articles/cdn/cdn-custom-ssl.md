---
title: HTTPS op een aangepaste Azure CDN-domein inschakelen | Microsoft Docs
description: Informatie over het inschakelen van HTTPS voor uw Azure CDN-eindpunt met een aangepast domein.
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
ms.openlocfilehash: b334ba6bbec1d0a7e23a514174bffae01c7fff05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="d31b8-103">HTTPS op een aangepast domein van Azure CDN inschakelen</span><span class="sxs-lookup"><span data-stu-id="d31b8-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="d31b8-104">HTTPS-ondersteuning voor aangepaste domeinen Azure CDN kunt u beveiligde inhoud met SSL-beveiliging met behulp van uw eigen domeinnaam voor het verbeteren van de beveiliging van gegevens die onderweg leveren.</span><span class="sxs-lookup"><span data-stu-id="d31b8-104">HTTPS support for Azure CDN custom domains enables you to deliver secure content via SSL using your own domain name to improve the security of data while in transit.</span></span> <span data-ttu-id="d31b8-105">De end-to-end werkstroom HTTPS inschakelen voor uw aangepaste domein wordt vereenvoudigd, via één klik inschakelen, Certificaatbeheer voltooid en alle met zonder extra kosten.</span><span class="sxs-lookup"><span data-stu-id="d31b8-105">The end-to-end workflow to enable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="d31b8-106">Het is essentieel om te controleren of de privacy en integriteit van gegevens van al uw web-toepassingen gevoelige gegevens die onderweg.</span><span class="sxs-lookup"><span data-stu-id="d31b8-106">It's critical to ensure the privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="d31b8-107">Met behulp van het HTTPS-protocol, zorgt u ervoor dat uw vertrouwelijke gegevens worden versleuteld wanneer ze via internet worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="d31b8-107">Using the HTTPS protocol ensures that your sensitive data is encrypted when it is sent across the internet.</span></span> <span data-ttu-id="d31b8-108">Het biedt vertrouwt, verificatie en uw webtoepassingen worden beschermd tegen aanvallen.</span><span class="sxs-lookup"><span data-stu-id="d31b8-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="d31b8-109">Op dit moment ondersteunt Azure CDN HTTPS op een CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="d31b8-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="d31b8-110">Als u een CDN-eindpunt vanaf Azure CDN (bijvoorbeeld https://contoso.azureedge.net) maakt, wordt HTTPS bijvoorbeeld standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d31b8-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="d31b8-111">Nu met het aangepaste domein HTTPS kunt u beveiligde levering voor een aangepast domein (bijvoorbeeld https://www.contoso.com) ook.</span><span class="sxs-lookup"><span data-stu-id="d31b8-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="d31b8-112">Enkele van de belangrijkste kenmerken van HTTPS-functie zijn:</span><span class="sxs-lookup"><span data-stu-id="d31b8-112">Some of the key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="d31b8-113">Kan zonder extra kosten: Er zijn geen kosten voor het verkrijgen van het certificaat of vernieuwen en zonder extra kosten voor HTTPS-verkeer.</span><span class="sxs-lookup"><span data-stu-id="d31b8-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="d31b8-114">U betaalt alleen uitgaande GB vanaf de CDN.</span><span class="sxs-lookup"><span data-stu-id="d31b8-114">You just pay for GB egress from the CDN.</span></span>

- <span data-ttu-id="d31b8-115">Eenvoudige activering: één klik inrichting is beschikbaar via de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d31b8-115">Simple enablement: One click provisioning is available from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d31b8-116">U kunt ook REST-API of andere ontwikkelhulpprogramma's gebruiken de functie in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="d31b8-116">You can also use REST API or other developer tools to enable the feature.</span></span>

- <span data-ttu-id="d31b8-117">Voltooien van Certificaatbeheer: alle aanschaf van het certificaat en u wordt beheerd.</span><span class="sxs-lookup"><span data-stu-id="d31b8-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="d31b8-118">Certificaten worden automatisch worden ingericht en vóór de vervaldatum worden vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="d31b8-118">Certificates are automatically provisioned and renewed prior to expiration.</span></span> <span data-ttu-id="d31b8-119">Hiermee verwijdert u volledig de risico's van de service wordt onderbroken als gevolg van een certificaat verloopt.</span><span class="sxs-lookup"><span data-stu-id="d31b8-119">This completely removes the risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="d31b8-120">Voordat het HTTPS-ondersteuning wordt ingeschakeld, u moet hebben al een [aangepaste Azure CDN-domein](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="d31b8-120">Prior to enabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-the-feature"></a><span data-ttu-id="d31b8-121">Stap 1: Het inschakelen van de functie</span><span class="sxs-lookup"><span data-stu-id="d31b8-121">Step 1: Enabling the feature</span></span> 

1. <span data-ttu-id="d31b8-122">In de [Azure-portal](https://portal.azure.com), blader naar uw Verizon standard of premium CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="d31b8-122">In the [Azure portal](https://portal.azure.com), browse to your Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="d31b8-123">Klik op het eindpunt met uw aangepaste domein in de lijst met eindpunten.</span><span class="sxs-lookup"><span data-stu-id="d31b8-123">In the list of endpoints, click the endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="d31b8-124">Klik op het aangepaste domein waarvoor u wilt inschakelen van HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d31b8-124">Click the custom domain for which you want to enable HTTPS.</span></span>

    ![De blade een eindpunt](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="d31b8-126">Klik op **op** HTTPS inschakelen en sla de wijziging op.</span><span class="sxs-lookup"><span data-stu-id="d31b8-126">Click **On** to enable HTTPS and save the change.</span></span>

    ![Dialoogvenster voor aangepaste HTTPS](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="d31b8-128">Stap 2: Validatie van domein</span><span class="sxs-lookup"><span data-stu-id="d31b8-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="d31b8-129">U moet domeinvalidatie voltooien voordat HTTPS actief op uw aangepaste domein zijn.</span><span class="sxs-lookup"><span data-stu-id="d31b8-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="d31b8-130">U hebt 6 werkdagen goedkeuren van het domein.</span><span class="sxs-lookup"><span data-stu-id="d31b8-130">You have 6 business days to approve the domain.</span></span> <span data-ttu-id="d31b8-131">Aanvraag worden met geen goedkeuring binnen 6 werkdagen geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="d31b8-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="d31b8-132">Nadat HTTPS op uw aangepaste domein is ingeschakeld, valideert onze certificaatprovider HTTPS DigiCert eigendom van uw domein Neem contact op met de registrant voor uw domein, op basis van WHOIS registrant informatie via e-mail (standaard) of telefoon.</span><span class="sxs-lookup"><span data-stu-id="d31b8-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting the registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="d31b8-133">DigiCert ontvangt ook de e-verificatie aan de onderstaande adressen.</span><span class="sxs-lookup"><span data-stu-id="d31b8-133">DigiCert will also send the verification email to the below addresses.</span></span> <span data-ttu-id="d31b8-134">Als WHOIS registrant informatie persoonlijke, zorg er dan voor dat u rechtstreeks vanuit een van deze adressen kan goedkeuren.</span><span class="sxs-lookup"><span data-stu-id="d31b8-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="d31b8-135">beheerder @ beheerder < uw-domain-name.com > @< uw-domain-name.com ></span><span class="sxs-lookup"><span data-stu-id="d31b8-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="d31b8-136">webbeheerder @< uw-domain-name.com ></span><span class="sxs-lookup"><span data-stu-id="d31b8-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="d31b8-137">hostmaster @< uw-domain-name.com ></span><span class="sxs-lookup"><span data-stu-id="d31b8-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="d31b8-138">postbeheerder @< uw-domain-name.com ></span><span class="sxs-lookup"><span data-stu-id="d31b8-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="d31b8-139">Bij ontvangst van het e-mailbericht, hebt u twee opties voor verificatie:</span><span class="sxs-lookup"><span data-stu-id="d31b8-139">Upon receiving the email, you have two verification options:</span></span>

1. <span data-ttu-id="d31b8-140">U kunt alle toekomstige orders geplaatst via dezelfde account voor het domein in dezelfde hoofdmap, bijvoorbeeld consoto.com goedkeuren.</span><span class="sxs-lookup"><span data-stu-id="d31b8-140">You can approve all future orders placed through the same account for the same root domain, e.g. consoto.com.</span></span> <span data-ttu-id="d31b8-141">Dit is een aanbevolen aanpak als u van plan bent extra aangepaste domeinen toevoegen in de toekomst voor het hoofddomein van dezelfde.</span><span class="sxs-lookup"><span data-stu-id="d31b8-141">This is a recommended approach if you are planning to add additional custom domains in the future for the same root domain.</span></span>
 
2. <span data-ttu-id="d31b8-142">U kunt alleen de specifieke host-naam die in deze aanvraag goedkeuren.</span><span class="sxs-lookup"><span data-stu-id="d31b8-142">You can just approve the specific host name used in this request.</span></span> <span data-ttu-id="d31b8-143">Aanvullende goedkeuring is vereist voor de volgende aanvragen.</span><span class="sxs-lookup"><span data-stu-id="d31b8-143">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="d31b8-144">Voorbeeld e-mailadres:</span><span class="sxs-lookup"><span data-stu-id="d31b8-144">Example email:</span></span>
    
    ![Dialoogvenster voor aangepaste HTTPS](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="d31b8-146">Na de goedkeuring, wordt de DigiCert uw aangepaste domeinnaam toevoegen aan de SAN-certificaat.</span><span class="sxs-lookup"><span data-stu-id="d31b8-146">After approval, DigiCert will add your custom domain name to the SAN certificate.</span></span> <span data-ttu-id="d31b8-147">Het certificaat wordt één jaar geldig zijn en wordt automatisch vernieuwd voordat deze is verlopen.</span><span class="sxs-lookup"><span data-stu-id="d31b8-147">The certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-the-propagation-then-start-using-your-feature"></a><span data-ttu-id="d31b8-148">Stap 3: Wacht totdat de doorgifte en start met behulp van de functie</span><span class="sxs-lookup"><span data-stu-id="d31b8-148">Step 3: Wait for the propagation then start using your feature</span></span>

<span data-ttu-id="d31b8-149">Het duurt maximaal 6-8 uur voor de functie aangepast domein HTTPS actief nadat de domeinnaam is gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="d31b8-149">After the domain name is validated it will take up to 6-8 hours for the custom domain HTTPS feature to be active.</span></span> <span data-ttu-id="d31b8-150">Nadat het proces voltooid is, wordt de status 'aangepaste HTTPS' in de Azure portal worden ingesteld op 'Enabled'.</span><span class="sxs-lookup"><span data-stu-id="d31b8-150">After the process is complete, the "custom HTTPS" status in the Azure portal will be set to "Enabled".</span></span> <span data-ttu-id="d31b8-151">HTTPS met uw aangepaste domein is nu gereed voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="d31b8-151">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="d31b8-152">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="d31b8-152">Frequently asked questions</span></span>

1. <span data-ttu-id="d31b8-153">*Wie is de certificaatprovider en type van het certificaat dat wordt gebruikt?*</span><span class="sxs-lookup"><span data-stu-id="d31b8-153">*Who is the certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="d31b8-154">We gebruiken namen met alternatieve onderwerp (SAN)-certificaat opgegeven door DigiCert.</span><span class="sxs-lookup"><span data-stu-id="d31b8-154">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="d31b8-155">Een SAN-certificaat kan meerdere FQDN-namen met één certificaat kunt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="d31b8-155">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="d31b8-156">*Kan ik mijn speciaal certificaatarchief gebruiken?*</span><span class="sxs-lookup"><span data-stu-id="d31b8-156">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="d31b8-157">Momenteel niet, maar het is in het overzicht.</span><span class="sxs-lookup"><span data-stu-id="d31b8-157">Not currently, but it's on the roadmap.</span></span>

3. <span data-ttu-id="d31b8-158">*Wat gebeurt er als ik ontvang geen bevestigingsmail van het domein van DigiCert?*</span><span class="sxs-lookup"><span data-stu-id="d31b8-158">*What if I don't receive the domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="d31b8-159">Neem contact op met Microsoft als u een e-mailbericht niet binnen 24 uur ontvangt.</span><span class="sxs-lookup"><span data-stu-id="d31b8-159">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="d31b8-160">*Maakt gebruik van een SAN-certificaat minder veilig dan een speciaal certificaatarchief?*</span><span class="sxs-lookup"><span data-stu-id="d31b8-160">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="d31b8-161">Een SAN-certificaat voldoet aan de dezelfde codering en beveiliging standaarden als een certificaat dat is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d31b8-161">A SAN cert follows the same encryption and security standards as a dedicated cert.</span></span> <span data-ttu-id="d31b8-162">Alle uitgegeven certificaten voor SSL gebruikt SHA-256 voor uitgebreide beveiliging.</span><span class="sxs-lookup"><span data-stu-id="d31b8-162">All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="d31b8-163">*Kan ik het aangepaste domein HTTPS gebruiken met Azure CDN van Akamai?*</span><span class="sxs-lookup"><span data-stu-id="d31b8-163">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="d31b8-164">Deze functie is momenteel alleen beschikbaar met Azure CDN van Verizon.</span><span class="sxs-lookup"><span data-stu-id="d31b8-164">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="d31b8-165">We werken aan deze functie met Azure CDN van Akamai ondersteunende in de komende maanden.</span><span class="sxs-lookup"><span data-stu-id="d31b8-165">We are working on supporting this feature with Azure CDN from Akamai in the coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d31b8-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d31b8-166">Next steps</span></span>

- <span data-ttu-id="d31b8-167">Meer informatie over het instellen van een [aangepast domein op uw Azure CDN-eindpunt](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="d31b8-167">Learn how to set up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


