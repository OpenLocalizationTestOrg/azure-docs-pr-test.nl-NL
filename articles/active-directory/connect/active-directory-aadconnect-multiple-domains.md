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
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a>Ondersteuning voor meerdere domeinen voor federatie met Azure AD
Hallo volgende documentatie bevat richtlijnen voor het toouse meerdere op het hoogste niveau domeinen en subdomeinen wanneer Federatie met Office 365 of Azure AD-domeinen.

## <a name="multiple-top-level-domain-support"></a>Ondersteuning voor meerdere domeinen op het hoogste niveau
Federeren van meerdere topleveldomeinen met Azure AD die is niet vereist voor federatie met één topleveldomein aanvullende configuratie vereist.

Wanneer een domein is gefedereerd met Azure AD, worden verschillende eigenschappen worden ingesteld op Hallo domein in Azure.  Een is belangrijk IssuerUri.  Dit is een URI die wordt gebruikt door Azure AD tooidentify Hallo-domein dat Hallo token is gekoppeld.  Hallo URI tooresolve tooanything niet nodig, maar u moet een geldige URI.  Standaard Azure AD stelt deze waarde toohello van Hallo federation service-id in uw on-premises AD FS configuration.

> [!NOTE]
> Hallo federation service-id is een URI die een unieke identificatie van een federation-service.  Hallo federation-service is een exemplaar van AD FS die functies als Hallo beveiligingstokenservice. 
> 
> 

U kunt vew IssuerUri Hallo PowerShell-opdracht met `Get-MsolDomainFederationSettings -DomainName <your domain>`.

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

Een probleem ontstaat wanneer er meer dan één topleveldomein tooadd wilt.  Bijvoorbeeld, Stel dat u setup federation tussen Azure AD hebt en uw on-premises omgeving.  Ik gebruik bmcontoso.com voor dit document.  Nu ik heb een domein tweede, op het hoogste niveau toegevoegd bmfabrikam.com.

![Domeinen](./media/active-directory-multiple-domains/domains.png)

Wanneer we onze bmfabrikam.com domein toobe federatieve tooconvert proberen, wordt een foutbericht.  Hallo reden hiervoor is dat Azure AD heeft een beperking waarvoor Hallo IssuerUri eigenschap toohave Hallo dezelfde voor meer dan één domein waarde niet is toegestaan.  

![Federation-fout](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a>De SupportMultipleDomain Parameter
tooworkaround, moeten we tooadd een andere IssuerUri dat u doen kunt met behulp van Hallo `-SupportMultipleDomain` parameter.  Deze parameter wordt gebruikt door hello cmdlets volgen:

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

Deze parameter kunt u Azure AD Hallo IssuerUri zodanig configureren dat deze is gebaseerd op Hallo-naam van het Hallo-domein.  Dit is de unieke op mappen in Azure AD.  Met de parameter Hallo kunt Hallo PowerShell-opdracht toocomplete is.

![Federation-fout](./media/active-directory-multiple-domains/convert.png)

Bekijkt hello-instellingen van onze nieuwe bmfabrikam.com domein u ziet Hallo volgende:

![Federation-fout](./media/active-directory-multiple-domains/settings.png)

Houd er rekening mee dat `-SupportMultipleDomain` verandert niet Hallo andere eindpunten die zijn nog steeds toopoint tooour federation-service op adfs.bmcontoso.com geconfigureerd.

Een andere ding die `-SupportMultipleDomain` biedt is het zorgt ervoor dat Hallo AD FS system Hallo juiste verlener waarde in tokens die zijn uitgegeven voor Azure AD bevat. Dit wordt door te nemen Hallo domeingedeelte van Hallo gebruikers UPN en in te stellen als Hallo domein in Hallo IssuerUri, dat wil zeggen https://{upn achtervoegsel} / services-adfs-vertrouwen. 

Tijdens verificatie tooAzure AD of Office 365 is Hallo IssuerUri-element in Hallo gebruikerstoken dus gebruikte toolocate Hallo domein in Azure AD.  Als er een overeenkomst wordt gevonden Hallo verificatie mislukt. 

Bijvoorbeeld, als een gebruiker de UPN is bsimon@bmcontoso.com, Hallo IssuerUri-element in het token AD FS problemen Hallo toohttp://bmcontoso.com/adfs/services/trust worden ingesteld. Dit komt overeen met de Hallo Azure AD-configuratie en verificatie slaagt.

Hallo volgt Hallo aangepaste claimregel die deze logica implementeert:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> In de volgorde toouse Hallo - SupportMultipleDomain switch tijdens een poging de nieuwe tooadd of Converteer al domeinen toegevoegd, moet u toohave instellen van uw federatieve vertrouwensrelatie toosupport ze oorspronkelijk.  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a>Hoe tooupdate Hallo vertrouwensrelatie tussen AD FS en Azure AD
Als u geen Hallo federatieve vertrouwensrelatie tussen AD FS en uw exemplaar van Azure AD instellen hebt, moet u mogelijk toore-deze vertrouwensrelatie maken.  Dit is omdat, als het oorspronkelijk installatie zonder Hallo `-SupportMultipleDomain` parameter, Hallo IssuerUri is ingesteld met Hallo-standaardwaarde.  In Hallo ziet schermafbeelding hieronder u Hallo IssuerUri toohttps://adfs.bmcontoso.com/adfs/services/trust is ingesteld.

In dat geval nu, als er een nieuw domein in hello Azure AD-portal hebt toegevoegd en vervolgens tooconvert probeert met behulp van `Convert-MsolDomaintoFederated -DomainName <your domain>`, krijgen we de volgende fout Hallo.

![Federation-fout](./media/active-directory-multiple-domains/trust1.png)

Als u tooadd hello probeert `-SupportMultipleDomain` switch we Hallo volgende fout ontvangen:

![Federation-fout](./media/active-directory-multiple-domains/trust2.png)

Gewoon probeert toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` op Hallo oorspronkelijke domein wordt ook leiden tot een fout opgetreden.

![Federation-fout](./media/active-directory-multiple-domains/trust3.png)

Gebruik Hallo stappen hieronder tooadd een extra domein op het hoogste niveau.  Als u al een domein hebt toegevoegd en is geen gebruik Hallo `-SupportMultipleDomain` parameter start met Hallo stappen voor het verwijderen en bijwerken van uw oorspronkelijke domein.  Als u een domein op het hoogste niveau niet hebt toegevoegd kunt nog u starten met Hallo stappen voor het toevoegen van een domein met behulp van PowerShell van Azure AD Connect.

Gebruik Hallo stappen tooremove Hallo Microsoft Online vertrouwensrelatie te volgen en bijwerken van uw oorspronkelijke domein.

1. Op de AD FS-federatieserver open **AD FS-beheer.** 
2. Vouw op Hallo links **vertrouwensrelaties** en **Relying Party-vertrouwensrelaties**
3. Verwijder op de juiste Hallo, Hallo **Identiteitsplatform van Microsoft Office 365** vermelding.
   ![Verwijder Microsoft Online](./media/active-directory-multiple-domains/trust4.png)
4. Op een computer die is [Azure Active Directory-Module voor Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) geïnstalleerd op het Hallo volgende uitvoeren: `$cred=Get-Credential`.  
5. Voer Hallo gebruikersnaam en wachtwoord van een globale beheerder voor Hallo u Federatie met Azure AD-domein
6. Voer in PowerShell`Connect-MsolService -Credential $cred`
7. Voer in PowerShell `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.  Dit is voor de oorspronkelijke Hallo-domein.  Met behulp van Hallo boven het normaal zou zijn domeinen:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`

Gebruik Hallo volgende stappen uit tooadd Hallo nieuwe topleveldomein met behulp van PowerShell

1. Op een computer die is [Azure Active Directory-Module voor Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) geïnstalleerd op het Hallo volgende uitvoeren: `$cred=Get-Credential`.  
2. Voer Hallo gebruikersnaam en wachtwoord van een globale beheerder voor Hallo u Federatie met Azure AD-domein
3. Voer in PowerShell`Connect-MsolService -Credential $cred`
4. Voer in PowerShell`New-MsolFederatedDomain –SupportMultipleDomain –DomainName`

Volgende stappen tooadd Hallo nieuw op het hoogste niveau domein via Azure AD Connect hello gebruiken.

1. Azure AD Connect vanaf Hallo bureaublad starten of het menu start
2. Kies 'Een extra Azure AD-domein toevoegen' ![toevoegen van een extra Azure AD-domein](./media/active-directory-multiple-domains/add1.png)
3. Voer uw Azure AD en Active Directory-referenties
4. Selecteer Hallo tweede domein dat u wenst dat tooconfigure voor Federatie.
   ![Toevoegen van een extra Azure AD-domein](./media/active-directory-multiple-domains/add2.png)
5. Klik op installeren

### <a name="verify-hello-new-top-level-domain"></a>Controleer of de nieuwe topleveldomein Hallo
Met behulp van PowerShell-opdracht Hallo `Get-MsolDomainFederationSettings -DomainName <your domain>`vindt u Hallo IssuerUri bijgewerkt.  Hallo schermafbeelding hieronder ziet u Hallo federatie-instellingen zijn bijgewerkt op de oorspronkelijke domein http://bmcontoso.com/adfs/services/trust

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

En Hallo IssuerUri in onze nieuwe domein toohttps://bmfabrikam.com/adfs/services/trust is ingesteld

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a>Ondersteuning voor subdomeinen
Wanneer u een subdomein toevoegt, wordt vanwege Hallo manier Azure AD domeinen verwerkt, wordt het Hallo-instellingen van de bovenliggende Hallo worden overgenomen.  Dit betekent dat Hallo IssuerUri moet toomatch Hallo ouders.

Zo kunnen zeggen bijvoorbeeld ik bmcontoso.com hebt en voeg vervolgens corp.bmcontoso.com.  Dit betekent dat Hallo IssuerUri voor een gebruiker vanuit corp.bmcontoso.com toobe moet **http://bmcontoso.com/adfs/services/trust.**  Maar Hallo standaard regel hierboven voor Azure AD wordt geïmplementeerd, wordt een token genereren met een verlener als **http://corp.bmcontoso.com/adfs/services/trust.** Dit wordt niet overeen met de vereiste waarde van het domein Hallo en mislukt de verificatie.

### <a name="how-tooenable-support-for-sub-domains"></a>Hoe tooenable ondersteuning bieden voor subdomeinen
In de volgorde toowork rond deze Hallo moet de AD FS vertrouwensrelatie van relying party voor Microsoft Online toobe bijgewerkt.  toodo, moet u een aangepaste claimregel configureren zodat deze uit alle subdomeinen van UPN-achtervoegsel van de gebruiker Hallo ontdoet tijdens het construeren van de waarde voor aangepaste Issuer Hallo. 

Hallo claim te volgen, wordt dit doen:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
Hallo laatste nummer in de reguliere expressie Hallo ingesteld Hallo hoeveel bovenliggende domeinen zich in het hoofddomein. Ik heb hier bmcontoso.com zodat twee bovenliggende domeinen nodig zijn. Als u drie domeinen bovenliggende toobe bewaard zijn (dat wil zeggen: corp.bmcontoso.com), en vervolgens Hallo nummer drie zijn zou. Een bereik Eventualy kan worden aangegeven, Hallo overeenkomst wordt altijd worden aangebracht toomatch Hallo maximum van domeinen. '{2,3}' komt overeen met twee toothree domeinen (dat wil zeggen: bmfabrikam.com en corp.bmcontoso.com).

Volgende stappen tooadd Hallo een aangepaste claim subdomeinen voor toosupport gebruiken.

1. Open AD FS-beheer
2. Vertrouwensrelatie van de Microsoft Online RP Hallo Klik met de rechtermuisknop en kies claimregels bewerken
3. Selecteer de derde claimregel Hallo en vervang ![Edit claim](./media/active-directory-multiple-domains/sub1.png)
4. Vervang de huidige claim Hallo:
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Claim vervangen](./media/active-directory-multiple-domains/sub2.png)

5. Klik op Ok.  Klik op toepassen.  Klik op Ok.  Sluit AD FS-beheer.

