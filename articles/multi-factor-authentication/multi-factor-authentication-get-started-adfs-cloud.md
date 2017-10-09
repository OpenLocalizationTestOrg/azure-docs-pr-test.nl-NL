---
title: cloudresources aaaSecure met Azure MFA en AD FS | Microsoft Docs
description: Dit is hello Azure multi-factor authentication-pagina waarop wordt beschreven hoe tooget de slag met Azure MFA en AD FS in Hallo cloud.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="66417-103">Cloudresources beveiligen met Azure Multi-Factor Authentication en AD FS</span><span class="sxs-lookup"><span data-stu-id="66417-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="66417-104">Als uw organisatie is gefedereerd met Azure Active Directory, gebruikt u Azure multi-factor Authentication of Active Directory Federation Services (AD FS) toosecure resources die worden gebruikt door Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66417-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) toosecure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="66417-105">Hallo volgende procedures toosecure Azure Active Directory-resources met Azure multi-factor Authentication of Active Directory Federation Services gebruiken.</span><span class="sxs-lookup"><span data-stu-id="66417-105">Use hello following procedures toosecure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="66417-106">Azure AD-resources beveiligen met behulp van AD FS</span><span class="sxs-lookup"><span data-stu-id="66417-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="66417-107">toosecure uw cloudresource, instellen van een regel voor claims zodat Active Directory Federation Services Hallo multipleauthn claim verzendt wanneer een gebruiker wordt verificatie in twee stappen is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="66417-107">toosecure your cloud resource, set up a claims rule so that Active Directory Federation Services emits hello multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="66417-108">Deze claim is tooAzure AD doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="66417-108">This claim is passed on tooAzure AD.</span></span> <span data-ttu-id="66417-109">Volg deze procedure toowalk Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="66417-109">Follow this procedure toowalk through hello steps:</span></span>


1. <span data-ttu-id="66417-110">Open AD FS-beheer.</span><span class="sxs-lookup"><span data-stu-id="66417-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="66417-111">Selecteer aan de linkerkant Hallo **Relying Party-vertrouwensrelaties**.</span><span class="sxs-lookup"><span data-stu-id="66417-111">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="66417-112">Klik met de rechtermuisknop op **Identiteitsplatform van Microsoft Office 365** en selecteer **Claimregels bewerken**.</span><span class="sxs-lookup"><span data-stu-id="66417-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="66417-114">Klik bij Uitgifte transformatieregels op**Regel toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="66417-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="66417-116">Op Hallo transformeren Wizard Claimregel voor toevoegen, selecteert u **doorgeven of filteren van een binnenkomende Claim** in Hallo vervolgkeuzelijst en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="66417-116">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="66417-118">Geef de regel een naam.</span><span class="sxs-lookup"><span data-stu-id="66417-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="66417-119">Selecteer **Verwijdingen verificatiemethode** als Hallo binnenkomende claimtype.</span><span class="sxs-lookup"><span data-stu-id="66417-119">Select **Authentication Methods References** as hello Incoming claim type.</span></span>
8. <span data-ttu-id="66417-120">Selecteer **Alle claimwaarden doorgeven**.</span><span class="sxs-lookup"><span data-stu-id="66417-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="66417-121">![Wizard Claimregel voor transformatie toevoegen](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="66417-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="66417-122">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="66417-122">Click **Finish**.</span></span> <span data-ttu-id="66417-123">Sluit Hallo AD FS-beheerconsole.</span><span class="sxs-lookup"><span data-stu-id="66417-123">Close hello AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="66417-124">Goedgekeurde IP-adressen voor federatieve gebruikers</span><span class="sxs-lookup"><span data-stu-id="66417-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="66417-125">Goedgekeurde IP-adressen kunnen beheerders de verificatie in twee stappen tooby pass voor specifieke IP-adressen of voor federatieve gebruikers met verzoeken die afkomstig zijn van hun eigen intranet.</span><span class="sxs-lookup"><span data-stu-id="66417-125">Trusted IPs allow administrators tooby-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="66417-126">Hallo volgende secties wordt beschreven hoe tooconfigure Azure multi-factor Authentication goedgekeurde IP-adressen met federatieve gebruikers en de verificatie in twee stappen overslaan wanneer een aanvraag afkomstig van een federatieve gebruikers het intranet is.</span><span class="sxs-lookup"><span data-stu-id="66417-126">hello following sections describe how tooconfigure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="66417-127">Dit wordt bereikt door het configureren van AD FS toouse doorgangsschijf of filteren van een binnenkomende claimsjabloon Hello claimtype binnen bedrijfsnetwerk.</span><span class="sxs-lookup"><span data-stu-id="66417-127">This is achieved by configuring AD FS toouse a pass-through or filter an incoming claim template with hello Inside Corporate Network claim type.</span></span>

<span data-ttu-id="66417-128">In dit voorbeeld wordt Office 365 gebruikt voor onze Relying Party-vertrouwensrelaties.</span><span class="sxs-lookup"><span data-stu-id="66417-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-hello-ad-fs-claims-rules"></a><span data-ttu-id="66417-129">Regels voor Hallo AD FS-claims configureren</span><span class="sxs-lookup"><span data-stu-id="66417-129">Configure hello AD FS claims rules</span></span>
<span data-ttu-id="66417-130">Hallo eerst moet toodo is tooconfigure Hallo AD FS-claims.</span><span class="sxs-lookup"><span data-stu-id="66417-130">hello first thing we need toodo is tooconfigure hello AD FS claims.</span></span> <span data-ttu-id="66417-131">Twee claimregels maken, één voor Hallo binnen bedrijfsnetwerk claimtype en een extra regel om onze gebruikers aangemeld te houden.</span><span class="sxs-lookup"><span data-stu-id="66417-131">Create two claims rules, one for hello Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="66417-132">Open AD FS-beheer.</span><span class="sxs-lookup"><span data-stu-id="66417-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="66417-133">Selecteer aan de linkerkant Hallo **Relying Party-vertrouwensrelaties**.</span><span class="sxs-lookup"><span data-stu-id="66417-133">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="66417-134">Klik met de rechtermuisknop op het **identiteitsplatform van Microsoft Office 365** en selecteer **Claimregels bewerken...**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="66417-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="66417-135">Klik bij Uitgifte transformatieregels op**Regel toevoegen.**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="66417-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="66417-136">Op Hallo transformeren Wizard Claimregel voor toevoegen, selecteert u **doorgeven of filteren van een binnenkomende Claim** in Hallo vervolgkeuzelijst en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="66417-136">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>
   <span data-ttu-id="66417-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="66417-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="66417-138">Hallo vak volgende tooClaim regelnaam de regel een naam geven.</span><span class="sxs-lookup"><span data-stu-id="66417-138">In hello box next tooClaim rule name, give your rule a name.</span></span> <span data-ttu-id="66417-139">Bijvoorbeeld: BinnenBedrijfsNet.</span><span class="sxs-lookup"><span data-stu-id="66417-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="66417-140">Uit de vervolgkeuzelijst hello, volgende tooIncoming claimtype, selecteert **binnen bedrijfsnetwerk**.</span><span class="sxs-lookup"><span data-stu-id="66417-140">From hello drop-down, next tooIncoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="66417-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="66417-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="66417-142">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="66417-142">Click **Finish**.</span></span>
9. <span data-ttu-id="66417-143">Klik bij Uitgifte transformatieregels op**Regel toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="66417-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="66417-144">Op Hallo transformeren Wizard Claimregel voor toevoegen, selecteert u **Claims verzenden met een aangepaste regel** in Hallo vervolgkeuzelijst en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="66417-144">On hello Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from hello drop-down and click **Next**.</span></span>
11. <span data-ttu-id="66417-145">In het vak onder naam Claimregel Hallo: Voer *gebruikers aangemeld houden*.</span><span class="sxs-lookup"><span data-stu-id="66417-145">In hello box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="66417-146">Voer in het vak van het Hallo aangepaste regel:</span><span class="sxs-lookup"><span data-stu-id="66417-146">In hello Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="66417-148">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="66417-148">Click **Finish**.</span></span>
14. <span data-ttu-id="66417-149">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="66417-149">Click **Apply**.</span></span>
15. <span data-ttu-id="66417-150">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="66417-150">Click **Ok**.</span></span>
16. <span data-ttu-id="66417-151">Sluit AD FS-beheer.</span><span class="sxs-lookup"><span data-stu-id="66417-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="66417-152">Goedgekeurde IP-adressen van Azure Multi-Factor Authentication configureren bij federatieve gebruikers</span><span class="sxs-lookup"><span data-stu-id="66417-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="66417-153">Nu dat Hallo claims gemaakt zijn, kunnen we goedgekeurde IP-adressen configureren.</span><span class="sxs-lookup"><span data-stu-id="66417-153">Now that hello claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="66417-154">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="66417-154">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="66417-155">Klik aan de linkerkant Hallo op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="66417-155">On hello left, click **Active Directory**.</span></span>
3. <span data-ttu-id="66417-156">Selecteer onder adreslijst Hallo directory waar u tooset van goedgekeurde IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="66417-156">Under Directory, select hello directory where you want tooset up trusted IPs.</span></span>
4. <span data-ttu-id="66417-157">Op Hallo Directory die u hebt geselecteerd, klikt u op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="66417-157">On hello Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="66417-158">Klik in de sectie multi-factor authentication hello, **service-instellingen beheren**.</span><span class="sxs-lookup"><span data-stu-id="66417-158">In hello multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="66417-159">Selecteer op Hallo pagina Service-instellingen onder goedgekeurde IP-adressen, **meerdere-multi-factor-verificatie overslaan voor aanvragen van federatieve gebruikers op mijn intranet**.</span><span class="sxs-lookup"><span data-stu-id="66417-159">On hello Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="66417-161">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="66417-161">Click **save**.</span></span>
8. <span data-ttu-id="66417-162">Zodra het Hallo-updates zijn toegepast, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="66417-162">Once hello updates have been applied, click **close**.</span></span>

<span data-ttu-id="66417-163">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="66417-163">That’s it!</span></span> <span data-ttu-id="66417-164">Federatieve gebruikers van Office 365 mag op dit moment alleen toouse MFA hebben wanneer een claim afkomstig van buiten Hallo bedrijfsintranet is.</span><span class="sxs-lookup"><span data-stu-id="66417-164">At this point, federated Office 365 users should only have toouse MFA when a claim originates from outside hello corporate intranet.</span></span>
