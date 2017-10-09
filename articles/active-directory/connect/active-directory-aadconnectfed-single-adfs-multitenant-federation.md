---
title: "aaaFederating meerdere Azure AD met één AD FS | Microsoft Docs"
description: In dit document wordt uitgelegd hoe toofederate meerdere Azure AD met een enkel AD FS.
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
ms.openlocfilehash: 442192896b3b13f7bf9388396cd3769e194329d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a>Meerdere exemplaren van Azure AD federeren met één exemplaar van AD FS

Een enkele AD FS-farm met hoge beschikbaarheid kan meerdere forests federeren als er sprake is van een tweerichtingsvertrouwensrelatie. Deze meerdere forests kan of kunnen niet overeen met toohello dezelfde Azure Active Directory. In dit artikel vindt u instructies voor hoe tooconfigure federatie tussen één AD FS-implementatie en meer dan één die synchronisatie toodifferent Azure AD-forests.

![Federatie tussen meerdere tenants en één AD FS-exemplaar](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> Apparaat terugschrijven en automatisch toevoegen worden niet ondersteund in dit scenario.

> [!NOTE]
> Azure AD Connect kan gebruikte tooconfigure federation in dit scenario niet als Azure AD Connect federation voor domeinen in een enkel Azure AD kunt configureren.

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a>Stappen voor het federeren van AD FS met meerdere Azure AD-exemplaren

U kunt dat een domein contoso.com in Azure Active Directory-contoso.onmicrosoft.com al is gefedereerd met AD FS Hallo on-premises geïnstalleerd in contoso.com on-premises Active Directory-omgeving. Fabrikam.com is een domein in de Azure Active Directory fabrikam.onmicrosoft.com.

##<a name="step-1-establish-a-two-way-trust"></a>Stap 1: een tweerichtingsvertrouwensrelatie tot stand brengen
 
Voor AD FS in contoso.com toobe tooauthenticate kunnen gebruikers in fabrikam.com, is een wederzijdse vertrouwensrelatie tussen contoso.com en fabrikam.com nodig. Ga als volgt Hallo richtlijn in deze [artikel](https://technet.microsoft.com/library/cc816590.aspx) toocreate Hallo wederzijdse vertrouwensrelatie.
 
##<a name="step-2-modify-contosocom-federation-settings"></a>Stap 2: federatie-instellingen voor contoso.com wijzigen 
 
Hallo standaard certificaatverlener is ingesteld voor een enkel domein federatieve tooAD FS is 'http://ADFSServiceFQDN/adfs/services/trust', bijvoorbeeld 'http://fs.contoso.com/adfs/services/trust'. Voor Azure Active Directory is een unieke verlener vereist voor elk federatief domein. Aangezien Hallo dezelfde AD FS toofederate twee domeinen gaat, moet Hallo verlener waarde toobe zodat deze uniek is voor elk domein dat AD FS federates met Azure Active Directory is gewijzigd. 
 
Op Hallo AD FS-server, opent u Azure AD PowerShell en Voer Hallo stappen te volgen:
 
Verbinding maken met Azure Active Directory met Hallo domein contoso.com Connect MsolService Update Hallo federation-instellingen voor contoso.com Update MsolFederatedDomain - domeinnaam contoso.com toohello – SupportMultipleDomain
 
Certificaatverlener in de instelling voor domeinfederatie hello wordt gewijzigd te 'http://contoso.com/adfs/services/trust' en een uitgifte claim regel voor hello Azure AD Relying Party Trust tooissue Hallo juist issuerId waarde op basis van Hallo UPN-achtervoegsel wordt toegevoegd.
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a>Stap 3: fabrikam.com federeren met AD FS
 
In Azure AD powershell-sessie uitvoeren Hallo stappen te volgen: verbinding maken met Active Directory met Hallo domein fabrikam.com tooAzure

    Connect-MsolService
Hallo fabrikam.com beheerd domein toofederated converteren:

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
Hallo hierboven bewerking wordt federeren Hallo domein fabrikam.com Hello dezelfde AD FS. U kunt Hallo domeininstellingen controleren met behulp van Get-MsolDomainFederationSettings voor beide domeinen.

## <a name="next-steps"></a>Volgende stappen
[Active Directory verbinden met Azure Active Directory](active-directory-aadconnect.md)
