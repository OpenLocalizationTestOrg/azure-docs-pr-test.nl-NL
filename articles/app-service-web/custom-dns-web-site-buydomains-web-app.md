---
title: aaaBuy een aangepaste domeinnaam voor Azure-Web-Apps
description: Meer informatie over hoe een aangepast domein toobuy naam met een web-app in Azure App Service.
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a>Een aangepaste domeinnaam voor Azure-Web-Apps kopen

App Service-domeinen (preview) zijn op het hoogste niveau van de domeinen die worden beheerd rechtstreeks in Azure. Ze kunnen aangepaste domeinen eenvoudig toomanage [Azure Web Apps](app-service-web-overview.md). Deze zelfstudie leert u hoe namen tooAzure Web Apps toobuy een App Service-domein en DNS toewijzen.

Dit artikel is voor Azure App Service (Web-Apps, API-Apps, Mobile Apps, Logic Apps). Zie voor de virtuele machine in Azure of Azure Storage, [toewijzen App Service domein tooAzure VM of Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/). Zie voor Cloud-Services, [configureren van een aangepaste domeinnaam voor een Azure cloudservice](../cloud-services/cloud-services-custom-domain-name-portal.md).

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie:

* [Een App Service-app maken](/azure/app-service/), of gebruik een app die u hebt gemaakt voor een andere zelfstudie.

## <a name="prepare-hello-app"></a>Hallo app voorbereiden

aangepaste domeinen in Azure Web Apps, uw web-app van toouse [App Service-abonnement](https://azure.microsoft.com/pricing/details/app-service/) moet een betaald laag (**gedeelde**, **Basic**, **standaard**, of **Premium**). In deze stap maakt ervoor u zorgen dat Hallo web-app wordt in Hallo ondersteund prijscategorie.

### <a name="sign-in-tooazure"></a>Meld u aan tooAzure

Open Hallo [Azure-portal](https://portal.azure.com) en meld u aan met uw Azure-account.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Navigeer in hello Azure-portal toohello app

Selecteer in het linkermenu Hallo **App Services**, en selecteer vervolgens de naam Hallo van Hallo-app.

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-domain/select-app.png)

U ziet de pagina voor het beheren van App Service-app Hallo Hallo.  

### <a name="check-hello-pricing-tier"></a>Hallo prijscategorie controleren

Schuif in Hallo linkernavigatiebalk van de pagina app hello, toohello **instellingen** sectie en selecteer **opschalen (App Service-abonnement)**.

![Omhoog schalen-menu](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

de huidige tier Hallo-app wordt door een rand gemarkeerd. Controleren of die Hallo-app niet Hallo toomake **vrije** laag. Aangepaste DNS wordt niet ondersteund in Hallo **vrije** laag. 

![Controleer de prijscategorie](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Hallo App Service-abonnement is niet als **vrije**, sluit Hallo **Kies uw prijscategorie** pagina en te overslaan[kopen Hallo domein](#buy-the-domain).

### <a name="scale-up-hello-app-service-plan"></a>Hallo opschalen met App Service-abonnement

Selecteer een van de Hallo-free lagen (**gedeelde**, **Basic**, **standaard**, of **Premium**). 

Klik op **Selecteren**.

![Controleer de prijscategorie](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Wanneer u de volgende kennisgeving Hallo ziet, is Hallo schaalbewerking is voltooid.

![Schaal bewerking bevestigen](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a>Hallo domein kopen

### <a name="sign-in-tooazure"></a>Meld u aan tooAzure
Open Hallo [Azure-portal](https://portal.azure.com/) en meld u aan met uw Azure-account.

### <a name="launch-buy-domains"></a>Kopen domeinen starten
In Hallo **Web-Apps** en klik op Hallo-naam van uw web-app, selecteer **instellingen**, en selecteer vervolgens **aangepaste domeinen**
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

In Hallo **aangepaste domeinen** pagina, klikt u op **domeinen kopen**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a>Hallo domein aankoop configureren

In Hallo **Service toepassingsdomein** pagina in Hallo **zoeken naar domein** vak, Hallo-domeinnaam voor het type gewenste toobuy en het type `Enter`. Hallo worden voorgestelde beschikbare domeinen weergegeven onder het tekstvak Hallo. Selecteer een of meer domeinen die u wilt dat toobuy. 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

Klik op Hallo **contactgegevens** en van het domein Hallo contactgegevens formulier invullen. Wanneer u klaar bent, klikt u op **OK** tooreturn toohello Service toepassingsdomein pagina.
   
Het is belangrijk dat u alle vereiste velden met zo nauwkeurig mogelijk invullen. Onjuiste gegevens voor de contactgegevens kan resulteren in fout toopurchase domeinen. 

Selecteer vervolgens de gewenste Hallo opties voor uw domein. Zie Hallo tabel uitleg:

| Instelling | Voorgestelde waarde | Beschrijving |
|-|-|-|
|Automatisch vernieuwen | **Inschakelen** | Hiermee vernieuwt u uw App Service-domein automatisch elk jaar. Uw creditcard in rekening gebracht dezelfde aankoopbedrag Hallo op Hallo moment van verlenging. |
|Privacybescherming | Inschakelen | Opt-in te 'Privacy protection', dat van het aankoopbedrag Hallo uitmaakt deel _gratis_ (met uitzondering van het hoogste niveau domeinen die het register ondersteunen geen privacybescherming, zoals _. co.in_, _. CO.uk_, enzovoort). |
| Standaard hostnamen toewijzen | **www** en**@** | Selecteer Hallo gewenste hostnaambindings, indien gewenst. Wanneer Hallo domein aankoop voltooid is, kan uw web-app op geselecteerde Hallo hostnamen worden benaderd. Als de web-app Hallo zich achter [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), er geen Hallo optie tooassign Hallo-hoofddomein (@), omdat het Traffic Manager biedt geen ondersteuning voor A-records. U kunt wijzigingen aanbrengen toohello hostnaam toewijzingen nadat Hallo domein aankoop is voltooid. |

### <a name="accept-terms-and-purchase"></a>Voorwaarden accepteren en kopen

Klik op **juridische voorwaarden** tooreview Hallo voorwaarden en Hallo kosten, klik vervolgens op **kopen**.

> [!NOTE]
> App Service-domeinen Azure DNS toohost Hallo domeinen gebruiken. Daarnaast toohello domain registration kosten gebruikskosten voor Azure DNS-toepassing. Zie voor informatie [prijzen van Azure DNS-](https://azure.microsoft.com/pricing/details/dns/).
>
>

Terug in Hallo **Service toepassingsdomein** pagina, klikt u op **OK**. Tijdens het Hallo-bewerking wordt uitgevoerd, ziet u Hallo meldingen te volgen:

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a>Hallo hostnamen testen

Als u de standaard hostnamen tooyour web-app hebt toegewezen, ziet u ook een melding geslaagd voor elke geselecteerde hostnaam. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

U ziet ook Hallo geselecteerd hostnamen in Hallo **aangepaste domeinen** pagina in Hallo **hostnamen** sectie. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

tootest hello hostnamen, navigeer hostnamen toohello vermeld in de browser Hallo. Hallo-voorbeeld in Hallo voorgaande schermafbeelding probeert in too_kontoso.net_ navigeren en _www.kontoso.net_.

## <a name="assign-hostnames-tooweb-app"></a>Hostnamen tooweb app toewijzen

Als u ervoor geen tooassign een kiest of meer standaard hostnamen tooyour web-app tijdens Hallo aankoopproces, of als u een hostnaam tooassign niet moet worden weergegeven, kunt u een hostnaam op elk gewenst moment kunt toewijzen.

U kunt andere web-app ook hostnamen in Hallo App Service-domein tooany. Hallo stappen afhankelijk van of Hallo App Service-domein en Hallo web-app toohello behoren hetzelfde abonnement.

- Ander abonnement: aangepaste DNS-records van App Service-domein toohello web-app als een extern gekochte domein Hallo toewijzen. Zie voor informatie over het toevoegen van aangepaste DNS tooan App Service-domein namen, [aangepaste DNS-records beheren](#custom). een externe gekochte domein tooa web-app toomap Zie [toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps](app-service-web-tutorial-custom-domain.md). 
- Hetzelfde abonnement: gebruik Hallo stappen te volgen.

### <a name="launch-add-hostname"></a>Start de hostnaam toevoegen
In Hallo **App Services** pagina, selecteer Hallo-naam van uw web-app die u wilt dat tooassign hostnamen te selecteren **instellingen**, en selecteer vervolgens **aangepaste domeinen**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

Controleer of uw aangeschafte domein wordt vermeld in Hallo **Service AppDomains** sectie, maar niet selecteren. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> Alle App Service-domeinen in hetzelfde abonnement worden weergegeven in Hallo van web-app Hallo **aangepaste domeinen** pagina. Als uw domein in het abonnement Hallo van web-app, maar u deze niet in Hallo van web-app ziet **aangepaste domeinen** pagina, opnieuw Hallo **aangepaste domeinen** of Hallo webpagina Vernieuw deze pagina. Controleer ook Hallo melding Bel bovenaan Hallo hello Azure-portal voor fouten in de voortgang of maken.
>
>

Selecteer **hostnaam toevoegen**.

### <a name="configure-hostname"></a>Hostname configureren
In Hallo **hostnaam toevoegen** dialoogvenster, type Hallo volledig gekwalificeerde domeinnaam van uw App Service-domein of elk subdomein. Bijvoorbeeld:

- kontoso.NET
- www.kontoso.NET
- ABC.kontoso.NET

Wanneer u klaar bent, selecteert u **valideren**. Hallo hostnaam recordtype wordt automatisch geselecteerd voor u.

Selecteer **hostnaam toevoegen**.

Als het Hallo-bewerking is voltooid, ziet u een melding geslaagd voor Hallo hostnaam toegewezen.  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a>Sluit de hostnaam toevoegen
In Hallo **hostnaam toevoegen** pagina, een andere hostnaam tooyour web-app, desgewenst toewijzen. Wanneer u klaar bent, sluit u Hallo **hostnaam toevoegen** pagina.

U ziet nu Hallo zojuist toegewezen hostname(s) in uw app **aangepaste domeinen** pagina.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a>Hallo hostnamen testen

Navigeer hostnamen toohello vermeld in de browser Hallo. Probeer too_abc.kontoso.net_ navigeren in voorbeeld Hallo in Hallo voorgaande schermafbeelding.

<a name="custom" />

## <a name="manage-custom-dns-records"></a>Aangepaste DNS-records beheren

In Azure, DNS-records voor een App-domein worden beheerd met [Azure DNS](https://azure.microsoft.com/services/dns/). U kunt toevoegen, verwijderen, en DNS-records bijwerken, net als voor een extern gekochte domein.

### <a name="open-app-service-domain"></a>Open-App Service-domein

Selecteer in de Azure-portal in het linkermenu hello, Hallo **meer Services** > **Service AppDomains**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Selecteer Hallo domein toomanage. 

### <a name="access-dns-zone"></a>Toegang tot DNS-zone

Selecteer in het linkermenu Hallo-domein, **DNS-zone**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

Hiermee Hallo [DNS-zone](../dns/dns-zones-records.md) pagina van uw App Service-domein in Azure DNS. Voor meer informatie over tooedit DNS-records, Zie [hoe toomanage DNS-Zones in Azure-portal Hallo](../dns/dns-operations-dnszones-portal.md).

## <a name="cancel-purchase-delete-domain"></a>(Domein verwijderen) aankoop annuleren

Als u Hallo toepassingsdomein Service koopt, hebt u vijf dagen toocancel uw aankoop voor een volledige terugbetaling. Na vijf dagen Hallo App Service-domein kunt verwijderen, maar kan geen restitutie ontvangen.

### <a name="open-app-service-domain"></a>Open-App Service-domein

Selecteer in de Azure-portal in het linkermenu hello, Hallo **meer Services** > **Service AppDomains**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Hallo domein tooyou wilt toocancel selecteren of te verwijderen. 

### <a name="delete-hostname-bindings"></a>Hostnaambindings verwijderen

Selecteer in het linkermenu Hallo-domein, **hostnaambindings**. hostnaambindings Hallo van alle Azure-services worden hier weergegeven.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

U kunt Hallo App Service-domein niet verwijderen nadat alle hostnaambindings zijn verwijderd.

De binding voor elke hostnaam verwijderen door het selecteren van **...**   >  **Verwijderen**. Nadat alle Hallo-bindingen zijn verwijderd, selecteert u **opslaan**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a>Annuleren of verwijderen

Selecteer in het linkermenu Hallo-domein, **overzicht**. 

Als Hallo annulering periode op Hallo aangeschaft domein niet is verstreken, selecteert u **aankoop annuleren**. Anders ziet u een **verwijderen** knop in plaats daarvan. toodelete hello domein zonder een restitutie, selecteer **verwijderen**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

Selecteer **OK** tooconfirm Hallo-bewerking. Als u niet dat tooproceed wilt, klikt u buiten Hallo bevestigingsvenster.

Nadat het Hallo-bewerking is voltooid, Hallo domein is vrijgegeven voor uw abonnement en beschikbaar zijn voor iedereen toopurchase opnieuw. 
