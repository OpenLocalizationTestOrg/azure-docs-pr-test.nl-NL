---
title: aaaEnable Microsoft Windows Hello voor bedrijven in uw organisatie | Microsoft Docs
description: Implementatie-instructies tooenable Microsoft Passport in uw organisatie.
services: active-directory
documentationcenter: 
keywords: Microsoft Passport configureren, Microsoft Windows Hello voor bedrijven-implementatie
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 6041f5916f606752bc55844b1b2d0a423b913cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a><span data-ttu-id="e580c-104">Schakel Microsoft Windows Hello voor bedrijven in uw organisatie</span><span class="sxs-lookup"><span data-stu-id="e580c-104">Enable Microsoft Windows Hello for Business in your organization</span></span>
<span data-ttu-id="e580c-105">Na [domein Windows 10-apparaten verbinding te maken met Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), Hallo na tooenable Microsoft Windows Hello voor bedrijven in uw organisatie:</span><span class="sxs-lookup"><span data-stu-id="e580c-105">After [connecting Windows 10 domain-joined devices with Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), do hello following tooenable Microsoft Windows Hello for Business in your organization:</span></span>

1. <span data-ttu-id="e580c-106">System Center Configuration Manager implementeren</span><span class="sxs-lookup"><span data-stu-id="e580c-106">Deploy System Center Configuration Manager</span></span>  
2. <span data-ttu-id="e580c-107">Configureren van beleidsinstellingen</span><span class="sxs-lookup"><span data-stu-id="e580c-107">Configure policy settings</span></span>
3. <span data-ttu-id="e580c-108">Hallo-certificaatprofiel configureren</span><span class="sxs-lookup"><span data-stu-id="e580c-108">Configure hello certificate profile</span></span>  

## <a name="deploy-system-center-configuration-manager"></a><span data-ttu-id="e580c-109">System Center Configuration Manager implementeren</span><span class="sxs-lookup"><span data-stu-id="e580c-109">Deploy System Center Configuration Manager</span></span>
<span data-ttu-id="e580c-110">toodeploy gebruikerscertificaten op basis van Windows Hello voor bedrijven-sleutels, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="e580c-110">toodeploy user certificates based on Windows Hello for Business keys, you need hello following:</span></span>

* <span data-ttu-id="e580c-111">**System Center Configuration Manager Current Branch** -u moet tooinstall versie 1606 of hoger.</span><span class="sxs-lookup"><span data-stu-id="e580c-111">**System Center Configuration Manager Current Branch** - You need tooinstall version 1606 or better.</span></span> <span data-ttu-id="e580c-112">Zie voor meer informatie, Hallo [documentatie voor System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) en [System Center Configuration Manager-teamblog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span><span class="sxs-lookup"><span data-stu-id="e580c-112">For more information, see hello [Documentation for System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) and [System Center Configuration Manager Team Blog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span></span>
* <span data-ttu-id="e580c-113">**Openbare-sleutelinfrastructuur (PKI)** -tooenable Microsoft Windows Hello voor bedrijven met behulp van gebruikerscertificaten, u moet beschikken over een PKI.</span><span class="sxs-lookup"><span data-stu-id="e580c-113">**Public key infrastructure (PKI)** - tooenable Microsoft Windows Hello for Business by using user certificates, you must have a PKI in place.</span></span> <span data-ttu-id="e580c-114">Als u niet hebt of als u niet dat toouse wilt ervan voor gebruikerscertificaten u een nieuwe domeincontroller met Windows Server 2016 bouwen 10551 (of hoger) geïnstalleerd kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="e580c-114">If you don’t have one, or you don’t want toouse it for user certificates, you can deploy a new domain controller that has Windows Server 2016 build 10551 (or better) installed.</span></span> <span data-ttu-id="e580c-115">Hallo stappen te volgen[een replica-domeincontroller installeren in een bestaand domein](https://technet.microsoft.com/library/jj574134.aspx) of te[een nieuw Active Directory-forest installeren als u een nieuwe omgeving](https://technet.microsoft.com/library/jj574166).</span><span class="sxs-lookup"><span data-stu-id="e580c-115">Follow hello steps too[install a replica domain controller in an existing domain](https://technet.microsoft.com/library/jj574134.aspx) or too[install a new Active Directory forest, if you're creating a new environment](https://technet.microsoft.com/library/jj574166).</span></span> <span data-ttu-id="e580c-116">(Hallo ISO's zijn beschikbaar voor downloaden op [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span><span class="sxs-lookup"><span data-stu-id="e580c-116">(hello ISOs are available for download on [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span></span>

## <a name="configure-policy-settings"></a><span data-ttu-id="e580c-117">Configureren van beleidsinstellingen</span><span class="sxs-lookup"><span data-stu-id="e580c-117">Configure policy settings</span></span>
<span data-ttu-id="e580c-118">tooconfigure hello Microsoft Windows Hello voor bedrijven-beleidsinstellingen, hebt u twee opties:</span><span class="sxs-lookup"><span data-stu-id="e580c-118">tooconfigure hello Microsoft Windows Hello for Business policy settings, you have two options:</span></span>

* <span data-ttu-id="e580c-119">Groepsbeleid in Active Directory</span><span class="sxs-lookup"><span data-stu-id="e580c-119">Group Policy in Active Directory</span></span> 
* <span data-ttu-id="e580c-120">Hallo System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="e580c-120">hello System Center Configuration Manager</span></span> 

<span data-ttu-id="e580c-121">Via Groepsbeleid in Active Directory is Hallo aanbevolen methode tooconfigure Microsoft Windows Hello voor bedrijven-instellingen voor beleid.</span><span class="sxs-lookup"><span data-stu-id="e580c-121">Using Group Policy in Active Directory is hello recommended method tooconfigure Microsoft Windows Hello for Business policy settings.</span></span> 

<span data-ttu-id="e580c-122">Gebruik van System Center Configuration Manager is Hallo voorkeur methode wanneer u deze ook toodeploy certificaten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e580c-122">Using System Center Configuration Manager is hello preferred method when you also use it toodeploy certificates.</span></span> <span data-ttu-id="e580c-123">Dit scenario:</span><span class="sxs-lookup"><span data-stu-id="e580c-123">This scenario:</span></span>

* <span data-ttu-id="e580c-124">Zorgt voor compatibiliteit met Hallo nieuwere implementatiescenario 's</span><span class="sxs-lookup"><span data-stu-id="e580c-124">Ensures compatibility with hello newer deployment scenarios</span></span>
* <span data-ttu-id="e580c-125">Aan de clientzijde Hallo Windows 10 versie 1607 of hoger vereist.</span><span class="sxs-lookup"><span data-stu-id="e580c-125">Requires on hello client side Windows 10 Version 1607 or better.</span></span>

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a><span data-ttu-id="e580c-126">Configureer Microsoft Windows Hello voor bedrijven via Groepsbeleid in Active Directory</span><span class="sxs-lookup"><span data-stu-id="e580c-126">Configure Microsoft Windows Hello for Business via group policy in Active Directory</span></span>
<span data-ttu-id="e580c-127">**Stappen**:</span><span class="sxs-lookup"><span data-stu-id="e580c-127">**Steps**:</span></span>

1. <span data-ttu-id="e580c-128">Open Serverbeheer en te navigeren**extra** > **Group Policy Management**.</span><span class="sxs-lookup"><span data-stu-id="e580c-128">Open Server Manager, and navigate too**Tools** > **Group Policy Management**.</span></span>
2. <span data-ttu-id="e580c-129">Navigeer via Group Policy Management toohello domeinknooppunt die overeenkomt met toohello domein waarin u Azure AD Join tooenable wilt.</span><span class="sxs-lookup"><span data-stu-id="e580c-129">From Group Policy Management, navigate toohello domain node that corresponds toohello domain in which you want tooenable Azure AD Join.</span></span>
3. <span data-ttu-id="e580c-130">Met de rechtermuisknop op **Group Policy Objects**, en selecteer **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="e580c-130">Right-click **Group Policy Objects**, and select **New**.</span></span> <span data-ttu-id="e580c-131">Geef uw Group Policy Object een naam, bijvoorbeeld inschakelen Windows Hello voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="e580c-131">Give your Group Policy Object a name, for example, Enable Windows Hello for Business.</span></span> <span data-ttu-id="e580c-132">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e580c-132">Click **OK**.</span></span>
4. <span data-ttu-id="e580c-133">Met de rechtermuisknop op uw nieuwe groepsbeleidsobject en selecteer vervolgens **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="e580c-133">Right-click your new Group Policy Object, and then select **Edit**.</span></span>
5. <span data-ttu-id="e580c-134">Navigeer te**Computerconfiguratie** > **beleid** > **Beheersjablonen** > **Windows Onderdelen** > **Windows Hello voor bedrijven**.</span><span class="sxs-lookup"><span data-stu-id="e580c-134">Navigate too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Hello for Business**.</span></span>
6. <span data-ttu-id="e580c-135">Met de rechtermuisknop op **inschakelen Windows Hello voor bedrijven**, en selecteer vervolgens **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="e580c-135">Right-click **Enable Windows Hello for Business**, and then select **Edit**.</span></span>
7. <span data-ttu-id="e580c-136">Selecteer Hallo **ingeschakeld** keuzerondje en klik vervolgens op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="e580c-136">Select hello **Enabled** option button, and then click **Apply**.</span></span> <span data-ttu-id="e580c-137">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e580c-137">Click **OK**.</span></span>
8. <span data-ttu-id="e580c-138">U kunt nu Hallo Group Policy Object tooa locatie van uw keuze koppelen.</span><span class="sxs-lookup"><span data-stu-id="e580c-138">You can now link hello Group Policy Object tooa location of your choice.</span></span> <span data-ttu-id="e580c-139">tooenable dit beleid voor alle Hallo domein Windows 10-apparaten in uw organisatie, koppeling Hallo Groepsbeleid toohello domein.</span><span class="sxs-lookup"><span data-stu-id="e580c-139">tooenable this policy for all of hello domain-joined Windows 10 devices in your organization, link hello Group Policy toohello domain.</span></span> <span data-ttu-id="e580c-140">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e580c-140">For example:</span></span>
   * <span data-ttu-id="e580c-141">Een specifieke organisatie-eenheid (OE) in Active Directory waarop Windows 10-computers domein geplaatst worden</span><span class="sxs-lookup"><span data-stu-id="e580c-141">A specific organizational unit (OU) in Active Directory where Windows 10 domain-joined computers will be located</span></span>
   * <span data-ttu-id="e580c-142">Een specifieke beveiligingsgroep met Windows 10 domeincomputers die automatisch wordt geregistreerd met Azure AD</span><span class="sxs-lookup"><span data-stu-id="e580c-142">A specific security group that contains Windows 10 domain-joined computers that will be automatically registered with Azure AD</span></span>

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a><span data-ttu-id="e580c-143">Windows Hello voor bedrijven met System Center Configuration Manager configureren</span><span class="sxs-lookup"><span data-stu-id="e580c-143">Configure Windows Hello for Business using System Center Configuration Manager</span></span>
<span data-ttu-id="e580c-144">**Stappen**:</span><span class="sxs-lookup"><span data-stu-id="e580c-144">**Steps**:</span></span>

1. <span data-ttu-id="e580c-145">Open Hallo **System Center Configuration Manager**, en navigeert u vervolgens te**activa en naleving > instellingen voor naleving > toegang tot bedrijfsbronnen > Windows Hello voor bedrijven-profielen**.</span><span class="sxs-lookup"><span data-stu-id="e580c-145">Open hello **System Center Configuration Manager**, and then navigate too**Assets & Compliance > Compliance Settings > Company Resource Access > Windows Hello for Business Profiles**.</span></span>
   
    ![Windows Hello voor bedrijven configureren](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. <span data-ttu-id="e580c-147">Klik in de werkbalk bovenaan Hallo Hallo op **Windows Hello voor bedrijven-profiel maken**.</span><span class="sxs-lookup"><span data-stu-id="e580c-147">In hello toolbar on hello top, click **Create Windows Hello for business Profile**.</span></span>
   
    ![Windows Hello voor bedrijven configureren](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. <span data-ttu-id="e580c-149">Op Hallo **algemene** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="e580c-149">On hello **General** dialog, perform hello following steps:</span></span>
   
    ![Windows Hello voor bedrijven configureren](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    <span data-ttu-id="e580c-151">a.</span><span class="sxs-lookup"><span data-stu-id="e580c-151">a.</span></span> <span data-ttu-id="e580c-152">In Hallo **naam** textbox, typ een naam voor uw profiel bijvoorbeeld **mijn WHfB profiel**.</span><span class="sxs-lookup"><span data-stu-id="e580c-152">In hello **Name** textbox, type a name for your profile, for example, **My WHfB Profile**.</span></span>
   
    <span data-ttu-id="e580c-153">b.</span><span class="sxs-lookup"><span data-stu-id="e580c-153">b.</span></span> <span data-ttu-id="e580c-154">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="e580c-154">Click **Next**.</span></span>
4. <span data-ttu-id="e580c-155">Op Hallo **ondersteunde Platforms** dialoogvenster, selecteer Hallo-platforms die worden ingericht met dit Windows Hello voor bedrijven-profiel en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e580c-155">On hello **Supported Platforms** dialog, select hello platforms that will be provisioned with this Windows Hello for business profile, and then click **Next**.</span></span>
   
    ![Windows Hello voor bedrijven configureren](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. <span data-ttu-id="e580c-157">Op Hallo **instellingen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="e580c-157">On hello **Settings** dialog, perform hello following steps:</span></span>
   
    ![Windows Hello voor bedrijven configureren](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    <span data-ttu-id="e580c-159">a.</span><span class="sxs-lookup"><span data-stu-id="e580c-159">a.</span></span> <span data-ttu-id="e580c-160">Als **configureren Windows Hello voor bedrijven**, selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="e580c-160">As **Configure Windows Hello for Business**, select **Enabled**.</span></span>
   
    <span data-ttu-id="e580c-161">b.</span><span class="sxs-lookup"><span data-stu-id="e580c-161">b.</span></span> <span data-ttu-id="e580c-162">Als **Trusted Platform Module (TPM) gebruiken**, selecteer **vereist**.</span><span class="sxs-lookup"><span data-stu-id="e580c-162">As **Use a Trusted Platform Module (TPM)**, select **Required**.</span></span> 
   
    <span data-ttu-id="e580c-163">c.</span><span class="sxs-lookup"><span data-stu-id="e580c-163">c.</span></span> <span data-ttu-id="e580c-164">Als **verificatiemethode**, selecteer **op basis van certificaten**.</span><span class="sxs-lookup"><span data-stu-id="e580c-164">As **Authentication method**, select **Certificate-based**.</span></span>
   
    <span data-ttu-id="e580c-165">d.</span><span class="sxs-lookup"><span data-stu-id="e580c-165">d.</span></span> <span data-ttu-id="e580c-166">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="e580c-166">Click **Next**.</span></span>
6. <span data-ttu-id="e580c-167">Op Hallo **samenvatting** dialoogvenster, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e580c-167">On hello **Summary** dialog, click **Next**.</span></span>
7. <span data-ttu-id="e580c-168">Op Hallo **voltooiing** dialoogvenster, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="e580c-168">On hello **Completion** dialog, click **Close**.</span></span>
8. <span data-ttu-id="e580c-169">Klik in de werkbalk bovenaan Hallo Hallo op **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="e580c-169">In hello toolbar on hello top, click **Deploy**.</span></span>
   
    ![Windows Hello voor bedrijven configureren](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-hello-certificate-profile"></a><span data-ttu-id="e580c-171">Hallo-certificaatprofiel configureren</span><span class="sxs-lookup"><span data-stu-id="e580c-171">Configure hello certificate profile</span></span>
<span data-ttu-id="e580c-172">Als u verificatie op basis van certificaten voor lokale verificatie gebruikt, kunt u tooconfigure nodig en een certificaatprofiel implementeert.</span><span class="sxs-lookup"><span data-stu-id="e580c-172">If you are using certificate-based authentication for on-premises authentication, you need tooconfigure and deploy a certificate profile.</span></span> <span data-ttu-id="e580c-173">Deze taak moet u tooset van een NDES-server en de siterol Certificaatregistratiepunt in Hallo System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="e580c-173">This task requires you tooset up an NDES server and Certificate Registration Point site role in hello System Center Configuration Manager.</span></span> <span data-ttu-id="e580c-174">Zie voor meer informatie, Hallo [vereisten voor Certificaatprofielen in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span><span class="sxs-lookup"><span data-stu-id="e580c-174">For more details, see hello [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span></span>

1. <span data-ttu-id="e580c-175">Open Hallo **System Center Configuration Manager**, en navigeert u vervolgens te**activa en naleving > instellingen voor naleving > toegang tot bedrijfsbronnen > Certificaatprofielen**.</span><span class="sxs-lookup"><span data-stu-id="e580c-175">Open hello **System Center Configuration Manager**, and then navigate too**Assets & Compliance > Compliance Settings > Company Resource Access > Certificate Profiles**.</span></span>
2. <span data-ttu-id="e580c-176">Selecteer een sjabloon met een smartcard aanmelden uitgebreide-sleutelgebruik (EKU).</span><span class="sxs-lookup"><span data-stu-id="e580c-176">Select a template that has Smart Card sign-in extended key usage (EKU).</span></span>

<span data-ttu-id="e580c-177">Op Hallo **SCEP-registratie** pagina Hallo certificaatprofiel, moet u toochoose **tooPassport voor Work, anders niet installeren** als Hallo **Key Storage Provider**.</span><span class="sxs-lookup"><span data-stu-id="e580c-177">On hello **SCEP Enrollment** page of hello certificate profile, you need toochoose **Install tooPassport for Work otherwise fail** as hello **Key Storage Provider**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e580c-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e580c-178">Next steps</span></span>
* [<span data-ttu-id="e580c-179">Windows 10 voor Hallo ondernemingen: manieren toouse apparaten for work.</span><span class="sxs-lookup"><span data-stu-id="e580c-179">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="e580c-180">Cloud-mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join uitbreiden</span><span class="sxs-lookup"><span data-stu-id="e580c-180">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="e580c-181">Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren</span><span class="sxs-lookup"><span data-stu-id="e580c-181">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* <span data-ttu-id="e580c-182">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)</span><span class="sxs-lookup"><span data-stu-id="e580c-182">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)</span></span>
* [<span data-ttu-id="e580c-183">Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring</span><span class="sxs-lookup"><span data-stu-id="e580c-183">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="e580c-184">Azure AD Join instellen</span><span class="sxs-lookup"><span data-stu-id="e580c-184">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

