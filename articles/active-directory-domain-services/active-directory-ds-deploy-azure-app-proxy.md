---
title: 'Azure Active Directory Domain Services: Azure Active Directory-toepassingsproxy implementeren | Microsoft Docs'
description: Azure AD-toepassingsproxy gebruiken op de beheerde domeinen Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 4142111231d0256960d0c02d686d51533ba2171c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a>Azure AD-toepassingsproxy op een beheerd domein van Azure AD Domain Services implementeren
Toepassingsproxy van Azure Active Directory (AD) kunt u ondersteuning voor externe werknemers door het publiceren van lokale toepassingen toobe toegankelijk is via Hallo internet. U kunt nu lift-en-shift oudere toepassingen met lokale tooAzure Infrastructure Services met Azure AD Domain Services. Vervolgens kunt u deze toepassingen met behulp van hello Azure AD-toepassingsproxy, tooprovide veilige externe toegang toousers in uw organisatie publiceren.

Als u nieuwe toohello Azure AD-toepassingsproxy, meer informatie over deze functie hello volgende artikel: [hoe tooprovide veilige externe toegang tot het tooon-premises toepassingen](../active-directory/active-directory-application-proxy-get-started.md).


## <a name="before-you-begin"></a>Voordat u begint
tooperform hello taken die in dit artikel worden vermeld, hebt u nodig:

1. Een geldige **Azure-abonnement**.
2. Een **Azure AD-directory** -ofwel gesynchroniseerd met een on-premises adreslijst of een map alleen in de cloud.
3. Een **Azure AD Basic of Premium-licentie** is vereist toouse hello Azure AD-toepassingsproxy.
4. **Azure AD Domain Services** moet zijn ingeschakeld voor hello Azure AD-directory. Als u dit nog niet hebt gedaan, volgt u alle Hallo taken die worden beschreven in Hallo [handleiding](active-directory-ds-getting-started.md).

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a>Taak 1: toepassingsproxy van Azure AD inschakelen voor uw Azure AD-directory
Volgende stappen tooenable hello Azure AD-toepassingsproxy voor uw Azure AD-directory Hallo uitvoeren.

1. Meld u aan als een beheerder in Hallo [Azure-portal](http://portal.azure.com).

2. Klik op **Azure Active Directory** toobring up overzicht Hallo-directory. Klik op **bedrijfstoepassingen**.

    ![Azure AD-directory selecteren](./media/app-proxy/app-proxy-enable-start.png)
3. Klik op **toepassingsproxy**. Als u niet een Azure AD Basic of Azure AD Premium-abonnement hebt, ziet u een optie tooenable een proefversie. Wisselknop **toepassingsproxy inschakelen?** te**inschakelen** en klik op **opslaan**.

    ![Toepassingsproxy inschakelen](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. toodownload Hallo connector, klikt u op Hallo **Connector** knop.

    ![Connector downloaden](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. Op de downloadpagina hello, accepteer Hallo licentievoorwaarden en privacyovereenkomst en klik op Hallo **downloaden** knop.

    ![Download bevestigen](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-toodeploy-hello-azure-ad-application-proxy-connector"></a>Taak 2 - inrichten domein Windows servers toodeploy hello Azure AD-toepassingsproxy-connector
U moet lid zijn van het domein Windows Server virtuele machines waarop u hello Azure AD-toepassingsproxy connector kunt installeren. Afhankelijk van de toepassingen hello wordt gepubliceerd, kunt u tooprovision meerdere servers waarop Hallo-connector is geïnstalleerd. Deze Implementatieoptie krijgt u groter beschikbaarheid en helpt bij het verwerken van zwaardere belastingen voor verificatie.

Servers met de Hallo connector richten op Hallo van hetzelfde virtuele netwerk (of een virtueel netwerk met verbonden/brengen) in die u hebt ingeschakeld uw beheerde domein van Azure AD Domain Services. Op deze manier Hallo-servers die als host fungeert voor Hallo-toepassingen die u via Hallo toepassingsproxy publiceert toobe geïnstalleerd op Hallo moeten hetzelfde virtuele Azure-netwerk.

tooprovision Connectorservers, volg Hallo taken die worden beschreven in artikel Hallo [lid worden van een beheerd domein voor Windows virtuele machine tooa](active-directory-ds-admin-guide-join-windows-vm.md).


## <a name="task-3---install-and-register-hello-azure-ad-application-proxy-connector"></a>Taak 3: Installeer en registreer hello Azure AD-Application Proxy Connector
Eerder ingerichte van een virtuele machine van Windows Server en deze toohello beheerd domein toegevoegd. In deze taak kunt u hello Azure AD-toepassingsproxy connector wilt installeren op deze virtuele machine.

1. Kopieer Hallo connector installatie pakket toohello VM waarop u hello Azure AD Web Application Proxy connector installeert.

2. Voer **AADApplicationProxyConnectorInstaller.exe** op Hallo virtuele machine. Licentievoorwaarden Hallo-software accepteren.

    ![Accepteer de voorwaarden voor installatie](./media/app-proxy/app-proxy-install-connector-terms.png)
3. Tijdens de installatie bent u na vragen aan gebruiker tooregister Hallo connector met Hallo toepassingsproxy van uw Azure AD-directory.
    * Geef uw **Azure AD-referenties globale beheerder**. De referenties van uw globale beheerderstenant kunnen afwijken van uw Microsoft Azure-referenties.
    * Hallo beheerder account gebruikt tooregister Hallo connector moet behoren toohello dezelfde map waarin u Hallo-service voor toepassingsproxy hebt ingeschakeld. Bijvoorbeeld, als Hallo tenant domein contoso.com is, Hallo beheerder moet admin@contoso.com of andere geldige alias in dat domein.
    * Als Verbeterde beveiliging van Internet Explorer is ingeschakeld voor Hallo server waarop u Hallo-connector installeert, kunt u Hallo registratiescherm mogelijk geblokkeerd. tooallow toegang, volg de instructies in Hallo in Hallo-bericht. Zorg ervoor dat de verbeterde beveiliging van Internet Explorer is uitgeschakeld.
    * Zie [Troubleshoot Application Proxy](../active-directory/active-directory-application-proxy-troubleshoot.md) (Engelstalig) als de registratie van de connector niet lukt.

    ![Connector is geïnstalleerd](./media/app-proxy/app-proxy-connector-installed.png)
4. tooensure hello connector werkt goed uitgevoerde hello Azure AD Application Proxy Connector probleemoplosser. U ziet een geslaagde rapport na actieve Hallo probleemoplosser.

    ![Probleemoplosser geslaagd](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. U ziet Hallo onlangs geïnstalleerde connector vermeld op Hallo Application proxy pagina in uw Azure AD-directory.

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> U kunt tooguarantee hoge beschikbaarheid voor het verifiëren van toepassingen die zijn gepubliceerd via hello Azure AD-toepassingsproxy tooinstall connectors op meerdere servers. Hallo dezelfde stappen tooinstall Hallo connector op andere servers lid tooyour beheerde domeinen bovenstaande uitvoeren.
>
>

## <a name="next-steps"></a>Volgende stappen
U hebt Azure AD-toepassingsproxy Hallo instellen en deze geïntegreerd met uw Azure AD Domain Services beheerd domein.

* **Uw toepassingen tooAzure virtuele machines migreren:** kunt lift en shift uw toepassingen van lokale servers tooAzure virtuele machines lid tooyour beheerde domein. In dat geval kunt u van kosten van de infrastructuur van het uitvoeren van servers lokale Hallo afvoeren.

* **Toepassingen publiceren met Azure AD-toepassingsproxy:** publiceren van toepassingen die op uw virtuele machines in Azure met Azure AD-toepassingsproxy Hallo uitgevoerd. Zie voor meer informatie [toepassingen publiceren met Azure AD-toepassingsproxy](../active-directory/application-proxy-publish-azure-portal.md)


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a>Opmerking van de implementatie - publiceren IWA (geïntegreerde Windows-verificatie)-toepassingen die gebruikmaken van Azure AD-toepassingsproxy
Eenmalige aanmelding tooyour-toepassingen die gebruikmaken van geïntegreerde Windows-verificatie (IWA) Application Proxy Connectors toestemming verleent tooimpersonate gebruikers, inschakelen en verzenden en ontvangen van tokens in hun naam. Kerberos-beperkte delegatie (KCD) voor Hallo connector toogrant Hallo vereist machtigingen tooaccess bronnen op Hallo beheerd domein configureren. Gebruik Hallo resources gebaseerde KCD mechanisme op beheerde domeinen voor een betere beveiliging.


### <a name="enable-resource-based-kerberos-constrained-delegation-for-hello-azure-ad-application-proxy-connector"></a>Op basis van bronnen kerberos-beperkte overdracht voor hello Azure AD-toepassingsproxy connector inschakelen
Hello Azure Application Proxy connector moet worden geconfigureerd voor kerberos-beperkte delegatie (KCD), zodat gebruikers kunnen worden geïmiteerd op Hallo beheerde domein. Op een beheerd domein van Azure AD Domain Services er geen domeinadministratorrechten. Daarom **traditionele account niveau KCD kan niet worden geconfigureerd op een beheerd domein**.

Gebruik KCD op basis van bronnen zoals beschreven in dit [artikel](active-directory-ds-enable-kcd.md).

> [!NOTE]
> U moet toobe lid van Hallo ' AAD DC' beheerdersgroep tooadminister Hallo beheerd domein met AD PowerShell-cmdlets.
>
>

Hallo Get-ADComputer PowerShell cmdlet tooretrieve Hallo instellingen gebruiken voor Hallo-computer op welke hello Azure AD-toepassingsproxy-connector is geïnstalleerd.
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

Gebruik daarna Hallo Set-ADComputer cmdlet tooset up KCD op basis van een resource voor Hallo resource-server.
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

Als u meerdere toepassingsproxy connectors voor uw beheerde domein hebt geïmplementeerd, moet u tooconfigure KCD voor elk dergelijke connector-exemplaar op basis van bronnen.


## <a name="related-content"></a>Gerelateerde inhoud
* [Azure AD Domain Services - handleiding aan de slag](active-directory-ds-getting-started.md)
* [Kerberos-beperkte overdracht configureren op een beheerd domein](active-directory-ds-enable-kcd.md)
* [Kerberos-beperkte overdracht overzicht](https://technet.microsoft.com/library/jj553400.aspx)
