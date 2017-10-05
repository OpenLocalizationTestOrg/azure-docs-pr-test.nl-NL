---
title: "Meerdere exemplaren van Azure AD federeren met één exemplaar van AD FS | Microsoft Docs"
description: "In dit document leert u hoe u meerdere exemplaren van Azure AD federeert met één exemplaar van AD FS."
keywords: "federeren, ADFS, AD FS, meerdere tenants, één AD FS, één ADFS, federatie met meerdere tenants, adfs met meerdere forests, aad connect, federatie, federatie tussen tenants"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 436bf5905d2b203dc4cceea97f4fb90593df7111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a>Meerdere exemplaren van Azure AD federeren met één exemplaar van AD FS

Een enkele AD FS-farm met hoge beschikbaarheid kan meerdere forests federeren als er sprake is van een tweerichtingsvertrouwensrelatie. Deze meerdere forests komen al dan niet overeen met de dezelfde Azure Active Directory. In dit artikel leest u hoe u een federatie configureert tussen één AD FS-implementatie en meerdere forests die synchroniseren met verschillende exemplaren van Azure AD.

![Federatie tussen meerdere tenants en één AD FS-exemplaar](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> Apparaat terugschrijven en automatisch toevoegen worden niet ondersteund in dit scenario.

> [!NOTE]
> Azure AD Connect kan niet worden gebruikt om in dit scenario federatie te configureren, omdat Azure AD Connect alleen federatie kan configureren voor domeinen in één Azure AD-exemplaar.

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a>Stappen voor het federeren van AD FS met meerdere Azure AD-exemplaren

Ga ervan uit dat het domein contoso.com in de Azure Active Directory contoso.onmicrosoft.com al is gefedereerd met de on-premises AD FS die is geïnstalleerd in de on-premises Active Directory-omgeving contoso.com. Fabrikam.com is een domein in de Azure Active Directory fabrikam.onmicrosoft.com.

##<a name="step-1-establish-a-two-way-trust"></a>Stap 1: een tweerichtingsvertrouwensrelatie tot stand brengen
 
AD FS in contoso.com kan alleen gebruikers in fabrikam.com verifiëren als er een tweerichtingsvertrouwensrelatie tussen contoso.com en fabrikam.com bestaat. Volg de stappen in [dit artikel](https://technet.microsoft.com/library/cc816590.aspx) om een tweerichtingsvertrouwensrelatie tot stand te brengen.
 
##<a name="step-2-modify-contosocom-federation-settings"></a>Stap 2: federatie-instellingen voor contoso.com wijzigen 
 
De standaardverlener die voor een enkel met AD FS gefedereerd domein wordt ingesteld, is 'http://ADFSServiceFQDN/adfs/services/trust', bijvoorbeeld 'http://fs.contoso.com/adfs/services/trust'. Voor Azure Active Directory is een unieke verlener vereist voor elk federatief domein. Aangezien dezelfde AD FS twee domeinen gaat federeren, moet de waarde voor de verlener zodanig worden gewijzigd dat deze uniek is voor elk domein dat AD FS federeert met Azure Active Directory. 
 
Open Azure AD PowerShell op de AD FS-server en voer de volgende stappen uit:
 
Maak verbinding met de Azure Active Directory met het domein contoso.com
Connect-MsolService
Werk de federatie-instellingen bij voor contoso.com
Update-MsolFederatedDomain-DomainName contoso.com-SupportMultipleDomain
 
De verlener in de federatie-instelling van het domein wordt gewijzigd in 'http://contoso.com/adfs/services/trust' en er wordt een claimregel voor uitgifte toegevoegd voor de Relying Party Trust van Azure AD, om de juiste issuerId-waarde uit te geven op basis van het UPN-achtervoegsel.
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a>Stap 3: fabrikam.com federeren met AD FS
 
Voer de volgende stappen uit in een PowerShell-sessie in Azure AD: maak verbinding met de Azure Active Directory met het domein fabrikam.com.

    Connect-MsolService
Converteer het beheerde domein fabrikam.com dat u wilt federeren:

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
Met de bovenstaande bewerking wordt het domein fabrikam.com gefedereerd met dezelfde AD FS. U kunt de domeininstellingen voor beide domeinen controleren met Get-MsolDomainFederationSettings.

## <a name="next-steps"></a>Volgende stappen
[Active Directory verbinden met Azure Active Directory](active-directory-aadconnect.md)
