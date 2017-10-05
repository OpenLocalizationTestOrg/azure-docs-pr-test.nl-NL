---
title: <span data-ttu-id="828b1-101">Gebruik van certificaten met Enterprise Integration Pack | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="828b1-101">Using certificates with Enterprise Integration Pack | Microsoft Docs</span></span>
description: <span data-ttu-id="828b1-102">Informatie over het gebruik van certificaten met de Enterprise Integration Pack | Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="828b1-102">Learn how to use certificates with the Enterprise Integration Pack | Azure Logic Apps</span></span>
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
ms.openlocfilehash: 0570aab14283b38f9efcc50636f0c0c1c8e3ed13
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="828b1-103">Meer informatie over certificaten en het Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="828b1-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="828b1-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="828b1-104">Overview</span></span>
<span data-ttu-id="828b1-105">Enterprise-integratie gebruikt certificaten voor het beveiligen van B2B-communicatie.</span><span class="sxs-lookup"><span data-stu-id="828b1-105">Enterprise integration uses certificates to secure B2B communications.</span></span> <span data-ttu-id="828b1-106">U kunt twee typen certificaten gebruiken in uw onderneming integratie-apps:</span><span class="sxs-lookup"><span data-stu-id="828b1-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="828b1-107">Openbare certificaten, moeten worden aangeschaft van een certificeringsinstantie (CA).</span><span class="sxs-lookup"><span data-stu-id="828b1-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="828b1-108">Persoonlijke certificaten, kunt u zelf uitgeven.</span><span class="sxs-lookup"><span data-stu-id="828b1-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="828b1-109">Deze certificaten worden soms aangeduid als zelfondertekende certificaten.</span><span class="sxs-lookup"><span data-stu-id="828b1-109">These certificates are sometimes referred to as self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="828b1-110">Wat zijn certificaten?</span><span class="sxs-lookup"><span data-stu-id="828b1-110">What are certificates?</span></span>
<span data-ttu-id="828b1-111">Certificaten worden digitale documenten die de identiteit van de deelnemers aan elektronische communicatie verifiëren en die ook elektronische communicatie beveiligen.</span><span class="sxs-lookup"><span data-stu-id="828b1-111">Certificates are digital documents that verify the identity of the participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="828b1-112">Waarom certificaten gebruiken?</span><span class="sxs-lookup"><span data-stu-id="828b1-112">Why use certificates?</span></span>
<span data-ttu-id="828b1-113">Soms moet B2B-communicatie vertrouwelijk worden behandeld.</span><span class="sxs-lookup"><span data-stu-id="828b1-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="828b1-114">Enterprise integration maakt gebruik van certificaten voor het beveiligen van deze communicatie op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="828b1-114">Enterprise integration uses certificates to secure these communications in two ways:</span></span>

* <span data-ttu-id="828b1-115">Door de inhoud van berichten te versleutelen</span><span class="sxs-lookup"><span data-stu-id="828b1-115">By encrypting the contents of messages</span></span>
* <span data-ttu-id="828b1-116">Door berichten digitaal te ondertekenen</span><span class="sxs-lookup"><span data-stu-id="828b1-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="828b1-117">Een openbaar certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="828b1-117">Upload a public certificate</span></span>

<span data-ttu-id="828b1-118">Gebruik een *openbaar certificaat* in logic apps met B2B-mogelijkheden, moet u eerst het certificaat te uploaden naar uw integratie-account.</span><span class="sxs-lookup"><span data-stu-id="828b1-118">To use a *public certificate* in your logic apps with B2B capabilities, you first need to upload the certificate into your integration account.</span></span>  

<span data-ttu-id="828b1-119">Nadat u een certificaat hebt geüpload, wordt het beschikbaar om te helpen beveiligen van uw B2B-berichten bij het definiëren van de eigenschappen in de [overeenkomsten](logic-apps-enterprise-integration-agreements.md) die u maakt.</span><span class="sxs-lookup"><span data-stu-id="828b1-119">After you upload a certificate, it's available to help you secure your B2B messages when you define their properties in the [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="828b1-120">Hier worden de gedetailleerde stappen voor het uploaden van uw certificaten voor openbare toegang tot je account integratie nadat u zich aanmeldt bij de Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="828b1-120">Here are the detailed steps for uploading your public certificates into your integration account after you sign in to the Azure portal:</span></span>

1. <span data-ttu-id="828b1-121">Selecteer **meer services** en voer **integratie** in het zoekvak van het filter.</span><span class="sxs-lookup"><span data-stu-id="828b1-121">Select **More services** and enter **integration** in the filter search box.</span></span> <span data-ttu-id="828b1-122">Selecteer **Integratieaccounts** uit de lijst met resultaten</span><span class="sxs-lookup"><span data-stu-id="828b1-122">Select **Integration Accounts** from the results list</span></span>     
<span data-ttu-id="828b1-123">![Selecteer Bladeren](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="828b1-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="828b1-124">Selecteer de integratie-account waarnaar u wilt het certificaat niet toevoegen.</span><span class="sxs-lookup"><span data-stu-id="828b1-124">Select the integration account to which you want to add the certificate.</span></span>  
![Selecteer de integratie-account waarnaar u wilt het certificaat toevoegen](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="828b1-126">Selecteer de **certificaten** tegel.</span><span class="sxs-lookup"><span data-stu-id="828b1-126">Select the **Certificates** tile.</span></span>  
<span data-ttu-id="828b1-127">![Selecteer de tegel certificaten](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="828b1-127">![Select the Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="828b1-128">In de **certificaten** blade die wordt geopend, selecteert de **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="828b1-128">In the **Certificates** blade that opens, select the **Add** button.</span></span>   
<span data-ttu-id="828b1-129">![Klik op de knop toevoegen](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="828b1-129">![Select the Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="828b1-130">Voer een **naam** voor uw certificaat en selecteer vervolgens typt u het certificaat als **openbare** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="828b1-130">Enter a **Name** for your certificate, and then select the certificate type as **public** from the dropdown.</span></span>  
6. <span data-ttu-id="828b1-131">Selecteer het mappictogram aan de rechterkant van de **certificaat** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="828b1-131">Select the folder icon on the right side of the **Certificate** text box.</span></span> <span data-ttu-id="828b1-132">Wanneer de bestandskiezer wordt geopend, zoek en selecteer het certificaatbestand dat u wilt uploaden naar uw integratie-account.</span><span class="sxs-lookup"><span data-stu-id="828b1-132">When the file picker opens, find and select the certificate file that you want to upload to your integration account.</span></span>
7. <span data-ttu-id="828b1-133">Selecteer het certificaat en selecteer vervolgens **OK** in de bestandskiezer.</span><span class="sxs-lookup"><span data-stu-id="828b1-133">Select the certificate, and then select **OK** in the file picker.</span></span> <span data-ttu-id="828b1-134">Dit valideert en uploadt het certificaat aan uw account integratie.</span><span class="sxs-lookup"><span data-stu-id="828b1-134">This validates and uploads the certificate to your integration account.</span></span>
8. <span data-ttu-id="828b1-135">Back-ten slotte op de **certificaat toevoegen** blade, selecteer de **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="828b1-135">Finally, back on the **Add certificate** blade, select the **OK** button.</span></span>  
<span data-ttu-id="828b1-136">![Selecteer de knop OK](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="828b1-136">![Select the OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="828b1-137">Selecteer de **certificaten** tegel.</span><span class="sxs-lookup"><span data-stu-id="828b1-137">Select the **Certificates** tile.</span></span> <span data-ttu-id="828b1-138">U ziet het zojuist toegevoegde certificaat.</span><span class="sxs-lookup"><span data-stu-id="828b1-138">You should see the newly added certificate.</span></span>  
<span data-ttu-id="828b1-139">![Zie het nieuwe certificaat](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="828b1-139">![See the new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="828b1-140">Een persoonlijk certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="828b1-140">Upload a private certificate</span></span>

<span data-ttu-id="828b1-141">Gebruik een *persoonlijk certificaat* in logic apps met B2B-mogelijkheden, kunt u een persoonlijk certificaat uploaden naar uw account integratie met de volgende stappen</span><span class="sxs-lookup"><span data-stu-id="828b1-141">To use a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate to your integration account by taking the following steps</span></span>

1. <span data-ttu-id="828b1-142">[Uw persoonlijke sleutel te uploaden naar Sleutelkluis](../key-vault/key-vault-get-started.md "meer informatie over Sleutelkluis") en geef een **sleutelnaam**</span><span class="sxs-lookup"><span data-stu-id="828b1-142">[Upload your private key to Key Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="828b1-143">U kunt logische Apps op bewerkingen uitvoeren op de Sleutelkluis moet autoriseren.</span><span class="sxs-lookup"><span data-stu-id="828b1-143">You must authorize Logic Apps to perform operations on Key Vault.</span></span> <span data-ttu-id="828b1-144">U kunt toegang verlenen tot de service-principal van Logic Apps met behulp van de volgende PowerShell-opdracht:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="828b1-144">You can grant access to the Logic Apps service principal by using the following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="828b1-145">Nadat u de vorige stap hebt gemaakt, moet u een persoonlijk certificaat toevoegen aan integratie-account.</span><span class="sxs-lookup"><span data-stu-id="828b1-145">After you've taken the previous step, add a private certificate to integration account.</span></span>

<span data-ttu-id="828b1-146">Hier volgen gedetailleerde stappen voor het uploaden van uw persoonlijke certificaten bij uw account integratie nadat u zich aanmeldt bij de Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="828b1-146">Following are the detailed steps for uploading your private certificates into your integration account after you sign in to the Azure portal:</span></span>  
 
1. <span data-ttu-id="828b1-147">Selecteer de integratie-account die u wilt het certificaat toevoegen en selecteer de **certificaten** tegel.</span><span class="sxs-lookup"><span data-stu-id="828b1-147">Select the integration account to which you want to add the certificate and select the **Certificates** tile.</span></span>  
<span data-ttu-id="828b1-148">![Selecteer de tegel certificaten](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="828b1-148">![Select the Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="828b1-149">In de **certificaten** blade die wordt geopend, selecteert de **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="828b1-149">In the **Certificates** blade that opens, select the **Add** button.</span></span>   
<span data-ttu-id="828b1-150">![Klik op de knop toevoegen](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="828b1-150">![Select the Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="828b1-151">Voer een **naam** voor het certificaat en selecteer het certificaat typt als **persoonlijke** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="828b1-151">Enter a **Name** for your certificate, and select the certificate type as **private** from the dropdown.</span></span>   
4. <span data-ttu-id="828b1-152">Selecteer het mappictogram aan de rechterkant van de **certificaat** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="828b1-152">select the folder icon on the right side of the **Certificate** text box.</span></span> <span data-ttu-id="828b1-153">Wanneer de bestandskiezer wordt geopend, moet u het bijbehorende openbare certificaat dat u wilt uploaden naar uw account integratie vinden.</span><span class="sxs-lookup"><span data-stu-id="828b1-153">When the file picker opens, find the corresponding public certificate that you want to upload to your integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="828b1-154">Tijdens het toevoegen van een persoonlijk certificaat is het belangrijk om het openbare certificaat van de bijbehorende om weer te geven toevoegen [AS2-overeenkomst](logic-apps-enterprise-integration-as2.md) ontvangen en verzenden van instellingen voor het ondertekenen en versleutelen van berichten.</span><span class="sxs-lookup"><span data-stu-id="828b1-154">While adding a private certificate it is important to add corresponding public certificate to show in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting the messages.</span></span>
   > 
   >   

5. <span data-ttu-id="828b1-155">Selecteer de **resourcegroep**, **Sleutelkluis**, **sleutelnaam** en selecteer de **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="828b1-155">Select the **Resource Group**, **Key Vault**, **Key Name** and select the **OK** button.</span></span>  
<span data-ttu-id="828b1-156">![Certificaat toevoegen](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="828b1-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="828b1-157">Selecteer de **certificaten** tegel.</span><span class="sxs-lookup"><span data-stu-id="828b1-157">Select the **Certificates** tile.</span></span> <span data-ttu-id="828b1-158">U ziet het zojuist toegevoegde certificaat.</span><span class="sxs-lookup"><span data-stu-id="828b1-158">You should see the newly added certificate.</span></span>
<span data-ttu-id="828b1-159">![Zie het nieuwe certificaat](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="828b1-159">![See the new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="828b1-160">Maken van een B2B-overeenkomst</span><span class="sxs-lookup"><span data-stu-id="828b1-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="828b1-161">Meer informatie over Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="828b1-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "meer informatie over Sleutelkluis")  

