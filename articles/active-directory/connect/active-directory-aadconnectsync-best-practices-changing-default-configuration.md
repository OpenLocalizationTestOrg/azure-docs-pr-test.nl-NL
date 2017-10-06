---
title: 'Azure AD Connect-synchronisatie: Hallo standaardconfiguratie wijzigen | Microsoft Docs'
description: Bevat de aanbevolen procedures voor het wijzigen van de standaardconfiguratie Hallo van Azure AD Connect-synchronisatie.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7638a031-1635-4942-94c3-fce8f09eed5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: aa05e935edd02c49c3c3fdc198b854f50327847c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-best-practices-for-changing-hello-default-configuration"></a>Azure AD Connect-synchronisatie: aanbevolen procedures voor het wijzigen van de standaardconfiguratie Hallo
Hallo-doel van dit onderwerp is toodescribe en ondersteund wijzigingen tooAzure AD Connect-synchronisatie.

Hallo configuratie wordt gemaakt met Azure AD Connect werkt 'als zodanig' voor de meeste omgevingen die op de lokale Active Directory met Azure AD synchroniseren. In sommige gevallen kan is het echter nodig tooapply moet een aantal wijzigingen tooa configuratie toosatisfy een bepaald of de vereiste.

## <a name="changes-toohello-service-account"></a>Wijzigingen toohello-serviceaccount
Azure AD Connect-synchronisatie wordt uitgevoerd onder een serviceaccount dat is gemaakt door de installatiewizard Hallo. Dit serviceaccount bevat Hallo versleuteling sleutels toohello database die door synchronisatie wordt gebruikt. Deze is gemaakt met een lang wachtwoord 127 tekens en Hallo wachtwoord is ingesteld toonot verlopen.

* Het is **niet-ondersteunde** toochange of opnieuw instellen van Hallo-wachtwoord van Hallo-serviceaccount. In dat geval worden vernietigd versleutelingssleutels Hallo en Hallo-service is niet kunnen tooaccess Hallo database en niet kunnen toostart.

## <a name="changes-toohello-scheduler"></a>Wijzigingen toohello scheduler
Beginnen met Hallo releases van versie 1.1 (februari 2016) kunt u Hallo [scheduler](active-directory-aadconnectsync-feature-scheduler.md) toohave een andere synchronisatie cyclus dan Hallo standaard 30 minuten.

## <a name="changes-toosynchronization-rules"></a>Wijzigingen tooSynchronization regels
Hallo-installatiewizard biedt een configuratie die u toowork voor Hallo meest voorkomende scenario's moet. Als u toomake wijzigingen toohello configuratie nodig hebt, moet u deze regels toostill beschikt over een ondersteunde configuratie volgen.

* U kunt [kenmerkstromen wijzigen](active-directory-aadconnectsync-change-the-configuration.md#other-common-attribute-flow-changes) als Hallo standaard directe kenmerkstromen niet geschikt is voor uw organisatie zijn.
* Als u wilt dat te[niet stromen een kenmerk](active-directory-aadconnectsync-change-the-configuration.md#do-not-flow-an-attribute) en wordt verwijderd, een bestaand kenmerk in Azure AD, waarden moet u een regel toocreate voor dit scenario.
* [Uitschakelen van een ongewenste Synchronisatieregel](#disable-an-unwanted-sync-rule) in plaats van te verwijderen. Een verwijderde regel is gemaakt tijdens een upgrade.
* te[wijzigen van een regel voor out-of-box](#change-an-out-of-box-rule), moet u een kopie van Hallo oorspronkelijke regel en Hallo out of box regel uitschakelen. Hallo Sync Rule Editor wordt gevraagd en helpt u bij.
* Exporteer uw aangepaste synchronisatieregels met Hallo regeleditor synchronisatie. Hallo-editor kunt u met een PowerShell-script kunt u de tooeasily ze opnieuw maken in een noodherstelscenario.

> [!WARNING]
> Hallo out-of-box-sync-regels hebben een vingerafdruk. Als u een wijziging toothese regels aanbrengt wordt Hallo vingerafdruk niet langer overeenkomen. Mogelijk hebt u problemen in toekomstige Hallo wanneer u een nieuwe release van Azure AD Connect tooapply. Controleer alleen wijzigingen Hallo manier die wordt beschreven in dit artikel.

### <a name="disable-an-unwanted-sync-rule"></a>Een ongewenste Synchronisatieregel uitschakelen
Een synchronisatieregel voor out-of-box-niet verwijderen. Dit wordt opnieuw gemaakt tijdens de volgende upgrade.

In sommige gevallen Hallo-installatiewizard heeft heeft geleid tot een configuratie die voor uw topologie niet werkt. Bijvoorbeeld, als u een topologie met account-resource forest hebt, maar hebt u uitgebreide Hallo schema in Hallo account-forest met de Exchange-schema Hallo, worden vervolgens regels voor het uitwisselen van gemaakt voor Hallo accountforest- en Hallo bron-forest. In dit geval moet u toodisable hello Synchronisatieregel voor Exchange.

![Uitgeschakelde synchronisatieregel](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/exchangedisabledrule.png)

In Hallo afbeelding hierboven heeft Hallo-installatiewizard een oude Exchange 2003 schema gevonden in Hallo account-forest. Dit schema-uitbreiding is toegevoegd voordat het bronforest Hallo werd geïntroduceerd in de omgeving van Fabrikam. tooensure geen kenmerken van de oude Exchange-implementatie Hallo zijn gesynchroniseerd, Hallo synchronisatieregel moet worden uitgeschakeld, zoals wordt weergegeven.

### <a name="change-an-out-of-box-rule"></a>Een regel voor out-of-box wijzigen
de enige keer Hallo die moet u een out-of-box-regel is wanneer u toochange Hallo join regel. Als u een kenmerkstroom toochange moet, moet u een synchronisatieregel met hogere prioriteit dan Hallo out-of-box-regels maken. Hallo alleen regel moet u vrijwel tooclone Hallo regel **In uit Active Directory - gebruiker toevoegen**. U kunt alle andere regels met een hogere prioriteit regel onderdrukken.

Als u toomake wijzigingen tooan out of box regel moet, moet u een kopie maken van Hallo out-of-box-regel en de oorspronkelijke regel Hallo uitschakelen. Maak vervolgens een Hallo wijzigingen toohello gekloonde regel. Hallo regeleditor synchronisatie helpt u met deze stappen. Wanneer u een regel voor out-of-box opent, krijgt u dit dialoogvenster:  
![Waarschuwing buiten het vak regel](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/warningoutofboxrule.png)

Selecteer **Ja** toocreate een kopie van het Hallo-regel. Hallo gekloonde regel wordt geopend.  
![Gekloonde regel](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/clonedrule.png)

Breng eventuele vereiste wijzigingen tooscope, join en transformaties op deze gekloonde regel.

## <a name="next-steps"></a>Volgende stappen
**Overzichtsonderwerpen**

* [Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen](active-directory-aadconnectsync-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
