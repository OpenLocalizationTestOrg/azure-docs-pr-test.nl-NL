---
title: Azure AD Connect meerdere domeinen
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
ms.openlocfilehash: 8e3f496c2868cc3430e0efd47805aec2205168aa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="c698f-103">Ondersteuning voor meerdere domeinen voor federatie met Azure AD</span><span class="sxs-lookup"><span data-stu-id="c698f-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="c698f-104">De volgende documentatie biedt richtlijnen voor het gebruik van meerdere op het hoogste niveau domeinen en subdomeinen wanneer Federatie met Office 365 of Azure AD-domeinen.</span><span class="sxs-lookup"><span data-stu-id="c698f-104">The following documentation provides guidance on how to use multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="c698f-105">Ondersteuning voor meerdere domeinen op het hoogste niveau</span><span class="sxs-lookup"><span data-stu-id="c698f-105">Multiple top-level domain support</span></span>
<span data-ttu-id="c698f-106">Federeren van meerdere topleveldomeinen met Azure AD die is niet vereist voor federatie met één topleveldomein aanvullende configuratie vereist.</span><span class="sxs-lookup"><span data-stu-id="c698f-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="c698f-107">Wanneer een domein is gefedereerd met Azure AD, worden verschillende eigenschappen ingesteld voor het domein in Azure.</span><span class="sxs-lookup"><span data-stu-id="c698f-107">When a domain is federated with Azure AD, several properties are set on the domain in Azure.</span></span>  <span data-ttu-id="c698f-108">Een is belangrijk IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="c698f-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="c698f-109">Dit is een URI die door Azure AD wordt gebruikt voor het identificeren van het domein waaraan het token is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="c698f-109">This is a URI that is used by Azure AD to identify the domain that the token is associated with.</span></span>  <span data-ttu-id="c698f-110">De URI hoeft niet omzetten naar een andere waarde dan dat het moet een geldige URI.</span><span class="sxs-lookup"><span data-stu-id="c698f-110">The URI doesn’t need to resolve to anything but it must be a valid URI.</span></span>  <span data-ttu-id="c698f-111">Standaard Azure AD stelt dit aan de waarde van de federation service-id in uw on-premises AD FS configuration.</span><span class="sxs-lookup"><span data-stu-id="c698f-111">By default, Azure AD sets this to the value of the federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="c698f-112">De federation service-id is een URI die een unieke identificatie van een federation-service.</span><span class="sxs-lookup"><span data-stu-id="c698f-112">The federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="c698f-113">De federation-service is een exemplaar van AD FS die functies als de service voor beveiligingstokens.</span><span class="sxs-lookup"><span data-stu-id="c698f-113">The federation service is an instance of AD FS that functions as the security token service.</span></span> 
> 
> 

<span data-ttu-id="c698f-114">U kunt vew IssuerUri met behulp van de PowerShell-opdracht `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span><span class="sxs-lookup"><span data-stu-id="c698f-114">You can vew IssuerUri by using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="c698f-116">Een probleem ontstaat wanneer we willen meer dan één site op het hoogste domein toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c698f-116">A problem arises when we want to add more than one top-level domain.</span></span>  <span data-ttu-id="c698f-117">Bijvoorbeeld, Stel dat u setup federation tussen Azure AD hebt en uw on-premises omgeving.</span><span class="sxs-lookup"><span data-stu-id="c698f-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="c698f-118">Ik gebruik bmcontoso.com voor dit document.</span><span class="sxs-lookup"><span data-stu-id="c698f-118">For this document I am using bmcontoso.com.</span></span>  <span data-ttu-id="c698f-119">Nu ik heb een domein tweede, op het hoogste niveau toegevoegd bmfabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="c698f-119">Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![Domeinen](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="c698f-121">Wanneer we proberen te converteren van onze bmfabrikam.com domein dat gefedereerd, moet er een foutbericht ontvangt.</span><span class="sxs-lookup"><span data-stu-id="c698f-121">When we attempt to convert our bmfabrikam.com domain to be federated, we receive an error.</span></span>  <span data-ttu-id="c698f-122">De reden hiervoor is dat Azure AD heeft een beperking waarvoor de eigenschap IssuerUri hebben dezelfde waarde voor meer dan één domein niet is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="c698f-122">The reason for this is, Azure AD has a constraint that does not allow the IssuerUri property to have the same value for more than one domain.</span></span>  

![Federation-fout](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="c698f-124">De SupportMultipleDomain Parameter</span><span class="sxs-lookup"><span data-stu-id="c698f-124">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="c698f-125">Als tijdelijke oplossing, moeten we het toevoegen van een andere IssuerUri dat u doen met behulp van kunt de `-SupportMultipleDomain` parameter.</span><span class="sxs-lookup"><span data-stu-id="c698f-125">To workaround this, we need to add a different IssuerUri which can be done by using the `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="c698f-126">Deze parameter wordt gebruikt met de volgende cmdlets:</span><span class="sxs-lookup"><span data-stu-id="c698f-126">This parameter is used with the following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="c698f-127">Deze parameter kunt u Azure AD de IssuerUri zodanig configureren dat deze is gebaseerd op de naam van het domein.</span><span class="sxs-lookup"><span data-stu-id="c698f-127">This parameter makes Azure AD configure the IssuerUri so that it is based on the name of the domain.</span></span>  <span data-ttu-id="c698f-128">Dit is de unieke op mappen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c698f-128">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="c698f-129">Met de parameter, kunt de PowerShell-opdracht te voltooien.</span><span class="sxs-lookup"><span data-stu-id="c698f-129">Using the parameter allows the PowerShell command to complete successfully.</span></span>

![Federation-fout](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="c698f-131">De instellingen van onze nieuwe bmfabrikam.com domein ziet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="c698f-131">Looking at the settings of our new bmfabrikam.com domain you can see the following:</span></span>

![Federation-fout](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="c698f-133">Houd er rekening mee dat `-SupportMultipleDomain` verandert niets aan de andere eindpunten die worden nog geconfigureerd om te verwijzen naar onze adfs.bmcontoso.com federation-service.</span><span class="sxs-lookup"><span data-stu-id="c698f-133">Note that `-SupportMultipleDomain` does not change the other endpoints which are still configured to point to our federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="c698f-134">Een andere ding die `-SupportMultipleDomain` biedt is het zorgt ervoor dat het systeem AD FS de juiste waarde van de verlener in de tokens die zijn uitgegeven voor Azure AD opgenomen.</span><span class="sxs-lookup"><span data-stu-id="c698f-134">Another thing that `-SupportMultipleDomain` does is that it ensures that the AD FS system includes the proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="c698f-135">Dit wordt door te nemen het domeingedeelte van de UPN van gebruikers en in te stellen als het domein in de IssuerUri, dat wil zeggen https://{upn achtervoegsel} / services-adfs-vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="c698f-135">It does this by taking the domain portion of the users UPN and setting this as the domain in the IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="c698f-136">Dus tijdens de verificatie met Azure AD of Office 365, het IssuerUri-element in het token van de gebruiker wordt gebruikt voor het domein niet vinden in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c698f-136">Thus during authentication to Azure AD or Office 365, the IssuerUri element in the user’s token is used to locate the domain in Azure AD.</span></span>  <span data-ttu-id="c698f-137">Als er een overeenkomst wordt gevonden dat de verificatie mislukt.</span><span class="sxs-lookup"><span data-stu-id="c698f-137">If a match cannot be found the authentication will fail.</span></span> 

<span data-ttu-id="c698f-138">Bijvoorbeeld, als een gebruiker de UPN is bsimon@bmcontoso.com, het IssuerUri-element in de problemen met het token AD FS wordt zo ingesteld dat http://bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="c698f-138">For example, if a user’s UPN is bsimon@bmcontoso.com, the IssuerUri element in the token AD FS issues will be set to http://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="c698f-139">Dit komt overeen met de Azure AD-configuratie en verificatie slaagt.</span><span class="sxs-lookup"><span data-stu-id="c698f-139">This will match the Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="c698f-140">Hier volgt de aangepaste claimregel die deze logica implementeert:</span><span class="sxs-lookup"><span data-stu-id="c698f-140">The following is the customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="c698f-141">Om de schakeloptie - SupportMultipleDomain gebruikt bij het toevoegen van domeinen bij het toevoegen of al converteren, moet u het installatieprogramma de federatieve vertrouwensrelatie worden oorspronkelijk ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c698f-141">In order to use the -SupportMultipleDomain switch when attempting to add new or convert already added domains, you need to have setup your federated trust to support them originally.</span></span>  
> 
> 

## <a name="how-to-update-the-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="c698f-142">Het bijwerken van de vertrouwensrelatie tussen AD FS en Azure AD</span><span class="sxs-lookup"><span data-stu-id="c698f-142">How to update the trust between AD FS and Azure AD</span></span>
<span data-ttu-id="c698f-143">Als u niet de federatieve vertrouwensrelatie tussen AD FS en uw exemplaar van Azure AD instellen hebt, moet u mogelijk om deze vertrouwensrelatie opnieuw te maken.</span><span class="sxs-lookup"><span data-stu-id="c698f-143">If you did not setup the federated trust between AD FS and your instance of Azure AD, you may need to re-create this trust.</span></span>  <span data-ttu-id="c698f-144">Dit is omdat, als het oorspronkelijk installatie zonder het `-SupportMultipleDomain` parameter, de IssuerUri is ingesteld met de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="c698f-144">This is because, when it is originally setup without the `-SupportMultipleDomain` parameter, the IssuerUri is set with the default value.</span></span>  <span data-ttu-id="c698f-145">In de schermafbeelding hieronder u ziet dat de IssuerUri is ingesteld op https://adfs.bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="c698f-145">In the screenshot below you can see the IssuerUri is set to https://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="c698f-146">In dat geval nu, als er een nieuw domein in de Azure AD-portal hebt toegevoegd en vervolgens probeert te converteren met behulp van `Convert-MsolDomaintoFederated -DomainName <your domain>`, krijgen we de volgende fout.</span><span class="sxs-lookup"><span data-stu-id="c698f-146">So now, if we have successfully added an new domain in the Azure AD portal and then attempt to convert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get the following error.</span></span>

![Federation-fout](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="c698f-148">Als u probeert toe te voegen de `-SupportMultipleDomain` switch we de volgende fout ontvangen:</span><span class="sxs-lookup"><span data-stu-id="c698f-148">If you try to add the `-SupportMultipleDomain` switch we will receive the following error:</span></span>

![Federation-fout](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="c698f-150">Gewoon probeert uit te voeren `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` op het oorspronkelijke domein wordt ook leiden tot een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="c698f-150">Simply trying to run `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on the original domain will also result in an error.</span></span>

![Federation-fout](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="c698f-152">Gebruik de volgende stappen uit om toe te voegen een extra domein op het hoogste niveau.</span><span class="sxs-lookup"><span data-stu-id="c698f-152">Use the steps below to add an additional top-level domain.</span></span>  <span data-ttu-id="c698f-153">Als u al een domein hebt toegevoegd en niet gebruikt de `-SupportMultipleDomain` parameter starten met de stappen voor het verwijderen en bijwerken van uw oorspronkelijke domein.</span><span class="sxs-lookup"><span data-stu-id="c698f-153">If you have already added a domain and did not use the `-SupportMultipleDomain` parameter start with the steps for removing and updating your original domain.</span></span>  <span data-ttu-id="c698f-154">Als u een domein op het hoogste niveau niet hebt toegevoegd kunt nog u starten met de stappen voor het toevoegen van een domein met behulp van PowerShell van Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c698f-154">If you have not added a top-level domain yet you can start with the steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="c698f-155">Gebruik de volgende stappen voor het verwijderen van de vertrouwensrelatie van de Microsoft Online en bijwerken van uw oorspronkelijke domein.</span><span class="sxs-lookup"><span data-stu-id="c698f-155">Use the following steps to remove the Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="c698f-156">Op de AD FS-federatieserver open **AD FS-beheer.**</span><span class="sxs-lookup"><span data-stu-id="c698f-156">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="c698f-157">Vouw op de links **vertrouwensrelaties** en **Relying Party-vertrouwensrelaties**</span><span class="sxs-lookup"><span data-stu-id="c698f-157">On the left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="c698f-158">Aan de rechterkant verwijderen de **Identiteitsplatform van Microsoft Office 365** vermelding.</span><span class="sxs-lookup"><span data-stu-id="c698f-158">On the right, delete the **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="c698f-159">![Verwijder Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="c698f-159">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="c698f-160">Op een computer die is [Azure Active Directory-Module voor Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) geïnstalleerd op het volgende uitvoeren: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="c698f-160">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="c698f-161">Voer de gebruikersnaam en het wachtwoord van een globale beheerder voor de door u Federatie met Azure AD-domein</span><span class="sxs-lookup"><span data-stu-id="c698f-161">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="c698f-162">Voer in PowerShell`Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="c698f-162">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="c698f-163">Voer in PowerShell `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span><span class="sxs-lookup"><span data-stu-id="c698f-163">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="c698f-164">Dit is voor het oorspronkelijke domein.</span><span class="sxs-lookup"><span data-stu-id="c698f-164">This is for the original domain.</span></span>  <span data-ttu-id="c698f-165">Met behulp van de bovenstaande domeinen die het normaal zou zijn:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="c698f-165">So using the above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="c698f-166">Gebruik de volgende stappen om toe te voegen van de nieuwe topleveldomein met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="c698f-166">Use the following steps to add the new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="c698f-167">Op een computer die is [Azure Active Directory-Module voor Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) geïnstalleerd op het volgende uitvoeren: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="c698f-167">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="c698f-168">Voer de gebruikersnaam en het wachtwoord van een globale beheerder voor de door u Federatie met Azure AD-domein</span><span class="sxs-lookup"><span data-stu-id="c698f-168">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="c698f-169">Voer in PowerShell`Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="c698f-169">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="c698f-170">Voer in PowerShell`New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="c698f-170">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="c698f-171">Gebruik de volgende stappen uit om toe te voegen van de nieuwe topleveldomein met Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c698f-171">Use the following steps to add the new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="c698f-172">Azure AD Connect vanaf het bureaublad te starten of het menu start</span><span class="sxs-lookup"><span data-stu-id="c698f-172">Launch Azure AD Connect from the desktop or start menu</span></span>
2. <span data-ttu-id="c698f-173">Kies 'Een extra Azure AD-domein toevoegen' ![toevoegen van een extra Azure AD-domein](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="c698f-173">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="c698f-174">Voer uw Azure AD en Active Directory-referenties</span><span class="sxs-lookup"><span data-stu-id="c698f-174">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="c698f-175">Selecteer het tweede domein dat u wilt configureren voor Federatie.</span><span class="sxs-lookup"><span data-stu-id="c698f-175">Select the second domain you wish to configure for federation.</span></span>
   <span data-ttu-id="c698f-176">![Toevoegen van een extra Azure AD-domein](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="c698f-176">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="c698f-177">Klik op installeren</span><span class="sxs-lookup"><span data-stu-id="c698f-177">Click Install</span></span>

### <a name="verify-the-new-top-level-domain"></a><span data-ttu-id="c698f-178">Controleer of het nieuwe domein op het hoogste niveau</span><span class="sxs-lookup"><span data-stu-id="c698f-178">Verify the new top-level domain</span></span>
<span data-ttu-id="c698f-179">Met behulp van de PowerShell-opdracht `Get-MsolDomainFederationSettings -DomainName <your domain>`kunt u de bijgewerkte IssuerUri weergeven.</span><span class="sxs-lookup"><span data-stu-id="c698f-179">By using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view the updated IssuerUri.</span></span>  <span data-ttu-id="c698f-180">De onderstaande schermafbeelding ziet u de federatie instellingen zijn bijgewerkt op de oorspronkelijke domein http://bmcontoso.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="c698f-180">The screenshot below shows the federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="c698f-182">En de IssuerUri in onze nieuwe domein is ingesteld op https://bmfabrikam.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="c698f-182">And the IssuerUri on our new domain has been set to https://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="c698f-184">Ondersteuning voor subdomeinen</span><span class="sxs-lookup"><span data-stu-id="c698f-184">Support for Sub-domains</span></span>
<span data-ttu-id="c698f-185">Wanneer u een subdomein vanwege de manier waarop Azure AD verwerkt domeinen toevoegt, worden overgenomen door de instellingen van het bovenliggende item.</span><span class="sxs-lookup"><span data-stu-id="c698f-185">When you add a sub-domain, because of the way Azure AD handled domains, it will inherit the settings of the parent.</span></span>  <span data-ttu-id="c698f-186">Dit betekent dat de IssuerUri moet overeenkomen met de bovenliggende items.</span><span class="sxs-lookup"><span data-stu-id="c698f-186">This means that the IssuerUri needs to match the parents.</span></span>

<span data-ttu-id="c698f-187">Zo kunnen zeggen bijvoorbeeld ik bmcontoso.com hebt en voeg vervolgens corp.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="c698f-187">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.</span></span>  <span data-ttu-id="c698f-188">Dit betekent dat de IssuerUri voor een gebruiker vanuit corp.bmcontoso.com moet **http://bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="c698f-188">This means that the IssuerUri for a user from corp.bmcontoso.com will need to be **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="c698f-189">Maar de standaard regel boven geïmplementeerd voor Azure AD, wordt een token genereren met een verlener als **http://corp.bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="c698f-189">However the standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="c698f-190">waarde die niet overeenkomt met het domein nodig en mislukt de verificatie.</span><span class="sxs-lookup"><span data-stu-id="c698f-190">which will not match the domain's required value and authentication will fail.</span></span>

### <a name="how-to-enable-support-for-sub-domains"></a><span data-ttu-id="c698f-191">Het inschakelen van ondersteuning voor subdomeinen</span><span class="sxs-lookup"><span data-stu-id="c698f-191">How To enable support for sub-domains</span></span>
<span data-ttu-id="c698f-192">Relying party trust voor Microsoft Online moet worden bijgewerkt om dit probleem oplossen door de AD FS.</span><span class="sxs-lookup"><span data-stu-id="c698f-192">In order to work around this the AD FS relying party trust for Microsoft Online needs to be updated.</span></span>  <span data-ttu-id="c698f-193">Om dit te doen, moet u een aangepaste claimregel configureren zodat deze uit alle subdomeinen van UPN-achtervoegsel van de gebruiker ontdoet bij het maken van de aangepaste waarde van de verlener.</span><span class="sxs-lookup"><span data-stu-id="c698f-193">To do this, you must configure a custom claim rule so that it strips off any sub-domains from the user’s UPN suffix when constructing the custom Issuer value.</span></span> 

<span data-ttu-id="c698f-194">De volgende claim wordt dit doen:</span><span class="sxs-lookup"><span data-stu-id="c698f-194">The following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="c698f-195">De laatste waarde in de reguliere expressie instellen hoeveel bovenliggende domeinen zich in het hoofddomein.</span><span class="sxs-lookup"><span data-stu-id="c698f-195">The last number in the regular expression set the how many parent domains there is in your root domain.</span></span> <span data-ttu-id="c698f-196">Ik heb hier bmcontoso.com zodat twee bovenliggende domeinen nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="c698f-196">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="c698f-197">Als u drie bovenliggende domeinen worden bewaard zijn (dat wil zeggen: corp.bmcontoso.com), en vervolgens het aantal drie zijn zou.</span><span class="sxs-lookup"><span data-stu-id="c698f-197">If three parent domains were to be kept (i.e.: corp.bmcontoso.com), then the number would have been three.</span></span> <span data-ttu-id="c698f-198">Een bereik Eventualy kunnen worden aangegeven, de overeenkomst altijd worden aangebracht aan overeen met het maximum van domeinen.</span><span class="sxs-lookup"><span data-stu-id="c698f-198">Eventualy a range can be indicated, the match will always be made to match the maximum of domains.</span></span> <span data-ttu-id="c698f-199">'{2,3}' komt overeen met twee of drie domeinen (dat wil zeggen: bmfabrikam.com en corp.bmcontoso.com).</span><span class="sxs-lookup"><span data-stu-id="c698f-199">"{2,3}" will match two to three domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="c698f-200">Gebruik de volgende stappen uit een aangepaste claim ter ondersteuning van subdomeinen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c698f-200">Use the following steps to add a custom claim to support sub-domains.</span></span>

1. <span data-ttu-id="c698f-201">Open AD FS-beheer</span><span class="sxs-lookup"><span data-stu-id="c698f-201">Open AD FS Management</span></span>
2. <span data-ttu-id="c698f-202">Klik met de rechtermuisknop op de vertrouwensrelatie van de Microsoft Online RP en kies claimregels bewerken</span><span class="sxs-lookup"><span data-stu-id="c698f-202">Right click the Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="c698f-203">Selecteer de derde claimregel en vervang ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="c698f-203">Select the third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="c698f-204">Vervang de huidige claim:</span><span class="sxs-lookup"><span data-stu-id="c698f-204">Replace the current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Claim vervangen](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="c698f-206">Klik op Ok.</span><span class="sxs-lookup"><span data-stu-id="c698f-206">Click Ok.</span></span>  <span data-ttu-id="c698f-207">Klik op toepassen.</span><span class="sxs-lookup"><span data-stu-id="c698f-207">Click Apply.</span></span>  <span data-ttu-id="c698f-208">Klik op Ok.</span><span class="sxs-lookup"><span data-stu-id="c698f-208">Click Ok.</span></span>  <span data-ttu-id="c698f-209">Sluit AD FS-beheer.</span><span class="sxs-lookup"><span data-stu-id="c698f-209">Close AD FS Management.</span></span>

