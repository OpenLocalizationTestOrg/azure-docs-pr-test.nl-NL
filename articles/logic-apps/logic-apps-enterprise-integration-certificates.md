---
title: certificaten met Enterprise Integration Pack aaaUsing | Microsoft Docs
description: Meer informatie over hoe toouse certificaten Hello Enterprise Integration Pack | Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="de478-103">Meer informatie over certificaten en het Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="de478-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="de478-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="de478-104">Overview</span></span>
<span data-ttu-id="de478-105">Enterprise integration maakt gebruik van certificaten toosecure B2B-communicatie.</span><span class="sxs-lookup"><span data-stu-id="de478-105">Enterprise integration uses certificates toosecure B2B communications.</span></span> <span data-ttu-id="de478-106">U kunt twee typen certificaten gebruiken in uw onderneming integratie-apps:</span><span class="sxs-lookup"><span data-stu-id="de478-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="de478-107">Openbare certificaten, moeten worden aangeschaft van een certificeringsinstantie (CA).</span><span class="sxs-lookup"><span data-stu-id="de478-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="de478-108">Persoonlijke certificaten, kunt u zelf uitgeven.</span><span class="sxs-lookup"><span data-stu-id="de478-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="de478-109">Deze certificaten zijn soms waarnaar wordt verwezen tooas zelfondertekende certificaten.</span><span class="sxs-lookup"><span data-stu-id="de478-109">These certificates are sometimes referred tooas self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="de478-110">Wat zijn certificaten?</span><span class="sxs-lookup"><span data-stu-id="de478-110">What are certificates?</span></span>
<span data-ttu-id="de478-111">Certificaten worden digitale documenten die Hallo identiteit van de deelnemers Hallo in elektronische communicatie verifiëren en die ook elektronische communicatie beveiligen.</span><span class="sxs-lookup"><span data-stu-id="de478-111">Certificates are digital documents that verify hello identity of hello participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="de478-112">Waarom certificaten gebruiken?</span><span class="sxs-lookup"><span data-stu-id="de478-112">Why use certificates?</span></span>
<span data-ttu-id="de478-113">Soms moet B2B-communicatie vertrouwelijk worden behandeld.</span><span class="sxs-lookup"><span data-stu-id="de478-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="de478-114">Enterprise integration maakt gebruik van certificaten toosecure deze communicatie op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="de478-114">Enterprise integration uses certificates toosecure these communications in two ways:</span></span>

* <span data-ttu-id="de478-115">Door het Hallo-inhoud van berichten versleutelen</span><span class="sxs-lookup"><span data-stu-id="de478-115">By encrypting hello contents of messages</span></span>
* <span data-ttu-id="de478-116">Door berichten digitaal te ondertekenen</span><span class="sxs-lookup"><span data-stu-id="de478-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="de478-117">Een openbaar certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="de478-117">Upload a public certificate</span></span>

<span data-ttu-id="de478-118">toouse een *openbaar certificaat* in logic apps met B2B-mogelijkheden, moet u eerst tooupload Hallo certificaat bij uw account integratie.</span><span class="sxs-lookup"><span data-stu-id="de478-118">toouse a *public certificate* in your logic apps with B2B capabilities, you first need tooupload hello certificate into your integration account.</span></span>  

<span data-ttu-id="de478-119">Nadat u een certificaat hebt geüpload, is beschikbaar toohelp beveiligen van uw B2B-berichten bij het definiëren van de eigenschappen in Hallo [overeenkomsten](logic-apps-enterprise-integration-agreements.md) die u maakt.</span><span class="sxs-lookup"><span data-stu-id="de478-119">After you upload a certificate, it's available toohelp you secure your B2B messages when you define their properties in hello [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="de478-120">Hier volgen gedetailleerde stappen voor het uploaden van uw certificaten voor openbare toegang tot je account integratie nadat u zich aanmeldt toohello Azure-portal Hallo:</span><span class="sxs-lookup"><span data-stu-id="de478-120">Here are hello detailed steps for uploading your public certificates into your integration account after you sign in toohello Azure portal:</span></span>

1. <span data-ttu-id="de478-121">Selecteer **meer services** en voer **integratie** in zoekvak Hallo-filter.</span><span class="sxs-lookup"><span data-stu-id="de478-121">Select **More services** and enter **integration** in hello filter search box.</span></span> <span data-ttu-id="de478-122">Selecteer **Integratieaccounts** uit de lijst met resultaten Hallo</span><span class="sxs-lookup"><span data-stu-id="de478-122">Select **Integration Accounts** from hello results list</span></span>     
<span data-ttu-id="de478-123">![Selecteer Bladeren](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="de478-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="de478-124">Hallo-integratie account toowhich u tooadd Hallo certificaat wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="de478-124">Select hello integration account toowhich you want tooadd hello certificate.</span></span>  
![Hallo-integratie account toowhich gewenste tooadd Hallo certificaat selecteren](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="de478-126">Selecteer Hallo **certificaten** tegel.</span><span class="sxs-lookup"><span data-stu-id="de478-126">Select hello **Certificates** tile.</span></span>  
<span data-ttu-id="de478-127">![Selecteer Hallo certificaten tegel](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="de478-127">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="de478-128">In Hallo **certificaten** blade die wordt geopend, selecteer Hallo **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="de478-128">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="de478-129">![Klik op de knop toevoegen Hallo](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="de478-129">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="de478-130">Voer een **naam** voor het certificaat en selecteer vervolgens Hallo certificaattype als **openbare** uit Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="de478-130">Enter a **Name** for your certificate, and then select hello certificate type as **public** from hello dropdown.</span></span>  
6. <span data-ttu-id="de478-131">Selecteer Hallo mappictogram aan de rechterkant Hallo Hallo **certificaat** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="de478-131">Select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="de478-132">Wanneer de bestandskiezer hello wordt geopend, zoeken en Hallo certificaatbestand dat u wilt dat tooupload tooyour integratie account selecteren.</span><span class="sxs-lookup"><span data-stu-id="de478-132">When hello file picker opens, find and select hello certificate file that you want tooupload tooyour integration account.</span></span>
7. <span data-ttu-id="de478-133">Hallo certificaat selecteren en selecteer vervolgens **OK** in Hallo bestandskiezer.</span><span class="sxs-lookup"><span data-stu-id="de478-133">Select hello certificate, and then select **OK** in hello file picker.</span></span> <span data-ttu-id="de478-134">Dit valideert en uploadt Hallo certificaat tooyour integratie-account.</span><span class="sxs-lookup"><span data-stu-id="de478-134">This validates and uploads hello certificate tooyour integration account.</span></span>
8. <span data-ttu-id="de478-135">Ten slotte op Hallo back **certificaat toevoegen** blade, selecteer Hallo **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="de478-135">Finally, back on hello **Add certificate** blade, select hello **OK** button.</span></span>  
<span data-ttu-id="de478-136">![Selecteer OK om Hallo](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="de478-136">![Select hello OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="de478-137">Selecteer Hallo **certificaten** tegel.</span><span class="sxs-lookup"><span data-stu-id="de478-137">Select hello **Certificates** tile.</span></span> <span data-ttu-id="de478-138">U ziet Hallo toegevoegde certificaat.</span><span class="sxs-lookup"><span data-stu-id="de478-138">You should see hello newly added certificate.</span></span>  
<span data-ttu-id="de478-139">![Zie het nieuwe certificaat Hallo](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="de478-139">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="de478-140">Een persoonlijk certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="de478-140">Upload a private certificate</span></span>

<span data-ttu-id="de478-141">toouse een *persoonlijk certificaat* in logic apps met B2B-mogelijkheden, kunt u een persoonlijk certificaat tooyour integratie account uploaden door duurt Hallo stappen te volgen</span><span class="sxs-lookup"><span data-stu-id="de478-141">toouse a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate tooyour integration account by taking hello following steps</span></span>

1. <span data-ttu-id="de478-142">[Uploaden van uw persoonlijke sleutel tooKey kluis](../key-vault/key-vault-get-started.md "meer informatie over Sleutelkluis") en geef een **sleutelnaam**</span><span class="sxs-lookup"><span data-stu-id="de478-142">[Upload your private key tooKey Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="de478-143">U moet Logic Apps tooperform bewerkingen op Sleutelkluis autoriseren.</span><span class="sxs-lookup"><span data-stu-id="de478-143">You must authorize Logic Apps tooperform operations on Key Vault.</span></span> <span data-ttu-id="de478-144">U kunt toegang toohello Logic Apps-service-principal met behulp van de volgende PowerShell-opdracht Hallo verlenen:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="de478-144">You can grant access toohello Logic Apps service principal by using hello following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="de478-145">Nadat u Hallo vorige stap hebt gemaakt, moet u een persoonlijk certificaat toointegration-account toevoegen.</span><span class="sxs-lookup"><span data-stu-id="de478-145">After you've taken hello previous step, add a private certificate toointegration account.</span></span>

<span data-ttu-id="de478-146">Hieronder worden de gedetailleerde stappen voor het uploaden van uw persoonlijke certificaten bij uw account integratie nadat u Azure-portal toohello aanmelden Hallo:</span><span class="sxs-lookup"><span data-stu-id="de478-146">Following are hello detailed steps for uploading your private certificates into your integration account after you sign in toohello Azure portal:</span></span>  
 
1. <span data-ttu-id="de478-147">Selecteer Hallo integratie account toowhich u tooadd Hallo certificaat wilt en selecteer Hallo **certificaten** tegel.</span><span class="sxs-lookup"><span data-stu-id="de478-147">Select hello integration account toowhich you want tooadd hello certificate and select hello **Certificates** tile.</span></span>  
<span data-ttu-id="de478-148">![Selecteer Hallo certificaten tegel](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="de478-148">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="de478-149">In Hallo **certificaten** blade die wordt geopend, selecteer Hallo **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="de478-149">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="de478-150">![Klik op de knop toevoegen Hallo](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="de478-150">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="de478-151">Voer een **naam** voor het certificaat en selecteer Hallo certificaattype als **persoonlijke** uit Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="de478-151">Enter a **Name** for your certificate, and select hello certificate type as **private** from hello dropdown.</span></span>   
4. <span data-ttu-id="de478-152">Selecteer Hallo mappictogram aan de rechterkant Hallo Hallo **certificaat** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="de478-152">select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="de478-153">Wanneer Hallo bestandskiezer wordt geopend, Hallo overeenkomende openbare-certificaat vinden dat u wilt dat tooupload tooyour integratie rekening.</span><span class="sxs-lookup"><span data-stu-id="de478-153">When hello file picker opens, find hello corresponding public certificate that you want tooupload tooyour integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="de478-154">Tijdens het toevoegen van een persoonlijk certificaat is het belangrijk tooshow in van het certificaat overeenkomt openbare tooadd [AS2-overeenkomst](logic-apps-enterprise-integration-as2.md) instellingen voor het ondertekenen en versleutelen Hallo-berichten verzenden en ontvangen.</span><span class="sxs-lookup"><span data-stu-id="de478-154">While adding a private certificate it is important tooadd corresponding public certificate tooshow in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting hello messages.</span></span>
   > 
   >   

5. <span data-ttu-id="de478-155">Selecteer Hallo **resourcegroep**, **Sleutelkluis**, **sleutelnaam** en selecteer Hallo **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="de478-155">Select hello **Resource Group**, **Key Vault**, **Key Name** and select hello **OK** button.</span></span>  
<span data-ttu-id="de478-156">![Certificaat toevoegen](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="de478-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="de478-157">Selecteer Hallo **certificaten** tegel.</span><span class="sxs-lookup"><span data-stu-id="de478-157">Select hello **Certificates** tile.</span></span> <span data-ttu-id="de478-158">U ziet Hallo toegevoegde certificaat.</span><span class="sxs-lookup"><span data-stu-id="de478-158">You should see hello newly added certificate.</span></span>
<span data-ttu-id="de478-159">![Zie het nieuwe certificaat Hallo](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="de478-159">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="de478-160">Maken van een B2B-overeenkomst</span><span class="sxs-lookup"><span data-stu-id="de478-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="de478-161">Meer informatie over Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="de478-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "meer informatie over Sleutelkluis")  

