---
title: 'Azure Active Directory B2C: ADFS als SAML-identiteitsprovider gebruik van aangepast beleid toevoegen'
description: Een hoe-tooarticle over het instellen van ADFS-2016 met SAML-protocol en aangepaste beleidsregels
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a><span data-ttu-id="ec43e-103">Azure Active Directory B2C: ADFS als SAML-identiteitsprovider gebruik van aangepast beleid toevoegen</span><span class="sxs-lookup"><span data-stu-id="ec43e-103">Azure Active Directory B2C: Add ADFS as a SAML identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="ec43e-104">Dit artikel ziet u hoe tooenable aanmelden voor gebruikers van AD FS-account door gebruik van Hallo [aangepast beleid](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="ec43e-104">This article shows you how tooenable sign-in for users from ADFS account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec43e-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ec43e-105">Prerequisites</span></span>

<span data-ttu-id="ec43e-106">Volledige Hallo stappen voor het Hallo [aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="ec43e-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="ec43e-107">Deze stappen omvatten:</span><span class="sxs-lookup"><span data-stu-id="ec43e-107">These steps include:</span></span>

1.  <span data-ttu-id="ec43e-108">Maken van een Relying Party Trust ADFS.</span><span class="sxs-lookup"><span data-stu-id="ec43e-108">Creating an ADFS Relying Party Trust.</span></span>
2.  <span data-ttu-id="ec43e-109">Hallo ADFS Relying Party Trust certificaat tooAzure AD B2C wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ec43e-109">Adding hello ADFS Relying Party Trust certificate tooAzure AD B2C.</span></span>
3.  <span data-ttu-id="ec43e-110">Claims provider tooa beleid toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ec43e-110">Adding claims provider tooa policy.</span></span>
4.  <span data-ttu-id="ec43e-111">Account van de AD FS registreren Hallo claims provider tooa gebruiker reis.</span><span class="sxs-lookup"><span data-stu-id="ec43e-111">Registering hello ADFS account claims provider tooa user journey.</span></span>
5.  <span data-ttu-id="ec43e-112">Uploaden Hallo beleid tooan Azure AD B2C-tenant en testen.</span><span class="sxs-lookup"><span data-stu-id="ec43e-112">Uploading hello policy tooan Azure AD B2C tenant and test it.</span></span>

## <a name="toocreate-a-claims-aware-relying-party-trust"></a><span data-ttu-id="ec43e-113">een claimbewuste Relying Party Trust toocreate</span><span class="sxs-lookup"><span data-stu-id="ec43e-113">toocreate a claims-aware Relying Party Trust</span></span>

<span data-ttu-id="ec43e-114">toouse ADFS als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een AD FS vertrouwen voor Relying Party toocreate en leveren met de juiste parameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="ec43e-114">toouse ADFS as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an ADFS Relying Party Trust and supply it with hello right parameters.</span></span>

<span data-ttu-id="ec43e-115">tooadd een nieuwe relying party trust met behulp van Hallo AD FS-beheermodule en Hallo-instellingen handmatig configureren uitvoeren Hallo procedure te volgen op een federatieserver.</span><span class="sxs-lookup"><span data-stu-id="ec43e-115">tooadd a new relying party trust by using hello AD FS Management snap-in and manually configure hello settings, perform hello following procedure on a federation server.</span></span>

<span data-ttu-id="ec43e-116">Lidmaatschap van **beheerders**, of gelijkwaardig op de lokale computer Hallo is de minimale vereiste toocomplete Hallo deze procedure.</span><span class="sxs-lookup"><span data-stu-id="ec43e-116">Membership in **Administrators**, or equivalent, on hello local computer is hello minimum required toocomplete this procedure.</span></span> <span data-ttu-id="ec43e-117">Bekijk de details over het gebruik van de relevante Hallo-accounts en groepslidmaatschappen op [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)</span><span class="sxs-lookup"><span data-stu-id="ec43e-117">Review details about using hello appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)</span></span>

1.  <span data-ttu-id="ec43e-118">Klik in Serverbeheer op **extra**, en selecteer vervolgens **ADFS Management**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-118">In Server Manager, click **Tools**, and then select **ADFS Management**.</span></span>

2.  <span data-ttu-id="ec43e-119">Klik op **Add Relying Party Trust**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-119">Click on **Add Relying Party Trust**.</span></span>
    <span data-ttu-id="ec43e-120">![Vertrouwensrelatie van Relying Party toevoegen](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span><span class="sxs-lookup"><span data-stu-id="ec43e-120">![Add Relying Party Trust](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span></span>

3.  <span data-ttu-id="ec43e-121">Op Hallo **Welkom** pagina **Claims aware** en klik op **Start**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-121">On hello **Welcome** page, choose **Claims aware** and click **Start**.</span></span>
    <span data-ttu-id="ec43e-122">![Kies op de welkomstpagina hello, Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span><span class="sxs-lookup"><span data-stu-id="ec43e-122">![On hello Welcome page, choose Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span></span>
4.  <span data-ttu-id="ec43e-123">Op Hallo **gegevensbron selecteren** pagina, klikt u op **gegevens over Hallo relying party handmatig invoeren**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-123">On hello **Select Data Source** page, click **Enter data about hello relying party manually**, and then click **Next**.</span></span>
    <span data-ttu-id="ec43e-124">![Gegevens over de relying party Hallo invoeren](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span><span class="sxs-lookup"><span data-stu-id="ec43e-124">![Enter data about hello relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span></span>

5.  <span data-ttu-id="ec43e-125">Op Hallo **weergavenaam opgeven** pagina, typ een naam in **weergavenaam**onder **notities** Typ een beschrijving voor deze vertrouwensrelatie van relying party en klik vervolgens op **volgende** .</span><span class="sxs-lookup"><span data-stu-id="ec43e-125">On hello **Specify Display Name** page, type a name in **Display name**, under **Notes** type a description for this relying party trust, and then click **Next**.</span></span>
    <span data-ttu-id="ec43e-126">![Geef de weergavenaam en -opmerkingen](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span><span class="sxs-lookup"><span data-stu-id="ec43e-126">![Specify Display Name and notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span></span>
6.  <span data-ttu-id="ec43e-127">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="ec43e-127">Optional.</span></span> <span data-ttu-id="ec43e-128">Als er een certificaat met optionele tokenversleuteling, klikt u vervolgens op Hallo **certificaat configureren** pagina, klikt u op **Bladeren** toolocate uw certificaatbestand en klik vervolgens op **volgende** .</span><span class="sxs-lookup"><span data-stu-id="ec43e-128">If you have an optional token encryption certificate, then on hello **Configure Certificate** page, click **Browse** toolocate your certificate file, and then click **Next**.</span></span>
    <span data-ttu-id="ec43e-129">![Certificaat configureren](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span><span class="sxs-lookup"><span data-stu-id="ec43e-129">![Configure Certificate](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span></span>
7.  <span data-ttu-id="ec43e-130">Op Hallo **URL configureren** pagina, selecteer Hallo **ondersteuning voor Hallo SAML 2.0 WebSSO protocol inschakelen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="ec43e-130">On hello **Configure URL** page, select hello **Enable support for hello SAML 2.0 WebSSO protocol** check box.</span></span> <span data-ttu-id="ec43e-131">Onder **Relying party SAML 2.0 SSO service URL**, typt u Hallo Security Assertion Markup Language (SAML) service-eindpunt-URL voor deze relying party trust en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-131">Under **Relying party SAML 2.0 SSO service URL**, type hello Security Assertion Markup Language (SAML) service endpoint URL for this relying party trust, and then click **Next**.</span></span>  <span data-ttu-id="ec43e-132">Voor Hallo **Relying party SAML 2.0 SSO service URL**, plak Hallo `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span><span class="sxs-lookup"><span data-stu-id="ec43e-132">For hello **Relying party SAML 2.0 SSO service URL**, paste hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span></span> <span data-ttu-id="ec43e-133">{Tenant} vervangen door de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com) en Hallo {beleid} vervangen door de naam van uw uitbreidingen beleid (bijvoorbeeld B2C_1A_TrustFrameworkExtensions).</span><span class="sxs-lookup"><span data-stu-id="ec43e-133">Replace {tenant} with your tenant's name (for example, contosob2c.onmicrosoft.com), and replace hello {policy} with your extensions policy name (for example, B2C_1A_TrustFrameworkExtensions).</span></span>
    > [!IMPORTANT]
    ><span data-ttu-id="ec43e-134">Hallo beleidsnaam is Hallo een die signup_or_signin beleid eigenschappen overneemt van, in dit geval is: `B2C_1A_TrustFrameworkExtensions`.</span><span class="sxs-lookup"><span data-stu-id="ec43e-134">hello policy name  is hello one that signup_or_signin policy inherits from, in this case it is: `B2C_1A_TrustFrameworkExtensions`.</span></span>
    ><span data-ttu-id="ec43e-135">Bijvoorbeeld Hallo-URL is: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-135">For example hello URL could be:   https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span></span>

    ![Relying party SAML 2.0 SSO service URL](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. <span data-ttu-id="ec43e-137">Op Hallo **id's configureren** pagina, geeft u Hallo dezelfde URL als de vorige stap hello, klikt u op **toevoegen** tooadd ze toohello lijst en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-137">On hello **Configure Identifiers** page, specify hello same URL as hello previous step, click **Add** tooadd them toohello list, and then click **Next**.</span></span>
    <span data-ttu-id="ec43e-138">![Relying party trust-id 's](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span><span class="sxs-lookup"><span data-stu-id="ec43e-138">![Relying party trust identifiers](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span></span>
9.  <span data-ttu-id="ec43e-139">Op Hallo **beleid voor toegangsbeheer kiezen** selecteert u een beleid en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-139">On hello **Choose Access Control Policy** select a policy and click **Next**.</span></span>
    <span data-ttu-id="ec43e-140">![Beleid voor toegangsbeheer kiezen](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span><span class="sxs-lookup"><span data-stu-id="ec43e-140">![Choose Access Control Policy](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span></span>
10.  <span data-ttu-id="ec43e-141">Op Hallo **tooAdd vertrouwensrelatie gereed** pagina, Hallo instellingen bekijken en klik vervolgens op **volgende** toosave de relying party trust informatie.</span><span class="sxs-lookup"><span data-stu-id="ec43e-141">On hello **Ready tooAdd Trust** page, review hello settings, and then click **Next** toosave your relying party trust information.</span></span>
    <span data-ttu-id="ec43e-142">![Sla uw relying party trust-gegevens](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span><span class="sxs-lookup"><span data-stu-id="ec43e-142">![Save your relying party trust information](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span></span>
11.  <span data-ttu-id="ec43e-143">Op Hallo **voltooien** pagina, klikt u op **sluiten**, met deze actie wordt automatisch Hallo **Claimregels bewerken** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ec43e-143">On hello **Finish** page, click **Close**, this action automatically displays hello **Edit Claim Rules** dialog box.</span></span>
    <span data-ttu-id="ec43e-144">![Claimregels bewerken](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span><span class="sxs-lookup"><span data-stu-id="ec43e-144">![Edit Claim Rules](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span></span>
12. <span data-ttu-id="ec43e-145">Klik op **regel toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-145">Click **Add Rule**.</span></span>  
      <span data-ttu-id="ec43e-146">![Nieuwe regel toevoegen](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span><span class="sxs-lookup"><span data-stu-id="ec43e-146">![Add new rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span></span>
13.  <span data-ttu-id="ec43e-147">In **claimregelsjabloon**, selecteer **verzenden LDAP-kenmerken als claims**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-147">In **Claim rule template**, select **Send LDAP attributes as claims**.</span></span>
    <span data-ttu-id="ec43e-148">![Verzenden van LDAP-kenmerken als claims sjabloonregel selecteren](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span><span class="sxs-lookup"><span data-stu-id="ec43e-148">![Select Send LDAP attributes as claims template rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span></span>
14.  <span data-ttu-id="ec43e-149">Geef **naam Claimregel**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-149">Provide **Claim rule name**.</span></span> <span data-ttu-id="ec43e-150">Voor Hallo **kenmerkopslag** Selecteer **Active Directory selecteren** Hallo na claims toevoegen en klik vervolgens op **voltooien** en **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-150">For hello **Attribute store** select **Select Active Directory** Add hello following claims, then click **Finish** and **OK**.</span></span>
    <span data-ttu-id="ec43e-151">![Eigenschappen van de regel instellen](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span><span class="sxs-lookup"><span data-stu-id="ec43e-151">![Set rule properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span></span>
15.  <span data-ttu-id="ec43e-152">Selecteer in Serverbeheer **Relying Party-vertrouwensrelaties** vervolgens Selecteer Hallo relying party trust u hebt gemaakt en klik op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-152">In Server Manager, select **Relying Party Trusts** then select hello relying party trust you created and click **Properties**.</span></span>
    <span data-ttu-id="ec43e-153">![Eigenschappen van relying party bewerken](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span><span class="sxs-lookup"><span data-stu-id="ec43e-153">![Relying party edit properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span></span>
16.  <span data-ttu-id="ec43e-154">Een relying party trust (B2C Demo) eigenschappen venster Klik Hallo **handtekening** tabblad en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-154">One hello relying party trust (B2C Demo) properties window click **Signature** tab and click **Add**.</span></span>  
    <span data-ttu-id="ec43e-155">![Set-handtekening](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span><span class="sxs-lookup"><span data-stu-id="ec43e-155">![Set signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span></span>
17.  <span data-ttu-id="ec43e-156">Uw handtekeningcertificaat (.cert-bestand, zonder persoonlijke sleutel) toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ec43e-156">Add your signature certificate (.cert file, without private key).</span></span>  
    ![Uw handtekeningcertificaat toevoegen](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  <span data-ttu-id="ec43e-158">Klik op Hallo relying party trust (B2C Demo) van het eigenschappenvenster **Geavanceerd** tabblad en wijzig Hallo **veilige hash-algoritme** te**SHA-1**, klikt u op **Ok**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-158">On hello relying party trust (B2C Demo) properties window click **Advanced** tab and change hello **Secure hash algorithm** too**SHA-1**, Click **Ok**.</span></span>  
    <span data-ttu-id="ec43e-159">![Secure hash algorithm tooSHA-1 instellen](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span><span class="sxs-lookup"><span data-stu-id="ec43e-159">![Set secure hash algorithm tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span></span>

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="ec43e-160">Hallo ADFS account toepassing sleutel tooAzure AD B2C toevoegen</span><span class="sxs-lookup"><span data-stu-id="ec43e-160">Add hello ADFS account application key tooAzure AD B2C</span></span>
<span data-ttu-id="ec43e-161">Federatie met AD FS-accounts vereist een clientgeheim voor AD FS-account tootrust Azure AD B2C namens Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ec43e-161">Federation with ADFS accounts requires a client secret for ADFS account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="ec43e-162">U moet uw ADFS-certificaat toostore in uw Azure AD B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="ec43e-162">You need toostore your ADFS certificate in your Azure AD B2C tenant.</span></span> 

1.  <span data-ttu-id="ec43e-163">Ga tooyour Azure AD B2C-tenant en selecteer **B2C-instellingen** > **identiteit ervaring Framework**</span><span class="sxs-lookup"><span data-stu-id="ec43e-163">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="ec43e-164">Selecteer **beleid sleutels** tooview Hallo sleutels die beschikbaar zijn in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="ec43e-164">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="ec43e-165">Klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-165">Click **+Add**.</span></span>
4.  <span data-ttu-id="ec43e-166">Voor **opties**, gebruik **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-166">For **Options**, use **Upload**.</span></span>
5.  <span data-ttu-id="ec43e-167">Voor **naam**, gebruik `ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="ec43e-167">For **Name**, use `ADFSSamlCert`.</span></span>  
    <span data-ttu-id="ec43e-168">Hallo voorvoegsel `B2C_1A_` kunnen automatisch worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ec43e-168">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="ec43e-169">In het Hallo-bestand uploaden ** selecteert u het PFX-certificaatbestand met persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="ec43e-169">In hello File upload,** select your certificate .pfx file with private key.</span></span> <span data-ttu-id="ec43e-170">Opmerking: dit certificaat (met de persoonlijke sleutel Hallo) moet Hallo dezelfde een uitgegeven en die worden gebruikt voor Hallo ADFS relying party.</span><span class="sxs-lookup"><span data-stu-id="ec43e-170">Note: this certificate (with hello private key) should be hello same one that issued and used for hello ADFS relying party.</span></span>
<span data-ttu-id="ec43e-171">![Beleidssleutel uploaden](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span><span class="sxs-lookup"><span data-stu-id="ec43e-171">![Upload policy key](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span></span>
7.  <span data-ttu-id="ec43e-172">Klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-172">Click **Create**</span></span>
8.  <span data-ttu-id="ec43e-173">Bevestig dat u hebt gemaakt dat Hallo sleutel `B2C_1A_ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="ec43e-173">Confirm that you've created hello key `B2C_1A_ADFSSamlCert`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="ec43e-174">Toevoegen van een claimprovider in de uitbreiding beleid</span><span class="sxs-lookup"><span data-stu-id="ec43e-174">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="ec43e-175">Als u wilt dat gebruikers toosign in met behulp van AD FS-account, moet u toodefine ADFS-account als een claimprovider.</span><span class="sxs-lookup"><span data-stu-id="ec43e-175">If you want users toosign in by using ADFS account, you need toodefine ADFS account as a claims provider.</span></span> <span data-ttu-id="ec43e-176">Met andere woorden, moet u een eindpunt dat Azure AD B2C met communiceert toospecify.</span><span class="sxs-lookup"><span data-stu-id="ec43e-176">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="ec43e-177">Hallo-eindpunt biedt een set claims die worden gebruikt door Azure AD B2C-tooverify die een specifieke gebruiker is geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="ec43e-177">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="ec43e-178">ADFS definiëren als een claimprovider door toe te voegen `<ClaimsProvider>` knooppunt in het beleidsbestand extensie:</span><span class="sxs-lookup"><span data-stu-id="ec43e-178">Define ADFS as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="ec43e-179">Bestand met beleidsregel van Hallo-extensie (TrustFrameworkExtensions.xml) openen vanuit uw werkmap.</span><span class="sxs-lookup"><span data-stu-id="ec43e-179">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="ec43e-180">Als u een XML-editor moet [Visual Studio Code probeert](https://code.visualstudio.com/download), een lichtgewicht platformoverschrijdende-editor.</span><span class="sxs-lookup"><span data-stu-id="ec43e-180">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2. <span data-ttu-id="ec43e-181">Hallo zoeken `<ClaimsProviders>` sectie</span><span class="sxs-lookup"><span data-stu-id="ec43e-181">Find hello `<ClaimsProviders>` section</span></span>
3. <span data-ttu-id="ec43e-182">Toevoegen van de volgende XML-fragment onder Hallo Hallo `ClaimsProviders` element en vervang `identityProvider` met uw DNS (willekeurige waarde die aangeeft van uw domein) en Hallo bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="ec43e-182">Add hello following XML snippet under hello `ClaimsProviders` element and replace `identityProvider` with your DNS (Arbitrary value that indicates your domain), and save hello file.</span></span> 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="ec43e-183">Hallo ADFS account claims provider tooSign up registreren of aanmelden gebruiker reis</span><span class="sxs-lookup"><span data-stu-id="ec43e-183">Register hello ADFS account claims provider tooSign up or Sign in user journey</span></span>
<span data-ttu-id="ec43e-184">Op dit moment is Hallo id-provider ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ec43e-184">At this point, hello identity provider has been set up.</span></span>  <span data-ttu-id="ec43e-185">Het is echter niet beschikbaar in een van de Hallo sign-up-to-date/aanmelden schermen.</span><span class="sxs-lookup"><span data-stu-id="ec43e-185">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="ec43e-186">Nu u tooadd Hallo ADFS-account-id-provider tooyour gebruiker moet `SignUpOrSignIn` traject van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ec43e-186">Now you need tooadd hello ADFS account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="ec43e-187">toomake deze beschikbaar, maken we een duplicaat van een bestaande sjabloon gebruiker reis.</span><span class="sxs-lookup"><span data-stu-id="ec43e-187">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="ec43e-188">Vervolgens wijzigen we deze zodat het Hallo ADFS-identiteitsprovider omvat:</span><span class="sxs-lookup"><span data-stu-id="ec43e-188">Then, we modify it so it includes hello ADFS identity provider:</span></span>
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  <span data-ttu-id="ec43e-189">Open base Hallo-bestand van uw beleid (bijvoorbeeld TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="ec43e-189">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="ec43e-190">Hallo zoeken `<UserJourneys>` element en kopieer Hallo volledige inhoud van `<UserJourneys>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="ec43e-190">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="ec43e-191">Hallo-extensiebestand (bijvoorbeeld TrustFrameworkExtensions.xml) openen en zoeken van Hallo `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="ec43e-191">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="ec43e-192">Als Hallo element niet bestaat, Voeg een.</span><span class="sxs-lookup"><span data-stu-id="ec43e-192">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="ec43e-193">Hallo volledige inhoud van plakken `<UserJournesy>` knooppunt dat u hebt gekopieerd als een onderliggend element van Hallo `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="ec43e-193">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="ec43e-194">Hallo-knop weergave</span><span class="sxs-lookup"><span data-stu-id="ec43e-194">Display hello button</span></span>
<span data-ttu-id="ec43e-195">Hallo `<ClaimsProviderSelections>` element Hallo lijst met opties voor de selectie van claims provider en de volgorde gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="ec43e-195">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="ec43e-196">`<ClaimsProviderSelection>`element is vergelijkbaar tooan identiteit provider knop op een pagina sign-up-to-date/aanmelden.</span><span class="sxs-lookup"><span data-stu-id="ec43e-196">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="ec43e-197">Als u een `<ClaimsProviderSelection>` element voor AD FS-account, een nieuwe knop wordt weergegeven wanneer een gebruiker op de pagina Hallo terechtkomt.</span><span class="sxs-lookup"><span data-stu-id="ec43e-197">If you add a `<ClaimsProviderSelection>` element for  ADFS account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="ec43e-198">tooadd dit element:</span><span class="sxs-lookup"><span data-stu-id="ec43e-198">tooadd this element:</span></span>

1.  <span data-ttu-id="ec43e-199">Hallo zoeken `<UserJourney>` knooppunt met `Id="SignUpOrSignIn"` in Hallo gebruiker reis die u hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="ec43e-199">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="ec43e-200">Zoek Hallo `<OrchestrationStep>` knooppunt bevat`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="ec43e-200">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="ec43e-201">Plaats de volgende XML-fragment onder `<ClaimsProviderSelections>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="ec43e-201">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="ec43e-202">Koppeling Hallo knop tooan actie</span><span class="sxs-lookup"><span data-stu-id="ec43e-202">Link hello button tooan action</span></span>

<span data-ttu-id="ec43e-203">Nu u een knop hebt geïmplementeerd, moet u toolink het tooan in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="ec43e-203">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="ec43e-204">Hallo-actie is in dit geval voor Azure AD B2C toocommunicate met AD FS-account tooreceive een token.</span><span class="sxs-lookup"><span data-stu-id="ec43e-204">hello action, in this case, is for Azure AD B2C toocommunicate with ADFS account tooreceive a token.</span></span> <span data-ttu-id="ec43e-205">Koppeling Hallo knop tooan actie door Hallo technische profiel voor de claimprovider van uw AD FS-account koppelen:</span><span class="sxs-lookup"><span data-stu-id="ec43e-205">Link hello button tooan action by linking hello technical profile for your ADFS account claims provider:</span></span>

1.  <span data-ttu-id="ec43e-206">Hallo zoeken `<OrchestrationStep>` die omvat `Order="2"` in Hallo `<UserJourney>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="ec43e-206">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="ec43e-207">Plaats de volgende XML-fragment onder `<ClaimsExchanges>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="ec43e-207">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * <span data-ttu-id="ec43e-208">Zorg ervoor dat Hallo `Id` heeft dezelfde als die van waarde Hallo `TargetClaimsExchangeId` in de voorgaande sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="ec43e-208">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
> * <span data-ttu-id="ec43e-209">Zorg ervoor dat `TechnicalProfileReferenceId` toohello technische profiel gemaakt van eerdere (Contoso SAML2) is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ec43e-209">Ensure `TechnicalProfileReferenceId` is set toohello technical profile you created earlier (Contoso-SAML2).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="ec43e-210">Hallo beleid tooyour tenant uploaden</span><span class="sxs-lookup"><span data-stu-id="ec43e-210">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="ec43e-211">In Hallo [Azure-portal](https://portal.azure.com), schakel over naar Hallo [context van uw Azure AD B2C-tenant](active-directory-b2c-navigate-to-b2c-context.md), en open Hallo **Azure AD B2C** blade.</span><span class="sxs-lookup"><span data-stu-id="ec43e-211">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="ec43e-212">Selecteer **identiteit ervaring Framework**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-212">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="ec43e-213">Open Hallo **alle beleidsregels** blade.</span><span class="sxs-lookup"><span data-stu-id="ec43e-213">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="ec43e-214">Selecteer **uploaden beleid**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-214">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="ec43e-215">Controleer **Hallo beleid overschreven als deze bestaat** vak.</span><span class="sxs-lookup"><span data-stu-id="ec43e-215">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="ec43e-216">**Uploaden** TrustFrameworkExtensions.xml en zorg ervoor dat deze niet Hallo validatie mislukt</span><span class="sxs-lookup"><span data-stu-id="ec43e-216">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="ec43e-217">Hallo aangepast beleid testen met behulp van nu uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ec43e-217">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="ec43e-218">Open **Azure AD B2C-instellingen** en ga te**identiteit ervaring Framework**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-218">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="ec43e-219">Open **B2C_1A_signup_signin**, Hallo relying party (RP) aangepast beleid dat u hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="ec43e-219">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="ec43e-220">Selecteer **nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-220">Select **Run now**.</span></span>
3.  <span data-ttu-id="ec43e-221">U moet kunnen toosign met AD FS-account.</span><span class="sxs-lookup"><span data-stu-id="ec43e-221">You should be able toosign in using ADFS account.</span></span>

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="ec43e-222">[Optioneel] Hallo ADFS account claims provider tooProfile bewerken gebruiker reis registreren</span><span class="sxs-lookup"><span data-stu-id="ec43e-222">[Optional] Register hello ADFS account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="ec43e-223">U kunt aangeven tooadd Hallo ADFS account id-provider ook tooyour gebruiker `ProfileEdit` traject van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ec43e-223">You may want tooadd hello ADFS account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="ec43e-224">toomake deze beschikbaar zijn, herhaalt u Hallo laatste twee stappen:</span><span class="sxs-lookup"><span data-stu-id="ec43e-224">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="ec43e-225">Hallo-knop weergave</span><span class="sxs-lookup"><span data-stu-id="ec43e-225">Display hello button</span></span>
1.  <span data-ttu-id="ec43e-226">Open de extensiebestand Hallo van uw beleid (bijvoorbeeld TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="ec43e-226">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="ec43e-227">Hallo zoeken `<UserJourney>` knooppunt met `Id="ProfileEdit"` in Hallo gebruiker reis die u hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="ec43e-227">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="ec43e-228">Zoek Hallo `<OrchestrationStep>` knooppunt bevat`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="ec43e-228">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="ec43e-229">Plaats de volgende XML-fragment onder `<ClaimsProviderSelections>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="ec43e-229">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="ec43e-230">Koppeling Hallo knop tooan actie</span><span class="sxs-lookup"><span data-stu-id="ec43e-230">Link hello button tooan action</span></span>
1.  <span data-ttu-id="ec43e-231">Hallo zoeken `<OrchestrationStep>` die omvat `Order="2"` in Hallo `<UserJourney>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="ec43e-231">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="ec43e-232">Plaats de volgende XML-fragment onder `<ClaimsExchanges>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="ec43e-232">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="ec43e-233">Hallo aangepast profiel bewerken beleid testen met behulp van nu uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ec43e-233">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="ec43e-234">Open **Azure AD B2C-instellingen** en ga te**identiteit ervaring Framework**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-234">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="ec43e-235">Open **B2C_1A_ProfileEdit**, Hallo relying party (RP) aangepast beleid dat u hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="ec43e-235">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="ec43e-236">Selecteer **nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="ec43e-236">Select **Run now**.</span></span>
3.  <span data-ttu-id="ec43e-237">U moet kunnen toosign met AD FS-account.</span><span class="sxs-lookup"><span data-stu-id="ec43e-237">You should be able toosign in using ADFS account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="ec43e-238">Downloaden voltooid Hallo-beleidsbestanden</span><span class="sxs-lookup"><span data-stu-id="ec43e-238">Download hello complete policy files</span></span>
<span data-ttu-id="ec43e-239">Optioneel: We raden aan bouwen van uw scenario met behulp van uw eigen aangepaste beleidsbestanden na het voltooien van Hallo aan de slag met aangepast beleid dat is doorlopen.</span><span class="sxs-lookup"><span data-stu-id="ec43e-239">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through.</span></span> [<span data-ttu-id="ec43e-240">De voorbeeldbestanden beleid alleen ter informatie</span><span class="sxs-lookup"><span data-stu-id="ec43e-240">Policy sample files for reference only</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
