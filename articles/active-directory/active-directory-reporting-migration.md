---
title: aaaFind activiteit rapporten in hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe Azure Active Directory-activiteit toofind rapporten in hello Azure-portal.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a>Activiteitsrapporten niet vinden in hello Azure-portal

Als u van Azure classic portal toohello hello Azure-portal overstapt, krijgt u een nieuwe kijken activiteitenlogboeken Azure Active Directory (Azure AD). In een recente [blogbericht](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we uitleggen hoe u de activiteit geregistreerd in de context Hallo Hallo resource u in hello Azure-portal werkt kunt zien. In dit artikel wordt beschreven hoe toofind rapporten die u in de klassieke Azure-portal in de Azure-portal Hallo Hallo gebruikt.

## <a name="whats-new"></a>Nieuwe functies

Rapporten in de klassieke Azure-portal Hallo zijn ingedeeld in categorieën:

1.  Beveiligingsrapporten
2.  Activiteitsrapporten
3.  Geïntegreerde app-rapporten

### <a name="activity-and-integrated-app-reports"></a>Activiteit en geïntegreerde app-rapporten

Voor context gebaseerde rapportage in hello Azure-portal, worden bestaande rapporten samenvoegen in één weergave. Een enkele, onderliggende API biedt Hallo toohello gegevensweergave.

Deze weergave op Hallo toosee **Azure Active Directory** blade onder **activiteit**, selecteer **controlelogboeken**.

![Controlelogboeken](./media/active-directory-reporting-migration/482.png "Controlelogboeken")

Hallo volgende rapporten worden geconsolideerd in deze weergave:

-   Controlerapport
-   Activiteit voor wachtwoord opnieuw instellen
-   Registratie-activiteit wachtwoord opnieuw instellen
-   In activiteit
-   Wijzigingen in de groep Office365 naam
-   Inrichten van de activiteit van een account
-   Overschakeling van de status van het wachtwoord
-   Fouten bij het inrichten van een account


Hallo toepassingsgebruik rapport is uitgebreid en is opgenomen in Hallo **aanmeldingen** weergeven. Deze weergave op Hallo toosee **Azure Active Directory** blade onder **activiteit**, selecteer **aanmeldingen**.

![Aanmeldingen weergave](./media/active-directory-reporting-migration/483.png "aanmeldingen weergeven")

Hallo **aanmeldingen** weergave bevat alle gebruikersaanmeldingen. U kunt deze gebruiksgegevens informatie tooget toepassing gebruiken. Ook vindt u informatie over het gebruik van de toepassing in Hallo **bedrijfstoepassingen** -overzicht in Hallo **beheren** sectie.

![Bedrijfstoepassingen](./media/active-directory-reporting-migration/484.png "bedrijfstoepassingen")

## <a name="access-a-specific-report"></a>Toegang tot een specifiek rapport

Hoewel hello Azure-portal één weergave biedt, kunt ook u bekijken bepaalde rapporten.

### <a name="audit-logs"></a>Controlelogboeken

In het antwoord toocustomer feedback kunt in hello Azure-portal, u geavanceerde filteren tooaccess Hallo gegevens die u wilt gebruiken. Een filter kunt u een *activiteitscategorie*, welke verschillende soorten activiteit Hallo lijsten wordt geregistreerd in Azure AD. toonarrow resulteert toowhat die u zoekt, kunt u een categorie selecteren.

Bijvoorbeeld, als u alleen geïnteresseerd in activiteiten gerelateerde tooself-service opnieuw instellen van wachtwoorden, kunt u Hallo **Self-service wachtwoordbeheer** categorie. Hallo-categorieën die u ziet zijn gebaseerd op Hallo resource die u in werkt.  

![Opties voor de categorie op Hallo Filter controlelogboeken pagina](./media/active-directory-reporting-migration/06.png "categorie-opties op Hallo Filter controlelogboeken pagina")

Categorieën voor activiteiten omvatten:

- Hoofddirectory
- Self-service voor wachtwoordbeheer
- Self-service voor groepsbeheer
- Account inrichten

### <a name="application-usage"></a>Gebruik van de toepassing

tooview om details over het gebruik van de toepassing voor alle apps of voor een enkele app onder **activiteit**, selecteer **aanmeldingen**. toonarrow Hallo resultaten, kunt u filteren op gebruikersnaam of toepassing.

![Filter aanmelden gebeurtenissen pagina](./media/active-directory-reporting-migration/07.png "pagina aanmelden gebeurtenissen filteren")

### <a name="security-reports"></a>Beveiligingsrapporten

#### <a name="azure-ad-anomalous-activity-reports"></a>Azure AD afwijkende activiteit rapporten

Azure AD-beveiligingsgroep voor afwijkende activiteit zijn rapporten van de klassieke Azure-portal Hallo geconsolideerde tooprovide u met één centrale weergave. Deze weergave toont alle risicogebeurtenissen die betrekking hebben op beveiliging dat Azure AD kunt detecteren en van rapporteren.

Hallo volgende tabel geeft een lijst hello Azure AD afwijkende activiteit beveiligingsrapporten en bijbehorende risico gebeurtenistypen in hello Azure-portal.

| Azure AD afwijkende activiteitenrapport |  Identity protection risico gebeurtenistype|
| :--- | :--- |
| Gebruikers van wie de referenties zijn gelekt | Gelekte aanmeldingsreferenties |
| Onregelmatige aanmeldingsactiviteiten | Onmogelijke reis tooatypical locaties |
| Aanmeldingen vanaf mogelijk geïnfecteerde apparaten | Aanmeldingen vanaf geïnfecteerde apparaten|
| Aanmeldingen van onbekende bronnen | Aanmeldingen vanaf anonieme IP-adressen |
| Aanmeldingen van IP-adressen met verdachte activiteit | Aanmeldingen van IP-adressen met verdachte activiteit |
| - | Aanmeldingen vanaf onbekende locaties |

Hello Azure AD-beveiligingsgroep voor afwijkende activiteit volgende rapporten zijn niet opgenomen als risicogebeurtenissen in hello Azure-portal:

* Aanmeldingen na meerdere mislukte pogingen
* Aanmeldingen vanuit meerdere locaties

Deze rapporten zijn nog steeds beschikbaar in de klassieke Azure-portal hello, maar ze op een bepaald moment in toekomstige hello wordt afgeschaft.

Zie [Risicogebeurtenissen in Azure Active Directory](active-directory-identity-protection-risk-events.md) voor meer informatie.  


#### <a name="detected-risk-events"></a>Gedetecteerde risico 's

In hello Azure-portal, opent u rapporten over gedetecteerde risicogebeurtenissen op Hallo **Azure Active Directory** blade onder **beveiliging**. Gedetecteerde risicogebeurtenissen die worden bijgehouden in Hallo rapporten te volgen:   

- Gebruikers risico
- Riskante aanmeldingen

![Beveiligingsrapporten](./media/active-directory-reporting-migration/04.png "beveiligingsrapporten")

Zie voor meer informatie over beveiligingsrapporten:

- [Gebruikers op risico beveiligingsrapport in hello Azure Active Directory-portal](active-directory-reporting-security-user-at-risk.md)
- [Riskant aanmeldingen rapport in hello Azure Active Directory-portal](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a>Activiteitsrapporten in Hallo klassieke Azure-portal versus hello Azure-portal

Hallo-tabel in deze sectie bevat bestaande rapporten in Hallo klassieke Azure-portal. Ook wordt beschreven hoe u toegang krijgen Hallo dezelfde gegevens in hello Azure-portal.

tooview alle gegevens, op Hallo controle **Azure Active Directory** blade onder **activiteit**, gaat u te**controlelogboeken**.

![Controlelogboeken](./media/active-directory-reporting-migration/61.png "Controlelogboeken")

| Klassieke Azure-portal                 | toofind in hello Azure-portal                                                         |
| ---                                  | ---                                                                        |
| Controlelogboeken                           | Voor **activiteitscategorie**, selecteer **Core Directory**.                       |
| Activiteit voor wachtwoord opnieuw instellen              | Voor **activiteitscategorie**, selecteer **Self-service wachtwoordbeheer**. |
| Registratie-activiteit wachtwoord opnieuw instellen | Voor **activiteitscategorie**, selecteer **Self-service wachtwoordbeheer**.     |
| In activiteit         | Voor **activiteitscategorie**, selecteer **groepsbeheer met Self-service**.        |
| Inrichten van de activiteit van een account        | Voor **activiteitscategorie**, selecteer **Account gebruikersaanvragen**.         |
| Overschakeling van de status van het wachtwoord             | Voor **activiteitscategorie**, selecteer **automatische overschakeling van de App-wachtwoord**.      |
| Fouten bij het inrichten van een account          | Voor **activiteitscategorie**, selecteer **Account gebruikersaanvragen**.        |
| Wijzigingen in de groep Office365 naam         | Voor **activiteitscategorie**, selecteer **Self-service wachtwoordbeheer**. Voor **activiteit brontype**, selecteer **groep**. Voor **Activiteitbron**, selecteer **O365 groepen**.|

Hallo tooview **toepassingsgebruik** rapport op Hallo **Azure Active Directory** blade onder **beheren**, selecteer **bedrijfstoepassingen**, en selecteer vervolgens **aanmeldingen**.


![Enterprise toepassingen aanmeldingen rapport](./media/active-directory-reporting-migration/199.png "Enterprise toepassingen aanmeldingen rapport")

## <a name="next-steps"></a>Volgende stappen

Zie voor een overzicht van reporting Hallo [rapportage van Azure Active Directory](active-directory-reporting-azure-portal.md).
