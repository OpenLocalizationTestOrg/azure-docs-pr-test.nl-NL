---
title: 'Logic Apps B2B lijst met fouten en oplossingen: Azure App Service | Microsoft Docs'
description: Logic Apps B2B lijst met fouten en oplossingen
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 0340e2979f1972ba631354e206c93969e55946e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="9a5ff-103">Logic Apps B2B lijst met fouten en oplossingen</span><span class="sxs-lookup"><span data-stu-id="9a5ff-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="9a5ff-104">In dit artikel helpt u bij het oplossen van fouten die mogelijk in Logic Apps B2B-scenario's en stelt de nodige acties voor het oplossen van deze fouten.</span><span class="sxs-lookup"><span data-stu-id="9a5ff-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="9a5ff-105">Omzetting van de overeenkomst</span><span class="sxs-lookup"><span data-stu-id="9a5ff-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="9a5ff-106">* Geen overeenkomst gevonden</span><span class="sxs-lookup"><span data-stu-id="9a5ff-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="9a5ff-107">Foutbeschrijving</span><span class="sxs-lookup"><span data-stu-id="9a5ff-107">Error description</span></span> | <span data-ttu-id="9a5ff-108">Er is geen overeenkomst gevonden met de overeenkomst resolutie Parameters</span><span class="sxs-lookup"><span data-stu-id="9a5ff-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="9a5ff-109">Gebruikersactie</span><span class="sxs-lookup"><span data-stu-id="9a5ff-109">User action</span></span> | <span data-ttu-id="9a5ff-110">Hallo overeenkomst moet worden toegevoegd als toohello integratie account met overeengekomen business identiteiten.</span><span class="sxs-lookup"><span data-stu-id="9a5ff-110">hello agreement should be added toohello integration account with agreed business identities.</span></span></br> <span data-ttu-id="9a5ff-111">Hallo business identiteiten moeten overeenkomen met toohello invoerbericht-id 's</span><span class="sxs-lookup"><span data-stu-id="9a5ff-111">hello business identities should match toohello input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="9a5ff-112">* Geen overeenkomst gevonden met identiteiten</span><span class="sxs-lookup"><span data-stu-id="9a5ff-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="9a5ff-113">Foutbeschrijving</span><span class="sxs-lookup"><span data-stu-id="9a5ff-113">Error description</span></span> | <span data-ttu-id="9a5ff-114">Er is geen overeenkomst gevonden met identiteiten: 'AS2Identity':: 'Partner1' en 'AS2Identity':: 'Partner3'</span><span class="sxs-lookup"><span data-stu-id="9a5ff-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="9a5ff-115">Gebruikersactie</span><span class="sxs-lookup"><span data-stu-id="9a5ff-115">User action</span></span> | <span data-ttu-id="9a5ff-116">Ongeldige AS2-uit of AS2-tooconfigured voor overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="9a5ff-116">Invalid AS2-From or AS2-tooconfigured for agreement.</span></span> </br> <span data-ttu-id="9a5ff-117">Juiste AS2 bericht AS2-uit of AS2-tooheaders of overeenkomst toomatch AS2-id's in AS2 bericht headers met de configuraties van de overeenkomst</span><span class="sxs-lookup"><span data-stu-id="9a5ff-117">Correct AS2 message AS2-From or AS2-tooheaders or agreement toomatch AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="9a5ff-118">AS2</span><span class="sxs-lookup"><span data-stu-id="9a5ff-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="9a5ff-119">* AS2 berichtkoppen ontbreekt</span><span class="sxs-lookup"><span data-stu-id="9a5ff-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="9a5ff-120">Foutbeschrijving</span><span class="sxs-lookup"><span data-stu-id="9a5ff-120">Error description</span></span>| <span data-ttu-id="9a5ff-121">Ongeldige AS2-headers.</span><span class="sxs-lookup"><span data-stu-id="9a5ff-121">Invalid AS2 headers.</span></span> <span data-ttu-id="9a5ff-122">Een van de ' AS2-aan ' of ' AS2-van ' headers zijn leeg</span><span class="sxs-lookup"><span data-stu-id="9a5ff-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="9a5ff-123">Gebruikersactie</span><span class="sxs-lookup"><span data-stu-id="9a5ff-123">User action</span></span> | <span data-ttu-id="9a5ff-124">Een AS2-bericht is ontvangen die geen Hallo AS2 bevat-uit of AS2-tooor beide headers.</span><span class="sxs-lookup"><span data-stu-id="9a5ff-124">An AS2 message was received that did not contain hello AS2-From or AS2-tooor both headers.</span></span> </br> <span data-ttu-id="9a5ff-125">Controleer AS2 bericht AS2-vanaf en AS2-tooheaders en corrigeer deze op basis van overeenkomst configuratie</span><span class="sxs-lookup"><span data-stu-id="9a5ff-125">Check AS2 message AS2-From and AS2-tooheaders and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="9a5ff-126">* Ontbrekende AS2 berichttekst en -koppen</span><span class="sxs-lookup"><span data-stu-id="9a5ff-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="9a5ff-127">Foutbeschrijving</span><span class="sxs-lookup"><span data-stu-id="9a5ff-127">Error description</span></span>| <span data-ttu-id="9a5ff-128">Hallo aanvraaginhoud is null of leeg</span><span class="sxs-lookup"><span data-stu-id="9a5ff-128">hello request content is null or empty</span></span> | 
| <span data-ttu-id="9a5ff-129">Gebruikersactie</span><span class="sxs-lookup"><span data-stu-id="9a5ff-129">User action</span></span> | <span data-ttu-id="9a5ff-130">Een AS2-bericht is ontvangen die geen berichttekst Hallo bevat</span><span class="sxs-lookup"><span data-stu-id="9a5ff-130">An AS2 message was received that did not contain hello message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="9a5ff-131">* Ontsleutelingsfout AS2-bericht</span><span class="sxs-lookup"><span data-stu-id="9a5ff-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="9a5ff-132">Foutbeschrijving</span><span class="sxs-lookup"><span data-stu-id="9a5ff-132">Error description</span></span> |  <span data-ttu-id="9a5ff-133">[verwerkt/fout: ontsleuteling is mislukt]</span><span class="sxs-lookup"><span data-stu-id="9a5ff-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="9a5ff-134">Gebruikersactie</span><span class="sxs-lookup"><span data-stu-id="9a5ff-134">User action</span></span> | <span data-ttu-id="9a5ff-135">Voeg @base64ToBinary tooAS2Message voordat toopartner worden verzonden</span><span class="sxs-lookup"><span data-stu-id="9a5ff-135">Add @base64ToBinary tooAS2Message before sending toopartner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="9a5ff-136">* MDN ontsleutelingsfout</span><span class="sxs-lookup"><span data-stu-id="9a5ff-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="9a5ff-137">Foutbeschrijving</span><span class="sxs-lookup"><span data-stu-id="9a5ff-137">Error description</span></span> |  <span data-ttu-id="9a5ff-138">[verwerkt/fout: ontsleuteling is mislukt]</span><span class="sxs-lookup"><span data-stu-id="9a5ff-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="9a5ff-139">Gebruikersactie</span><span class="sxs-lookup"><span data-stu-id="9a5ff-139">User action</span></span> | <span data-ttu-id="9a5ff-140">Voeg @base64ToBinary tooMDN voordat toopartner worden verzonden</span><span class="sxs-lookup"><span data-stu-id="9a5ff-140">Add @base64ToBinary tooMDN before sending toopartner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="9a5ff-141">* Handtekeningcertificaat ontbreekt</span><span class="sxs-lookup"><span data-stu-id="9a5ff-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="9a5ff-142">Foutbeschrijving</span><span class="sxs-lookup"><span data-stu-id="9a5ff-142">Error description</span></span>| <span data-ttu-id="9a5ff-143">Hallo is certificaat voor ondertekening niet geconfigureerd voor AS2 partij.</span><span class="sxs-lookup"><span data-stu-id="9a5ff-143">hello Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="9a5ff-144">AS2-vanaf: partner1 AS2-te: partner2</span><span class="sxs-lookup"><span data-stu-id="9a5ff-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="9a5ff-145">Gebruikersactie</span><span class="sxs-lookup"><span data-stu-id="9a5ff-145">User action</span></span> | <span data-ttu-id="9a5ff-146">AS2-overeenkomst instellingen configureren met het juiste certificaat voor handtekening</span><span class="sxs-lookup"><span data-stu-id="9a5ff-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="9a5ff-147">X12 en EDIFACT</span><span class="sxs-lookup"><span data-stu-id="9a5ff-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="9a5ff-148">* Voorloop- of een afsluitende spatie gevonden</span><span class="sxs-lookup"><span data-stu-id="9a5ff-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="9a5ff-149">Foutbeschrijving</span><span class="sxs-lookup"><span data-stu-id="9a5ff-149">Error description</span></span> | <span data-ttu-id="9a5ff-150">Fout opgetreden tijdens het parseren.</span><span class="sxs-lookup"><span data-stu-id="9a5ff-150">Error encountered during parsing.</span></span> <span data-ttu-id="9a5ff-151">Edifact-transactie ingesteld met de id ' 123456 'opgenomen in de DIF (zonder groep) met id ' 987654' Hallo, met afzender-id 'Partner1', 'Partner2'-id van de ontvanger is onderbroken met de volgende fouten: voorloopspaties afsluitende scheidingsteken gevonden</span><span class="sxs-lookup"><span data-stu-id="9a5ff-151">hello Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="9a5ff-152">Gebruikersactie</span><span class="sxs-lookup"><span data-stu-id="9a5ff-152">User action</span></span> | <span data-ttu-id="9a5ff-153">Hallo overeenkomst instellingen toobe geconfigureerd tooallow voorloopspaties en afsluitende spatie.</span><span class="sxs-lookup"><span data-stu-id="9a5ff-153">hello agreement settings toobe configured tooallow leading and trailing space.</span></span> </br> <span data-ttu-id="9a5ff-154">Overeenkomst instellingen tooallow voorloopspaties en afsluitende spatie bewerken</span><span class="sxs-lookup"><span data-stu-id="9a5ff-154">Edit agreement settings tooallow leading and trailing space</span></span> |
|   |   |

![ruimte](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a><span data-ttu-id="9a5ff-156">* Dubbele selectievakje is ingeschakeld in Hallo overeenkomst</span><span class="sxs-lookup"><span data-stu-id="9a5ff-156">* Duplicate check has enabled in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="9a5ff-157">Foutbeschrijving</span><span class="sxs-lookup"><span data-stu-id="9a5ff-157">Error description</span></span> | <span data-ttu-id="9a5ff-158">Dubbele controle-aantal</span><span class="sxs-lookup"><span data-stu-id="9a5ff-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="9a5ff-159">Gebruikersactie</span><span class="sxs-lookup"><span data-stu-id="9a5ff-159">User action</span></span> | <span data-ttu-id="9a5ff-160">Deze fout geeft aan ontvangen Hallo-bericht heeft dubbele besturingselement cijfers.</span><span class="sxs-lookup"><span data-stu-id="9a5ff-160">This error indicates hello received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="9a5ff-161">Corrigeer Hallo besturingselementnummer en het Hallo-bericht te verzenden</span><span class="sxs-lookup"><span data-stu-id="9a5ff-161">Correct hello control number and resend hello message</span></span> |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a><span data-ttu-id="9a5ff-162">* Ontbrekende schema in Hallo overeenkomst</span><span class="sxs-lookup"><span data-stu-id="9a5ff-162">* Missing schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="9a5ff-163">Foutbeschrijving</span><span class="sxs-lookup"><span data-stu-id="9a5ff-163">Error description</span></span> | <span data-ttu-id="9a5ff-164">Fout opgetreden tijdens het parseren.</span><span class="sxs-lookup"><span data-stu-id="9a5ff-164">Error encountered during parsing.</span></span> <span data-ttu-id="9a5ff-165">Hallo X12 transactie set met id '564220001' opgenomen in functionele groep met id '56422', in het knooppunt met id '000056422' met afzender-id ' 12345678', ' 87654321-id van de ontvanger' wordt onderbroken met de volgende fouten 'Hallo-bericht heeft een onbekende document ty PE en tooany Hallo bestaande schema's geconfigureerd in de overeenkomst Hallo wordt niet omgezet '</span><span class="sxs-lookup"><span data-stu-id="9a5ff-165">hello X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement"</span></span> |
| <span data-ttu-id="9a5ff-166">Gebruikersactie</span><span class="sxs-lookup"><span data-stu-id="9a5ff-166">User action</span></span> | <span data-ttu-id="9a5ff-167">Schema in Hallo overeenkomst instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="9a5ff-167">Configure schema in hello agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a><span data-ttu-id="9a5ff-168">* Onjuist schema in Hallo overeenkomst</span><span class="sxs-lookup"><span data-stu-id="9a5ff-168">* Incorrect schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="9a5ff-169">Foutbeschrijving</span><span class="sxs-lookup"><span data-stu-id="9a5ff-169">Error description</span></span> | <span data-ttu-id="9a5ff-170">Hallo-bericht heeft een onbekend documenttype en tooany Hallo bestaande schema's geconfigureerd in de overeenkomst Hallo niet is opgelost.</span><span class="sxs-lookup"><span data-stu-id="9a5ff-170">hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement.</span></span> |
| <span data-ttu-id="9a5ff-171">Gebruikersactie</span><span class="sxs-lookup"><span data-stu-id="9a5ff-171">User action</span></span> | <span data-ttu-id="9a5ff-172">Juiste schema in Hallo overeenkomst instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="9a5ff-172">Configure correct schema in hello agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="9a5ff-173">Plat bestand</span><span class="sxs-lookup"><span data-stu-id="9a5ff-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="9a5ff-174">* Invoerbericht bij geen instantie</span><span class="sxs-lookup"><span data-stu-id="9a5ff-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="9a5ff-175">Foutbeschrijving</span><span class="sxs-lookup"><span data-stu-id="9a5ff-175">Error description</span></span> | <span data-ttu-id="9a5ff-176">InvalidTemplate.</span><span class="sxs-lookup"><span data-stu-id="9a5ff-176">InvalidTemplate.</span></span> <span data-ttu-id="9a5ff-177">Kan geen tooprocess sjabloontaalexpressies in de invoer van de actie 'Flat_File_Decoding' op regel '1' en kolom '1902': ' eigenschap 'inhoud' verwacht een waarde maar kreeg null vereist.</span><span class="sxs-lookup"><span data-stu-id="9a5ff-177">Unable tooprocess template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="9a5ff-178">Pad '.'.</span><span class="sxs-lookup"><span data-stu-id="9a5ff-178">Path ''.'.</span></span> |
| <span data-ttu-id="9a5ff-179">Gebruikersactie</span><span class="sxs-lookup"><span data-stu-id="9a5ff-179">User action</span></span> | <span data-ttu-id="9a5ff-180">Deze fout geeft aan dat invoer het Hallo-bericht bevat geen hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="9a5ff-180">This error indicates hello input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="9a5ff-181">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="9a5ff-181">Learn more</span></span>
[<span data-ttu-id="9a5ff-182">Meer informatie over Enterprise Integration Pack Hallo</span><span class="sxs-lookup"><span data-stu-id="9a5ff-182">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
