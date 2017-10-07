---
title: aaaAzure Active Directory Connect Health FAQ - Azure | Microsoft Docs
description: Deze Veelgestelde vragen over de antwoorden op vragen over Azure AD Connect Health. Deze Veelgestelde vragen worden vragen behandeld over Hallo service gebruiken, inclusief Hallo facturering model, mogelijkheden, beperkingen en ondersteuning.
services: active-directory
documentationcenter: 
author: billmath
manager: samueld
editor: curtand
ms.assetid: f1b851aa-54d7-4cb4-8f5c-60680e2ce866
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 3f15d9e9b557b09ef74ceff85806579dd51f2412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-frequently-asked-questions"></a>Veelgestelde vragen over Azure AD Connect Health
Dit artikel bevat toofrequently van antwoorden op veelgestelde vragen (FAQ's) over Azure Active Directory (Azure AD) Connect Health. Deze Veelgestelde vragen hebben betrekking op vragen over hoe toouse Hallo-service, waaronder Hallo facturering model, mogelijkheden, beperkingen en ondersteuning.

## <a name="general-questions"></a>Algemene vragen
**V: ik beheren meerdere directory's van Azure AD. Hoe schakel ik toohello heeft Azure Active Directory Premium**

tooswitch tussen verschillende Azure AD tenants Selecteer Hallo die momenteel is aangemeld **gebruikersnaam** op Hallo rechterbovenhoek en kies vervolgens de juiste account Hallo. Als het Hallo-account hier niet wordt weergegeven, selecteert u **Afmelden**, en vervolgens de referenties voor de globale beheerder van gebruiken Hallo van Hallo directory met Azure Active Directory Premium toosign in ingeschakeld.

**V: welke versie van de identiteit functies worden ondersteund door Azure AD Connect Health?**

Hallo volgende tabel bevat Hallo rollen en ondersteunde versies van besturingssystemen.

|Rol| Besturingssysteem / versie|
|--|--|
|Active Directory Federation Services (AD FS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|
|Azure AD Connect | Versie 1.0.9125 of hoger|
|Active Directory Domain Services (AD DS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|

Hallo functies die worden geleverd door de service Hallo afwijken gebaseerde op Hallo-rol en het Hallo-besturingssysteem. Met andere woorden, alle Hallo functies mogelijk niet beschikbaar voor alle versies van besturingssystemen. Zie Hallo functiebeschrijvingen voor meer informatie.

**V: hoeveel licenties kunnen ik mijn infrastructuur toomonitor nodig?**

* Hallo vereist eerste Connect Health-Agent ten minste één Azure AD Premium-licentie.
* Elke extra geregistreerde agent vereist 25 extra licenties voor Azure AD Premium.
* Aantal agents is gelijkwaardig toohello kunt u het totale aantal agents die zijn geregistreerd voor alle bewaakte rollen (AD FS, Azure AD Connect en/of AD DS).

Licentie-informatie is ook te vinden op Hallo [prijzen van Azure AD-pagina](https://aka.ms/aadpricing).

Voorbeeld:

| Geregistreerde agents | Licenties nodig | Voorbeeld van de configuratie van bewaking |
| ------ | --------------- | --- |
| 1 | 1 | 1 azure AD Connect-server |
| 2 | 26| 1 azure AD Connect-server en 1-domeincontroller |
| 3 | 51 | 1 active Directory Federation Services (AD FS)-server, 1 AD FS-proxy en 1-domeincontroller |
| 4 | 76 | 1 AD FS-server, 1 AD FS-proxy en 2 domeincontrollers |
| 5 | 101 | 1 azure AD Connect-server, 1 AD FS-server, 1 AD FS-proxy en 2-domeincontrollers |


## <a name="installation-questions"></a>Installatievragen

**V: Wat is Hallo gevolgen van het hello Azure AD Connect Health-Agent installeren op afzonderlijke servers?**

Hallo-impact van de installatie Hallo Microsoft Azure AD Connect Health-Agent, AD FS webtoepassingsproxyservers, Azure AD Connect (sync)-servers, domeincontrollers is minimale met opzicht toohello CPU, geheugen, netwerkbandbreedte en opslag.

Hallo cijfers na zijn een benadering:

* CPU-verbruik: ~ 1-5% verhogen.
* Geheugengebruik: too10% van het systeemgeheugen Hallo.

> [!NOTE]
> Als het Hallo-agent kan niet communiceren met Azure, slaat Hallo agent Hallo-gegevens voor een gedefinieerde maximumlimiet lokaal. Hallo-agent worden gegevens gedurende een 'in de cache' Hallo 'minst recentelijk onderhouden' op basis van een overschreven.
>
>

* Lokale buffer opslag voor Azure AD Connect Health-Agents: ~ 20 MB.
* Voor AD FS-servers, wordt u aangeraden dat u een schijfruimte van maximaal 1024 MB (1 GB) voor AD FS Hallo audit-kanaal van Azure AD Connect Health-Agents tooprocess alle Hallo controlegegevens inricht voordat deze wordt overschreven.

**V: ik heeft tooreboot mijn servers tijdens de installatie van hello Azure AD Connect Health-Agents Hallo?**

Nee. Hallo-installatie van agents hello wordt geen u tooreboot Hallo server vereist. Installatie van bepaalde vereiste stappen vereisen echter Hallo-server opnieuw worden opgestart.

Installatie van .NET-Framework 4.5 vereist bijvoorbeeld in Windows Server 2008 R2, server opnieuw opstarten.

**V: bevat Azure AD Connect Health werk via een Pass Through-HTTP-proxy?**

Ja. Voor lopende bewerkingen kunt u configureren Hallo Health Agent toouse een HTTP-proxy tooforward uitgaande HTTP-aanvragen.
Lees meer over [HTTP-Proxy voor Health-Agents configureren](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy).

Als u een proxy tooconfigure tijdens de agentregistratie moet, moet u mogelijk toomodify uw proxyinstellingen van Internet Explorer tevoren.

1. Open Internet Explorer > **instellingen** > **Internetopties** > **verbindingen** > **LAN-instellingen** .
2. Selecteer **een proxyserver gebruiken voor uw LAN**.
3. Selecteer **Geavanceerd** hebt u verschillende proxyservers poorten voor HTTP en HTTPS/Secure.

**V: bevat Azure AD Connect Health ondersteuning basisverificatie bij het verbinden van tooHTTP proxy's?**

Nee. Een mechanisme toospecify een willekeurige gebruikersnaam en wachtwoord voor basisverificatie is momenteel niet ondersteund.

**V: wat firewallpoorten doen ik tooopen nodig voor hello Azure AD Connect Health-Agent toowork?**

Zie Hallo [gedeelte vereisten](active-directory-aadconnect-health-agent-install.md#requirements) voor Hallo lijst met firewall-poorten en andere vereisten voor connectiviteit.

**V: Waarom zie ik twee servers met dezelfde naam in de portal hello Azure AD Connect Health Hallo?**

Wanneer u een agent van een server verwijderen, wordt Hallo-server niet automatisch verwijderd van hello Azure AD Connect Health-portal. Als u handmatig een agent van een server verwijderen of Hallo-server zelf verwijderen, moet u toomanually verwijderen Hallo server item in de portal hello Azure AD Connect Health.

U kunt installatiekopie van een server of een nieuwe server maken met de Hallo dezelfde informatie (zoals de naam van de machine). Als Hallo reeds geregistreerde server niet hebt verwijderd van de portal hello Azure AD Connect Health en u Hallo agent geïnstalleerd op de nieuwe server hello, ziet u mogelijk twee vermeldingen Hello dezelfde naam.

In dit geval Hallo-vermelding die deel uitmaakt van de oudere server toohello handmatig verwijderen. Hallo-gegevens voor deze server moet niet actueel zijn.

## <a name="health-agent-registration-and-data-freshness"></a>Registratie en gegevens versheid van Health-Agent

**V: wat zijn veelvoorkomende redenen voor Hallo Health Agent-registratiefouten en hoe kan ik problemen oplossen?**

Hallo health-agent kan mislukken tooregister vanwege de volgende toohello mogelijke redenen:

* Hallo-agent kan niet communiceren met de Hallo vereist eindpunten omdat verkeer door een firewall wordt geblokkeerd. Dit geldt met name op webtoepassingsproxyservers. Zorg ervoor dat u hebt toegestaan uitgaande communicatie vereist toohello eindpunten en poorten. Zie Hallo [gedeelte vereisten](active-directory-aadconnect-health-agent-install.md#requirements) voor meer informatie.
* Uitgaande communicatie is een SSL-inspectie ondergaan tooan door Hallo netwerklaag. Dit zorgt ervoor dat de Hallo-certificaat dat Hallo agent toobe vervangen door Hallo inspectie server/entiteit gebruikt en Hallo stappen toocomplete Hallo-agentregistratie mislukken.
* Hallo gebruiker heeft geen toegang tot tooperform Hallo registratie van Hallo-agent. Globale beheerders heeft standaard toegang. U kunt [rollen gebaseerd toegangsbeheer](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) toodelegate-tooother gebruikers.

**V: ik ben ophalen gewaarschuwd dat 'Health-servicegegevens is niet van toodate.' Hoe kan ik Hallo probleem oplossen?**

Azure AD Connect Health genereert Hallo waarschuwing als er geen alle Hallo gegevenspunten van Hallo-server in Hallo laatste twee uur ontvangt. Er kan ook meerdere oorzaken voor deze waarschuwing.

* Hallo-agent kan niet communiceren met de Hallo vereist eindpunten omdat verkeer door een firewall wordt geblokkeerd. Dit geldt met name op webtoepassingsproxyservers. Zorg ervoor dat u hebt toegestaan uitgaande communicatie vereist toohello eindpunten en poorten. Zie Hallo [gedeelte vereisten](active-directory-aadconnect-health-agent-install.md#requirements) voor meer informatie.
* Uitgaande communicatie is een SSL-inspectie ondergaan tooan door Hallo netwerklaag. Dit zorgt ervoor dat de Hallo-certificaat dat Hallo agent toobe vervangen door Hallo inspectie server/entiteit gebruikt en Hallo proces tooupload data toohello Azure AD Connect Health-service is mislukt.
* U kunt Hallo connectiviteitsopdracht ingebouwd in Hallo agent gebruiken. [Lees meer](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service).
* Hallo agents bieden ook ondersteuning voor uitgaande verbindingen via een niet-geverifieerde HTTP-Proxy. [Lees meer](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy).

## <a name="operations-questions"></a>Bewerkingen vragen
**V: moet ik tooenable controle op Hallo webtoepassingsproxyservers?**

Nee, controle hoeft niet ingeschakeld op Hallo webtoepassingsproxyservers toobe.

**V: hoe Azure AD Connect Health waarschuwingen opgelost ophalen?**

Waarschuwingen van Azure AD Connect Health ophalen van een voorwaarde geslaagd opgelost. Azure AD Connect Health-Agents detecteren en Hallo geslaagd voorwaarden toohello service periodiek rapporteren. Hallo onderdrukking is voor enkele waarschuwingen op basis van tijd. Met andere woorden, als hello dezelfde fout niet nageleefd binnen 72 uur van het genereren van waarschuwingen, Hallo waarschuwing automatisch opgelost.

**V: ik ben ophalen gewaarschuwd dat 'Test-verificatieaanvraag (synthetische transactie) is mislukt tooobtain een token.' Hoe kan ik Hallo probleem oplossen?**

Azure AD Connect Health voor AD FS wordt deze waarschuwing gegenereerd als Hallo Health-Agent is geïnstalleerd op een AD FS-server tooobtain een token als onderdeel van een synthetische transactie is gestart door Hallo Health-Agent is mislukt. Hallo Health-agent maakt gebruik van de lokale systeemcontext Hallo en probeert tooget een token voor een self relying party. Dit is een tooensure catch all-test die AD FS in een status is van de uitgifte van tokens.

Deze test mislukt meestal omdat Hallo Health-Agent kan geen tooresolve Hallo AD FS-farmnaam. Dit kan gebeuren als Hallo AD FS-servers zich achter een network load balancers en het Hallo-aanvraag wordt geïnitieerd vanaf een knooppunt, die zich achter Hallo load balancer (zoals reguliere client tegengestelde tooa die voor Hallo load balancer). Dit kan worden hersteld door Hallo 'hosts'-bestand onder 'C:\Windows\System32\drivers\etc' tooinclude Hallo IP-adres van Hallo AD FS-server of een loopback-IP-adres (127.0.0.1) bij te werken voor Hallo AD FS-farmnaam (bijvoorbeeld sts.contoso.com). Bestand van de host toe te voegen hello wordt kortsluiting Hallo netwerkaanroep, waardoor Hallo Health Agent tooget Hallo-token.

**V: Ik krijg een e-mailbericht dat aangeeft dat mijn machines zijn niet gevuld voor Hallo recente ransomeware aanvallen. Waarom krijg ik dit e-mailadres**

Azure AD Connect Health-service gescand alle Hallo machines monitoren tooensure Hallo vereist patches zijn geïnstalleerd. tenantbeheerders toohello is door Hallo e-mail verzonden als ten minste één machine geen Hallo essentiële patches. Hallo volgende logica gebruikte toomake is dit te bepalen.
1. Alle Hallo hotfixes zijn geïnstalleerd op Hallo machine vinden.
2. Controleer of ten minste één Hallo HotFixes van Hallo lijst gedefinieerd is geïnstalleerd.
3. Zo ja, is Hallo machine beveiligd. Als dat niet het geval is, Hallo machine bestaat het risico op aanvallen Hallo is.

U kunt gebruiken Hallo PowerShell script tooperform na deze controle handmatig. Het implementeert Hallo hierboven logica.

```
Function CheckForMS17-010 ()
{
    $hotfixes = "KB3205409", "KB3210720", "KB3210721", "KB3212646", "KB3213986", "KB4012212", "KB4012213", "KB4012214", "KB4012215", "KB4012216", "KB4012217", "KB4012218", "KB4012220", "KB4012598", "KB4012606", "KB4013198", "KB4013389", "KB4013429", "KB4015217", "KB4015438", "KB4015546", "KB4015547", "KB4015548", "KB4015549", "KB4015550", "KB4015551", "KB4015552", "KB4015553", "KB4015554", "KB4016635", "KB4019213", "KB4019214", "KB4019215", "KB4019216", "KB4019263", "KB4019264", "KB4019472", "KB4015221", "KB4019474", "KB4015219", "KB4019473"

    #checks hello computer it's run on if any of hello listed hotfixes are present
    $hotfix = Get-HotFix -ComputerName $env:computername | Where-Object {$hotfixes -contains $_.HotfixID} | Select-Object -property "HotFixID"

    #confirms whether hotfix is found or not
    if (Get-HotFix | Where-Object {$hotfixes -contains $_.HotfixID})
    {
        "Found HotFix: " + $hotfix.HotFixID
    } else {
        "Didn't Find HotFix"
    }
}

CheckForMS17-010

```



## <a name="related-links"></a>Verwante koppelingen
* [Azure AD Connect Health (Engelstalig)](active-directory-aadconnect-health.md)
* [De Azure AD Connect Health-agent installeren](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health-bewerkingen](active-directory-aadconnect-health-operations.md)
* [Azure AD Connect Health gebruiken met AD FS](active-directory-aadconnect-health-adfs.md)
* [Azure AD Connect Health for Sync gebruiken](active-directory-aadconnect-health-sync.md)
* [Azure AD Connect Health gebruiken met AD DS](active-directory-aadconnect-health-adds.md)
* [Versiegeschiedenis van Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
