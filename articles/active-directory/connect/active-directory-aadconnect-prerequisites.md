---
title: 'Azure AD Connect: Vereisten en hardware | Microsoft Docs'
description: Dit onderwerp wordt beschreven Hallo-vereisten en Hallo hardwarevereisten voor Azure AD Connect
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 91b88fda-bca6-49a8-898f-8d906a661f07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2ec8b5da9440c92e8f9d6702d5e5e20de952b588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-for-azure-ad-connect"></a>Vereisten voor Azure AD Connect
Dit onderwerp beschrijft vereisten Hallo en Hallo hardwarevereisten voor Azure AD Connect.

## <a name="before-you-install-azure-ad-connect"></a>Voordat u Azure AD Connect installeren
Voordat u Azure AD Connect installeert, zijn er enkele dingen die u nodig hebt.

### <a name="azure-ad"></a>Azure AD
* Een Azure-abonnement of een [Azure-proefabonnement](https://azure.microsoft.com/pricing/free-trial/). Dit abonnement is alleen vereist voor toegang tot hello Azure-portal en niet voor het gebruik van Azure AD Connect. Als u PowerShell of Office 365 gebruikt, hoeft niet u een Azure-abonnement toouse Azure AD Connect. Als u een licentie voor Office 365 hebt, kunt u ook Hallo Office 365-portal gebruiken. Met een betaald Office 365-licentie, kunt u ook krijgen in hello Azure-portal via Hallo Office 365-portal.
  * U kunt ook Hallo [Azure-portal](https://portal.azure.com). Deze portal is niet vereist voor een Azure AD-licentie.
* [Toevoegen en verifiëren Hallo domein](../active-directory-domains-add-azure-portal.md) u toouse plannen in Azure AD. Bijvoorbeeld, als u van plan toouse contoso.com voor uw gebruikers bent, moet u ervoor zorgen dit domein is geverifieerd en u niet alleen Hallo contoso.onmicrosoft.com standaarddomein gebruikt.
* Een Azure AD-tenant kan door 50k-standaardobjecten. Bij het controleren van uw domein is Hallo limiet toegenomen too300k objecten. Als u nog meer objecten in Azure AD, moet u een limiet van ondersteuning case toohave Hallo verhoogd nog verder tooopen. Als u meer dan 500 kB-objecten, moet u een licentie, zoals Office 365, Azure AD Basic, Azure AD Premium of Enterprise Mobility en beveiliging.

### <a name="prepare-your-on-premises-data"></a>Uw on-premises gegevens voorbereiden
* Gebruik [IdFix](https://support.office.com/article/Install-and-run-the-Office-365-IdFix-tool-f4bd2439-3e41-4169-99f6-3fabdfa326ac) tooidentify fouten zoals duplicaten en opmaak problemen in uw directory voordat u tooAzure AD en Office 365 synchroniseert.
* Bekijk [optionele synchronisatie-functies u in Azure AD inschakelen kunt](active-directory-aadconnectsyncservice-features.md) en evalueren van de functies die u moet inschakelen.

### <a name="on-premises-active-directory"></a>On-premises Active Directory
* Hallo AD schema versie en forest-functionaliteitsniveau moet WindowsServer 2003 of hoger. Hallo-domeincontrollers kunnen een versie uitvoeren, zolang het Hallo-schema- en forest-niveau vereisten wordt voldaan.
* Als u van plan toouse Hallo functie bent **wachtwoord terugschrijven**, moet het Hallo-domeincontrollers Windows Server 2008 (met de meest recente SP) of hoger. Als uw DC's op 2008 (pre-R2 worden), dan moet u ook toepassen [hotfix KB2386717](http://support.microsoft.com/kb/2386717).
* Hallo-domeincontroller die wordt gebruikt door Azure AD moet schrijfbaar zijn. Het is **niet ondersteund** toouse een RODC (alleen-lezen domeincontroller) en Azure AD Connect niet voldoet aan alle omleidingen schrijven.
* Het is **niet ondersteund** toouse on-premises forests/domeinen met behulp van niveaudomeinen (één Label domeinen).
* Het is **niet ondersteund** toouse on-premises forests/domeinen met behulp van 'scheidingspunten' (een punt bevat '. ') NetBIOS-namen.
* Het is raadzaam te[Hallo Active Directory-Prullenbak inschakelen](active-directory-aadconnectsync-recycle-bin.md).

### <a name="azure-ad-connect-server"></a>Azure AD Connect-server
* Azure AD Connect kan niet worden geïnstalleerd op Small Business Server of Windows Server Essentials. Hallo-server moet gebruikmaken van Windows Server standard of hoger.
* Hello Azure AD Connect-server moet een volledige GUI geïnstalleerd hebben. Het is **niet ondersteund** tooinstall op server core.
* Azure AD Connect moet worden geïnstalleerd op Windows Server 2008 of hoger. Deze server mogelijk een domeincontroller of lidserver wanneer u een snelle instellingen. Als u aangepaste instellingen, Hallo-server kan ook worden zelfstandige en heeft geen toobe gekoppelde tooa domein.
* Als u Azure AD Connect op Windows Server 2008 of Windows Server 2008 R2 installeert, moet u ervoor dat tooapply Hallo meest recente hotfixes via Windows Update. Hallo-installatie is niet kunnen toostart met een niet-gepatchte-server.
* Als u van plan toouse Hallo functie bent **Wachtwoordsynchronisatie**, en vervolgens hello Azure AD Connect-server op Windows Server 2008 R2 SP1 of later moet.
* Als u van plan toouse bent een **groep beheerd serviceaccount**, en vervolgens hello Azure AD Connect-server op Windows Server 2012 of later moet.
* Hello Azure AD Connect-server moet hebben [.NET Framework 4.5.1](#component-prerequisites) of hoger en [Microsoft PowerShell 3.0](#component-prerequisites) of hoger is geïnstalleerd.
* Hello Azure AD Connect-server geen PowerShell schrijffouten-Groepsbeleid is ingeschakeld.
* Als Active Directory Federation Services wordt geïmplementeerd, Hallo servers waar AD FS of Web Application Proxy zijn geïnstalleerd moet Windows Server 2012 R2 of hoger. [Windows remote management](#windows-remote-management) moet zijn ingeschakeld op deze servers voor installatie op afstand.
* Als Active Directory Federation Services wordt geïmplementeerd, moet u [SSL-certificaten](#ssl-certificate-requirements).
* Als Active Directory Federation Services wordt geïmplementeerd, moet u tooconfigure [naamomzetting](#name-resolution-for-federation-servers).
* Als uw globale beheerders MFA ingeschakeld hebt, klikt u vervolgens URL Hallo **https://secure.aadcdn.microsoftonline-p.com** moet zich in de lijst met vertrouwde websites Hallo. U bent na vragen aan gebruiker tooadd deze site toohello lijst met vertrouwde websites wanneer u wordt gevraagd om een challenge MFA en deze niet is toegevoegd voordat. U kunt Internet Explorer tooadd het tooyour vertrouwde websites.

### <a name="sql-server-used-by-azure-ad-connect"></a>SQL Server die wordt gebruikt door Azure AD Connect
* Azure AD Connect vereist een SQL Server-database toostore identity-gegevens. Een SQL Server 2012 Express LocalDB (een lichte versie van SQL Server Express) wordt standaard geïnstalleerd. SQL Server Express heeft een limiet van 10GB waarmee u toomanage ongeveer 100.000 objecten. Als u een groter volume van directory-objecten toomanage nodig hebt, moet u toopoint Hallo installatie wizard tooa andere installatie van SQL Server.
* Als u een afzonderlijke SQL Server gebruikt, is deze vereisten van toepassing:
  * Azure AD Connect ondersteunt alle versies van Microsoft SQL Server van SQL Server 2008 (met de meest recente servicepack) tooSQL Server 2016 SP1. Microsoft Azure SQL Database is **niet ondersteund** als een database.
  * U moet een niet-hoofdlettergevoelige SQL-sortering gebruiken. Deze sorteringen worden aangeduid met een \_CI_ in hun naam. Het is **niet ondersteund** toouse een hoofdlettergevoelige sortering geïdentificeerd door \_CS_ in hun naam.
  * U kunt slechts één synchronisatie-engine per SQL-exemplaar hebben. Het is **niet ondersteund** tooshare een SQL-exemplaar met FIM/MIM Sync en DirSync en Azure AD Sync.

### <a name="accounts"></a>Accounts
* Een globale beheerder van Azure AD-account voor de gewenste toointegrate met hello Azure AD-tenant. Deze account moet een **school of organisatie-account** en kan niet worden een **Microsoft-account**.
* Als u snelle instellingen gebruiken of een van DirSync upgrade, moet u een Enterprise-beheerdersaccount hebben voor uw lokale Active Directory.
* [Accounts in Active Directory](active-directory-aadconnect-accounts-permissions.md) als u Hallo aangepaste instellingen installatiepad gebruiken.

### <a name="connectivity"></a>Connectiviteit
* Hello Azure AD Connect-server moet een DNS-omzetting voor intranet en internet. Hallo DNS-server moet kunnen tooresolve namen tooyour on-premises Active Directory en hello Azure AD-eindpunten.
* Als u firewalls op uw Intranet hebt en u tooopen poorten tussen hello Azure AD Connect-servers en uw domeincontrollers moet, Zie [Azure AD Connect-poorten](active-directory-aadconnect-ports.md) voor meer informatie.
* Als uw proxy of firewall limiet URL's kunnen worden geopend, klikt u vervolgens Hallo URL's die worden beschreven in [Office 365-URL's en IP-adresbereiken](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) moet worden geopend.
  * Als u gebruikmaakt van Microsoft-Cloud in Duitsland of Hallo cloud van Microsoft Azure Government Hallo en vervolgens Zie [Azure AD Connect sync-service-exemplaren overwegingen](active-directory-aadconnect-instances.md) voor URL's.
* Azure AD Connect is standaard gebruik van TLS 1.0 toocommunicate met Azure AD. U kunt deze tooTLS 1.2 wijzigen door de stappen te volgen Hallo in [TLS 1.2 inschakelen voor Azure AD Connect](#enable-tls-12-for-azure-ad-connect).
* Als u een uitgaande proxyconfiguratie voor het verbinden van toohello Internet gebruikt, Hallo volgende instelling in Hallo **C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config** bestand moet worden toegevoegd voor Hallo-installatiewizard en Azure AD Connect-synchronisatie toobe kunnen tooconnect toohello Internet en Azure AD. Deze tekst moet worden ingevoerd onder Hallo van Hallo-bestand. In deze code &lt;PROXYADRESS&gt; vertegenwoordigt Hallo werkelijke IP-adres of de hostnaam proxynaam.

```
    <system.net>
        <defaultProxy>
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Als de proxyserver verificatie en vervolgens Hallo vereist [-serviceaccount](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) moet zich in Hallo domein en u Hallo aangepaste instellingen voor installatie pad toospecify moet gebruiken een [aangepaste serviceaccount](active-directory-aadconnect-get-started-custom.md#install-required-components). U moet ook een andere wijziging toomachine.config. Met deze wijziging in machine.config reageert Hallo installatie wizard en de synchronisatie-engine tooauthentication aanvragen van de proxyserver Hallo. In alle installatie wizardpagina's, met uitzondering van Hallo **configureren** pagina Hallo van de gebruiker aangemeld referenties worden gebruikt. Op Hallo **configureren** pagina achter Hallo Hallo-installatiewizard, Hallo context is uitgeschakeld toohello [-serviceaccount](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) die door u is gemaakt. sectie van machine.config Hallo ziet er als volgt.

```
    <system.net>
        <defaultProxy enabled="true" useDefaultCredentials="true">
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Als Azure AD Connect een web-aanvraag tooAzure AD als onderdeel van directory-synchronisatie verstuurt, kan Azure AD toorespond van too5 minuten duren. Het is gebruikelijk voor configuratie van proxy-servers toohave verbinding time-out voor inactiviteit. Zorg ervoor Hallo configuratie tooat minimaal 6 minuten of langer is ingesteld.

Zie MSDN voor meer informatie over Hallo [standaard proxy Element](https://msdn.microsoft.com/library/kd3cf2ex.aspx).  
Zie voor meer informatie wanneer u problemen met de connectiviteit hebt, [connectiviteitsproblemen oplossen](active-directory-aadconnect-troubleshoot-connectivity.md).

### <a name="other"></a>Overige
* Optioneel: Een test gebruiker account tooverify synchronisatie.

## <a name="component-prerequisites"></a>Vereisten voor onderdelen
### <a name="powershell-and-net-framework"></a>PowerShell en .net Framework
Azure AD Connect, hangt af van de Microsoft PowerShell en .NET Framework 4.5.1. U moet deze versie of een latere versie is geïnstalleerd op uw server. Afhankelijk van uw versie van Windows Server, Hallo te volgen:

* Windows Server 2012R2
  * Microsoft PowerShell wordt standaard geïnstalleerd. Er is geen actie vereist.
  * .NET framework 4.5.1 en latere versies worden aangeboden via Windows Update. Zorg ervoor dat u Hallo meest recente updates tooWindows Server hebt geïnstalleerd in het Configuratiescherm Hallo.
* Windows Server 2008 R2 en WindowsServer 2012
  * meest recente versie van Microsoft PowerShell Hallo is beschikbaar in **Windows Management Framework 4.0**, beschikbaar op [Microsoft Download Center](http://www.microsoft.com/downloads).
  * .NET framework 4.5.1 en latere versies zijn beschikbaar op [Microsoft Download Center](http://www.microsoft.com/downloads).
* Windows Server 2008
  * Hallo ondersteund meest recente versie van PowerShell is beschikbaar in **Windows Management Framework 3.0**, beschikbaar op [Microsoft Download Center](http://www.microsoft.com/downloads).
  * .NET framework 4.5.1 en latere versies zijn beschikbaar op [Microsoft Download Center](http://www.microsoft.com/downloads).

### <a name="enable-tls-12-for-azure-ad-connect"></a>TLS 1.2 inschakelen voor Azure AD Connect
Azure AD Connect maakt gebruik van TLS 1.0 standaard voor het versleutelen van Hallo communicatie tussen Hallo synchronisatie-engine-server en Azure AD. U kunt dit wijzigen door .net-toepassingen toouse TLS 1.2 standaard op Hallo-server te configureren. Meer informatie over TLS 1.2 vindt u in [Microsoft Security Advisory 2960358](https://technet.microsoft.com/security/advisory/2960358).

1. TLS 1.2 kan niet worden ingeschakeld op Windows Server 2008. U moet Windows Server 2008 R2 of hoger. Zorg ervoor dat u hebben Hallo .net 4.5.1 hotfix voor uw besturingssysteem is geïnstalleerd, Zie [Microsoft Security Advisory 2960358](https://technet.microsoft.com/security/advisory/2960358). U hebt deze hotfix of een latere versie is al geïnstalleerd op uw server.
2. Als u Windows Server 2008 R2 gebruikt, Controleer of dat TLS 1.2 is ingeschakeld. TLS 1.2 moeten al zijn ingeschakeld op de server met Windows Server 2012 en latere versies.
   ```
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2]
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   ```
3. Voor alle besturingssystemen, stelt u deze registersleutel en start Hallo-server.
   ```
   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319
   "SchUseStrongCrypto"=dword:00000001
   ```
4. Als u ook tooenable TLS 1.2 tussen Hallo synchronisatie-engine-server en een externe SQL Server wilt, wordt zorg ervoor dat u beschikt over Hallo vereist versies geïnstalleerd voor [TLS 1.2-ondersteuning voor Microsoft SQL Server](https://support.microsoft.com/kb/3135244).

## <a name="prerequisites-for-federation-installation-and-configuration"></a>Vereisten voor de federation-installatie en configuratie
### <a name="windows-remote-management"></a>Windows Remote Management
Wanneer u Azure AD Connect toodeploy Active Directory Federation Services of Hallo Web Application Proxy, Controleer de volgende vereisten:

* Als doelserver Hallo verbonden met het domein is, zorgt Windows extern beheerde is ingeschakeld
  * Gebruik in een venster met verhoogde bevoegdheid PSH opdracht de opdracht`Enable-PSRemoting –force`
* Als de doelserver Hallo WAP machine lid zijn van een niet-domein, worden er enkele aanvullende vereisten
  * Op de doelcomputer hello (WAP-machine):
    * Zorg ervoor dat Hallo winrm (Windows Remote Management / WS-Management)-service wordt uitgevoerd via Hallo-module Services
    * Gebruik in een venster met verhoogde bevoegdheid PSH opdracht de opdracht`Enable-PSRemoting –force`
  * Op de computer Hallo op welke Hallo wizard (als de doelmachine Hallo niet van het domein gekoppelde of niet-vertrouwd domein is) wordt uitgevoerd:
    * In een venster met verhoogde bevoegdheid PSH opdracht Hallo-opdracht gebruiken`Set-Item WSMan:\localhost\Client\TrustedHosts –Value <DMZServerFQDN> -Force –Concatenate`
    * In Serverbeheer:
      * DMZ WAP host toomachine van toepassingen toevoegen (Serverbeheer beheren ->-Servers toevoegen... > tabblad DNS gebruiken)
      * Tabblad Serverbeheer alle Servers: WAP-server met de rechtermuisknop op en kies beheren als..., lokale (niet domein) referenties invoeren voor Hallo WAP machine
      * toovalidate externe PSH connectivity in Server Manager alle Servers tabblad Hallo: klik met de rechtermuisknop op WAP-server en kies Windows PowerShell. Een externe PSH-sessie moet worden geopend tooensure externe PowerShell-sessies kunnen worden vastgesteld.

### <a name="ssl-certificate-requirements"></a>Vereisten voor SSL-certificaten
* Het wordt sterk aanbevolen toouse Hallo SSL-certificaat dat voor alle knooppunten van uw AD FS-farm en alle proxyservers van de webtoepassing.
* Hallo-certificaat moet een X509 certificaat.
* U kunt een zelfondertekend certificaat gebruiken op federatieservers in een testomgeving. We raden echter voor een productieomgeving aan dat u Hallo certificaat van een openbare Certificeringsinstantie verkrijgen.
  * Als een certificaat dat is niet openbaar worden vertrouwd, controleert u dat Hallo certificaat geïnstalleerd op elke server met Web Application Proxy wordt vertrouwd op beide Hallo lokale server en op alle federatieservers
* Hallo identiteit van het Hallo-certificaat moet overeenkomen met de naam Hallo federation-service (bijvoorbeeld sts.contoso.com).
  * Hallo-identiteit is ofwel een onderwerp alternatieve naam (SAN)-extensie van type dNSName of, als er geen SAN-items zijn, Hallo onderwerpnaam moet worden opgegeven als een algemene naam.  
  * Meerdere vermeldingen met SAN kunnen aanwezig zijn in Hallo-certificaat opgegeven één van deze overeenkomt met Hallo federatieve-servicenaam.
  * Als u van plan bent toouse Workplace Join, een extra SAN is vereist bij Hallo waarde **enterpriseregistratie.** gevolgd door Hallo UPN (User Principal Name)-achtervoegsel van uw organisatie, bijvoorbeeld **: enterpriseregistration.contoso.com**.
* Certificaten op basis van de volgende generation (CNG)-sleutels CryptoAPI en sleutelarchiefproviders worden niet ondersteund. Dit betekent dat u moet een certificaat dat op basis van een CSP (cryptographic serviceprovider) en niet een KSP (sleutelarchiefprovider) gebruiken.
* Jokertekens certificaten worden ondersteund.

### <a name="name-resolution-for-federation-servers"></a>Naamomzetting voor federatieservers
* DNS-records voor Hallo instellen met AD FS federation service name (bijvoorbeeld sts.contoso.com) voor het Hallo-intranet (uw interne DNS-server) en Hallo extranet (openbare DNS-server via uw domeinregistrar). Voor Hallo intranet DNS-record, zorg ervoor dat u A-records en geen CNAME-records. Dit is vereist voor windows-verificatie toowork correct van uw domein gekoppelde computer.
* Als u meer dan één AD FS-server of Web Application Proxy server implementeert, controleert u of u de load balancer hebt geconfigureerd en dat de load balancer Hallo DNS-records voor Hallo AD FS federation service name (bijvoorbeeld sts.contoso.com) punt toohello.
* Zorg ervoor dat Hallo AD FS federation service-naam (bijvoorbeeld sts.contoso.com) toohello intranetzone in Internet Explorer wordt toegevoegd voor windows geïntegreerde verificatie toowork voor browsertoepassingen met behulp van Internet Explorer in het intranet. Dit kan worden beheerd via Groepsbeleid en geïmplementeerde tooall de computers van uw domein.

## <a name="azure-ad-connect-supporting-components"></a>Azure AD Connect ondersteunende onderdelen
Hallo Hieronder volgt een lijst van onderdelen die Azure AD Connect installeert op Hallo-server waarop Azure AD Connect is geïnstalleerd. Deze lijst is bedoeld voor een basisinstallatie van Express. Als u toouse Kies een andere SQL Server op Hallo installatiepagina synchronisatie-services, vervolgens SQL Express LocalDB lokaal niet is geïnstalleerd.

* Azure AD Connect Health (Engelstalig)
* Microsoft Online Services-aanmeldhulp voor IT-Professionals (geïnstalleerd, maar er is geen afhankelijkheid van het)
* Microsoft SQL Server 2012 Command Line Utilities
* Microsoft SQL Server 2012 Express LocalDB
* Microsoft SQL Server 2012 Native Client
* Microsoft Visual C++ 2013-distributiepakket

## <a name="hardware-requirements-for-azure-ad-connect"></a>Hardwarevereisten voor Azure AD Connect
Hallo in de volgende tabel toont Hallo minimale vereisten voor hello Azure AD Connect sync-computer.

| Het aantal objecten in Active Directory | CPU | Geheugen | Grootte van de harde schijf |
| --- | --- | --- | --- |
| Minder dan 10.000 |1,6 GHz |4 GB |70 GB |
| 10,000–50,000 |1,6 GHz |4 GB |70 GB |
| 50,000–100,000 |1,6 GHz |16 GB |100 GB |
| 100.000 of meer objecten is Hallo volledige versie van SQL Server vereist voor | | | |
| 100,000–300,000 |1,6 GHz |32 GB |300 GB |
| 300,000–600,000 |1,6 GHz |32 GB |450 GB |
| Meer dan 600.000 |1,6 GHz |32 GB |500 GB |

minimale vereisten voor computers met AD FS Hallo of Webtoepassingsservers Hallo volgende is:

* CPU: Dual core 1,6 GHz of hoger
* GEHEUGEN: 2 GB of hoger
* Azure virtuele machine: Configuratie A2 of hoger

## <a name="next-steps"></a>Volgende stappen
Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory](active-directory-aadconnect.md).
