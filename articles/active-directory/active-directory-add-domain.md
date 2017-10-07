---
title: aaaAdd uw aangepaste domeinnaam tooAzure Active Directory | Microsoft Docs
description: Hoe tooadd van uw bedrijf van domeinnamen tooAzure Active Directory en hoe tooverify Hallo domeinnaam.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 35a6e20a-9907-432b-9d36-16b916a5c249
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: eb208138f2633aaecc54f68dc947caf80d856d23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-domain-name-tooazure-active-directory"></a>Toevoegen van een aangepast domein naam tooAzure Active Directory
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-domains-add-azure-portal.md)
> * [Klassieke Azure Portal](active-directory-add-domain.md)
> 
> 

U hebt een of meer domeinnamen dat uw organisatie gebruikmaakt van toodo bedrijven en uw gebruikers zich aanmelden met uw zakelijke domeinnaam tooyour-bedrijfsnetwerk. Nu u Azure Active Directory (Azure AD) gebruikt, kunt u uw bedrijfsdomein naam tooAzure AD ook toevoegen. Hiermee kunt u tooassign gebruikersnamen in Hallo directory die bekend tooyour gebruikers, zoals 'alice@contoso.com.' Hallo-proces is eenvoudig:

1. Hallo aangepast domein naam tooyour map toevoegen
2. Een DNS-vermelding voor de domeinnaam Hallo op Hallo domeinnaamregistrar toevoegen
3. Controleer of de aangepaste domeinnaam Hallo in Azure AD

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel. Voor hoe tooadd de naam van uw bedrijf domein in hello Azure AD-beheercentrum, Zie [beheerdersrollen toewijzen in Azure Active Directory](active-directory-domains-add-azure-portal.md).

Als u van plan tooconfigure uw aangepaste domein naam toobe gebruikt met Active Directory Federation Services (AD FS) of een andere beveiligingstokenservice (STS) in uw bedrijfsnetwerk bent, volgt u de instructies Hallo in [toevoegen en configureren van een domein Federatie met Azure Active Directory](active-directory-add-domain-federated.md). Dit is handig als u toosynchronize gebruikers van uw zakelijk directory tooAzure AD, plannen en [wachtwoordhashsynchronisatie](active-directory-aadconnectsync-implement-password-synchronization.md) voldoet niet aan uw vereisten.

## <a name="add-a-custom-domain-name-tooyour-directory"></a>Een aangepast domein naam tooyour map toevoegen
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com/) met een gebruikersaccount dat een globale beheerder van uw Azure AD-directory.
2. In **Active Directory**, open uw directory en selecteer Hallo **domeinen** tabblad.
3. Selecteer op de opdrachtbalk Hallo **toevoegen**. Naam van uw aangepaste domein, bijvoorbeeld 'contoso.com' hello invoeren. Zorg ervoor dat tooinclude Hallo .com, .net of een andere extensie op het hoogste niveau en laat Hallo selectievakje voor 'single sign-on' (federation) uitgeschakeld.
4. Selecteer **Toevoegen**.
5. Ophalen op de tweede pagina van wizard domein toevoegen op Hallo HALLO hallo DNS-vermelding dat Azure AD tooverify dat uw organisatie eigenaar is van de aangepaste domeinnaam hello wordt gebruikt.

Nu dat u Hallo domeinnaam hebt toegevoegd, moet uw organisatie eigenaar is van de domeinnaam Hallo Azure AD controleren. Azure AD om deze verificatie te kan uitvoeren, moet u een DNS-vermelding toevoegen in Hallo DNS-zonebestand voor Hallo domeinnaam. Deze taak wordt uitgevoerd op Hallo-website voor domeinnaamregistrar voor Hallo domeinnaam.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Hallo DNS-vermelding op Hallo domeinnaamregistrar voor Hallo domein toevoegen
Hallo volgende stap toouse uw aangepaste domeinnaam met Azure AD is tooupdate Hallo DNS-zonebestand voor Hallo-domein. Hierdoor kan uw organisatie eigenaar is van de aangepaste domeinnaam hello Azure AD-tooverify.

1. Meld u aan toohello domeinnaamregistrar voor Hallo-domein. Als u geen toegang tot tooupdate Hallo DNS-vermelding, vraagt u Hallo persoon of het team dat deze toegang toocomplete stap 2 is en toolet die u weet wanneer deze is voltooid.
2. Update Hallo DNS-zonebestand voor Hallo domein door toe te voegen Hallo DNS-vermelding opgegeven tooyou door Azure AD. Deze DNS-vermelding kan Azure AD tooverify u eigenaar bent van Hallo-domein. Hallo DNS-vermelding is niet gewijzigd gedrag van bijvoorbeeld mailroutering of webhosting.

Lees voor meer informatie over deze toe te voegen DNS-vermelding voor hello, [instructies voor het toevoegen van een DNS-vermelding bij populaire DNS-registrars](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Controleer of de domeinnaam Hallo met Azure AD
Nadat u Hallo DNS-vermelding hebt toegevoegd, bent u klaar tooverify Hallo domeinnaam met Azure AD.

Als er nog steeds Hallo **domein toevoegen** wizard openen, selecteer **controleren** op Hallo derde pagina van wizard Hallo. Wanneer u selecteert **controleren**, Azure AD wordt gezocht naar Hallo DNS-vermelding in Hallo DNS-zonebestand voor Hallo-domein. Azure AD kunt Hallo domeinnaam controleren nadat Hallo DNS-records zijn doorgegeven. Deze doorgifte duurt vaak slechts enkele seconden, maar het kan ook wel eens een uur of langer duren. Als verificatie niet Hallo eerst werkt, probeer het later opnieuw.

Als hello **domein toevoegen** wizard niet meer is geopend, kunt u controleren of Hallo domein in Hallo [klassieke Azure-portal](https://manage.windowsazure.com/):

1. Meld u aan met een gebruikersaccount met de rechten voor globale beheerder van uw Azure AD-directory.
2. Open uw directory en selecteer Hallo **domeinen** tabblad.
3. Selecteer Hallo domeinnaam dat u wilt dat tooverify en selecteer **controleren** op Hallo opdrachtbalk klikken.
4. Selecteer **controleren** Hallo dialoogvenster vak toocomplete Hallo verificatie.

Nu kunt u [gebruikersnamen toewijzen die uw aangepaste domeinnaam omvatten](active-directory-add-domain-add-users.md).

## <a name="troubleshooting"></a>Problemen oplossen
Als u een aangepaste domeinnaam niet kunt verifiëren, voer een van de volgende Hallo. We beginnen met Hallo veelgebruikte en werk omlaag toohello minst voorkomende.

1. **Wacht een uur**. DNS-records moeten toopropagate voordat u Azure AD domain Hallo kunt controleren. Dit kan een uur of langer duren.
2. **Zorg ervoor dat Hallo DNS-record is ingevoerd en of deze juist is**. Deze stap op Hallo-website voor domeinnaamregistrar voor domein Hallo Hallo hebt voltooid. Azure AD kan Hallo domeinnaam niet controleren als Hallo DNS-vermelding niet is aanwezig zijn op Hallo DNS-zonebestand, of als het is niet exact overeen met de Hallo DNS-vermelding die Azure AD u opgegeven. Als u geen toegang tot tooupdate DNS-records voor Hallo domein op Hallo domeinnaamregistrar, Hallo DNS-vermelding delen met Hallo persoon die of het team van uw organisatie die deze toegang heeft en vraagt u ze tooadd Hallo DNS-vermelding.
3. **Hallo-domeinnaam verwijderen uit een andere map in Azure AD**. Een domeinnaam kan maar in één map worden geverifieerd. Als een domeinnaam eerder is geverifieerd in een andere map, moet de domeinnaam daar eerst uit worden verwijderd voordat deze kan worden geverifieerd in een nieuwe map. toolearn over het verwijderen van domeinnamen gelezen [aangepaste domeinnamen beheren](active-directory-add-manage-domain-names.md).

## <a name="add-more-custom-domain-names"></a>Meer aangepaste domeinnamen toevoegen
Als uw organisatie gebruikmaakt van meerdere aangepaste domeinnamen, zoals 'contoso.com' en 'contosobank.com', kunt u deze up tooa maximaal 900 domeinnamen toevoegen. Hallo dezelfde in dit artikel tooadd elk van uw domeinnamen stappen gebruiken.

## <a name="next-steps"></a>Volgende stappen
* [Gebruikersnamen toewijzen die uw aangepaste domeinnaam omvatten](active-directory-add-domain-add-users.md)
* [Aangepaste domeinnamen beheren](active-directory-add-manage-domain-names.md)
* [Meer informatie over concepten met betrekking tot domeinbeheer in Azure AD](active-directory-add-domain-concepts.md)
* [De huisstijl van uw bedrijf weergeven wanneer uw gebruikers zich aanmelden](active-directory-add-company-branding.md)
* [Gebruik PowerShell toomanage domeinnamen in Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

