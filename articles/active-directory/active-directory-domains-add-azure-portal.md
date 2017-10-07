---
title: aaaAdd uw aangepaste domeinnaam tooAzure Active Directory | Microsoft Docs
description: Hoe tooadd van uw bedrijf van domeinnamen tooAzure Active Directory en hoe tooverify Hallo domeinnaam.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d97e57c6-578a-4929-8fb8-42e858a711c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 88d5f443cd10b098a9a9ffb3137f5e1ca33b6aad
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

Met Azure Active Directory (Azure AD), kunt u uw bedrijfsdomein naam tooAzure AD ook toevoegen. U wellicht een domeinnamen die uw organisatie gebruikt toodo bedrijf en gebruikers die zich aanmeldt met uw zakelijke domeinnaam. Hallo domain name tooAzure AD toe te voegen kunt u tooassign gebruikersnamen in Hallo directory die bekend tooyour gebruikers, zoals 'alice@contoso.com.' Hallo-proces is eenvoudig:

1. Hallo aangepast domein naam tooyour map toevoegen
2. Een DNS-vermelding voor de domeinnaam Hallo op Hallo domeinnaamregistrar toevoegen
3. Controleer of de aangepaste domeinnaam Hallo in Azure AD

## <a name="how-do-i-add-a-domain-name"></a>Hoe kan ik een domeinnaam toevoegen
1. Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **meer services**, voer **Azure Active Directory** in het tekstvak Hallo en selecteer vervolgens **Enter**.
   
   ![Gebruikersbeheer openen](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Op Hallo ***mapnaam*** blade Selecteer **domeinnamen**.
4. Op Hallo  ***mapnaam* -domeinnamen** blade, selecteer Hallo **toevoegen** opdracht.
   
   ![Hallo Add-opdracht selecteren](./media/active-directory-domains-add-azure-portal/add-command.png)
5. Op Hallo **domeinnaam** blade Hallo-naam van uw aangepaste domein in Hallo vak opgeven, bijvoorbeeld 'contoso.com' en selecteer vervolgens **domein toevoegen**. Ervoor tooinclude Hallo .com, .net of een andere extensie op het hoogste niveau zijn.
6. Op Hallo ***domainname*** blade (dat wil zeggen, Hallo blade die wordt geopend met de naam van het nieuwe domein in Hallo titel), krijgen Hallo DNS-vermelding informatie die Azure AD tooverify dat uw organisatie eigenaar is van de aangepaste domeinnaam Hallo gebruikt.
   
   ![DNS-vermelding informatie ophalen](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

Nu dat u Hallo domeinnaam hebt toegevoegd, moet uw organisatie eigenaar is van de domeinnaam Hallo Azure AD controleren. Azure AD om deze verificatie te kan uitvoeren, moet u een DNS-vermelding toevoegen in Hallo DNS-zonebestand voor Hallo domeinnaam. Deze taak wordt uitgevoerd op Hallo-website voor domeinnaamregistrar voor Hallo domeinnaam.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Hallo DNS-vermelding op Hallo domeinnaamregistrar voor Hallo domein toevoegen
Hallo volgende stap toouse uw aangepaste domeinnaam met Azure AD is tooupdate Hallo DNS-zonebestand voor Hallo-domein. Hierdoor kan uw organisatie eigenaar is van de aangepaste domeinnaam hello Azure AD-tooverify.

1. Meld u aan toohello domeinnaamregistrar voor Hallo-domein. Als u geen toegang tot tooupdate Hallo DNS-vermelding, vraagt u Hallo persoon of het team dat deze toegang toocomplete stap 2 is en toolet die u weet wanneer deze is voltooid.
2. Update Hallo DNS-zonebestand voor Hallo domein door toe te voegen Hallo DNS-vermelding opgegeven tooyou door Azure AD. Deze DNS-vermelding kan Azure AD tooverify u eigenaar bent van Hallo-domein. Hallo DNS-vermelding is niet gewijzigd gedrag van bijvoorbeeld mailroutering of webhosting.

Lees voor meer informatie over deze toe te voegen DNS-vermelding voor hello, [instructies voor het toevoegen van een DNS-vermelding bij populaire DNS-registrars](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Controleer of de domeinnaam Hallo met Azure AD
Nadat u Hallo DNS-vermelding hebt toegevoegd, bent u klaar tooverify Hallo domeinnaam met Azure AD.

De naam van een domein kan worden gecontroleerd nadat de Hallo DNS-records zijn doorgegeven. Deze doorgifte duurt vaak slechts enkele seconden, maar het kan ook wel eens een uur of langer duren. Als verificatie niet Hallo eerst werkt, probeer het later opnieuw.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **Bladeren**Gebruikersbeheer invoeren in het tekstvak Hallo en selecteer vervolgens **Enter**.
   
   ![Gebruikersbeheer openen](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Op Hallo **Gebruikersbeheer - domeinnamen** blade, selecteer Hallo niet-geverifieerde domeinnaam die u tooverify wilt.
4. Op Hallo ***domainname*** blade (dat wil zeggen, Hallo blade die wordt geopend met de naam van het nieuwe domein in Hallo titel), selecteer **controleren** toocomplete Hallo verificatie.

Nu kunt u [gebruikersnamen toewijzen die uw aangepaste domeinnaam omvatten](active-directory-users-create-azure-portal.md).

## <a name="troubleshooting"></a>Problemen oplossen
Als u een aangepaste domeinnaam niet kunt verifiëren, voer een van de volgende Hallo. We beginnen met Hallo veelgebruikte en werk omlaag toohello minst voorkomende.

1. **Wacht een uur**. DNS-records moeten toopropagate voordat u Azure AD domain Hallo kunt controleren. Dit kan een uur of langer duren.
2. **Zorg ervoor dat Hallo DNS-record is ingevoerd en of deze juist is**. Deze stap op Hallo-website voor domeinnaamregistrar voor domein Hallo Hallo hebt voltooid. Azure AD kan Hallo domeinnaam niet controleren als Hallo DNS-vermelding niet is aanwezig zijn op Hallo DNS-zonebestand, of als het is niet exact overeen met de Hallo DNS-vermelding die Azure AD u opgegeven. Als u geen toegang tot tooupdate DNS-records voor Hallo domein op Hallo domeinnaamregistrar, Hallo DNS-vermelding delen met Hallo persoon die of het team van uw organisatie die deze toegang heeft en vraagt u ze tooadd Hallo DNS-vermelding.
3. **Hallo-domeinnaam verwijderen uit een andere map in Azure AD**. Een domeinnaam kan maar in één map worden geverifieerd. Als een domeinnaam eerder is geverifieerd in een andere map, moet de domeinnaam daar eerst uit worden verwijderd voordat deze kan worden geverifieerd in een nieuwe map. toolearn over het verwijderen van domeinnamen gelezen [aangepaste domeinnamen beheren](active-directory-domains-manage-azure-portal.md).    

## <a name="add-more-custom-domain-names"></a>Meer aangepaste domeinnamen toevoegen
Als uw organisatie gebruikmaakt van meerdere aangepaste domeinnamen, zoals 'contoso.com' en 'contosobank.com', kunt u deze up tooa maximaal 900 domeinnamen toevoegen. Hallo dezelfde in dit artikel tooadd elk van uw domeinnamen stappen gebruiken.

## <a name="next-steps"></a>Volgende stappen
[Aangepaste domeinnamen beheren](active-directory-domains-manage-azure-portal.md)

