---
title: aaaTranslate koppelingen en URL's Azure AD-toepassingsproxy | Microsoft Docs
description: Bevat informatie over Hallo basisbeginselen van Azure AD-toepassingsproxy connectors.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7ec2b9fb01617067cf5d676037877bf72c19217b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="redirect-hardcoded-links-for-apps-published-with-azure-ad-application-proxy"></a>Koppelingen voor apps die zijn gepubliceerd met Azure AD-toepassingsproxy hardcoded omleiden

Azure AD-toepassingsproxy kunt u uw lokale apps beschikbaar toousers die extern zijn of op hun eigen apparaten. Sommige apps echter zijn ontwikkeld met lokale koppelingen ingesloten in Hallo HTML. Deze koppelingen werkt niet correct wanneer het Hallo-app op afstand wordt gebruikt. Wanneer er meerdere lokale toepassingen punt tooeach andere, verwachten uw gebruikers Hallo koppelingen tookeep werken wanneer ze niet op kantoor Hallo bent. 

Hallo aanbevolen manier toomake ervoor dat koppelingen werk Hallo dezelfde zowel binnen en buiten uw bedrijfsnetwerk tooconfigure Hallo externe URL's van uw apps toobe Hallo dezelfde als de interne URL's. Gebruik [aangepaste domeinen](active-directory-application-proxy-custom-domains.md) tooconfigure uw externe URL's toohave uw zakelijke domeinnaam in plaats van toepassing hello-proxy standaarddomein.

Als u aangepaste domeinen niet in uw tenant gebruiken, houdt uw koppelingen werken ongeacht waar uw gebruikers zich met Hallo koppeling NAT-functie van Application Proxy. Wanneer u apps die rechtstreeks toointernal eindpunten of poorten, kunt u toewijzen verwijzen hebt gepubliceerd deze interne URL's toohello externe toepassing Proxy-URL's. Wanneer de vertaling van koppelingen is ingeschakeld en toepassingsproxy doorzoekt HTML, CSS en JavaScript-select-tags voor gepubliceerde interne koppelingen. Vervolgens zet Hallo service voor toepassingsproxy deze om zodat uw gebruikers beschikken over een ononderbroken ervaring.

>[!NOTE]
>Hallo koppeling vertaling functie is voor tenants die voor welke reden dan ook niet met aangepaste domeinen toohave Hallo dezelfde interne en externe URL's voor hun apps. Voordat u deze functie inschakelt, zien als [aangepaste domeinen in Azure AD-toepassingsproxy](active-directory-application-proxy-custom-domains.md) voor u kan doen.
>
>Of Zie als Hallo-toepassing moet u tooconfigure met vertaling van koppelingen SharePoint is [alternatieve toegangstoewijzingen voor SharePoint 2013 configureren](https://technet.microsoft.com/library/cc263208.aspx) voor een andere benadering toomapping koppelingen.

## <a name="how-link-translation-works"></a>Hoe werkt de vertaling koppelen

Na verificatie wanneer de proxyserver Hallo Hallo toepassing gegevens toohello gebruiker verstrijkt toepassingsproxy scant Hallo-toepassing voor hardcoded koppelingen en vervangen door hun respectieve externe URL's gepubliceerd.

Toepassingsproxy wordt ervan uitgegaan dat de toepassingen zijn gecodeerd in UTF-8. Als dat niet Hallo geval is, geef Hallo coderingstype in een http-antwoordheader zoals `Content-Type:text/html;charset=utf-8`.

### <a name="which-links-are-affected"></a>Welke koppelingen worden beïnvloed?

Hallo koppeling NAT-functie wordt alleen gezocht voor koppelingen die in de code-codes in Hallo hoofdtekst van een app. Toepassingsproxy heeft een afzonderlijke functie voor het omzetten van cookies of URL's in de headers. 

Er zijn twee algemene typen interne koppelingen in on-premises toepassingen:

- **Relatieve interne koppelingen** dat punt tooa gedeelde bron in de structuur van een lokaal bestand zoals `/claims/claims.html`. Deze koppelingen werken automatisch in apps die zijn gepubliceerd via toepassingsproxy en doorgaan toowork met of zonder de vertaling van koppelingen. 
- **Interne koppelingen hardcoded** tooother lokale apps zoals `http://expenses` of bestanden zoals gepubliceerde `http://expenses/logo.jpg`. Hallo koppeling vertaling functie werkt op hardcoded interne koppelingen en toopoint toohello externe URL's die externe gebruikers toogo via moeten worden aangepast.

### <a name="how-do-apps-link-tooeach-other"></a>Hoe kunnen apps tooeach andere koppelen?

De vertaling van de koppeling is ingeschakeld voor elke toepassing zodat u controle over de gebruikerservaring Hallo op Hallo per app-niveau hebt. De vertaling van de koppeling voor een app inschakelen als u wilt dat Hallo koppelingen *van* die toobe app vertaald, geen koppelingen *naar* die app. 

Stel bijvoorbeeld dat u hebt drie toepassingen die zijn gepubliceerd via toepassingsproxy dat alle andere tooeach koppelen: voordelen, kosten en reizen. Er is een vierde Feedback, die niet is gepubliceerd via toepassingsproxy-app.

Wanneer u de vertaling van koppelingen voor Hallo voordelen app inschakelt, Hallo koppelingen tooExpenses en reizen omgeleide toohello externe URL's van deze apps zijn, maar Hallo koppeling tooFeedback omdat er geen externe URL niet wordt omgeleid. Koppelingen van kosten en reizen back tooBenefits niet werken, omdat de vertaling van de koppeling is niet ingeschakeld voor deze twee apps.

![Koppelingen van voordelen tooother apps wanneer de vertaling van koppelingen is ingeschakeld](./media/application-proxy-link-translation/one_app.png)

### <a name="which-links-arent-translated"></a>Welke koppelingen worden niet vertaald?

tooimprove prestaties en beveiliging, enkele koppelingen zijn niet omgezet:

- De koppelingen niet binnen de codetags. 
- Koppelingen niet in HTML, CSS of JavaScript. 
- Interne koppelingen geopend vanuit andere programma's. Koppelingen verzonden via e-mail of chatbericht of in andere documenten opgenomen won't worden vertaald. Hallo-gebruikers moeten tooknow toogo toohello externe URL.

Als u moet toosupport een van deze twee scenario's, gebruiken dezelfde Hallo interne en externe URL's in plaats van de vertaling van koppelingen.  

## <a name="enable-link-translation"></a>Link-omzetting inschakelen

Aan de slag met de vertaling van koppelingen is net zo eenvoudig als het klikken op een knop:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) als beheerder.
2. Ga te**Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen** > Selecteer Hallo app gewenste toomanage > **Toepassingsproxy**.
3. Schakel **vertalen URL's in de hoofdtekst van de toepassing** te**Ja**.

   ![Selecteer Ja tootranslate URL's in de hoofdtekst van de toepassing](./media/application-proxy-link-translation/select_yes.png).
4. Selecteer **opslaan** tooapply uw wijzigingen.

Nu wanneer uw gebruikers toegang krijgen deze toepassing tot, scant Hallo proxy automatisch voor interne URL's die zijn gepubliceerd via toepassingsproxy van uw tenant.

## <a name="send-feedback"></a>Feedback verzenden

We willen dit functie werk uw toomake help voor al uw apps. We zoeken naar meer dan 30 labels in HTML en CSS en welke JavaScript gevallen toosupport overweegt. Als u een voorbeeld van de gegenereerde koppelingen die niet zijn wordt vertaald hebt, stuurt u een codefragment te[Application Proxy Feedback](mailto:aadapfeedback@microsoft.com). 

## <a name="next-steps"></a>Volgende stappen
[Aangepaste domeinen gebruiken met Azure AD-toepassingsproxy](active-directory-application-proxy-custom-domains.md) toohave Hallo dezelfde interne en externe URL

[Alternatieve toegangstoewijzingen voor SharePoint 2013 configureren](https://technet.microsoft.com/library/cc263208.aspx)
