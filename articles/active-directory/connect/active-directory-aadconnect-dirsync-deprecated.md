---
title: aaaUpgrade van DirSync en Azure AD Sync | Microsoft Docs
description: Hierin wordt beschreven hoe tooupgrade van DirSync en Azure AD Sync tooAzure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: bd68fb88-110b-4d76-978a-233e15590803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d465b137fb54f0c6e28ccf73429c4bd3aafd8698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a>Upgrade van Windows Azure Active Directory-synchronisatie en Azure Active Directory-synchronisatie
Azure AD Connect is Hallo aanbevolen manier tooconnect uw on-premises directory met Azure AD en Office 365. Dit is een fantastische tijd tooupgrade tooAzure AD Connect van Windows Azure Active Directory-synchronisatie (DirSync) of Azure AD Sync omdat deze hulpprogramma's zijn nu afgeschaft en zal bereiken op 13 April 2017 ondersteuning eindigt.

Hallo twee identiteit synchronisatie hulpprogramma's die zijn afgeschaft zijn beschikbaar voor klanten met één forest (DirSync) en voor meerdere forests en andere geavanceerde klanten (Azure AD Sync). Deze oudere hulpprogramma's zijn vervangen door een enkele oplossing die beschikbaar is voor alle scenario's: Azure AD Connect. Dit biedt nieuwe functionaliteit, verbeteringen en ondersteuning voor nieuwe scenario's. toobe kunnen toocontinue toosynchronize uw lokale identiteit gegevens tooAzure AD en Office 365, wordt aangeraden dat u een upgrade tooAzure AD uitvoert Connect.

Hallo laatste versie van DirSync in juli 2014 is uitgebracht en de laatste versie van Azure AD Sync Hallo werd uitgebracht in mei 2015.

## <a name="what-is-azure-ad-connect"></a>Wat is Azure AD Connect?
Azure AD Connect is Hallo opvolgende tooDirSync en Azure AD Sync. Het combineert alle scenario's deze twee ondersteund. U kunt meer lezen over in [uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).

## <a name="deprecation-schedule"></a>Afschaffing planning
| Date | Opmerking |
| --- | --- |
| 13 april 2016 |Windows Azure Active Directory-synchronisatie (DirSync') en Microsoft Azure Active Directory-synchronisatie ('Azure AD Sync) worden vermeld als afgeschaft. |
| 13 april 2017 |Ondersteuning eindigt. Klanten kunnen tooopen een ondersteuningsaanvraag zonder tooAzure AD upgrade niet meer worden eerst verbinding. |
|31 december 2017|Azure AD wordt communicatie van Windows Azure Active Directory-synchronisatie (DirSync') en Microsoft Azure Active Directory-synchronisatie ('Azure AD Sync') niet meer accepteren.

## <a name="how-tootransition-tooazure-ad-connect"></a>Hoe tootransition tooAzure AD Connect
Als u DirSync worden uitgevoerd, er zijn twee manieren waarop u een upgrade kunt uitvoeren: In-place upgrade en parallelle implementatie. Een in-place upgrade wordt aanbevolen voor de meeste klanten en als er een recent besturingssysteem en minder dan 50.000 objecten. In andere gevallen wordt het aanbevolen toodo een parallelle implementatie waar uw DirSync-configuratie is verplaatst tooa van de nieuwe server met Azure AD Connect.

Als u Azure AD Sync gebruikt, wordt een in-place upgrade aanbevolen. Als u wilt mogelijk tooinstall is een nieuwe Azure AD Connect-server parallel en doet een swing migratie van uw Azure AD Sync server tooAzure AD Connect.

| Oplossing | Scenario |
| --- | --- |
| [Upgraden van DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Als u een bestaande DirSync-server al wordt uitgevoerd.</li> |
| [Upgrade uitvoeren vanaf Azure AD Sync](active-directory-aadconnect-upgrade-previous-version.md) |<li>Als u Azure AD Sync overstapt.</li> |

Als u wilt dat toosee hoe toodo een in-place upgrade van DirSync tooAzure AD Connect en vervolgens deze Channel 9 video bekijken:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a>Veelgestelde vragen
**V: ik heb een e-mailbericht ontvangen van hello Azure Team en/of een bericht van Office 365-berichtencentrum hello, maar ik gebruik verbinding maken.**  
Hallo-melding is ook toocustomers met Azure AD Connect met een build-nummer 1.0 verzonden. \*.0 (met een pre-1.1-release). Microsoft raadt aan klanten toostay huidige met Azure AD Connect worden vrijgegeven. Hallo [Automatische upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) functie die is geïntroduceerd in 1.1 maakt het eenvoudig tooalways een recente versie van Azure AD Connect geïnstalleerd hebt.

**V: wordt DirSync/Azure AD Sync niet meer werken op 13 April 2017?**  
DirSync/Azure AD Sync blijven toowork op 13 April-2017.  Azure AD wordt echter niet meer communicatie van DirSync/Azure AD Sync accepteren op December 31 2017.

**V: welke versies DirSync kan ik upgraden van**  
Ondersteunde tooupgrade elke versie van de DirSync momenteel in gebruik is.

**V: hoe zit hello Azure AD-Connector voor FIM/MIM?**  
Hello Azure AD-Connector voor FIM/MIM heeft **niet** is aangekondigd als afgeschaft. Het is ingesteld op **functie bevriezing**; er is geen nieuwe functionaliteit is toegevoegd en het ontvangt geen oplossingen voor problemen. Microsoft raadt u aan klanten die gebruikmaken van tooplan toomove hieruit tooAzure AD Connect. Het wordt ten zeerste aanbevolen toonot start met behulp van deze nieuwe implementaties. Deze Connector worden aangekondigd afgeschaft in toekomstige Hallo.

## <a name="additional-resources"></a>Aanvullende resources
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
