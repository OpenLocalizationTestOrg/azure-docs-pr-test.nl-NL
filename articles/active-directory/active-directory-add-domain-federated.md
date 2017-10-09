---
title: aaaAdd uw aangepaste domeinnaam en het instellen van de federatieve aanmelding tooAzure Active Directory | Microsoft Docs
description: Hoe tooadd van uw bedrijf van domeinnamen tooAzure Active Directory tooset van federatieve aanmelden tussen Azure Active Directory en uw on-premises federation-oplossing
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 27126c7e-e6d6-4ef3-a4fb-f5f0706e749d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 77f8cc87c27871ac96581360762aaa8d24c0eb8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-your-custom-domain-name-tooazure-active-directory"></a>Uw aangepaste domein naam tooAzure Active Directory toevoegen
U kunt een aangepaste domeinnaam, zoals contoso.com configureren, zodat gebruikers in contoso.com een federatieve ervaring voor eenmalige aanmelding bij het bedrijfsnetwerk kunnen hebben. Als u al Active Directory Federation Services (AD FS hebt) of een andere federation-server uitgevoerd op uw bedrijfsnetwerk, kunt u uw aangepaste domeinnaam hello Azure AD Connect-hulpprogramma toouse Azure AD configureren. U kunt ook gebruik van Azure AD Connect toodeploy een nieuwe AD FS-omgeving en kunt u dit configureren voor federatieve eenmalige aanmelding tooAzure AD.

Als u geen hebt en bent niet van plan toodeploy AD FS of een andere federatieserver, volgt u deze instructies: [toevoegen van een aangepast domein naam tooAzure Active Directory](active-directory-add-domain.md).

## <a name="add-a-custom-domain-name-tooyour-directory"></a>Een aangepast domein naam tooyour map toevoegen
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com/) met een gebruikersaccount dat een globale beheerder van uw Azure AD-directory.
2. In **Active Directory**, open uw directory en selecteer Hallo **domeinen** tabblad.
3. Selecteer op de opdrachtbalk Hallo **toevoegen**, en voer vervolgens de naam van uw aangepaste domein, bijvoorbeeld 'contoso.com' Hallo. Ervoor tooinclude Hallo .com, .net of een andere extensie op het hoogste niveau zijn.
4. Selecteer Hallo **ik rekening houden tooconfigure dit domein voor eenmalige aanmelding met mijn lokale Active Directory** selectievakje.
5. Selecteer **Toevoegen**.

Hello Azure AD Connect-hulpprogramma tooget Hallo DNS-vermelding uitgevoerd gebruik die Azure AD tooverify Hallo domein. U ziet Hallo DNS-vermelding in Hallo **Azure AD Domain** stap in de wizard Hallo. U kunt zien welke stap in het Hallo-wizard lijkt [in deze instructies](connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation). Als u geen hello Azure AD Connect-hulpprogramma hebt, kunt u [hier downloaden](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Hallo DNS-vermelding op Hallo domeinnaamregistrar voor Hallo domein toevoegen
Hallo volgende stap toouse uw aangepaste domeinnaam met Azure AD is tooupdate Hallo DNS-zonebestand voor Hallo-domein. Hierdoor kan uw organisatie eigenaar is van de aangepaste domeinnaam hello Azure AD-tooverify.

1. Meld u aan toohello-website voor domeinnaamregistrar voor uw domeinnaam. Als u geen toegang tot toodo dit, vraagt u Hallo persoon die of het team in uw organisatie die over deze toegang toocomplete stap 2 en toolet die u weet wanneer deze is voltooid.
2. Update Hallo DNS-zonebestand voor Hallo domein door toe te voegen Hallo DNS-vermelding opgegeven tooyou door Azure AD. Deze DNS-vermelding kan Azure AD tooverify u eigenaar bent van Hallo-domein. Hallo DNS-vermelding is niet gewijzigd gedrag van bijvoorbeeld mailroutering of webhosting.

Voor hulp bij deze stap leest u de [Instructies voor het toevoegen van een DNS-vermelding bij populaire DNS-registrars](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Controleer of de domeinnaam Hallo met Azure AD
Nadat u Hallo DNS-vermelding hebt toegevoegd, bent u klaar tooverify Hallo domeinnaam met Azure AD.

tooverify hello domein, selecteer **volgende** op Hallo **Azure AD Domain** stap van hello Azure AD Connect-wizard. Azure AD zoekt Hallo DNS-vermelding in Hallo DNS-zonebestand voor Hallo-domein. Azure AD Controleer alleen Hallo-domeinnaam zodra Hallo DNS-records zijn doorgegeven. Doorgifte duurt vaak slechts enkele seconden, maar het kan ook een uur of langer duren. Als verificatie niet Hallo eerst werkt, probeer het later opnieuw.

Vervolgens kunt u doorgaan met de Hallo resterende stappen in hello Azure AD Connect-wizard. Hiermee worden de gebruikers van uw Windows Server AD-tooAzure AD gesynchroniseerd. Gesynchroniseerde gebruikers in Hallo-domein dat u hebt geconfigureerd voor Federatie kunnen kunnen tooget uit uw bedrijfsnetwerk tooAzure AD ondervindt een federatieve eenmalige aanmelding.

## <a name="troubleshooting"></a>Problemen oplossen
Als u een aangepaste domeinnaam niet kunt verifiëren, voer een van de volgende Hallo. We beginnen met Hallo veelgebruikte en werk omlaag toohello minst voorkomende.

1. **Wacht een uur**. DNS-records moeten toopropagate voordat u Azure AD domain Hallo kunt controleren. Dit kan een uur of langer duren.
2. **Zorg ervoor dat Hallo DNS-record is ingevoerd en of deze juist is**. Deze stap op Hallo-website voor domeinnaamregistrar voor domein Hallo Hallo hebt voltooid. Azure AD kan Hallo domeinnaam niet controleren als Hallo DNS-vermelding niet is aanwezig zijn op Hallo DNS-zonebestand, of als het is niet exact overeen met de Hallo DNS-vermelding die Azure AD u opgegeven. Als u geen toegang tot tooupdate DNS-records voor Hallo domein op Hallo domeinnaamregistrar, Hallo DNS-vermelding delen met Hallo persoon die of het team van uw organisatie die deze toegang heeft en vraagt u ze tooadd Hallo DNS-vermelding.
3. **Hallo-domeinnaam verwijderen uit een andere map in Azure AD**. Een domeinnaam kan maar in één map worden geverifieerd. Als een domeinnaam eerder is geverifieerd in een andere map, moet de domeinnaam daar eerst uit worden verwijderd voordat deze kan worden geverifieerd in een nieuwe map. toolearn over het verwijderen van domeinnamen gelezen [aangepaste domeinnamen beheren](active-directory-add-manage-domain-names.md).

## <a name="add-more-custom-domain-names"></a>Meer aangepaste domeinnamen toevoegen
Als uw organisatie gebruikmaakt van meerdere aangepaste domeinnamen, zoals 'contoso.com' en 'contosobank.com', kunt u deze up tooa maximaal 900 domeinnamen toevoegen. Hallo dezelfde in dit artikel tooadd elk van uw domeinnamen stappen gebruiken.

## <a name="next-steps"></a>Volgende stappen
* [Aangepaste domeinnamen beheren](active-directory-add-manage-domain-names.md)
* [Meer informatie over concepten met betrekking tot domeinbeheer in Azure AD](active-directory-add-domain-concepts.md)
* [De huisstijl van uw bedrijf weergeven wanneer uw gebruikers zich aanmelden](active-directory-add-company-branding.md)
* [Gebruik PowerShell toomanage domeinnamen in Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

