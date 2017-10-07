---
title: aaaAssign licenties tooa groep in Azure Active Directory | Microsoft Docs
description: Hoe tooassign toousers licenties via Azure Active Directory-groep licentieverlening
services: active-directory
keywords: Azure AD-licentieverlening
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 148fe1bdd6c7f477a00c1f76bd8fa7d29c7b1f2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-licenses-toousers-by-group-membership-in-azure-active-directory"></a>Toewijzen van licenties toousers door het lidmaatschap in Azure Active Directory

Dit artikel begeleidt u bij het toewijzen van licenties tooa productgroep van gebruikers in Azure Active Directory (Azure AD) en vervolgens verifiëren dat ze correct zijn gelicentieerd.

In dit voorbeeld bevat Hallo tenant een beveiligingsgroep met de naam **HR-afdeling**. Deze groep bevat alle leden van de afdeling human resources voor hello (ongeveer 1000 gebruikers). Wilt u tooassign Office 365 Enterprise E3 licenties toohello hele afdeling. Hallo Yammer Enterprise-service die opgenomen in het Hallo-product moet tijdelijk worden uitgeschakeld totdat Hallo afdeling is gereed toostart gebruiken. Wilt u er ook toodeploy Enterprise Mobility + Security licenties toohello dezelfde groep gebruikers.

> [!NOTE]
> Sommige Microsoft-services zijn niet beschikbaar op alle locaties. Voordat u een licentie kan tooa gebruiker worden toegewezen, heeft Hallo beheerder toospecify Hallo gebruik locatie-eigenschap op Hallo-gebruiker.

> Groep licentie wilt toewijzen neemt alle gebruikers zonder een gebruikslocatie opgegeven locatie op Hallo van Hallo directory. Als u gebruikers op meerdere locaties hebt, raden wij aan altijd gebruikslocatie ingesteld als onderdeel van de stroom van de gebruiker maken in Azure AD (bijvoorbeeld via AAD Connect-configuratie) - Hallo resultaat van de licentietoewijzing altijd juist is en gebruikers ontvangen geen zo dat Services in de locaties die niet zijn toegestaan.

## <a name="step-1-assign-hello-required-licenses"></a>Stap 1: Hallo vereist licenties toewijzen

1. Meld u aan toohello [ **Azure-portal** ](https://portal.azure.com) met een administratoraccount. toomanage licenties Hallo-account moet een globale beheerder rol of de gebruiker de accountbeheerder.

2. Selecteer **meer services** in het navigatiedeelvenster links Hallo en selecteer vervolgens **Azure Active Directory**. U kunt deze blade tooFavorites toevoegen of toohello portal dashboard vastmaken.

3. Op Hallo **Azure Active Directory** blade Selecteer **licenties**. Hiermee opent u een blade kunt u zien en beheren van alle licensable producten in Hallo-tenant.

4. Onder **alle producten**, selecteert u Office 365 Enterprise E3 en de Enterprise Mobility + Security door Hallo productnamen te selecteren. toostart hello toewijzing, selecteer **toewijzen** Hallo boven aan het Hallo-blade.

   ![Alle producten toewijzen licentie](media/active-directory-licensing-group-assignment-azure-portal/all-products-assign.png)

5. Op Hallo **licentie toewijzen** blade, klikt u op **gebruikers en groepen** tooopen hello **gebruikers en groepen** blade. Zoeken naar Hallo groepsnaam *HR-afdeling*Hallo groep selecteren en vervolgens worden ervoor tooconfirm door te klikken op **Selecteer** Hallo Hallo blade onderaan in.

   ![Selecteer een groep](media/active-directory-licensing-group-assignment-azure-portal/select-a-group.png)

6. Op Hallo **licentie toewijzen** blade, klikt u op **toewijzingsopties (optioneel)**, weergeven met alle service-abonnementen worden opgenomen in Hallo twee producten dat we eerder hebt geselecteerd. Zoeken naar **Enterprise Yammer** en schakel het **uit** toodisable die van de productlicentie Hallo. Controleren door te klikken op **OK** Hallo onderaan in **toewijzingsopties**.

   ![Opties voor toewijzing](media/active-directory-licensing-group-assignment-azure-portal/assignment-options.png)

7. toocomplete hello toewijzing op Hallo **licentie toewijzen** blade, klikt u op **toewijzen** Hallo Hallo blade onderaan in.

8. Een melding wordt weergegeven in Hallo rechterbovenhoek waarin Hallo status en het resultaat van Hallo-proces. Hallo toewijzing toohello groep kan niet worden voltooid (bijvoorbeeld vanwege bestaande licenties in de groep Hallo), klikt u op Hallo melding tooview details van Hallo-fout.

We hebt nu een licentiesjabloon voor Hallo HR-afdeling groep opgegeven. Een achtergrondproces in Azure AD is gestart tooprocess alle bestaande leden van die groep. Deze eerste bewerking kan even duren, afhankelijk van de huidige grootte van de groep Hallo Hallo. In de volgende stap Hallo we beschrijven hoe tooverify dat Hallo-proces is voltooid en vaststellen of verdere actie vereist tooresolve problemen.

> [!NOTE]
> U kunt starten dezelfde toewijzing van een alternatieve locatie Hallo: **gebruikers en groepen** in Azure AD. Ga te**Azure Active Directory** > **gebruikers en groepen** > **alle groepen**. Vervolgens zoeken Hallo groep, selecteert u deze en ga toohello **licenties** tabblad Hallo **toewijzen** knop boven op de blade Hallo Hallo licentie toewijzing blade wordt geopend.

## <a name="step-2-verify-that-hello-initial-assignment-has-finished"></a>Stap 2: Controleren of de eerste toewijzing Hallo is voltooid

1. Ga te**Azure Active Directory** > **gebruikers en groepen** > **alle groepen**. Hallo gaat u naar **HR-afdeling** die licenties zijn toegewezen aan.

2. Op Hallo **HR-afdeling** Selecteer groep blade **licenties**. Hiermee kunt u snel bevestigen als licenties volledig toousers toegewezen is en als er geen fouten bevat die u nodig hebt toolook in. Hallo volgende informatie is beschikbaar:

   - Lijst met productlicenties die momenteel toohello groep toegewezen. Selecteer een vermelding tooshow Hallo specifieke services die zijn ingeschakeld en toomake wordt gewijzigd.

   - Status van het meest recente licentie wijzigingen hello, die zijn aangebracht toohello groep (als Hallo wijzigingen worden verwerkt of als verwerking is voltooid voor alle leden van de gebruiker).

   - Informatie over gebruikers die zich in een foutstatus omdat licenties toothem kunnen niet worden toegewezen.

   ![Opties voor toewijzing](media/active-directory-licensing-group-assignment-azure-portal/assignment-errors.png)

3. Meer gedetailleerde informatie over het verwerken van onder licentie **Azure Active Directory** > **gebruikers en groepen** > *groepsnaam* > **controlelogboeken**. Houd er rekening mee Hallo activiteiten te volgen:

   - Activiteit: **toe te passen op basis van groep licentie toousers**. Dit wordt geregistreerd wanneer Hallo systeem hervat Hallo licentie-toewijzing wijzigen op het Hallo-groep en toepassen van tooall gebruiker leden is gestart. Bevat informatie over Hallo wijziging die is gemaakt.

   - Activiteit: **klaar bent met het toepassen van de groep op basis van licentie toousers**. Dit wordt geregistreerd wanneer Hallo systeem klaar is met verwerking van alle gebruikers in de groep Hallo. Het bevat een overzicht van hoeveel gebruikers zijn verwerkt en hoeveel gebruikers groep licenties kunnen niet worden toegewezen.

   [Lees dit gedeelte](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity) toolearn meer informatie over hoe controlelogboeken gebruikte tooanalyze wijzigingen uit op basis van een groep licenties kunnen worden.

## <a name="step-3-check-for-license-problems-and-resolve-them"></a>Stap 3: Controleren of er licentieproblemen en deze kunt oplossen

1. Ga te**Azure Active Directory** > **gebruikers en groepen** > **alle groepen**, en zoek Hallo **HR-afdeling**die licenties zijn toegewezen aan.
2. Op Hallo **HR-afdeling** Selecteer groep blade **licenties**. Hallo-melding boven op Hallo blade geeft aan dat er 10 gebruikers die licenties kunnen niet worden toegewezen aan. Erop te klikken, opent u een lijst van alle gebruikers in een status-licentieverlening fout voor deze groep.
3. Hallo **toewijzingen mislukt** kolom vertellen beide productlicenties toohello gebruikers kunnen niet worden toegewezen. Hallo **belangrijkste reden voor fout** kolom Hallo oorzaak van de Hallo fout bevat. In dit geval heeft **serviceplannen conflicterende**.

   ![Mislukte toewijzingen](media/active-directory-licensing-group-assignment-azure-portal/failed-assignments.png)

4. Selecteer een gebruiker tooopen hello **licenties** blade. Deze blade ziet u alle licenties die momenteel toohello gebruiker zijn toegewezen. In dit voorbeeld Hallo gebruiker Hallo Office 365 Enterprise E1 licentie is die is overgenomen van Hallo **kioskmodus gebruikers** groep. Dit veroorzaakt een conflict met de Hallo E3-licentie die systeem probeert tooapply van Hallo Hallo **HR-afdeling** groep. Als gevolg hiervan is geen Hallo licenties van die groep toegewezen toohello gebruiker.

   ![Licenties voor een gebruiker weergeven](media/active-directory-licensing-group-assignment-azure-portal/user-license-view.png)

5. toosolve dit conflict Hallo-gebruiker verwijderen uit Hallo **kioskmodus gebruikers** groep. Nadat u Azure AD verwerkt Hallo wijziging, Hallo **HR-afdeling** licenties correct zijn toegewezen.

   ![Correct toegewezen licentie](media/active-directory-licensing-group-assignment-azure-portal/license-correctly-assigned.png)

## <a name="next-steps"></a>Volgende stappen

informatie over de functie Hallo instellen voor Licentiebeheer van de via groepen, toolearn Zie Hallo artikelen te volgen:

* [Wat is licentieverlening in Azure Active Directory op basis van groep?](active-directory-licensing-whatis-azure-portal.md)
* [Opsporen en oplossen van licentieproblemen met een voor een groep in Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Hoe toomigrate afzonderlijk in licentie gegeven gebruikers licentieverlening in Azure Active Directory op basis van toogroup](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory-licentieverlening voor aanvullende scenario's op basis van groep](active-directory-licensing-group-advanced.md)
