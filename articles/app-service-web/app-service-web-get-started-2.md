---
title: aaaAdd functionaliteit tooyour eerste web-app | Microsoft Docs
description: Handige functies tooyour eerste web-app in een paar minuten toevoegen.
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 542671c2-22f0-4f20-8b4b-fa477264c492
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2016
ms.author: cephalin
ms.openlocfilehash: 46c9b118c2c188508cb0a369c691a79073b7d7b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-functionality-tooyour-first-web-app"></a>Functionaliteit tooyour eerste web-app toevoegen
In [implementeren van uw eerste web-app tooAzure binnen vijf minuten](app-service-web-get-started-dotnet.md), u een voorbeeld-web-app aan geïmplementeerd [Azure App Service](../app-service/app-service-value-prop-what-is.md). In dit artikel hebt u snel een aantal handige functies tooyour geïmplementeerde web-app toevoegen. U gaat zo dadelijk het volgende doen:

* verificatie voor uw gebruikers afdwingen
* uw app automatisch schalen
* meldingen ontvangen op Hallo prestaties van uw app

Ongeacht welke voorbeeld-app u in het vorige artikel Hallo hebt geïmplementeerd, kunt u volgen langs in Hallo zelfstudie.

Hallo drie activiteiten in deze zelfstudie zijn slechts enkele voorbeelden van Hallo vele handige voorzieningen waarover die u krijgt wanneer u uw web-app in App Service plaatst. Veel van Hallo functies zijn beschikbaar in Hallo **vrije** laag (dit is wat uw eerste web-app wordt uitgevoerd), en u kunt uw proefabonnement tegoed tootry functies die een hogere prijscategorie vereisen. Erop vertrouwen dat uw web-app blijft in **vrije** servicetier tenzij u deze expliciet wijzigt tooa andere prijscategorie.

> [!NOTE]
> Hallo WebApp die u hebt gemaakt met Azure CLI wordt uitgevoerd in **vrije** laag, waardoor slechts één exemplaar in de gedeelde virtuele machine met resourcequota toe. Zie [App Service-beperkingen](../azure-subscription-service-limits.md#app-service-limits) voor meer informatie over wat u in de categorie **Gratis** krijgt.
> 
> 

## <a name="authenticate-your-users"></a>Uw gebruikers verifiëren
Nu gaan we kijken hoe gemakkelijk het is tooadd authentication tooyour-app (Lees hier meer over op [App Service-verificatie/autorisatie](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)).

1. Hallo-portalblade voor uw app, die u zojuist hebt geopend, klikt u op **instellingen** > **verificatie / autorisatie**.  
    ![Verificatie - blade Instellingen](./media/app-service-web-get-started/aad-login-settings.png)
2. Klik op **op** tooturn op verificatie.  
3. Klik in **Verificatieproviders** op **Azure Active Directory**.  
    ![Verificatie - Azure AD selecteren](./media/app-service-web-get-started/aad-login-config.png)
4. In Hallo **Azure Active Directory-instellingen** blade, klikt u op **Express**, klikt u vervolgens op **OK**. Hallo standaardinstellingen voor het maken van een nieuwe Azure AD-toepassing in de standaardmap.  
    ![Verificatie - express-configuratie](./media/app-service-web-get-started/aad-login-express.png)
5. Klik op **Opslaan**.  
    ![Verificatie - configuratie opslaan](./media/app-service-web-get-started/aad-login-save.png)
   
    Wanneer Hallo wijziging voltooid is, ziet u Hallo meldingenbel groen, samen met een bericht.
6. Terug in de portalblade van uw app hello, klikt u op Hallo **URL** koppeling (of **Bladeren** in de menubalk Hallo). Hallo-koppeling is een HTTP-adres.  
    ![Verificatie - bladeren tooURL](./media/app-service-web-get-started/aad-login-browse-click.png)  
    Maar nadat het Hallo-app geopend in een nieuw tabblad, Hallo URL vak omleidingen meermaals en eindigt op uw app met een HTTPS-adres. Wat u ziet, is dat u al bent aangemeld tooyour Azure-abonnement en u automatisch bent geverifieerd in Hallo-app.  
    ![Verificatie - aangemeld](./media/app-service-web-get-started/aad-login-browse-http-postclick.png)  
    Dus als u nu een niet-geverifieerde sessie in een andere browser opent, u een aanmeldingsscherm ziet als u toohello gaat dezelfde URL.  
    <!-- ![Authenticate - login page](./media/app-service-web-get-started/aad-login-browse.png)  -->
    Als u nooit eerder iets met Azure Active Directory hebt gedaan, bevat de standaardmap wellicht geen Azure AD-gebruikers. In dat geval is waarschijnlijk de enige account Hallo daar Hallo Microsoft-account met uw Azure-abonnement. Dat is waarom u automatisch aangemeld in toohello app Hallo dezelfde browser eerder.
    Op deze aanmeldingspagina ook kunt u die dezelfde toolog van Microsoft-account in.

Gefeliciteerd, u verifieert nu alle verkeer tooyour web-app.

Hebt u wellicht in Hallo **verificatie / autorisatie** -blade waarmee u veel meer, zoals doen kunt:

* Aanmelden bij sociale media inschakelen
* Opties voor meerdere aanmeldingen inschakelen
* Hallo-standaardgedrag wijzigen wanneer gebruikers eerst tooyour app navigeren

App Service biedt dat een directe oplossing voor een aantal algemene verificatiebehoeften Hallo moet dus u tooprovide hello verificatielogica zelf hoeft.
Zie [App Service-verificatie/autorisatie](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/) voor meer informatie.

## <a name="scale-your-app-automatically-based-on-demand"></a>Uw app automatisch schalen op basis van de vraag
Daarna laten we automatisch schalen uw app zodat deze automatisch wordt aangepast capaciteit toorespond toouser verzoek (Lees hier meer over op [opschalen van uw app in Azure](web-sites-scale.md) en [aantal exemplaren handmatig of automatisch schalen](../monitoring-and-diagnostics/insights-how-to-scale.md)).

Kort samengevat kunt u een web-app op twee manieren schalen:

* [Omhoog schalen](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): het verkrijgen van meer CPU, geheugen, schijfruimte en extra functies, zoals toegewezen virtuele machines, aangepaste domeinen en certificaten, faseringssites, automatisch schalen en meer. U opschalen door Hallo prijscategorie van uw app tot behoort de App Service-abonnement wijzigen.
* [Uitschalen](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Hallo aantal VM-exemplaren die worden uitgevoerd van uw app te verhogen.
  U kunt uitschalen tooas veel als 50 exemplaren, afhankelijk van uw prijscategorie.

We laten de details verder achterwege en gaan automatisch schalen instellen.

1. Eerst schalen we omhoog tooenable automatisch schalen. Hallo-portalblade van uw app, klikt u op **instellingen** > **omhoog schalen (App Service-Plan)**.  
    ![Omhoog schalen - blade Instellingen](./media/app-service-web-get-started/scale-up-settings.png)
2. Blader en selecteer Hallo **S1-standaard** servicetier, Hallo laagste categorie die ondersteuning biedt voor automatisch schalen (omcirkeld in de schermafbeelding) en klik op **Selecteer**.  
    ![Omhoog schalen - categorie kiezen](./media/app-service-web-get-started/scale-up-select.png)
   
    U bent klaar met omhoog schalen.
   
   > [!IMPORTANT]
   > Deze categorie verbruikt tegoeden van uw gratis proefversie. Als u een account voor betalen per gebruik hebt, worden er accountkosten kosten tooyour account.
   > 
   > 
3. Nu gaan we automatisch schalen configureren. Hallo-portalblade van uw app, klikt u op **instellingen** > **uitschalen (App Service-Plan)**.  
    ![Uitschalen - blade Instellingen](./media/app-service-web-get-started/scale-out-settings.png)
4. Wijziging **schalen door** te**CPU-Percentage**. Hallo schuifregelaars onder Hallo vervolgkeuzelijst worden dienovereenkomstig bijgewerkt. Vervolgens definieert u een bereik van **Exemplaren** tussen **1** en **2** en een **Doelbereik** tussen **40** en **80**. Dit doen door te typen in de vakken Hallo of Hallo schuifregelaars worden verplaatst.  
    ![Uitschalen - automatisch schalen configureren](./media/app-service-web-get-started/scale-out-configure.png)
   
    Op basis van deze configuratie wordt uw app automatisch uitgeschaald wanneer het CPU-gebruik hoger is dan 80% en ingeschaald wanneer het CPU-gebruik lager is dan 40%.
5. Klik op **opslaan** in de menubalk Hallo.

Gefeliciteerd, uw app wordt nu automatisch geschaald.

Hebt u wellicht in Hallo **schaalinstellingen** -blade waarmee u veel meer, zoals doen kunt:

* Tooa specifiek aantal exemplaren handmatig schalen
* Schalen op andere prestatiegegevens, zoals geheugenpercentage of wachtrij voor schijf
* Het schaalgedrag aanpassen wanneer er een prestatieregel wordt geactiveerd
* Automatisch schalen volgens een schema
* Gedrag van automatisch schalen instellen voor een toekomstige gebeurtenis

Zie [Scale up your app in Azure](web-sites-scale.md) (Uw app omhoog schalen in Azure) voor meer informatie over het omhoog schalen van uw app. Zie [Aantal exemplaren handmatig of automatisch schalen](../monitoring-and-diagnostics/insights-how-to-scale.md) voor meer informatie over uitschalen.

## <a name="receive-alerts-for-your-app"></a>Waarschuwingen voor uw app ontvangen
Nu dat uw app automatisch geschaald wordt, wat er gebeurt wanneer het maximumaantal instanties hello (2) is bereikt en CPU hoger is dan het gewenste verbruik (80%)?
U kunt een waarschuwing instellen (Lees hier meer over op [meldingen van waarschuwingen ontvangen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)) tooinform u deze situatie zodat u verder kunt omhoog of uitschalen uw app, bijvoorbeeld schalen. We gaan snel een waarschuwing instellen voor dit scenario.

1. Hallo-portalblade van uw app, klikt u op **extra** > **waarschuwingen**.  
    ![Waarschuwingen - blade Instellingen](./media/app-service-web-get-started/alert-settings.png)
2. Klik op **Waarschuwing toevoegen**. Klik op Hallo **Resource** vak, selecteer Hallo resource die eindigt op **(serverfarms)**. Dit is uw App Service-plan.  
    ![Waarschuwingen - waarschuwing toevoegen voor App Service-plan](./media/app-service-web-get-started/alert-add.png)
3. In **Naam** geeft u `CPU Maxed` op, in **Metriek** kiest u **CPU-percentage** en in **Drempelwaarde** de optie `90`. Selecteer vervolgens **E-mailadressen van eigenaren, bijdragers en lezers** en klik op **OK**.   
    ![Waarschuwingen - waarschuwing configureren](./media/app-service-web-get-started/alert-configure.png)
   
    Wanneer Azure is voltooid maken Hallo waarschuwing, wordt deze weergegeven in Hallo **waarschuwingen** blade.  
    ![Waarschuwingen - voltooid](./media/app-service-web-get-started/alert-done.png)

Gefeliciteerd, u krijgt nu waarschuwingen.

Met deze waarschuwingsinstelling wordt het CPU-verbruik elke vijf minuten gecontroleerd. Als deze waarde hoger is dan 90%, ontvangen u en iedereen die is geautoriseerd, per e-mail een waarschuwing. toosee iedereen die is toegelaten tooreceive Hallo waarschuwingen, gaat u back-toohello portalblade van uw app en klikt u op Hallo **toegang** knop.  
![Zien wie er waarschuwingen ontvangen](./media/app-service-web-get-started/alert-rbac.png)

U ziet dat **abonnementsbeheerders** zijn al Hallo **eigenaar** van Hallo-app. Deze groep zou u als u de accountbeheerder Hallo van uw Azure-abonnement (bijvoorbeeld uw proefabonnement) bevatten. Zie [Op rollen gebaseerd Azure-toegangsbeheer](../active-directory/role-based-access-control-configure.md) voor meer informatie over op rollen gebaseerd toegangsbeheer.

> [!NOTE]
> Waarschuwingsregels is een functie van Azure. Zie [Meldingen van waarschuwingen ontvangen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) voor meer informatie.
> 
> 

## <a name="next-steps"></a>Volgende stappen
Op uw manier tooconfigure Hallo waarschuwing, hebt u wellicht een uitgebreide set hulpprogramma's in Hallo **extra** blade. U kunt hier oplossen problemen, prestaties bewaken, testen op beveiligingsproblemen, resources beheren, communiceren met Hallo VM-console en nuttige extensies toevoegen. We nodigen u tooclick op elk van deze hulpprogramma's voor toodiscover Hallo eenvoudige maar krachtige hulpprogramma's op uw vinger tips.

Ontdek hoe u kunt meer met uw geïmplementeerde app toodo. Dit zijn slechts enkele voorbeelden:

* [Een aangepaste domeinnaam kopen en configureren](custom-dns-web-site-buydomains-web-app.md): koop een aantrekkelijke domeinnaam voor uw web-app in plaats van het domein *.azurewebsites.net. Of gebruik een domein dat u al hebt.
* [Faseringsomgevingen instellen](web-sites-staged-publishing.md) -implementeren van uw app tooa tijdelijke URL voordat u deze in productie. Werk uw live web-app probleemloos bij. Stel een uitgebreide DevOps-oplossing in met meerdere implementatiesites.
* [Continue implementatie instellen](app-service-continuous-deployment.md): integreer app-implementatie in uw bronbeheersysteem. Implementeer naar Azure met elke doorvoer.
* [Toegang tot on-premises resources](web-sites-hybrid-connection-get-started.md): maak gebruik van een bestaande on-premises database of een bestaand CRM-systeem.
* [Een back-up maken van uw app](web-sites-backup.md): stel voor uw web-app back-up- en herstelfunctionaliteit in. Bereid u voor op onverwachte problemen en het herstel daarvan.
* [Schakel diagnostische logboeken](web-sites-enable-diagnostic-log.md) -lezen Hallo IIS registreert van Azure of toepassingstraceringen. Lees ze in een stream, download ze of plaats ze in [Application Insights](../application-insights/app-insights-overview.md) voor directe analyse.
* [Uw app scannen op beveiligingsproblemen](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) -
  Scan uw web-app op actieve bedreigingen met behulp van de service die wordt geleverd door [Tinfoil Security](https://www.tinfoilsecurity.com/).
* [Achtergrondtaken uitvoeren](../azure-functions/functions-overview.md): voer taken uit voor gegevensverwerking, rapportage, enzovoort.
* [Ontdek hoe App Service werkt](../app-service/app-service-how-works-readme.md)

