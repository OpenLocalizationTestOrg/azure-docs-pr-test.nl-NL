---
title: Aan de slag met voorwaardelijke toegang in Azure Active Directory | Microsoft Docs
description: Voorwaardelijke toegang met behulp van een locatie voorwaarde testen.
services: active-directory
keywords: voorwaardelijke toegang tot apps, voorwaardelijke toegang met Azure AD, beveiligde toegang tot bedrijfsresources, beleidsregels voor voorwaardelijke toegang
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
ms.openlocfilehash: cd53e8be32d1e98aaf9f72177895871dba69df86
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="25160-104">Aan de slag met voorwaardelijke toegang in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25160-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="25160-105">Voorwaardelijke toegang is een functie van Azure Active Directory waarmee u kunt de voorwaarden waaronder gemachtigde gebruikers toegang uw apps tot hebben definiëren.</span><span class="sxs-lookup"><span data-stu-id="25160-105">Conditional access is a capability of Azure Active Directory that enables you to define conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="25160-106">In dit onderwerp vindt u instructies voor het testen van een voorwaardelijke toegang op basis van de voorwaarde van een locatie in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="25160-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="25160-107">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="25160-107">Scenario description</span></span>

<span data-ttu-id="25160-108">Een van de algemene vereisten in veel organisaties is het alleen meervoudige verificatie vereisen voor toegang tot apps die niet van het bedrijfsintranet wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="25160-108">One common requirement in many organizations is to only require multi-factor authentication for access to apps that is not performed from the corporate intranet.</span></span> <span data-ttu-id="25160-109">Met Azure Active Directory, kunt u eenvoudig deze doelstelling uitvoeren door het configureren van beleid voor voorwaardelijke toegang op basis van locatie.</span><span class="sxs-lookup"><span data-stu-id="25160-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="25160-110">Dit onderwerp vindt u gedetailleerde instructies voor het configureren van een gerelateerd beleid.</span><span class="sxs-lookup"><span data-stu-id="25160-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="25160-111">Het beleid maakt gebruik van [goedgekeurde IP-adressen](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) onderscheid maken tussen toegangspogingen tot van het bedrijf de intranet- en alle andere locaties.</span><span class="sxs-lookup"><span data-stu-id="25160-111">The policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) to distinguish between access attempts made from the corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="25160-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="25160-112">Prerequisites</span></span>

<span data-ttu-id="25160-113">Het scenario in dit onderwerp wordt ervan uitgegaan dat u bekend met de concepten die worden beschreven bent in [voorwaardelijke toegang van Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="25160-113">The scenario outlined in this topic assumes that you are familiar with the concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="25160-114">Als u wilt testen van dit scenario, moet u:</span><span class="sxs-lookup"><span data-stu-id="25160-114">To test this scenario, you need to:</span></span>

- <span data-ttu-id="25160-115">Een testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="25160-115">Create a test user</span></span> 

- <span data-ttu-id="25160-116">Een Azure AD Premium-licentie toewijzen aan de testgebruiker</span><span class="sxs-lookup"><span data-stu-id="25160-116">Assign an Azure AD Premium license to the test user</span></span>

- <span data-ttu-id="25160-117">Configureren van een beheerde app en uw testgebruiker toekennen</span><span class="sxs-lookup"><span data-stu-id="25160-117">Configure a managed app and assign your test user to it</span></span>

- <span data-ttu-id="25160-118">Goedgekeurde IP-adressen configureren</span><span class="sxs-lookup"><span data-stu-id="25160-118">Configure trusted IPs</span></span>

<span data-ttu-id="25160-119">Als u meer informatie over de goedgekeurde IP-adressen, Zie [goedgekeurde IP-adressen](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="25160-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="25160-120">Beleid configuratiestappen</span><span class="sxs-lookup"><span data-stu-id="25160-120">Policy configuration steps</span></span>

<span data-ttu-id="25160-121">**Ga voor het configureren van uw beleid voor voorwaardelijke toegang:**</span><span class="sxs-lookup"><span data-stu-id="25160-121">**To configure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="25160-122">In de Azure-portal op de navigatiebalk links, klikt u op **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="25160-122">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span></span> 

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="25160-124">Op de **Azure Active Directory** blade in de **beheren** sectie, klikt u op **voorwaardelijke toegang**.</span><span class="sxs-lookup"><span data-stu-id="25160-124">On the **Azure Active Directory** blade, in the **Manage** section, click **Conditional access**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="25160-126">Op de **voorwaardelijke toegang** blade openen de **nieuw** blade in de werkbalk bovenaan, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="25160-126">On the **Conditional Access** blade, to open the **New** blade, in the toolbar on the top, click **Add**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="25160-128">Op de **nieuw** blade in de **naam** textbox, typ een naam voor uw beleid.</span><span class="sxs-lookup"><span data-stu-id="25160-128">On the **New** blade, in the **Name** textbox, type a name for your policy.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="25160-130">In de **toewijzing** sectie, klikt u op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="25160-130">In the **Assignment** section, click **Users and groups**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="25160-132">Op de **gebruikers en groepen** blade, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="25160-132">On the **Users and groups** blade, perform the following steps:</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="25160-134">a.</span><span class="sxs-lookup"><span data-stu-id="25160-134">a.</span></span> <span data-ttu-id="25160-135">Klik op **gebruikers en groepen selecteren**.</span><span class="sxs-lookup"><span data-stu-id="25160-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="25160-136">b.</span><span class="sxs-lookup"><span data-stu-id="25160-136">b.</span></span> <span data-ttu-id="25160-137">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="25160-137">Click **Select**.</span></span>

    <span data-ttu-id="25160-138">c.</span><span class="sxs-lookup"><span data-stu-id="25160-138">c.</span></span> <span data-ttu-id="25160-139">Op de **Selecteer** blade uw testgebruiker selecteren en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="25160-139">On the **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="25160-140">d.</span><span class="sxs-lookup"><span data-stu-id="25160-140">d.</span></span> <span data-ttu-id="25160-141">Op de **gebruikers en groepen** blade, klikt u op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="25160-141">On the **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="25160-142">Op de **nieuw** blade openen de **Cloud-apps** blade in de **toewijzing** sectie, klikt u op **Cloud-apps**.</span><span class="sxs-lookup"><span data-stu-id="25160-142">On the **New** blade, to open the **Cloud apps** blade, in the **Assignment** section, click **Cloud apps**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="25160-144">Op de **Cloud-apps** blade, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="25160-144">On the **Cloud apps** blade, perform the following steps:</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="25160-146">a.</span><span class="sxs-lookup"><span data-stu-id="25160-146">a.</span></span> <span data-ttu-id="25160-147">Klik op **apps selecteren**.</span><span class="sxs-lookup"><span data-stu-id="25160-147">Click **Select apps**.</span></span>

    <span data-ttu-id="25160-148">b.</span><span class="sxs-lookup"><span data-stu-id="25160-148">b.</span></span> <span data-ttu-id="25160-149">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="25160-149">Click **Select**.</span></span>

    <span data-ttu-id="25160-150">c.</span><span class="sxs-lookup"><span data-stu-id="25160-150">c.</span></span> <span data-ttu-id="25160-151">Op de **Selecteer** blade uw cloud-app selecteren en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="25160-151">On the **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="25160-152">d.</span><span class="sxs-lookup"><span data-stu-id="25160-152">d.</span></span> <span data-ttu-id="25160-153">Op de **Cloud-apps** blade, klikt u op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="25160-153">On the **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="25160-154">Op de **nieuw** blade openen de **voorwaarden** blade in de **toewijzing** sectie, klikt u op **voorwaarden**.</span><span class="sxs-lookup"><span data-stu-id="25160-154">On the **New** blade, to open the **Conditions** blade, in the **Assignment** section, click **Conditions**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="25160-156">Op de **voorwaarden** blade openen de **locaties** blade, klikt u op **locaties**.</span><span class="sxs-lookup"><span data-stu-id="25160-156">On the **Conditions** blade, to open the **Locations** blade, click **Locations**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="25160-158">Op de **locaties** blade, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="25160-158">On the **Locations** blade, perform the following steps:</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="25160-160">a.</span><span class="sxs-lookup"><span data-stu-id="25160-160">a.</span></span> <span data-ttu-id="25160-161">Onder **configureren**, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="25160-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="25160-162">b.</span><span class="sxs-lookup"><span data-stu-id="25160-162">b.</span></span> <span data-ttu-id="25160-163">Onder **opnemen**, klikt u op **alle locaties**.</span><span class="sxs-lookup"><span data-stu-id="25160-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="25160-164">c.</span><span class="sxs-lookup"><span data-stu-id="25160-164">c.</span></span> <span data-ttu-id="25160-165">Klik op **uitsluiten**, en klik vervolgens op **alle goedgekeurde IP-adressen**.</span><span class="sxs-lookup"><span data-stu-id="25160-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="25160-167">d.</span><span class="sxs-lookup"><span data-stu-id="25160-167">d.</span></span> <span data-ttu-id="25160-168">Klik op **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="25160-168">Click **Done**.</span></span>

12. <span data-ttu-id="25160-169">Op de **voorwaarden** blade, klikt u op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="25160-169">On the **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="25160-170">Op de **nieuw** blade openen de **Grant** blade in de **besturingselementen** sectie, klikt u op **Grant**.</span><span class="sxs-lookup"><span data-stu-id="25160-170">On the **New** blade, to open the **Grant** blade, in the **Controls** section, click **Grant**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="25160-172">Op de **Grant** blade, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="25160-172">On the **Grant** blade, perform the following steps:</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="25160-174">a.</span><span class="sxs-lookup"><span data-stu-id="25160-174">a.</span></span> <span data-ttu-id="25160-175">Selecteer **meervoudige authenticatie**.</span><span class="sxs-lookup"><span data-stu-id="25160-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="25160-176">b.</span><span class="sxs-lookup"><span data-stu-id="25160-176">b.</span></span> <span data-ttu-id="25160-177">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="25160-177">Click **Select**.</span></span>

15. <span data-ttu-id="25160-178">Op de **nieuw** blade onder **beleid inschakelen**, klikt u op **op**.</span><span class="sxs-lookup"><span data-stu-id="25160-178">On the **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="25160-180">Op de **nieuw** blade, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="25160-180">On the **New** blade, click **Create**.</span></span>


## <a name="testing-the-policy"></a><span data-ttu-id="25160-181">Het beleid testen</span><span class="sxs-lookup"><span data-stu-id="25160-181">Testing the policy</span></span>

<span data-ttu-id="25160-182">Als u wilt testen van uw beleid, moet u toegang tot uw app vanaf een apparaat dat:</span><span class="sxs-lookup"><span data-stu-id="25160-182">To test your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="25160-183">Heeft een IP-adres dat binnen de geconfigureerde goedgekeurde IP-adressen</span><span class="sxs-lookup"><span data-stu-id="25160-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="25160-184">Heeft een IP-adres dat is niet binnen de geconfigureerde goedgekeurde IP-adressen</span><span class="sxs-lookup"><span data-stu-id="25160-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="25160-185">Multi-factor authentication-server zijn moet alleen tijdens een verbindingspoging die is gemaakt van een apparaat dat is niet binnen de geconfigureerde goedgekeurde IP-adressen vereist.</span><span class="sxs-lookup"><span data-stu-id="25160-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="25160-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="25160-186">Next steps</span></span>

<span data-ttu-id="25160-187">Als u meer informatie over voorwaardelijke toegang wilt, Zie [voorwaardelijke toegang van Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="25160-187">If you would like to learn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

