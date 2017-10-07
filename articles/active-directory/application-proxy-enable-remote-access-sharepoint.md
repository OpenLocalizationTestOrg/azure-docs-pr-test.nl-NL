---
title: aaaEnable RAS tooSharePoint met Azure AD-toepassingsproxy | Microsoft Docs
description: Bevat informatie over de basisprincipes van Hallo over het toointegrate een on-premises SharePoint server met Azure AD-toepassingsproxy.
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
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 6ab413462fcaf387e150449df9c97505c4108bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-access-toosharepoint-with-azure-ad-application-proxy"></a>Externe toegang tooSharePoint met Azure AD-toepassingsproxy inschakelen

Dit artikel wordt beschreven hoe toointegrate een on-premises SharePoint server met toepassingsproxy van Azure Active Directory (Azure AD).

tooenable RAS tooSharePoint met Azure AD-toepassingsproxy, volg Hallo secties in dit artikel stap voor stap.

## <a name="prerequisites"></a>Vereisten

In dit artikel wordt ervan uitgegaan dat u SharePoint 2013 of nieuwer al in uw omgeving hebt. Bovendien kunt u overwegen Hallo volgende vereisten:

* SharePoint bevat systeemeigen ondersteuning van Kerberos. Gebruikers die toegang interne sites op afstand via Azure AD-toepassingsproxy tot kunnen daarom een eenmalige aanmelding (SSO) optreden toohave aannemen.

* U moet enkele wijzigingen tooyour SharePoint configuratieserver toomake. U wordt aangeraden met behulp van een testomgeving. Op deze manier u kunt updates tooyour testserver eerst maken en vervolgens een cyclus testen voordat u doorgaat naar de productie te vergemakkelijken.

* Er wordt ervan uitgegaan dat u hebt al ingesteld SSL voor SharePoint, omdat SSL op Hallo gepubliceerde URL is vereist. U moet toohave die SSL ingeschakeld op uw interne site, tooensure dat koppelingen verzonden/correct zijn toegewezen. Als u dit nog niet hebt geconfigureerd dat SSL, Zie [SSL configureren voor SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) voor instructies. Zorg ook dat Hallo connector machine vertrouwensrelaties Hallo certificaat dat u de opdracht. (Hallo certificaat heeft geen openbaar uitgegeven toobe nodig.)

## <a name="step-1-set-up-single-sign-on-toosharepoint"></a>Stap 1: TooSharePoint voor eenmalige aanmelding instellen

Onze klanten willen Hallo best SSO-ervaring bieden voor hun back-end-toepassingen, SharePoint-server in dit geval. In dit veelvoorkomende scenario voor het Azure AD Hallo gebruiker slechts één keer geverifieerd omdat ze niet gevraagd om het opnieuw.

Voor on-premises toepassingen die vereisen of Windows-verificatie gebruiken, kunt u eenmalige aanmelding kunt bereiken met behulp van Kerberos-verificatieprotocol Hallo en een functie voor Kerberos-beperkte delegatie (KCD). KCD, wanneer geconfigureerd, een windows hello Application Proxy connector tooobtain kan ticket/token voor een gebruiker, zelfs als Hallo gebruiker nog niet aangemeld tooWindows rechtstreeks. toolearn meer informatie over KCD, Zie [overzicht van Kerberos-beperkte overdracht](https://technet.microsoft.com/library/jj553400.aspx).

tooset up KCD voor een SharePoint-server, gebruik Hallo procedures in Hallo opeenvolgende secties volgen:

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a>Controleer of SharePoint wordt uitgevoerd onder een serviceaccount

Controleer eerst of of SharePoint wordt uitgevoerd onder een gedefinieerde serviceaccount--niet lokaal systeem, lokale service of Netwerkservice. Dit doen zodat u de service principal names (SPN's) tooa geldig account kunt koppelen. SPN's zijn hoe Hallo Kerberos-protocol verschillende services identificeert. En u moet Hallo account later tooconfigure hello KCD.

tooensure die uw sites worden uitgevoerd onder een gedefinieerde serviceaccount uitvoeren Hallo stappen te volgen:

1. Open Hallo **Centraal beheer van SharePoint 2013** site.
2. Ga te**beveiliging** en selecteer **serviceaccounts configureren**.
3. Selecteer **Web-groep van toepassingen - SharePoint - 80**. Hallo opties mogelijk enigszins verschillen op basis van het Hallo-naam van uw web-toepassingen of als hello webpool SSL wordt standaard gebruikt.

  ![Opties voor het configureren van een serviceaccount](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. Als **Selecteer een account voor dit onderdeel** is **lokale Service** of **netwerkservice**, moet u een account toocreate. Zo niet, u klaar bent en de volgende sectie toohello kunt verplaatsen.
5. Selecteer **nieuw beheerd account registreren**. Nadat u uw account is gemaakt, moet u instellen **toepassingen** voordat u Hallo account kunt gebruiken.

> [!NOTE]
U moet toohave een eerder gemaakt van Azure AD-account voor Hallo-service. Het is raadzaam dat u een automatische wachtwoordwijziging toestaan. Zie voor meer informatie over de volledige set Hallo van stappen en het oplossen van problemen, [automatische wachtwoordwijziging configureren in SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).

### <a name="configure-sharepoint-for-kerberos"></a>SharePoint configureren voor Kerberos

U KCD tooperform eenmalige aanmelding toohello SharePoint-server gebruikt en dit werkt alleen met Kerberos.

tooconfigure uw SharePoint-site voor Kerberos-verificatie:

1. Open Hallo **Centraal beheer van SharePoint 2013** site.
2. Ga te**Toepassingsbeheer**, selecteer **beheren van webtoepassingen**, en selecteert u de SharePoint-site. In dit voorbeeld is het **SharePoint - 80**.

  ![Hallo SharePoint-site selecteren](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. Klik op **verificatieproviders** op Hallo-werkbalk.
4. In Hallo **verificatieproviders** Klik **standaardzone** tooview Hallo instellingen.
5. In Hallo **Authentication bewerken** dialoogvenster vak, schuif omlaag totdat u ziet **typen claimverificatie** en zorg ervoor dat beide **Windows-verificatie inschakelen** en  **Geïntegreerde Windows-verificatie** zijn geselecteerd.
6. Controleer of in de vervolgkeuzelijst hello, **onderhandelen (Kerberos)** is geselecteerd.

  ![Dialoogvenster Verificatie bewerken](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. Hallo Hallo onderaan in **Authentication bewerken** in het dialoogvenster, klikt u op **opslaan**.

### <a name="set-a-service-principal-name-for-hello-sharepoint-service-account"></a>Een naam voor de service-principal voor Hallo SharePoint-serviceaccount instellen

Voordat u Hallo KCD configureert, moet u tooidentify Hallo SharePoint-service wordt uitgevoerd als het Hallo-serviceaccount die u hebt geconfigureerd. U doen dit door een SPN instellen. Zie voor meer informatie [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx).

Hallo SPN-indeling is:

```
<service class>/<host>:<port>
```

Hallo SPN-indeling:

* _Service-klasse_ is een unieke naam voor het Hallo-service. Voor SharePoint, gebruikt u **HTTP**.

* _host_ is Hallo FQDN of NetBIOS-naam van het Hallo-host die Hallo service wordt uitgevoerd op. Deze tekst mogelijk toobe Hallo URL van de site hello, afhankelijk van Hallo-versie van IIS die u moet voor een SharePoint-site.

* _poort_ is optioneel.

Als de FQDN-naam van de SharePoint-server Hallo Hallo is:

```
sharepoint.demo.o365identity.us
```

Hallo SPN is dan:

```
HTTP/ sharepoint.demo.o365identity.us demo
```

Mogelijk moet u ook tooset SPN's voor bepaalde websites op uw server. Zie voor meer informatie [Configureer Kerberos-verificatie](https://technet.microsoft.com/library/cc263449(v=office.12).aspx). Betalen aandacht toohello sectie 'Service Principal Names maken voor uw webtoepassingen Kerberos-verificatie gebruiken'.

Hallo voor tooset SPN's gemakkelijkst toofollow Hallo SPN-indelingen die al aanwezig om uw sites zijn mogelijk. Kopieer deze tooregister SPN's tegen Hallo-serviceaccount. toodo dit:

1. Blader toohello site Hello SPN vanaf een andere computer.
 Wanneer u dit doet, Hallo relevante set van Kerberos-tickets opgeslagen in de cache op Hallo-machine. Deze tickets bevatten Hallo SPN-naam van de doelsite Hallo die u hebt gebladerd.

2. Pull-hallo SPN voor die site kunt u met een hulpprogramma aangeroepen [Klist uit](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html). In een opdrachtvenster die worden uitgevoerd in Hallo Hallo dezelfde context als Hallo-gebruiker die site gebruikte Hallo in browser Hallo uitvoeren na de opdracht:
```
Klist
```
Klist uit retourneert vervolgens Hallo van doel-SPN's. In dit voorbeeld is gemarkeerd Hallo waarde Hallo SPN die nodig is:

  ![Voorbeeld Klist uit resultaten](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. Nu u Hallo SPN hebt, moet u ervoor dat deze juist geconfigureerd op Hallo-serviceaccount die u hebt ingesteld voor webtoepassing eerder Hallo toomake. Voer Hallo volgende opdracht uit Hallo opdrachtprompt als beheerder van Hallo domein:

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 Met deze opdracht sets hello SPN voor de SharePoint-service Hallo uitgevoerd als account _demo\sp_svc_.

 Vervang _http/sharepoint.demo.o365identity.us_ Hello SPN-naam voor uw server en _demo\sp_svc_ met Hallo-serviceaccount in uw omgeving. Hallo Setspn-opdracht wordt gezocht naar Hallo SPN voordat deze wordt toegevoegd. In dit geval ziet u mogelijk een **dubbele SPN waarde** fout. Als u deze fout ziet, zorg dat Hallo-waarde gekoppeld aan het Hallo-serviceaccount is.

U kunt die SPN is toegevoegd door het uitvoeren van Hallo Setspn-opdracht bij de optie -l Hallo Hallo controleren. Zie toolearn meer informatie over deze opdracht [Setspn](https://technet.microsoft.com/library/cc731241.aspx).

### <a name="ensure-that-hello-connector-is-set-as-a-trusted-delegate-toosharepoint"></a>Zorg ervoor dat Hallo-connector is ingesteld als een vertrouwde gemachtigde tooSharePoint

Hallo KCD zodanig configureren dat hello Azure AD-toepassingsproxy service gebruiker identiteiten toohello SharePoint-service kan overdragen. U doen dit door Hallo Application Proxy connector in te schakelen tooretrieve Kerberos-tickets voor uw gebruikers die in Azure AD zijn geverifieerd. Deze server stuurt vervolgens Hallo context toohello doeltoepassing of SharePoint in dit geval.

tooconfigure hello KCD, herhaaldelijk Hallo volgende stappen uit voor elke connector machine:

1. Meld u aan als een domein beheerder tooa DC en open vervolgens **Active Directory: gebruikers en Computers**.
2. Zoeken op Hallo-computer die Hallo connector wordt uitgevoerd. In dit voorbeeld is het Hallo dezelfde SharePoint-server.
3. Dubbelklik op Hallo-computer en klik vervolgens op Hallo **delegering** tabblad.
4. Zorg ervoor dat de Overdrachtinstellingen Hallo te worden ingesteld**deze computer overdracht toohello opgegeven services alleen**, en selecteer vervolgens **elk verificatieprotocol voor gebruiken**.

  ![Delegatie-instellingen](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. Klik op Hallo **toevoegen** klikken, klik op **gebruikers of Computers**, en zoek Hallo-serviceaccount.

  ![Toe te voegen Hallo SPN voor Hallo-serviceaccount](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. Selecteer in de lijst van de Hallo van SPN-namen, Hallo die u eerder hebt gemaakt voor Hallo-serviceaccount.
7. Klik op **OK**. Klik op **OK** opnieuw toosave Hallo wijzigingen.

## <a name="step-2-enable-remote-access-toosharepoint"></a>Stap 2: RAS-tooSharePoint inschakelen

Nu u SharePoint voor Kerberos is ingeschakeld en geconfigureerd KCD, bent u klaar tooset up tooSharePoint voor eenmalige aanmelding. U kunt vervolgens Hallo SharePoint-farm voor externe toegang via Azure AD-toepassingsproxy publiceren van Hallo-connector.

Hallo tooperform volgende stappen, moet u lid zijn van Hallo rol globale beheerder in uw organisatie Azure Active Directory-account toobe.

1. Meld u aan toohello [Azure-portal](https://manage.windowsazure.com) en Ga naar uw Azure AD-tenant.
2. Klik op **toepassingen**, en klik vervolgens op **toevoegen**.
3. Selecteer **Een toepassing publiceren die toegankelijk is van buiten uw netwerk**. Als u deze optie niet ziet, zorg ervoor dat u Azure AD Basic hebt of Premium, in Hallo-tenant instellen.
4. Elk van de opties Hallo als volgt uitvoeren:
 * **Naam**: gebruik van elke waarde die u bijvoorbeeld wilt **SharePoint**.
 * **Interne URL**: dit is Hallo-URL van de SharePoint-site Hallo intern, zoals **https://SharePoint/**. Zorg ervoor dat toouse in dit voorbeeld **https**.
 * **Methode voor verificatie vooraf**: Selecteer **Azure Active Directory**.

  ![Opties voor het toevoegen van een toepassing](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. Nadat het Hallo-app wordt gepubliceerd, klikt u op Hallo **configureren** tabblad.
6. Schuif omlaag in de optie toohello **URL vertalen in Headers**. de standaardwaarde Hallo is **Ja**. Ook wijzigen**Nee**.

 SharePoint maakt gebruik van Hallo _Host-Header_ waarde toolook Hallo-site. Koppelingen op basis van deze waarde wordt ook gegenereerd. Hallo netto effect is toomake zorgen dat koppelingen die SharePoint genereert een gepubliceerde URL toouse Hallo externe URL correct is ingesteld. Instellingswaarde hello te**Ja** ook schakelt connector tooforward Hallo aanvraag toohello back-endtoepassing Hallo. Echter instellingswaarde hello te**Nee** betekent dat Hallo connector verzendt geen interne Hallo-hostnaam. Hallo-connector verzendt Hallo host-header in plaats daarvan zoals Hallo URL toohello back-endtoepassing gepubliceerd.

 Bovendien tooensure dat SharePoint deze URL accepteert, moet u toocomplete na één meer configuratie op Hallo SharePoint-server. U doet dat in de volgende sectie Hallo.

7. Wijziging **interne verificatiemethode** te**geïntegreerde Windows-verificatie**. Als uw Azure AD-tenant gebruikmaakt van een UPN in Hallo cloud die verschilt van Hallo UPN on-premises, vergeet dan niet tooupdate **overgedragen aanmelding identiteit** ook.
8. Stel **interne toepassing SPN** toohello-waarde die u eerder hebt ingesteld. Bijvoorbeeld: **http/sharepoint.demo.o365identity.us**.
9. Hallo toepassing tooyour Doelgebruikers toewijzen.

Uw toepassing ziet vergelijkbare toohello voorbeeld te volgen:

  ![Voltooide toepassing](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-hello-external-url"></a>Stap 3: Zorg ervoor dat SharePoint op de hoogte van de externe URL Hallo

De laatste stap tooensure die SharePoint Hallo-site op basis van de externe URL hello, vindt zodat deze koppelingen op basis van die externe URL worden weergegeven. Hiervoor alternatieve toegangstoewijzingen voor Hallo SharePoint-site configureren.

1. Open Hallo **Centraal beheer van SharePoint 2013** site.
2. Onder **systeeminstellingen**, selecteer **alternatieve toegangstoewijzingen configureren**.

 Hiermee opent u Hallo **alternatieve toegangstoewijzingen** vak.

  ![Alternatieve toegangstoewijzingen vak](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. In Hallo vervolgkeuzelijst naast **alternatieve toewijzing collectie**, selecteer **alternatieve toewijzing collectie wijzigen**.
4. Selecteer uw site--bijvoorbeeld **SharePoint - 80**.

  ![Een site selecteren](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. U kunt tooadd Hallo URL gepubliceerd als een interne URL of een openbare URL. Dit voorbeeld wordt een openbare URL als Hallo extranet.
6. Klik op **openbare URL's bewerken** in Hallo **Extranet** pad, en voer vervolgens Hallo pad voor Hallo toepassing, zoals in de vorige stap Hallo gepubliceerd. Voer bijvoorbeeld **https://sharepoint-iddemo.msappproxy.net**.

  ![Hallo-pad](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. Klik op **Opslaan**.

 U kunt nu toegang tot de SharePoint-site Hallo extern via Azure AD-toepassingsproxy.

## <a name="next-steps"></a>Volgende stappen

- [Hoe tooprovide veilige externe toegang tot het tooon-premises toepassingen](active-directory-application-proxy-get-started.md)
- [Azure AD-toepassingsproxy connectors begrijpen](application-proxy-understand-connectors.md)
- [Publicatie van SharePoint 2016 en Office Online-Server met Azure AD-toepassingsproxy](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)
