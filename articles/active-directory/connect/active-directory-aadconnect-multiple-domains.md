---
title: aaaAzure AD verbinding maken met meerdere domeinen
description: Dit document beschrijft instellen en configureren van meerdere topleveldomeinen met O365 en Azure AD.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="278d9-103">Ondersteuning voor meerdere domeinen voor federatie met Azure AD</span><span class="sxs-lookup"><span data-stu-id="278d9-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="278d9-104">Hallo volgende documentatie bevat richtlijnen voor het toouse meerdere op het hoogste niveau domeinen en subdomeinen wanneer Federatie met Office 365 of Azure AD-domeinen.</span><span class="sxs-lookup"><span data-stu-id="278d9-104">hello following documentation provides guidance on how toouse multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="278d9-105">Ondersteuning voor meerdere domeinen op het hoogste niveau</span><span class="sxs-lookup"><span data-stu-id="278d9-105">Multiple top-level domain support</span></span>
<span data-ttu-id="278d9-106">Federeren van meerdere topleveldomeinen met Azure AD die is niet vereist voor federatie met één topleveldomein aanvullende configuratie vereist.</span><span class="sxs-lookup"><span data-stu-id="278d9-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="278d9-107">Wanneer een domein is gefedereerd met Azure AD, worden verschillende eigenschappen worden ingesteld op Hallo domein in Azure.</span><span class="sxs-lookup"><span data-stu-id="278d9-107">When a domain is federated with Azure AD, several properties are set on hello domain in Azure.</span></span>  <span data-ttu-id="278d9-108">Een is belangrijk IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="278d9-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="278d9-109">Dit is een URI die wordt gebruikt door Azure AD tooidentify Hallo-domein dat Hallo token is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="278d9-109">This is a URI that is used by Azure AD tooidentify hello domain that hello token is associated with.</span></span>  <span data-ttu-id="278d9-110">Hallo URI tooresolve tooanything niet nodig, maar u moet een geldige URI.</span><span class="sxs-lookup"><span data-stu-id="278d9-110">hello URI doesn’t need tooresolve tooanything but it must be a valid URI.</span></span>  <span data-ttu-id="278d9-111">Standaard Azure AD stelt deze waarde toohello van Hallo federation service-id in uw on-premises AD FS configuration.</span><span class="sxs-lookup"><span data-stu-id="278d9-111">By default, Azure AD sets this toohello value of hello federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="278d9-112">Hallo federation service-id is een URI die een unieke identificatie van een federation-service.</span><span class="sxs-lookup"><span data-stu-id="278d9-112">hello federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="278d9-113">Hallo federation-service is een exemplaar van AD FS die functies als Hallo beveiligingstokenservice.</span><span class="sxs-lookup"><span data-stu-id="278d9-113">hello federation service is an instance of AD FS that functions as hello security token service.</span></span> 
> 
> 

<span data-ttu-id="278d9-114">U kunt vew IssuerUri Hallo PowerShell-opdracht met `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span><span class="sxs-lookup"><span data-stu-id="278d9-114">You can vew IssuerUri by using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="278d9-116">Een probleem ontstaat wanneer er meer dan één topleveldomein tooadd wilt.</span><span class="sxs-lookup"><span data-stu-id="278d9-116">A problem arises when we want tooadd more than one top-level domain.</span></span>  <span data-ttu-id="278d9-117">Bijvoorbeeld, Stel dat u setup federation tussen Azure AD hebt en uw on-premises omgeving.</span><span class="sxs-lookup"><span data-stu-id="278d9-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="278d9-118">Ik gebruik bmcontoso.com voor dit document.  Nu ik heb een domein tweede, op het hoogste niveau toegevoegd bmfabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="278d9-118">For this document I am using bmcontoso.com.  Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![Domeinen](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="278d9-120">Wanneer we onze bmfabrikam.com domein toobe federatieve tooconvert proberen, wordt een foutbericht.</span><span class="sxs-lookup"><span data-stu-id="278d9-120">When we attempt tooconvert our bmfabrikam.com domain toobe federated, we receive an error.</span></span>  <span data-ttu-id="278d9-121">Hallo reden hiervoor is dat Azure AD heeft een beperking waarvoor Hallo IssuerUri eigenschap toohave Hallo dezelfde voor meer dan één domein waarde niet is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="278d9-121">hello reason for this is, Azure AD has a constraint that does not allow hello IssuerUri property toohave hello same value for more than one domain.</span></span>  

![Federation-fout](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="278d9-123">De SupportMultipleDomain Parameter</span><span class="sxs-lookup"><span data-stu-id="278d9-123">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="278d9-124">tooworkaround, moeten we tooadd een andere IssuerUri dat u doen kunt met behulp van Hallo `-SupportMultipleDomain` parameter.</span><span class="sxs-lookup"><span data-stu-id="278d9-124">tooworkaround this, we need tooadd a different IssuerUri which can be done by using hello `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="278d9-125">Deze parameter wordt gebruikt door hello cmdlets volgen:</span><span class="sxs-lookup"><span data-stu-id="278d9-125">This parameter is used with hello following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="278d9-126">Deze parameter kunt u Azure AD Hallo IssuerUri zodanig configureren dat deze is gebaseerd op Hallo-naam van het Hallo-domein.</span><span class="sxs-lookup"><span data-stu-id="278d9-126">This parameter makes Azure AD configure hello IssuerUri so that it is based on hello name of hello domain.</span></span>  <span data-ttu-id="278d9-127">Dit is de unieke op mappen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="278d9-127">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="278d9-128">Met de parameter Hallo kunt Hallo PowerShell-opdracht toocomplete is.</span><span class="sxs-lookup"><span data-stu-id="278d9-128">Using hello parameter allows hello PowerShell command toocomplete successfully.</span></span>

![Federation-fout](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="278d9-130">Bekijkt hello-instellingen van onze nieuwe bmfabrikam.com domein u ziet Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="278d9-130">Looking at hello settings of our new bmfabrikam.com domain you can see hello following:</span></span>

![Federation-fout](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="278d9-132">Houd er rekening mee dat `-SupportMultipleDomain` verandert niet Hallo andere eindpunten die zijn nog steeds toopoint tooour federation-service op adfs.bmcontoso.com geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="278d9-132">Note that `-SupportMultipleDomain` does not change hello other endpoints which are still configured toopoint tooour federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="278d9-133">Een andere ding die `-SupportMultipleDomain` biedt is het zorgt ervoor dat Hallo AD FS system Hallo juiste verlener waarde in tokens die zijn uitgegeven voor Azure AD bevat.</span><span class="sxs-lookup"><span data-stu-id="278d9-133">Another thing that `-SupportMultipleDomain` does is that it ensures that hello AD FS system includes hello proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="278d9-134">Dit wordt door te nemen Hallo domeingedeelte van Hallo gebruikers UPN en in te stellen als Hallo domein in Hallo IssuerUri, dat wil zeggen https://{upn achtervoegsel} / services-adfs-vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="278d9-134">It does this by taking hello domain portion of hello users UPN and setting this as hello domain in hello IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="278d9-135">Tijdens verificatie tooAzure AD of Office 365 is Hallo IssuerUri-element in Hallo gebruikerstoken dus gebruikte toolocate Hallo domein in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="278d9-135">Thus during authentication tooAzure AD or Office 365, hello IssuerUri element in hello user’s token is used toolocate hello domain in Azure AD.</span></span>  <span data-ttu-id="278d9-136">Als er een overeenkomst wordt gevonden Hallo verificatie mislukt.</span><span class="sxs-lookup"><span data-stu-id="278d9-136">If a match cannot be found hello authentication will fail.</span></span> 

<span data-ttu-id="278d9-137">Bijvoorbeeld, als een gebruiker de UPN is bsimon@bmcontoso.com, Hallo IssuerUri-element in het token AD FS problemen Hallo toohttp://bmcontoso.com/adfs/services/trust worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="278d9-137">For example, if a user’s UPN is bsimon@bmcontoso.com, hello IssuerUri element in hello token AD FS issues will be set toohttp://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="278d9-138">Dit komt overeen met de Hallo Azure AD-configuratie en verificatie slaagt.</span><span class="sxs-lookup"><span data-stu-id="278d9-138">This will match hello Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="278d9-139">Hallo volgt Hallo aangepaste claimregel die deze logica implementeert:</span><span class="sxs-lookup"><span data-stu-id="278d9-139">hello following is hello customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="278d9-140">In de volgorde toouse Hallo - SupportMultipleDomain switch tijdens een poging de nieuwe tooadd of Converteer al domeinen toegevoegd, moet u toohave instellen van uw federatieve vertrouwensrelatie toosupport ze oorspronkelijk.</span><span class="sxs-lookup"><span data-stu-id="278d9-140">In order toouse hello -SupportMultipleDomain switch when attempting tooadd new or convert already added domains, you need toohave setup your federated trust toosupport them originally.</span></span>  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="278d9-141">Hoe tooupdate Hallo vertrouwensrelatie tussen AD FS en Azure AD</span><span class="sxs-lookup"><span data-stu-id="278d9-141">How tooupdate hello trust between AD FS and Azure AD</span></span>
<span data-ttu-id="278d9-142">Als u geen Hallo federatieve vertrouwensrelatie tussen AD FS en uw exemplaar van Azure AD instellen hebt, moet u mogelijk toore-deze vertrouwensrelatie maken.</span><span class="sxs-lookup"><span data-stu-id="278d9-142">If you did not setup hello federated trust between AD FS and your instance of Azure AD, you may need toore-create this trust.</span></span>  <span data-ttu-id="278d9-143">Dit is omdat, als het oorspronkelijk installatie zonder Hallo `-SupportMultipleDomain` parameter, Hallo IssuerUri is ingesteld met Hallo-standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="278d9-143">This is because, when it is originally setup without hello `-SupportMultipleDomain` parameter, hello IssuerUri is set with hello default value.</span></span>  <span data-ttu-id="278d9-144">In Hallo ziet schermafbeelding hieronder u Hallo IssuerUri toohttps://adfs.bmcontoso.com/adfs/services/trust is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="278d9-144">In hello screenshot below you can see hello IssuerUri is set toohttps://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="278d9-145">In dat geval nu, als er een nieuw domein in hello Azure AD-portal hebt toegevoegd en vervolgens tooconvert probeert met behulp van `Convert-MsolDomaintoFederated -DomainName <your domain>`, krijgen we de volgende fout Hallo.</span><span class="sxs-lookup"><span data-stu-id="278d9-145">So now, if we have successfully added an new domain in hello Azure AD portal and then attempt tooconvert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get hello following error.</span></span>

![Federation-fout](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="278d9-147">Als u tooadd hello probeert `-SupportMultipleDomain` switch we Hallo volgende fout ontvangen:</span><span class="sxs-lookup"><span data-stu-id="278d9-147">If you try tooadd hello `-SupportMultipleDomain` switch we will receive hello following error:</span></span>

![Federation-fout](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="278d9-149">Gewoon probeert toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` op Hallo oorspronkelijke domein wordt ook leiden tot een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="278d9-149">Simply trying toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on hello original domain will also result in an error.</span></span>

![Federation-fout](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="278d9-151">Gebruik Hallo stappen hieronder tooadd een extra domein op het hoogste niveau.</span><span class="sxs-lookup"><span data-stu-id="278d9-151">Use hello steps below tooadd an additional top-level domain.</span></span>  <span data-ttu-id="278d9-152">Als u al een domein hebt toegevoegd en is geen gebruik Hallo `-SupportMultipleDomain` parameter start met Hallo stappen voor het verwijderen en bijwerken van uw oorspronkelijke domein.</span><span class="sxs-lookup"><span data-stu-id="278d9-152">If you have already added a domain and did not use hello `-SupportMultipleDomain` parameter start with hello steps for removing and updating your original domain.</span></span>  <span data-ttu-id="278d9-153">Als u een domein op het hoogste niveau niet hebt toegevoegd kunt nog u starten met Hallo stappen voor het toevoegen van een domein met behulp van PowerShell van Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="278d9-153">If you have not added a top-level domain yet you can start with hello steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="278d9-154">Gebruik Hallo stappen tooremove Hallo Microsoft Online vertrouwensrelatie te volgen en bijwerken van uw oorspronkelijke domein.</span><span class="sxs-lookup"><span data-stu-id="278d9-154">Use hello following steps tooremove hello Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="278d9-155">Op de AD FS-federatieserver open **AD FS-beheer.**</span><span class="sxs-lookup"><span data-stu-id="278d9-155">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="278d9-156">Vouw op Hallo links **vertrouwensrelaties** en **Relying Party-vertrouwensrelaties**</span><span class="sxs-lookup"><span data-stu-id="278d9-156">On hello left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="278d9-157">Verwijder op de juiste Hallo, Hallo **Identiteitsplatform van Microsoft Office 365** vermelding.</span><span class="sxs-lookup"><span data-stu-id="278d9-157">On hello right, delete hello **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="278d9-158">![Verwijder Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="278d9-158">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="278d9-159">Op een computer die is [Azure Active Directory-Module voor Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) geïnstalleerd op het Hallo volgende uitvoeren: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="278d9-159">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="278d9-160">Voer Hallo gebruikersnaam en wachtwoord van een globale beheerder voor Hallo u Federatie met Azure AD-domein</span><span class="sxs-lookup"><span data-stu-id="278d9-160">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="278d9-161">Voer in PowerShell`Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="278d9-161">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="278d9-162">Voer in PowerShell `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span><span class="sxs-lookup"><span data-stu-id="278d9-162">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="278d9-163">Dit is voor de oorspronkelijke Hallo-domein.</span><span class="sxs-lookup"><span data-stu-id="278d9-163">This is for hello original domain.</span></span>  <span data-ttu-id="278d9-164">Met behulp van Hallo boven het normaal zou zijn domeinen:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="278d9-164">So using hello above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="278d9-165">Gebruik Hallo volgende stappen uit tooadd Hallo nieuwe topleveldomein met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="278d9-165">Use hello following steps tooadd hello new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="278d9-166">Op een computer die is [Azure Active Directory-Module voor Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) geïnstalleerd op het Hallo volgende uitvoeren: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="278d9-166">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="278d9-167">Voer Hallo gebruikersnaam en wachtwoord van een globale beheerder voor Hallo u Federatie met Azure AD-domein</span><span class="sxs-lookup"><span data-stu-id="278d9-167">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="278d9-168">Voer in PowerShell`Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="278d9-168">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="278d9-169">Voer in PowerShell`New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="278d9-169">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="278d9-170">Volgende stappen tooadd Hallo nieuw op het hoogste niveau domein via Azure AD Connect hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="278d9-170">Use hello following steps tooadd hello new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="278d9-171">Azure AD Connect vanaf Hallo bureaublad starten of het menu start</span><span class="sxs-lookup"><span data-stu-id="278d9-171">Launch Azure AD Connect from hello desktop or start menu</span></span>
2. <span data-ttu-id="278d9-172">Kies 'Een extra Azure AD-domein toevoegen' ![toevoegen van een extra Azure AD-domein](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="278d9-172">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="278d9-173">Voer uw Azure AD en Active Directory-referenties</span><span class="sxs-lookup"><span data-stu-id="278d9-173">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="278d9-174">Selecteer Hallo tweede domein dat u wenst dat tooconfigure voor Federatie.</span><span class="sxs-lookup"><span data-stu-id="278d9-174">Select hello second domain you wish tooconfigure for federation.</span></span>
   <span data-ttu-id="278d9-175">![Toevoegen van een extra Azure AD-domein](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="278d9-175">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="278d9-176">Klik op installeren</span><span class="sxs-lookup"><span data-stu-id="278d9-176">Click Install</span></span>

### <a name="verify-hello-new-top-level-domain"></a><span data-ttu-id="278d9-177">Controleer of de nieuwe topleveldomein Hallo</span><span class="sxs-lookup"><span data-stu-id="278d9-177">Verify hello new top-level domain</span></span>
<span data-ttu-id="278d9-178">Met behulp van PowerShell-opdracht Hallo `Get-MsolDomainFederationSettings -DomainName <your domain>`vindt u Hallo IssuerUri bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="278d9-178">By using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view hello updated IssuerUri.</span></span>  <span data-ttu-id="278d9-179">Hallo schermafbeelding hieronder ziet u Hallo federatie-instellingen zijn bijgewerkt op de oorspronkelijke domein http://bmcontoso.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="278d9-179">hello screenshot below shows hello federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="278d9-181">En Hallo IssuerUri in onze nieuwe domein toohttps://bmfabrikam.com/adfs/services/trust is ingesteld</span><span class="sxs-lookup"><span data-stu-id="278d9-181">And hello IssuerUri on our new domain has been set toohttps://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="278d9-183">Ondersteuning voor subdomeinen</span><span class="sxs-lookup"><span data-stu-id="278d9-183">Support for Sub-domains</span></span>
<span data-ttu-id="278d9-184">Wanneer u een subdomein toevoegt, wordt vanwege Hallo manier Azure AD domeinen verwerkt, wordt het Hallo-instellingen van de bovenliggende Hallo worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="278d9-184">When you add a sub-domain, because of hello way Azure AD handled domains, it will inherit hello settings of hello parent.</span></span>  <span data-ttu-id="278d9-185">Dit betekent dat Hallo IssuerUri moet toomatch Hallo ouders.</span><span class="sxs-lookup"><span data-stu-id="278d9-185">This means that hello IssuerUri needs toomatch hello parents.</span></span>

<span data-ttu-id="278d9-186">Zo kunnen zeggen bijvoorbeeld ik bmcontoso.com hebt en voeg vervolgens corp.bmcontoso.com.  Dit betekent dat Hallo IssuerUri voor een gebruiker vanuit corp.bmcontoso.com toobe moet **http://bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="278d9-186">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.  This means that hello IssuerUri for a user from corp.bmcontoso.com will need toobe **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="278d9-187">Maar Hallo standaard regel hierboven voor Azure AD wordt geïmplementeerd, wordt een token genereren met een verlener als **http://corp.bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="278d9-187">However hello standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="278d9-188">Dit wordt niet overeen met de vereiste waarde van het domein Hallo en mislukt de verificatie.</span><span class="sxs-lookup"><span data-stu-id="278d9-188">which will not match hello domain's required value and authentication will fail.</span></span>

### <a name="how-tooenable-support-for-sub-domains"></a><span data-ttu-id="278d9-189">Hoe tooenable ondersteuning bieden voor subdomeinen</span><span class="sxs-lookup"><span data-stu-id="278d9-189">How tooenable support for sub-domains</span></span>
<span data-ttu-id="278d9-190">In de volgorde toowork rond deze Hallo moet de AD FS vertrouwensrelatie van relying party voor Microsoft Online toobe bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="278d9-190">In order toowork around this hello AD FS relying party trust for Microsoft Online needs toobe updated.</span></span>  <span data-ttu-id="278d9-191">toodo, moet u een aangepaste claimregel configureren zodat deze uit alle subdomeinen van UPN-achtervoegsel van de gebruiker Hallo ontdoet tijdens het construeren van de waarde voor aangepaste Issuer Hallo.</span><span class="sxs-lookup"><span data-stu-id="278d9-191">toodo this, you must configure a custom claim rule so that it strips off any sub-domains from hello user’s UPN suffix when constructing hello custom Issuer value.</span></span> 

<span data-ttu-id="278d9-192">Hallo claim te volgen, wordt dit doen:</span><span class="sxs-lookup"><span data-stu-id="278d9-192">hello following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="278d9-193">Hallo laatste nummer in de reguliere expressie Hallo ingesteld Hallo hoeveel bovenliggende domeinen zich in het hoofddomein.</span><span class="sxs-lookup"><span data-stu-id="278d9-193">hello last number in hello regular expression set hello how many parent domains there is in your root domain.</span></span> <span data-ttu-id="278d9-194">Ik heb hier bmcontoso.com zodat twee bovenliggende domeinen nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="278d9-194">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="278d9-195">Als u drie domeinen bovenliggende toobe bewaard zijn (dat wil zeggen: corp.bmcontoso.com), en vervolgens Hallo nummer drie zijn zou.</span><span class="sxs-lookup"><span data-stu-id="278d9-195">If three parent domains were toobe kept (i.e.: corp.bmcontoso.com), then hello number would have been three.</span></span> <span data-ttu-id="278d9-196">Een bereik Eventualy kan worden aangegeven, Hallo overeenkomst wordt altijd worden aangebracht toomatch Hallo maximum van domeinen.</span><span class="sxs-lookup"><span data-stu-id="278d9-196">Eventualy a range can be indicated, hello match will always be made toomatch hello maximum of domains.</span></span> <span data-ttu-id="278d9-197">'{2,3}' komt overeen met twee toothree domeinen (dat wil zeggen: bmfabrikam.com en corp.bmcontoso.com).</span><span class="sxs-lookup"><span data-stu-id="278d9-197">"{2,3}" will match two toothree domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="278d9-198">Volgende stappen tooadd Hallo een aangepaste claim subdomeinen voor toosupport gebruiken.</span><span class="sxs-lookup"><span data-stu-id="278d9-198">Use hello following steps tooadd a custom claim toosupport sub-domains.</span></span>

1. <span data-ttu-id="278d9-199">Open AD FS-beheer</span><span class="sxs-lookup"><span data-stu-id="278d9-199">Open AD FS Management</span></span>
2. <span data-ttu-id="278d9-200">Vertrouwensrelatie van de Microsoft Online RP Hallo Klik met de rechtermuisknop en kies claimregels bewerken</span><span class="sxs-lookup"><span data-stu-id="278d9-200">Right click hello Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="278d9-201">Selecteer de derde claimregel Hallo en vervang ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="278d9-201">Select hello third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="278d9-202">Vervang de huidige claim Hallo:</span><span class="sxs-lookup"><span data-stu-id="278d9-202">Replace hello current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Claim vervangen](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="278d9-204">Klik op Ok.</span><span class="sxs-lookup"><span data-stu-id="278d9-204">Click Ok.</span></span>  <span data-ttu-id="278d9-205">Klik op toepassen.</span><span class="sxs-lookup"><span data-stu-id="278d9-205">Click Apply.</span></span>  <span data-ttu-id="278d9-206">Klik op Ok.</span><span class="sxs-lookup"><span data-stu-id="278d9-206">Click Ok.</span></span>  <span data-ttu-id="278d9-207">Sluit AD FS-beheer.</span><span class="sxs-lookup"><span data-stu-id="278d9-207">Close AD FS Management.</span></span>

