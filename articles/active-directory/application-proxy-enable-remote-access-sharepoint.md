---
title: Externe toegang voor SharePoint met Azure AD-toepassingsproxy inschakelen | Microsoft Docs
description: Bevat informatie over de basisprincipes voor het integreren van een on-premises SharePoint-server met Azure AD-toepassingsproxy.
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
ms.openlocfilehash: 97eeec3b3936bcbef6ac3966b890332901bcb153
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-remote-access-to-sharepoint-with-azure-ad-application-proxy"></a>Externe toegang voor SharePoint met Azure AD-toepassingsproxy inschakelen

In dit artikel wordt beschreven hoe een on-premises SharePoint server integreren met Azure Active Directory (Azure AD) Application Proxy.

Volg de secties in dit artikel stapsgewijze zodat externe toegang tot SharePoint met Azure AD-toepassingsproxy.

## <a name="prerequisites"></a>Vereisten

In dit artikel wordt ervan uitgegaan dat u SharePoint 2013 of nieuwer al in uw omgeving hebt. Bovendien kunt u overwegen de volgende vereisten:

* SharePoint bevat systeemeigen ondersteuning van Kerberos. Daarom gebruikers die toegang interne sites op afstand via Azure AD-toepassingsproxy tot kunnen wordt ervan uitgegaan dat een ervaring voor eenmalige aanmelding (SSO).

* U moet enkele configuratiewijzigingen aanbrengen in uw SharePoint-server. U wordt aangeraden met behulp van een testomgeving. Op deze manier u kunt updates eerst naar uw testserver maken en vervolgens een cyclus testen voordat u doorgaat naar de productie te vergemakkelijken.

* Er wordt ervan uitgegaan dat u hebt al ingesteld SSL voor SharePoint, omdat SSL op de gepubliceerde URL is vereist. U moet SSL is ingeschakeld op uw interne site, om ervoor te zorgen dat koppelingen verzonden/toegewezen correct zijn. Als u dit nog niet hebt geconfigureerd dat SSL, Zie [SSL configureren voor SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) voor instructies. Zorg ervoor dat het certificaat dat u de opdracht wordt vertrouwd door de connector-machine. (Het certificaat niet hoeft te openbaar worden uitgegeven.)

## <a name="step-1-set-up-single-sign-on-to-sharepoint"></a>Stap 1: Instellen van eenmalige aanmelding tot SharePoint

Onze klanten willen in dit geval de beste SSO-ervaring voor hun back-end-toepassingen, SharePoint-server. In dit veelvoorkomende scenario voor Azure AD, de gebruiker slechts één keer geverifieerd omdat ze niet gevraagd om het opnieuw.

Voor on-premises toepassingen die vereisen of Windows-verificatie gebruiken, kunt u eenmalige aanmelding kunt bereiken met behulp van het Kerberos-protocol voor verificatie en Kerberos-beperkte delegatie (KCD) een functie. KCD, wanneer geconfigureerd, kunt de connector voor toepassingsproxy verkrijgen van een windows-ticket/token voor een gebruiker, zelfs als de gebruiker nog niet aangemeld bij Windows rechtstreeks. Zie voor meer informatie over KCD, [overzicht van Kerberos-beperkte overdracht](https://technet.microsoft.com/library/jj553400.aspx).

Als u KCD instelt voor een SharePoint-server, gebruik de procedures in de volgende sequentiële secties:

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a>Controleer of SharePoint wordt uitgevoerd onder een serviceaccount

Controleer eerst of of SharePoint wordt uitgevoerd onder een gedefinieerde serviceaccount--niet lokaal systeem, lokale service of Netwerkservice. Dit doen zodat u de service principal names (SPN's) aan een geldig account toevoegen kunt. SPN's zijn hoe het Kerberos-protocol verschillende services identificeert. En u moet het account later naar de KCD configureren.

Om ervoor te zorgen dat uw sites onder een gedefinieerde serviceaccount worden uitgevoerd, moet u de volgende stappen uitvoeren:

1. Open de **Centraal beheer van SharePoint 2013** site.
2. Ga naar **beveiliging** en selecteer **serviceaccounts configureren**.
3. Selecteer **Web-groep van toepassingen - SharePoint - 80**. De opties mogelijk enigszins verschillen op basis van de naam van uw web-toepassingen, of als de webpool voor SSL standaard gebruikt.

  ![Opties voor het configureren van een serviceaccount](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. Als **Selecteer een account voor dit onderdeel** is **lokale Service** of **netwerkservice**, moet u een account maken. Zo niet, u klaar bent en u kunt verplaatsen naar de volgende sectie.
5. Selecteer **nieuw beheerd account registreren**. Nadat u uw account is gemaakt, moet u instellen **toepassingen** voordat u het account kunt gebruiken.

> [!NOTE]
Moet u beschikken over een eerder gemaakte Azure AD-account voor de service. Het is raadzaam dat u een automatische wachtwoordwijziging toestaan. Zie voor meer informatie over de volledige set van stappen en het oplossen van problemen, [automatische wachtwoordwijziging configureren in SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).

### <a name="configure-sharepoint-for-kerberos"></a>SharePoint configureren voor Kerberos

Met KCD voeren eenmalige aanmelding met de SharePoint-server en dit werkt alleen met Kerberos.

De SharePoint-site voor Kerberos-verificatie configureren:

1. Open de **Centraal beheer van SharePoint 2013** site.
2. Ga naar **Toepassingsbeheer**, selecteer **beheren van webtoepassingen**, en selecteert u de SharePoint-site. In dit voorbeeld is het **SharePoint - 80**.

  ![De SharePoint-site selecteren](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. Klik op **verificatieproviders** op de werkbalk.
4. In de **verificatieproviders** Klik **standaardzone** om de instellingen weer te geven.
5. In de **Authentication bewerken** dialoogvenster vak, schuif omlaag totdat u ziet **typen claimverificatie** en zorg ervoor dat beide **Windows-verificatie inschakelen** en **geïntegreerde Windows-verificatie** zijn geselecteerd.
6. Controleer of in de vervolgkeuzelijst **onderhandelen (Kerberos)** is geselecteerd.

  ![Dialoogvenster Verificatie bewerken](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. Aan de onderkant van de **Authentication bewerken** in het dialoogvenster, klikt u op **opslaan**.

### <a name="set-a-service-principal-name-for-the-sharepoint-service-account"></a>Instellen van een service-principal-naam voor de SharePoint-serviceaccount

Voordat u de KCD configureert, moet u het identificeren van de SharePoint-service wordt uitgevoerd als het serviceaccount dat u hebt geconfigureerd. U doen dit door een SPN instellen. Zie voor meer informatie [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx).

De SPN-indeling is:

```
<service class>/<host>:<port>
```

De SPN-indeling:

* _Service-klasse_ is een unieke naam voor de service. Voor SharePoint, gebruikt u **HTTP**.

* _host_ is de FQDN- of NetBIOS-naam van de host die de service wordt uitgevoerd op. Deze tekst mogelijk de URL van de site, afhankelijk van de versie van IIS die u voor een SharePoint-site.

* _poort_ is optioneel.

Als de FQDN van de SharePoint-server:

```
sharepoint.demo.o365identity.us
```

De SPN is dan:

```
HTTP/ sharepoint.demo.o365identity.us demo
```

Mogelijk moet u ook de SPN's instellen voor specifieke sites op uw server. Zie voor meer informatie [Configureer Kerberos-verificatie](https://technet.microsoft.com/library/cc263449(v=office.12).aspx). Aandacht besteedt aan de sectie 'Service Principal Names maken voor uw webtoepassingen Kerberos-verificatie gebruiken'.

De eenvoudigste manier voor het instellen van SPN's is de SPN-indelingen die al aanwezig om uw sites zijn mogelijk volgen. Kopieer de SPN-namen te registreren op basis van het serviceaccount. Om dit te doen:

1. Blader naar de site met de SPN-naam van een andere computer.
 Wanneer u dit doet, wordt de relevante reeks Kerberos-tickets in cache op de machine. Deze tickets bevatten de SPN-naam van de doelsite die u hebt gebladerd.

2. U kunt de SPN voor die site met een hulpprogramma aangeroepen pull- [Klist uit](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html). Voer de volgende opdracht in een opdrachtvenster in de context als de gebruiker die toegang de site in de browser tot wordt uitgevoerd:
```
Klist
```
Klist uit retourneert vervolgens de set van doel-SPN's. De gemarkeerde waarde is in dit voorbeeld wordt de SPN-naam die nodig is:

  ![Voorbeeld Klist uit resultaten](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. Nu u de SPN hebt, moet u om ervoor te zorgen dat deze juist geconfigureerd op het serviceaccount dat u voor de webtoepassing eerder instellen. Voer de volgende opdracht vanaf de opdrachtprompt als beheerder van het domein:

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 Deze opdracht stelt u de SPN voor de SharePoint-serviceaccount wordt uitgevoerd als _demo\sp_svc_.

 Vervang _http/sharepoint.demo.o365identity.us_ met de SPN-naam voor uw server en _demo\sp_svc_ met het serviceaccount in uw omgeving. De Setspn-opdracht wordt gezocht naar de SPN voordat deze wordt toegevoegd. In dit geval ziet u mogelijk een **dubbele SPN waarde** fout. Als u deze fout ziet, zorg ervoor dat de waarde van de serviceaccount.

U kunt controleren of de SPN-naam is toegevoegd door het uitvoeren van de Setspn-opdracht met de optie -l. Zie voor meer informatie over deze opdracht, [Setspn](https://technet.microsoft.com/library/cc731241.aspx).

### <a name="ensure-that-the-connector-is-set-as-a-trusted-delegate-to-sharepoint"></a>Zorg ervoor dat de connector is ingesteld als een vertrouwde gemachtigde naar SharePoint

De KCD zodanig configureren dat de service Azure AD-toepassingsproxy gebruikersidentiteiten naar de SharePoint-service delegeren kunt. U doen dit door de connector voor het ophalen van Kerberos-tickets voor uw gebruikers die zijn geverifieerd in Azure AD-toepassingsproxy in te schakelen. Vervolgens die server context wordt doorgegeven aan de doeltoepassing of SharePoint in dit geval.

Herhaal de volgende stappen uit voor elke connector-machine voor het configureren van de KCD:

1. Meld u aan als domeinadministrator op een domeincontroller en open vervolgens **Active Directory: gebruikers en Computers**.
2. De computer waarop de connector wordt uitgevoerd op vinden. In dit voorbeeld is de dezelfde SharePoint-server.
3. Dubbelklik op de computer en klik vervolgens op de **delegering** tabblad.
4. Zorg ervoor dat de Overdrachtinstellingen zijn ingesteld op **deze computer mag alleen de opgegeven services delegeren**, en selecteer vervolgens **elk verificatieprotocol voor gebruiken**.

  ![Delegatie-instellingen](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. Klik op de **toevoegen** klikken, klik op **gebruikers of Computers**, en zoek de serviceaccount.

  ![De SPN voor de serviceaccount toevoegen](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. Selecteer in de lijst van SPN's die u eerder hebt gemaakt voor het serviceaccount.
7. Klik op **OK**. Klik op **OK** opnieuw de wijzigingen wilt opslaan.

## <a name="step-2-enable-remote-access-to-sharepoint"></a>Stap 2: Externe toegang voor SharePoint inschakelen

Nu u SharePoint hebt ingeschakeld voor Kerberos en geconfigureerde KCD, bent u klaar voor het instellen van eenmalige aanmelding tot SharePoint. Vervolgens kunt u de SharePoint-farm voor externe toegang via Azure AD-toepassingsproxy publiceren van de connector.

Als u wilt de volgende stappen uitvoert, moet u lid zijn van de globale beheerdersrol in uw organisatie Azure Active Directory-account.

1. Aanmelden bij de [Azure-portal](https://manage.windowsazure.com) en Ga naar uw Azure AD-tenant.
2. Klik op **toepassingen**, en klik vervolgens op **toevoegen**.
3. Selecteer **Een toepassing publiceren die toegankelijk is van buiten uw netwerk**. Als u deze optie niet ziet, zorg ervoor dat u Azure AD Basic hebt of Premium, in de tenant instellen.
4. Elk van de opties als volgt uitvoeren:
 * **Naam**: gebruik van elke waarde die u bijvoorbeeld wilt **SharePoint**.
 * **Interne URL**: dit is de URL van de SharePoint-site intern, zoals **https://SharePoint/**. Controleer of u in dit voorbeeld **https**.
 * **Methode voor verificatie vooraf**: Selecteer **Azure Active Directory**.

  ![Opties voor het toevoegen van een toepassing](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. Nadat de app wordt gepubliceerd, klikt u op de **configureren** tabblad.
6. Blader omlaag naar de optie **URL vertalen in Headers**. De standaardwaarde is **Ja**. Wijzig dit in **Nee**.

 SharePoint maakt gebruik van de _Host-Header_ waarde voor het opzoeken van de site. Koppelingen op basis van deze waarde wordt ook gegenereerd. Het uiteindelijke resultaat is om ervoor te zorgen dat koppelingen die SharePoint genereert een gepubliceerde URL juist is ingesteld voor gebruik van de externe URL is. De waarde instelt op **Ja** kunt u ook de connector voor het doorsturen van de aanvraag voor de back-end-toepassing. Als u echter de waarde instelt op **Nee** betekent dit dat de connector wordt de interne hostnaam niet verzenden. In plaats daarvan verzendt de connector de host-header als de URL van de gepubliceerde naar de back-end-toepassing.

 Om ervoor te zorgen dat SharePoint deze URL accepteert, moet u ook een meer configuratie op de SharePoint-server te voltooien. U doet dat in de volgende sectie.

7. Wijziging **interne verificatiemethode** naar **geïntegreerde Windows-verificatie**. Als uw Azure AD-tenant gebruikmaakt van een UPN in de cloud die verschilt van de UPN-on-premises, houd er rekening mee te werken **overgedragen aanmelding identiteit** ook.
8. Stel **interne toepassing SPN** naar de waarde die u eerder hebt ingesteld. Bijvoorbeeld: **http/sharepoint.demo.o365identity.us**.
9. De toepassing aan uw Doelgebruikers toewijzen.

Uw toepassing ziet er ongeveer als volgt uitzien:

  ![Voltooide toepassing](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-the-external-url"></a>Stap 3: Zorg ervoor dat SharePoint op de hoogte van de externe URL

De laatste stap om ervoor te zorgen dat SharePoint de site op basis van de externe URL, vindt zodat deze koppelingen op basis van die externe URL worden weergegeven. Hiervoor alternatieve toegangstoewijzingen voor de SharePoint-site configureren.

1. Open de **Centraal beheer van SharePoint 2013** site.
2. Onder **systeeminstellingen**, selecteer **alternatieve toegangstoewijzingen configureren**.

 Hiermee opent u de **alternatieve toegangstoewijzingen** vak.

  ![Alternatieve toegangstoewijzingen vak](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. In de vervolgkeuzelijst naast **alternatieve toewijzing collectie**, selecteer **alternatieve toewijzing collectie wijzigen**.
4. Selecteer uw site--bijvoorbeeld **SharePoint - 80**.

  ![Een site selecteren](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. U kunt de gepubliceerde URL niet toevoegen als een interne URL of een openbare URL. Dit voorbeeld wordt een openbare URL als het extranet.
6. Klik op **openbare URL's bewerken** in de **Extranet** pad, en voer vervolgens het pad voor de gepubliceerde toepassing, zoals in de vorige stap. Voer bijvoorbeeld **https://sharepoint-iddemo.msappproxy.net**.

  ![Het pad](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. Klik op **Opslaan**.

 U kunt nu toegang tot de SharePoint-site extern via Azure AD-toepassingsproxy.

## <a name="next-steps"></a>Volgende stappen

- [Het verstrekken van veilige externe toegang tot on-premises toepassingen](active-directory-application-proxy-get-started.md)
- [Azure AD-toepassingsproxy connectors begrijpen](application-proxy-understand-connectors.md)
- [Publicatie van SharePoint 2016 en Office Online-Server met Azure AD-toepassingsproxy](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)
