---
title: aaaGet de slag met voorwaardelijke toegang in Azure Active Directory | Microsoft Docs
description: Voorwaardelijke toegang met behulp van een locatie voorwaarde testen.
services: active-directory
keywords: voorwaardelijke toegang tooapps, voorwaardelijke toegang in Azure AD, beveiligde toegang tot resources toocompany, beleidsregels voor voorwaardelijke toegang
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="cd223-104">Aan de slag met voorwaardelijke toegang in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd223-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="cd223-105">Voorwaardelijke toegang is een functie van Azure Active Directory waarmee u toodefine voorwaarden waaronder gemachtigde gebruikers toegang uw apps tot hebben.</span><span class="sxs-lookup"><span data-stu-id="cd223-105">Conditional access is a capability of Azure Active Directory that enables you toodefine conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="cd223-106">In dit onderwerp vindt u instructies voor het testen van een voorwaardelijke toegang op basis van de voorwaarde van een locatie in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="cd223-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="cd223-107">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="cd223-107">Scenario description</span></span>

<span data-ttu-id="cd223-108">Een van de algemene vereisten in veel organisaties is tooonly meervoudige verificatie vereisen voor toegang tooapps die niet van het bedrijfsintranet hello wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cd223-108">One common requirement in many organizations is tooonly require multi-factor authentication for access tooapps that is not performed from hello corporate intranet.</span></span> <span data-ttu-id="cd223-109">Met Azure Active Directory, kunt u eenvoudig deze doelstelling uitvoeren door het configureren van beleid voor voorwaardelijke toegang op basis van locatie.</span><span class="sxs-lookup"><span data-stu-id="cd223-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="cd223-110">Dit onderwerp vindt u gedetailleerde instructies voor het configureren van een gerelateerd beleid.</span><span class="sxs-lookup"><span data-stu-id="cd223-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="cd223-111">maakt gebruik van beleid Hallo [goedgekeurde IP-adressen](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish tussen toegangspogingen tot van zakelijke Hallo de intranet- en alle andere locaties.</span><span class="sxs-lookup"><span data-stu-id="cd223-111">hello policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish between access attempts made from hello corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="cd223-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cd223-112">Prerequisites</span></span>

<span data-ttu-id="cd223-113">Hallo scenario beschreven in dit onderwerp wordt ervan uitgegaan dat u bekend met Hallo concepten die worden beschreven bent in [voorwaardelijke toegang van Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cd223-113">hello scenario outlined in this topic assumes that you are familiar with hello concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="cd223-114">tootest dit scenario moet u:</span><span class="sxs-lookup"><span data-stu-id="cd223-114">tootest this scenario, you need to:</span></span>

- <span data-ttu-id="cd223-115">Een testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="cd223-115">Create a test user</span></span> 

- <span data-ttu-id="cd223-116">Wijs een licentie voor Azure AD Premium toohello testgebruiker</span><span class="sxs-lookup"><span data-stu-id="cd223-116">Assign an Azure AD Premium license toohello test user</span></span>

- <span data-ttu-id="cd223-117">Configureren van een beheerde app en uw test gebruiker tooit toewijzen</span><span class="sxs-lookup"><span data-stu-id="cd223-117">Configure a managed app and assign your test user tooit</span></span>

- <span data-ttu-id="cd223-118">Goedgekeurde IP-adressen configureren</span><span class="sxs-lookup"><span data-stu-id="cd223-118">Configure trusted IPs</span></span>

<span data-ttu-id="cd223-119">Als u meer informatie over de goedgekeurde IP-adressen, Zie [goedgekeurde IP-adressen](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="cd223-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="cd223-120">Beleid configuratiestappen</span><span class="sxs-lookup"><span data-stu-id="cd223-120">Policy configuration steps</span></span>

<span data-ttu-id="cd223-121">**tooconfigure uw beleid voor voorwaardelijke toegang, doen:**</span><span class="sxs-lookup"><span data-stu-id="cd223-121">**tooconfigure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="cd223-122">Klik in hello Azure-portal op Hallo links navigatiebalk, op **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cd223-122">In hello Azure portal, on hello left navbar, click **Azure Active Directory**.</span></span> 

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="cd223-124">Op Hallo **Azure Active Directory** blade in Hallo **beheren** sectie, klikt u op **voorwaardelijke toegang**.</span><span class="sxs-lookup"><span data-stu-id="cd223-124">On hello **Azure Active Directory** blade, in hello **Manage** section, click **Conditional access**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="cd223-126">Op Hallo **voorwaardelijke toegang** blade, tooopen hello **nieuw** blade in de werkbalk Hallo op Hallo boven, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cd223-126">On hello **Conditional Access** blade, tooopen hello **New** blade, in hello toolbar on hello top, click **Add**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="cd223-128">Op Hallo **nieuw** blade in Hallo **naam** textbox, typ een naam voor uw beleid.</span><span class="sxs-lookup"><span data-stu-id="cd223-128">On hello **New** blade, in hello **Name** textbox, type a name for your policy.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="cd223-130">In Hallo **toewijzing** sectie, klikt u op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="cd223-130">In hello **Assignment** section, click **Users and groups**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="cd223-132">Op Hallo **gebruikers en groepen** blade Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="cd223-132">On hello **Users and groups** blade, perform hello following steps:</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="cd223-134">a.</span><span class="sxs-lookup"><span data-stu-id="cd223-134">a.</span></span> <span data-ttu-id="cd223-135">Klik op **gebruikers en groepen selecteren**.</span><span class="sxs-lookup"><span data-stu-id="cd223-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="cd223-136">b.</span><span class="sxs-lookup"><span data-stu-id="cd223-136">b.</span></span> <span data-ttu-id="cd223-137">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="cd223-137">Click **Select**.</span></span>

    <span data-ttu-id="cd223-138">c.</span><span class="sxs-lookup"><span data-stu-id="cd223-138">c.</span></span> <span data-ttu-id="cd223-139">Op Hallo **Selecteer** blade uw testgebruiker selecteren en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="cd223-139">On hello **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="cd223-140">d.</span><span class="sxs-lookup"><span data-stu-id="cd223-140">d.</span></span> <span data-ttu-id="cd223-141">Op Hallo **gebruikers en groepen** blade, klikt u op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="cd223-141">On hello **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="cd223-142">Op Hallo **nieuw** blade, tooopen hello **Cloud-apps** blade in Hallo **toewijzing** sectie, klikt u op **Cloud-apps**.</span><span class="sxs-lookup"><span data-stu-id="cd223-142">On hello **New** blade, tooopen hello **Cloud apps** blade, in hello **Assignment** section, click **Cloud apps**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="cd223-144">Op Hallo **Cloud-apps** blade Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="cd223-144">On hello **Cloud apps** blade, perform hello following steps:</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="cd223-146">a.</span><span class="sxs-lookup"><span data-stu-id="cd223-146">a.</span></span> <span data-ttu-id="cd223-147">Klik op **apps selecteren**.</span><span class="sxs-lookup"><span data-stu-id="cd223-147">Click **Select apps**.</span></span>

    <span data-ttu-id="cd223-148">b.</span><span class="sxs-lookup"><span data-stu-id="cd223-148">b.</span></span> <span data-ttu-id="cd223-149">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="cd223-149">Click **Select**.</span></span>

    <span data-ttu-id="cd223-150">c.</span><span class="sxs-lookup"><span data-stu-id="cd223-150">c.</span></span> <span data-ttu-id="cd223-151">Op Hallo **Selecteer** blade uw cloud-app selecteren en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="cd223-151">On hello **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="cd223-152">d.</span><span class="sxs-lookup"><span data-stu-id="cd223-152">d.</span></span> <span data-ttu-id="cd223-153">Op Hallo **Cloud-apps** blade, klikt u op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="cd223-153">On hello **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="cd223-154">Op Hallo **nieuw** blade, tooopen hello **voorwaarden** blade in Hallo **toewijzing** sectie, klikt u op **voorwaarden**.</span><span class="sxs-lookup"><span data-stu-id="cd223-154">On hello **New** blade, tooopen hello **Conditions** blade, in hello **Assignment** section, click **Conditions**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="cd223-156">Op Hallo **voorwaarden** blade, tooopen hello **locaties** blade, klikt u op **locaties**.</span><span class="sxs-lookup"><span data-stu-id="cd223-156">On hello **Conditions** blade, tooopen hello **Locations** blade, click **Locations**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="cd223-158">Op Hallo **locaties** blade Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="cd223-158">On hello **Locations** blade, perform hello following steps:</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="cd223-160">a.</span><span class="sxs-lookup"><span data-stu-id="cd223-160">a.</span></span> <span data-ttu-id="cd223-161">Onder **configureren**, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="cd223-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="cd223-162">b.</span><span class="sxs-lookup"><span data-stu-id="cd223-162">b.</span></span> <span data-ttu-id="cd223-163">Onder **opnemen**, klikt u op **alle locaties**.</span><span class="sxs-lookup"><span data-stu-id="cd223-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="cd223-164">c.</span><span class="sxs-lookup"><span data-stu-id="cd223-164">c.</span></span> <span data-ttu-id="cd223-165">Klik op **uitsluiten**, en klik vervolgens op **alle goedgekeurde IP-adressen**.</span><span class="sxs-lookup"><span data-stu-id="cd223-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="cd223-167">d.</span><span class="sxs-lookup"><span data-stu-id="cd223-167">d.</span></span> <span data-ttu-id="cd223-168">Klik op **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="cd223-168">Click **Done**.</span></span>

12. <span data-ttu-id="cd223-169">Op Hallo **voorwaarden** blade, klikt u op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="cd223-169">On hello **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="cd223-170">Op Hallo **nieuw** blade, tooopen hello **Grant** blade in Hallo **besturingselementen** sectie, klikt u op **Grant**.</span><span class="sxs-lookup"><span data-stu-id="cd223-170">On hello **New** blade, tooopen hello **Grant** blade, in hello **Controls** section, click **Grant**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="cd223-172">Op Hallo **Grant** blade Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="cd223-172">On hello **Grant** blade, perform hello following steps:</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="cd223-174">a.</span><span class="sxs-lookup"><span data-stu-id="cd223-174">a.</span></span> <span data-ttu-id="cd223-175">Selecteer **meervoudige authenticatie**.</span><span class="sxs-lookup"><span data-stu-id="cd223-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="cd223-176">b.</span><span class="sxs-lookup"><span data-stu-id="cd223-176">b.</span></span> <span data-ttu-id="cd223-177">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="cd223-177">Click **Select**.</span></span>

15. <span data-ttu-id="cd223-178">Op Hallo **nieuw** blade onder **beleid inschakelen**, klikt u op **op**.</span><span class="sxs-lookup"><span data-stu-id="cd223-178">On hello **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="cd223-180">Op Hallo **nieuw** blade, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="cd223-180">On hello **New** blade, click **Create**.</span></span>


## <a name="testing-hello-policy"></a><span data-ttu-id="cd223-181">Hallo beleid testen</span><span class="sxs-lookup"><span data-stu-id="cd223-181">Testing hello policy</span></span>

<span data-ttu-id="cd223-182">tootest uw beleid, moet u toegang tot uw app vanaf een apparaat dat:</span><span class="sxs-lookup"><span data-stu-id="cd223-182">tootest your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="cd223-183">Heeft een IP-adres dat binnen de geconfigureerde goedgekeurde IP-adressen</span><span class="sxs-lookup"><span data-stu-id="cd223-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="cd223-184">Heeft een IP-adres dat is niet binnen de geconfigureerde goedgekeurde IP-adressen</span><span class="sxs-lookup"><span data-stu-id="cd223-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="cd223-185">Multi-factor authentication-server zijn moet alleen tijdens een verbindingspoging die is gemaakt van een apparaat dat is niet binnen de geconfigureerde goedgekeurde IP-adressen vereist.</span><span class="sxs-lookup"><span data-stu-id="cd223-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="cd223-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cd223-186">Next steps</span></span>

<span data-ttu-id="cd223-187">Als u meer informatie over voorwaardelijke toegang toolearn, Zie [voorwaardelijke toegang van Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cd223-187">If you would like toolearn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

