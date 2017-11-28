---
title: Cloudresources beveiligen met Azure MFA en AD FS | Microsoft Docs
description: Dit is de pagina Azure Multi-Factor Authentication waarop wordt beschreven hoe u aan de slag kunt met Azure MFA en AD FS in de cloud.
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
ms.openlocfilehash: 6cf4ec4f777ea1f2b852945ab82da2547946f378
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="dd6e6-103">Cloudresources beveiligen met Azure Multi-Factor Authentication en AD FS</span><span class="sxs-lookup"><span data-stu-id="dd6e6-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="dd6e6-104">Als uw organisatie is gefedereerd met behulp van Azure Active Directory, kunt u Azure Multi-Factor Authentication of Active Directory Federation Services (AD FS) gebruiken om resources te beveiligen die door Azure AD worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) to secure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="dd6e6-105">Gebruik de volgende procedures voor het beveiligen van Azure Active Directory-resources met ofwel Azure Multi-Factor Authentication of Active Directory Federation Services.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-105">Use the following procedures to secure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="dd6e6-106">Azure AD-resources beveiligen met behulp van AD FS</span><span class="sxs-lookup"><span data-stu-id="dd6e6-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="dd6e6-107">Voor de beveiliging van uw cloudresource stelt u een claimregel in die ervoor zorgt dat Active Directory Federation Services de multipleauthn-claim verstuurt wanneer een gebruiker de verificatie in twee stappen voltooit.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-107">To secure your cloud resource, set up a claims rule so that Active Directory Federation Services emits the multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="dd6e6-108">Deze claim wordt doorgegeven aan Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-108">This claim is passed on to Azure AD.</span></span> <span data-ttu-id="dd6e6-109">Volg deze procedure om de stappen te doorlopen:</span><span class="sxs-lookup"><span data-stu-id="dd6e6-109">Follow this procedure to walk through the steps:</span></span>


1. <span data-ttu-id="dd6e6-110">Open AD FS-beheer.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="dd6e6-111">Selecteer **Relying Party-vertrouwensrelaties** aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-111">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="dd6e6-112">Klik met de rechtermuisknop op **Identiteitsplatform van Microsoft Office 365** en selecteer **Claimregels bewerken**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="dd6e6-114">Klik bij Uitgifte transformatieregels op**Regel toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="dd6e6-116">Selecteer in de wizard Transformatieclaimregels toevoegen **Passthrough of Een binnenkomende claim filteren** in de vervolgkeuzelijst en klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-116">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="dd6e6-118">Geef de regel een naam.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="dd6e6-119">Selecteer **Authenticatiemethodereferenties** als het type voor binnenkomende claims.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-119">Select **Authentication Methods References** as the Incoming claim type.</span></span>
8. <span data-ttu-id="dd6e6-120">Selecteer **Alle claimwaarden doorgeven**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="dd6e6-121">![Wizard Claimregel voor transformatie toevoegen](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="dd6e6-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="dd6e6-122">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-122">Click **Finish**.</span></span> <span data-ttu-id="dd6e6-123">Sluit de AD FS-beheerconsole.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-123">Close the AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="dd6e6-124">Goedgekeurde IP-adressen voor federatieve gebruikers</span><span class="sxs-lookup"><span data-stu-id="dd6e6-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="dd6e6-125">Met goedgekeurde IP-adressen zijn beheerders in staat om verificatie in twee stappen te omzeilen voor bepaalde IP-adressen of voor federatieve gebruikers met verzoeken die afkomstig zijn uit hun eigen intranet.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-125">Trusted IPs allow administrators to by-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="dd6e6-126">In de volgende secties wordt beschreven hoe goedgekeurde IP-adressen van Azure Multi-Factor Authentication bij federatieve gebruikers moeten worden geconfigureerd en hoe verificatie in twee stappen kan worden omzeild als een verzoek afkomstig is uit het intranet van een federatieve gebruiker.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-126">The following sections describe how to configure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="dd6e6-127">Dit wordt bereikt door AD FS zo te configureren dat deze gebruikmaakt van een passthrough of een binnenkomende claimsjabloon filtert met het claimtype Binnen bedrijfsnetwerk.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-127">This is achieved by configuring AD FS to use a pass-through or filter an incoming claim template with the Inside Corporate Network claim type.</span></span>

<span data-ttu-id="dd6e6-128">In dit voorbeeld wordt Office 365 gebruikt voor onze Relying Party-vertrouwensrelaties.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-the-ad-fs-claims-rules"></a><span data-ttu-id="dd6e6-129">De claimregels van AD FS configureren</span><span class="sxs-lookup"><span data-stu-id="dd6e6-129">Configure the AD FS claims rules</span></span>
<span data-ttu-id="dd6e6-130">Het eerste wat we moeten doen is de AD FS-claims configureren.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-130">The first thing we need to do is to configure the AD FS claims.</span></span> <span data-ttu-id="dd6e6-131">U maakt twee claimregels: één voor het claimtype Binnen bedrijfsnetwerk en een extra regel om de gebruikers aangemeld te houden.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-131">Create two claims rules, one for the Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="dd6e6-132">Open AD FS-beheer.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="dd6e6-133">Selecteer **Relying Party-vertrouwensrelaties** aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-133">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="dd6e6-134">Klik met de rechtermuisknop op het **identiteitsplatform van Microsoft Office 365** en selecteer **Claimregels bewerken...**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="dd6e6-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="dd6e6-135">Klik bij Uitgifte transformatieregels op**Regel toevoegen.**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="dd6e6-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="dd6e6-136">Selecteer in de wizard Transformatieclaimregels toevoegen **Passthrough of Een binnenkomende claim filteren** in de vervolgkeuzelijst en klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-136">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>
   <span data-ttu-id="dd6e6-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="dd6e6-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="dd6e6-138">Geef de claimregel een naam in het vak bij Naam claimregel.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-138">In the box next to Claim rule name, give your rule a name.</span></span> <span data-ttu-id="dd6e6-139">Bijvoorbeeld: BinnenBedrijfsNet.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="dd6e6-140">In de vervolgkeuzelijst naast Binnenkomend claimtype, selecteert u **Binnen bedrijfsnetwerk**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-140">From the drop-down, next to Incoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="dd6e6-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="dd6e6-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="dd6e6-142">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-142">Click **Finish**.</span></span>
9. <span data-ttu-id="dd6e6-143">Klik bij Uitgifte transformatieregels op**Regel toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="dd6e6-144">Selecteer in de wizard Transformatieclaimregels toevoegen **Claim verzenden met een aangepaste regel** in de vervolgkeuzelijst en klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-144">On the Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from the drop-down and click **Next**.</span></span>
11. <span data-ttu-id="dd6e6-145">In het vak onder Naam claimregel typt u *Gebruikers aangemeld houden*.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-145">In the box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="dd6e6-146">In het vak Aangepaste regel typt u:</span><span class="sxs-lookup"><span data-stu-id="dd6e6-146">In the Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="dd6e6-148">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-148">Click **Finish**.</span></span>
14. <span data-ttu-id="dd6e6-149">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-149">Click **Apply**.</span></span>
15. <span data-ttu-id="dd6e6-150">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-150">Click **Ok**.</span></span>
16. <span data-ttu-id="dd6e6-151">Sluit AD FS-beheer.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="dd6e6-152">Goedgekeurde IP-adressen van Azure Multi-Factor Authentication configureren bij federatieve gebruikers</span><span class="sxs-lookup"><span data-stu-id="dd6e6-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="dd6e6-153">Nu de claims zijn gemaakt, kunnen we goedgekeurde IP-adressen gaan configureren.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-153">Now that the claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="dd6e6-154">Meld u aan bij de [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="dd6e6-154">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="dd6e6-155">Klik aan de linkerkant op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-155">On the left, click **Active Directory**.</span></span>
3. <span data-ttu-id="dd6e6-156">Selecteer onder Adreslijst de adreslijst waar u de goedgekeurde IP-adressen wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-156">Under Directory, select the directory where you want to set up trusted IPs.</span></span>
4. <span data-ttu-id="dd6e6-157">Klik op **Configureren** op de Adreslijst die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-157">On the Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="dd6e6-158">Klik in de sectie Multi-Factor Authentication op **Service-instellingen beheren**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-158">In the multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="dd6e6-159">Selecteer op de pagina Service-instellingen onder Goedgekeurde IP-adressen, **Meervoudige verificatie overslaan voor aanvragen van federatieve gebruikers op mijn intranet**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-159">On the Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="dd6e6-161">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-161">Click **save**.</span></span>
8. <span data-ttu-id="dd6e6-162">Nadat de updates zijn toegepast, klikt u op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-162">Once the updates have been applied, click **close**.</span></span>

<span data-ttu-id="dd6e6-163">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-163">That’s it!</span></span> <span data-ttu-id="dd6e6-164">Vanaf dit moment hoeven Office 365-gebruikers alleen MFA te gebruiken wanneer een claim afkomstig is van buiten het bedrijfsintranet.</span><span class="sxs-lookup"><span data-stu-id="dd6e6-164">At this point, federated Office 365 users should only have to use MFA when a claim originates from outside the corporate intranet.</span></span>
