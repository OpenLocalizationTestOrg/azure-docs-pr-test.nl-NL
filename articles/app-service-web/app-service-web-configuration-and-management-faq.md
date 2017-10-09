---
title: aaaConfiguration Veelgestelde vragen voor Azure-web-apps | Microsoft Docs
description: Toofrequently van antwoorden op veelgestelde vragen over configuratie en beheerproblemen voor de functie voor Hallo-Web-Apps van Azure App Service worden opgehaald.
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 5aa405582813291a4aaf144d2f821ecb20a5edcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-faqs-for-web-apps-in-azure"></a>Configuratie- en veelgestelde vragen voor Web-Apps in Azure

Dit artikel bevat antwoorden toofrequently gevraagd Veelgestelde vragen over configuratie en beheer problemen Hallo [functie van Azure App Service Web Apps](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="are-there-limitations-i-should-be-aware-of-if-i-want-toomove-app-service-resources"></a>Zijn er beperkingen die ik houden moet rekening als ik wil toomove App Service-bronnen?

Als u van plan toomove App Service resources tooa nieuwe resourcegroep of abonnement bent, zijn er enkele beperkingen toobe op de hoogte van. Zie voor meer informatie [App Service-beperkingen](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).

## <a name="how-do-i-use-a-custom-domain-name-for-my-web-app"></a>Hoe gebruik ik een aangepaste domeinnaam voor mijn web-app

Voor antwoorden toocommon vragen over het gebruik van een aangepaste domeinnaam met uw Azure-web-app raadpleegt u onze zeven minuten durende video [toevoegen van een aangepaste domeinnaam](https://channel9.msdn.com/blogs/Azure-App-Service-Self-Help/Add-a-Custom-Domain-Name). Hallo video biedt een overzicht van hoe tooadd een aangepaste domeinnaam. Hierin wordt beschreven hoe toouse uw eigen URL in plaats van Hallo *. azurewebsites.net URL met uw App Service-web-app. Ook ziet u een gedetailleerd overzicht van [hoe toomap een aangepaste domeinnaam](web-sites-custom-domain-name.md).


## <a name="how-do-i-purchase-a-new-custom-domain-for-my-web-app"></a>Hoe ik een nieuw aangepast domein aanschaffen voor mijn web-app?

hoe toopurchase en stelt u een aangepast domein voor uw App Service-web-app, zien toolearn [kopen en configureren van een aangepaste domeinnaam in App Service](custom-dns-web-site-buydomains-web-app.md).


## <a name="how-do-i-upload-and-configure-an-existing-ssl-certificate-for-my-web-app"></a>Hoe ik uploaden en configureren van een bestaand SSL-certificaat voor mijn web-app?

hoe tooupload en stelt u een bestaand aangepast SSL-certificaat, Zie toolearn [binden van een bestaande aangepaste SSL-certificaat tooan Azure-web-app](app-service-web-tutorial-custom-ssl.md#upload).


## <a name="how-do-i-purchase-and-configure-a-new-ssl-certificate-in-azure-for-my-web-app"></a>Hoe ik kopen en configureren van een nieuw SSL-certificaat in Azure voor mijn web-app?

hoe toopurchase en stel een SSL-certificaat voor uw App Service-web-app, zien toolearn [toevoegen van een SSL-certificaat tooyour App Service-app](web-sites-purchase-ssl-web-site.md).


## <a name="how-do-i-move-application-insights-resources"></a>Hoe kan ik Application Insights-resources verplaatsen?

Op dit moment ondersteunt Azure Application Insights niet Hallo move-bewerking. Als uw oorspronkelijke resourcegroep een Application Insights-resource bevat, kunt u deze bron niet verplaatsen. Als u Application Insights-resource Hallo opneemt wanneer u probeert een App Service-app toomove, verplaatsen Hallo gehele mislukt. Echter, Application Insights en Hallo App Service plan hoeft geen toobe in Hallo dezelfde resourcegroep als Hallo-app voor Hallo app toofunction correct.

Zie voor meer informatie [App Service-beperkingen](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).

## <a name="where-can-i-find-a-guidance-checklist-and-learn-more-about-resource-move-operations"></a>Waar kan ik een controlelijst richtlijnen en meer informatie over resource bewerkingen verplaatsen?

[App Service-beperkingen](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations) ziet u hoe toomove resources tooeither een nieuw abonnement of tooa nieuwe bron groeperen in Hallo hetzelfde abonnement. U kunt informatie ophalen over Hallo resource verplaatsen controlelijst, informatie over welke services Hallo move-bewerking te ondersteunen en meer informatie over App Service-beperkingen en andere onderwerpen.

## <a name="how-do-i-set-hello-server-time-zone-for-my-web-app"></a>Hoe stel Hallo servertijdzone voor mijn web-app?

tooset hello servertijdzone voor uw web-app:

1. Ga in de Azure-portal in uw App Service-abonnement Hallo toohello **toepassingsinstellingen** menu.
2. Onder **appinstellingen**, deze instelling toevoegen:
    * Sleutel = WEBSITE_TIME_ZONE
    * Waarde = *Hallo gewenste tijdzone*
3. Selecteer **Opslaan**.

## <a name="why-do-my-continuous-webjobs-sometimes-fail"></a>Waarom mijn doorlopende webtaken soms mislukt?

Standaard worden web-apps uit het geheugen verwijderd als ze inactief gedurende een bepaalde tijd zijn. Hiermee Hallo-systeem te besparen. In het basis en standaard-plan, kunt u Hallo inschakelen **altijd op** alle Hallo tijd tookeep Hallo web-app instellen geladen. Als u uw web-app doorlopende webtaken uitvoert, moet u inschakelen **altijd op**, of Hallo WebJobs mogelijk niet betrouwbaar uitgevoerd. Zie voor meer informatie [maken van een continu actief webtaak](web-sites-create-web-jobs.md#CreateContinuous).

## <a name="how-do-i-get-hello-outbound-ip-address-for-my-web-app"></a>Hoe krijg Hallo uitgaande IP-adres voor mijn web-app?

lijst met tooget Hallo uitgaande IP-adressen voor uw web-app:

1. Ga in de Azure-portal op de blade van uw web-app Hallo toohello **eigenschappen** menu.
2. Zoeken naar **uitgaande IP-adressen**.

Hallo-lijst van uitgaande IP-adressen wordt weergegeven.

Als uw website wordt gehost in App Service-omgeving voor PowerApps, toolearn hoe tooget uw uitgaande IP-adres, Zie [uitgaande netwerkadressen](app-service-app-service-environment-network-architecture-overview.md#outbound-network-addresses).

## <a name="how-do-i-get-a-reserved-or-dedicated-inbound-ip-address-for-my-web-app"></a>Hoe krijg ik een gereserveerde of toegewijd binnenkomende IP-adres voor mijn web-app

tooset een toegewezen of gereserveerd IP-adres voor binnenkomende oproepen tooyour Apps van Azure-website installeren en configureren van een IP-gebaseerde SSL-certificaat.

Houd er rekening mee dat een speciaal toouse of gereserveerd IP-adres voor binnenkomende oproepen, uw App Service-abonnement moet zich in een Basic of hoger service-abonnement.

## <a name="can-i-export-my-app-service-certificate-toouse-outside-azure-such-as-for-a-website-hosted-elsewhere"></a>Kan ik mijn App Service-certificaat toouse buiten Azure, exporteren, zoals voor een website die elders wordt gehost? 

App Service-certificaten worden beschouwd als Azure-resources. Ze zijn niet bedoeld toouse buiten uw Azure-services. U kan niet deze exporteren toouse buiten Azure. Zie voor meer informatie [Veelgestelde vragen over App Service-certificaten en aangepaste domeinen](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).

## <a name="can-i-export-my-app-service-certificate-toouse-with-other-azure-cloud-services"></a>Kan ik mijn App Service-certificaat toouse met andere Azure-cloud-services exporteren?

Hallo-portal biedt een uitstekende ervaring voor het implementeren van een App Service-certificaat via Azure Key Vault tooApp Service-apps. Echter, we hebben zijn ontvangen aanvragen van klanten toouse deze certificaten buiten Hallo App Service-platform, bijvoorbeeld met Azure Virtual Machines. Zie hoe toocreate een lokale PFX-kopie van uw App Service-certificaat zodat u Hallo certificaat kunt gebruiken met andere Azure-resources toolearn [maken van een lokale PFX-kopie van een App Service-certificaat](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/).

Zie voor meer informatie [Veelgestelde vragen over App Service-certificaten en aangepaste domeinen](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).


## <a name="why-do-i-see-hello-message-partially-succeeded-when-i-try-tooback-up-my-web-app"></a>Waarom zie ik 'Gedeeltelijk geslaagd' Hallo-bericht wanneer ik probeer tooback van mijn web-app?

Een veelvoorkomende oorzaak van de back-fout is dat bepaalde bestanden gebruikt door de toepassing hello zijn. Bestanden die in gebruik zijn vergrendeld terwijl u Hallo back-up uitvoert. Dit voorkomt dat deze bestanden back-up wordt gemaakt en kan leiden tot een status 'Gedeeltelijk is voltooid'. U kunt dit mogelijk voorkomen door de bestanden uitsluiten van de back-upproces Hallo voorkomen. U kunt tooback van informatie die nodig is. Zie voor meer informatie [back-up van belangrijke delen NET Hallo van uw site met Azure-web-apps](http://www.zainrizvi.io/2015/06/05/creating-partial-backups-of-your-site-with-azure-web-apps/).

## <a name="how-do-i-remove-a-header-from-hello-http-response"></a>Hoe verwijder ik een koptekst van Hallo HTTP-antwoord

tooremove hello headers van Hallo HTTP-antwoord bijwerken van uw site web.config-bestand. Zie voor meer informatie [Standard van SQL server-headers van uw Azure websites verwijderd](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/).

## <a name="is-app-service-compliant-with-pci-standard-30-and-31"></a>App Service voldoet aan de standaard PCI-3.0 en 3.1 is?

Functie voor Hallo-Web-Apps van Azure App Service is momenteel in overeenstemming met PCI Data Security Standard (DSS) versie 3.0-niveau 1. PCI DSS versie 3.1 is op onze roadmap. Planning wordt al uitgevoerd voor hoe de toepassing van de meest recente standaard hello wordt voortgezet.

PCI DSS vereist versie 3.1 Transport Layer Security (TLS) 1.0 uitschakelen. TLS 1.0 uitschakelen is momenteel geen een optie voor de meeste App Service-abonnementen. Als u App Service-omgeving gebruiken of bent bereid toomigrate uw werkbelasting tooApp Service-omgeving, kunt u meer controle over uw omgeving ophalen. Dit omvat het TLS 1.0 uitschakelen contact opnemen met de ondersteuning van Azure. In Hallo nabije toekomst zullen we toomake deze instellingen toegankelijk toousers.

Zie voor meer informatie [compatibiliteit van Microsoft Azure App Service web-app met PCI standaard 3.0 en 3.1](https://support.microsoft.com/help/3124528).

## <a name="how-do-i-use-hello-staging-environment-and-deployment-slots"></a>Hoe gebruik ik Hallo staging-omgeving en implementatiesites

Bij het implementeren van het tooApp in uw web-app Service, kunt u in een Standard en Premium-App Service-plan tooa afzonderlijke implementatiesleuf in plaats van toohello standaard productiesite implementeren. Implementatiesites zijn live web-apps die hun eigen hostnamen hebben. Web-app inhoud en configuratie-elementen worden ingewisseld tussen twee implementatiesites, met inbegrip van Hallo productiesite.

Zie voor meer informatie over het gebruik van implementatiesites [instellen van een testomgeving in App Service](web-sites-staged-publishing.md).

## <a name="how-do-i-access-and-review-webjob-logs"></a>Hoe ik toegang tot logboeken en controleren webtaak?

tooreview webtaak Logboeken:

1. Meld u aan tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).
2. Selecteer Hallo webtaak.
3. Selecteer Hallo **wisselknop uitvoer** knop.
4. toodownload hello uitvoerbestand, selecteer Hallo **downloaden** koppeling.
5. Selecteer voor afzonderlijke wordt uitgevoerd, **afzonderlijke aanroepen**.
6. Selecteer Hallo **wisselknop uitvoer** knop.
7. Selecteer Hallo downloadkoppeling.

## <a name="im-trying-toouse-hybrid-connections-with-sql-server-why-do-i-see-hello-message-systemoverflowexception-arithmetic-operation-resulted-in-an-overflow"></a>Ik probeer toouse hybride verbindingen met SQL Server. Waarom zie ik het Hallo-bericht ' System.OverflowException: rekenkundige bewerking resulteerde in een overloop '?

Als u hybride verbindingen tooaccess SQL Server gebruikt, kan een Microsoft .NET-update op 10 mei 2016 verbindingen toofail veroorzaken. U ziet dit bericht:

```
Exception: System.Data.Entity.Core.EntityException: hello underlying provider failed on Open. —> System.OverflowException: Arithmetic operation resulted in an overflow. or (64 bit Web app) System.OverflowException: Array dimensions exceeded supported range, at System.Data.SqlClient.TdsParser.ConsumePreLoginHandshake
```

### <a name="resolution"></a>Oplossing

We werken tooupdate hybride Verbindingsbeheer toofix dit probleem. Zie voor tijdelijke oplossingen, [fout hybride verbindingen met SQL Server: System.OverflowException: rekenkundige bewerking resulteerde in een overloop](https://blogs.msdn.microsoft.com/waws/2016/05/17/hybrid-connection-error-with-sql-server-system-overflowexception-arithmetic-operation-resulted-in-an-overflow/).

## <a name="how-do-i-add-or-edit-a-url-rewrite-rule"></a>Hoe ik toevoegen of bewerken van een regel voor het herschrijven van URL?

tooadd of een regel voor het herschrijven van URL bewerken:

1. Internet Information Services (IIS) Manager zo instellen dat deze verbinding maakt met tooyour App Service-web-app. hoe tooconnect tooApp van IIS-Service, bekijken toolearn [extern beheer van Azure websites met behulp van IIS-beheer](https://azure.microsoft.com/blog/remote-administration-of-windows-azure-websites-using-iis-manager/).
2. In de IIS-beheer toevoegen of bewerken van een regel voor het herschrijven van URL. Zie hoe tooadd of bewerken herschrijven van URL van een regel, toolearn [maken herschrijven regels voor URL Hallo herschrijven module](https://www.iis.net/learn/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module).

## <a name="how-do-i-control-inbound-traffic-tooapp-service"></a>Hoe bepaal ik binnenkomend verkeer tooApp Service

Op siteniveau hello hebt u twee opties voor het beheren van binnenkomend verkeer tooApp Service:

* Schakel dynamisch IP-beperkingen. hoe tooturn op dynamische IP-adresbeperkingen zien toolearn [IP- en domeinbeperkingen voor Azure websites](https://azure.microsoft.com/blog/ip-and-domain-restrictions-for-windows-azure-web-sites/).
* Schakel beveiliging van de Module. hoe tooturn aan beveiliging van de Module, Zie toolearn [ModSecurity web application firewall op Azure websites](https://azure.microsoft.com/blog/modsecurity-for-azure-websites/).

Als u App Service-omgeving gebruikt, kunt u [Barracuda firewall](https://azure.microsoft.com/blog/configuring-barracuda-web-application-firewall-for-azure-app-service-environment/).

## <a name="how-do-i-block-ports-in-an-app-service-web-app"></a>Hoe ik poorten in een App Service-web-app blokkeren?

In Hallo gedeelde App Service een tenant-omgeving, is niet mogelijk tooblock bepaalde poorten vanwege Hallo aard van Hallo-infrastructuur. TCP-poorten 4016 4018 en 4020 ook mogelijk voor foutopsporing op afstand Visual Studio is geopend.

In App Service-omgeving hebt u volledige controle over binnenkomend en uitgaand verkeer. U kunt Netwerkbeveiligingsgroepen toorestrict of blok specifieke poorten gebruiken. Zie voor meer informatie over App Service-omgeving, [introductie van App Service-omgeving](https://azure.microsoft.com/blog/introducing-app-service-environment/).

## <a name="how-do-i-capture-an-f12-trace"></a>Hoe ik een tracering F12 vastleggen?

U hebt twee opties voor het vastleggen van een tracering F12:

* F12 HTTP-tracering
* F12 console-uitvoer

### <a name="f12-http-trace"></a>F12 HTTP-tracering

1. Ga in Internet Explorer tooyour website. Het is belangrijk toosign in voordat u de volgende stappen Hallo. Anders worden Hallo F12 tracering gevoelige gegevens aanmelden.
2. Druk op F12.
3. Controleer of deze Hallo **netwerk** tabblad is geselecteerd en selecteer vervolgens Hallo groen **afspelen** knop.
4. Hallo-stappen die Hallo reproduceren verlenen.
5. Selecteer Hallo rode **stoppen** knop.
6. Selecteer Hallo **opslaan** knop (schijfpictogram) en sla Hallo HAR-bestand (in Internet Explorer en Edge) *of* Hallo HAR bestand met de rechtermuisknop en selecteer vervolgens **opslaan als HAR met inhoud** () in Chrome).

### <a name="f12-console-output"></a>F12 console-uitvoer

1. Selecteer Hallo **Console** tabblad.
2. Voor elk tabblad die groter zijn dan nul items bevat, selecteert u Hallo tabblad (**fout**, **waarschuwing**, of **informatie**). Als Hallo tabblad niet is geselecteerd, is Hallo tabblad pictogram grijs of zwart wanneer de cursor Hallo weg van deze.
3. Met de rechtermuisknop in het berichtgedeelte Hallo Hallo deelvenster en selecteer vervolgens **Kopieer alle**.
4. Plakken Hallo gekopieerde tekst in een bestand en sla Hallo-bestand.

een bestand HAR tooview, kunt u Hallo [HAR viewer](http://www.softwareishard.com/har/viewer/).

## <a name="why-do-i-get-an-error-when-i-try-tooconnect-an-app-service-web-app-tooa-virtual-network-that-is-connected-tooexpressroute"></a>Waarom krijg ik een fout wanneer ik probeer tooconnect een App Service web app tooa virtueel netwerk dat niet verbonden tooExpressRoute?

Als u een Azure-web-app tooa virtueel netwerk dat is verbonden tooAzure ExpressRoute tooconnect probeert, mislukt dit. Hallo volgende bericht wordt weergegeven: 'Gateway is niet een VPN-gateway'.

U kunt op dit moment geen punt-naar-site VPN-verbindingen tooa virtueel netwerk dat niet verbonden tooExpressRoute. Een punt-naar-site-VPN en ExpressRoute kunnen niet worden gecombineerd voor Hallo hetzelfde virtuele netwerk. Zie voor meer informatie [ExpressRoute en site-naar-site VPN-verbindingen limieten en beperkingen](../expressroute/expressroute-howto-coexist-classic.md#limits-and-limitations).

## <a name="how-do-i-connect-an-app-service-web-app-tooa-virtual-network-that-has-a-static-routing-policy-based-gateway"></a>Hoe kan ik een App Service web app tooa virtueel netwerk met een statische routering (op beleid gebaseerd) gateway verbinden?

Op dit moment kunnen wordt verbinden van een App Service web app tooa virtueel netwerk met een statische routering (op beleid gebaseerd)-gateway niet ondersteund. Als het virtuele doelnetwerk al bestaat, moet de punt-naar-site VPN is ingeschakeld, met een gateway voor dynamische routering kan pas verbonden tooan app worden hebben. Als uw gateway is ingesteld op toostatic routering, kunt u een punt-naar-site VPN niet inschakelen. 

Zie voor meer informatie [een app integreren met een Azure-netwerk](web-sites-integrate-with-vnet.md#getting-started).

## <a name="in-my-app-service-environment-why-can-i-create-only-one-app-service-plan-even-though-i-have-two-workers-available"></a>Mijn App-serviceomgeving waarom kan ik maken slechts één App Service-abonnement, zelfs als er twee werknemers beschikbaar?

tooprovide fouttolerantie, App Service-omgeving vereist dat elke worker-groep ten minste één extra Reken-bron moet. Hallo aanvullende compute resource kan niet worden toegewezen als een werkbelasting.

Zie voor meer informatie [hoe toocreate een App-serviceomgeving](app-service-web-how-to-create-an-app-service-environment.md).

## <a name="why-do-i-see-timeouts-when-i-try-toocreate-an-app-service-environment"></a>Waarom zie ik time-outs wanneer ik probeer een App-serviceomgeving toocreate?

Soms mislukt het maken van een App Service-omgeving. In dat geval ziet u de volgende fout in de logboeken van de activiteit Hallo Hallo:
```
ResourceID: /subscriptions/{SubscriptionID}/resourceGroups/Default-Networking/providers/Microsoft.Web/hostingEnvironments/{ASEname}
Error:{"error":{"code":"ResourceDeploymentFailure","message":"hello resource provision operation did not complete within hello allowed timeout period.”}}
```

tooresolve, zorg ervoor dat geen van Hallo volgende voorwaarden voldaan wordt:
* Hallo-subnet is te klein.
* Hallo-subnet is niet leeg.
* ExpressRoute wordt voorkomen dat de vereisten voor de connectiviteit van Hallo netwerk van een App Service-omgeving.
* Een onjuiste Netwerkbeveiligingsgroep voorkomt dat Hallo netwerkvereisten verbinding van een App Service-omgeving.
* Geforceerde tunneling is ingeschakeld.

Zie voor meer informatie [regelmatige problemen bij het implementeren van (maken) een nieuwe Azure App Service-omgeving](https://blogs.msdn.microsoft.com/waws/2016/05/13/most-frequent-issues-when-deploying-creating-a-new-azure-app-service-environment-ase/).

## <a name="why-cant-i-delete-my-app-service-plan"></a>Waarom kan ik mijn App Service-abonnement niet verwijderen

U kunt een App Service-abonnement niet verwijderen als een App Service-apps gekoppeld aan Hallo App Service-abonnement zijn. Voordat u een App Service-abonnement verwijdert, verwijdert u alle gekoppelde App Service-apps van Hallo App Service-abonnement.

## <a name="how-do-i-schedule-a-webjob"></a>Hoe kan ik een webtaak plannen?

U kunt een geplande webtaak maken met behulp van Cron expressies:

1. Maak een bestand settings.job.
2. Neem in dit JSON-bestand, een schema-eigenschap met behulp van een Cron-expressie: 
    ```
    { "schedule": "{second}
    {minute} {hour} {day}
    {month} {day of hello week}" }
    ```

Zie voor meer informatie over de geplande webtaken [een geplande webtaak maken met behulp van een expressie Cron](web-sites-create-web-jobs.md#CreateScheduledCRON).

## <a name="how-do-i-perform-penetration-testing-for-my-app-service-app"></a>Hoe voer ik binnendringen testen voor mijn App Service-app uit?

tooperform binnendringen testen, [een aanvraag indienen](https://security-forms.azure.com/penetration-testing/terms).

## <a name="how-do-i-configure-a-custom-domain-name-for-an-app-service-web-app-that-uses-traffic-manager"></a>Hoe kan ik een aangepaste domeinnaam voor een App Service-web-app die gebruikmaakt van Traffic Manager configureren?

hoe toouse een aangepaste domeinnaam met een App Service-app die gebruikmaakt van Azure Traffic Manager voor taakverdeling, Zie toolearn [een aangepaste domeinnaam configureren voor een Azure-web-app met Traffic Manager](web-sites-traffic-manager-custom-domain-name.md).

## <a name="my-app-service-certificate-is-flagged-for-fraud-how-do-i-resolve-this"></a>Mijn App Service-certificaat is gemarkeerd voor fraude. Hoe kan ik dit oplossen?

Tijdens het Hallo-domeinverificatie van een App Service-certificaat kopen ziet u mogelijk Hallo volgende bericht:

'Uw certificaat is gemarkeerd om mogelijke fraude. Hallo-aanvraag wordt momenteel onderzocht. Als Hallo certificaat niet gebruikt binnen 24 uur wordt, neem contact op met ondersteuning van Azure."

Als het Hallo-bericht aangeeft, kan dit verificatieproces fraude too24 uren toocomplete duren. Gedurende deze tijd, gaat u verder toosee Hallo-bericht.

Als uw App Service-certificaat tooshow dit bericht na 24 uur blijft, voer de volgende PowerShell-script Hallo. Hallo script contactpersonen Hallo [certificaatprovider](https://www.godaddy.com/) rechtstreeks tooresolve Hallo probleem.

```
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId <subId>
$actionProperties = @{
    "Name"= "<Customer Email Address>"
    };
Invoke-AzureRmResourceAction -ResourceGroupName "<App Service Certificate Resource Group Name>" -ResourceType Microsoft.CertificateRegistration/certificateOrders -ResourceName "<App Service Certificate Resource Name>" -Action resendRequestEmails -Parameters $actionProperties -ApiVersion 2015-08-01 -Force   
```

## <a name="how-do-authentication-and-authorization-work-in-app-service"></a>Hoe verificatie en autorisatie werken in App Service?

Zie voor gedetailleerde documentatie voor verificatie en autorisatie in App Service [App Service-beveiliging](../app-service/app-service-security-readme.md). Hallo documentatie bevat ook informatie over het instellen van App Service-toouse verschillende provider aanmeldingen identificeren:
* [Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)
* [Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md)
* [Google](../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md)
* [Microsoft-account](../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md)
* [Twitter](../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md)

## <a name="how-do-i-redirect-hello-default-azurewebsitesnet-domain-toomy-azure-web-apps-custom-domain"></a>Hoe leiden Hallo standaard *. azurewebsites.net domein toomy Azure-web-app van aangepast domein?

Wanneer u een nieuwe website maken met behulp van Web-Apps in Azure, een standaard *sitename*. domein azurewebsites.net tooyour site is toegewezen. Als u een aangepaste host naam tooyour site toevoegen en niet dat gebruikers toobe kunnen tooaccess uw standaard wilt *. azurewebsites.net domein, kunt u de standaard-URL Hallo omleiden. toolearn hoe tooredirect alle verkeer van uw website domein tooyour aangepaste standaarddomein raadpleegt [omleiding Hallo domein tooyour aangepaste standaarddomein in Azure-web-apps](http://www.zainrizvi.io/2016/04/07/block-default-azure-websites-domain/).

## <a name="how-do-i-determine-which-version-of-net-version-is-installed-in-app-service"></a>Hoe bepalen welke versie van .NET versie is geïnstalleerd in App Service?

Hallo snelste manier toofind Hallo versie van Microsoft .NET die in App Service geïnstalleerd is met behulp van Hallo Kudu-console. Hallo-portal of via Hallo-URL van uw app in App Service, kunt u Hallo Kudu-console openen. Zie voor gedetailleerde instructies [hello geïnstalleerd .NET versie in App Service](https://blogs.msdn.microsoft.com/waws/2016/11/02/how-to-determine-the-installed-net-version-in-azure-app-services/).

## <a name="why-isnt-autoscale-working-as-expected"></a>Waarom werkt niet voor automatisch schalen zoals verwacht?

Als Azure voor automatisch schalen die nog niet geschaald in of uitgebreid Hallo web-app-exemplaar zoals u verwacht, u kunt uitvoeren in een scenario waarin we opzettelijk kiezen niet tooscale tooavoid een oneindige lus vanwege te 'op en neer." Dit gebeurt meestal wanneer er geen een voldoende marge tussen Hallo scale-out en de schaal drempels. hoe tooavoid 'op en neer' en tooread over andere best practices voor automatisch schalen zien toolearn [aanbevolen procedures voor automatisch schalen](../monitoring-and-diagnostics/insights-autoscale-best-practices.md#autoscale-best-practices).

## <a name="why-does-autoscale-sometimes-scale-only-partially"></a>Waarom automatisch schalen soms schaalt slechts gedeeltelijk?

Automatisch schalen wordt geactiveerd wanneer de metrische gegevens overschrijden vooraf geconfigureerde grenzen. Soms moet wellicht u opgevallen dat Hallo capaciteit vergeleken toowhat u verwacht slechts gedeeltelijk is gevuld. Dit kan gebeuren wanneer het aantal exemplaren dat u wilt dat Hallo zijn niet beschikbaar. In dit scenario vult automatisch schalen gedeeltelijk met Hallo beschikbaar aantal exemplaren. Automatisch schalen voert Hallo deel opnieuw logica tooget meer capaciteit. Het wijst resterende exemplaren Hallo. Houd er rekening mee dat dit kan enkele minuten duren.

Als er geen Hallo verwacht aantal exemplaren na een paar minuten, is dit mogelijk doordat Hallo gedeeltelijke aanvulling voldoende toobring Hallo metrische gegevens binnen de grenzen van Hallo is. Of automatisch schalen kan omlaag geschaald omdat Hallo ondergrens metrische gegevens is bereikt.

Als geen van deze voorwaarden van toepassing hello probleem zich blijft voordoen, moet u een ondersteuningsaanvraag indienen.

## <a name="how-do-i-turn-on-http-compression-for-my-content"></a>Hoe schakel ik op HTTP-compressie voor mijn inhoud?

tooturn op compressie van statische en dynamische inhoudstypen toevoegen Hallo code toohello op toepassingsniveau web.config-bestand te volgen:

```
<system.webServer>
<urlCompression doStaticCompression="true" doDynamicCompression="true" />
< /system.webServer>
```

Ook kunt u specifieke Hallo-dynamische en statische MIME-typen die u toocompress wilt. Zie voor meer informatie onze antwoord tooa forumvraag in [httpCompression-instellingen op een eenvoudige Azure-website](https://social.msdn.microsoft.com/Forums/azure/890b6d25-f7dd-4272-8970-da7798bcf25d/httpcompression-settings-on-a-simple-azure-website?forum=windowsazurewebsitespreview).

## <a name="how-do-i-migrate-from-an-on-premises-environment-tooapp-service"></a>Hoe Migreer ik van een lokale omgeving tooApp Service?

toomigrate sites van Windows en Linux web servers tooApp Service, kunt u assistent Azure App Service-migratie. hulpprogramma voor migratie van Hallo web-apps en databases maakt in Azure indien nodig en vervolgens publiceert Hallo inhoud. Zie voor meer informatie [assistent Azure App Service-migratie](https://www.movemetothecloud.net/).
