---
title: aaaSettings en veelgestelde vragen voor dataroaming | Microsoft Docs
description: Biedt antwoorden toosome vragen IT-beheerders wellicht over de instellingen en synchroniseren van app-gegevens.
services: active-directory
keywords: Enterprise state roaming instellingen windows cloud, veelgestelde vragen op enterprise state roaming
documentationcenter: 
author: tanning
manager: swadhwa
editor: curtand
ms.assetid: c0824f5c-129b-4240-969f-921f6a64eae7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4d6d6619b3a5fbd1d274603808d89b73ed942cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="settings-and-data-roaming-faq"></a>Veelgestelde vragen over instellingen en gegevensroaming
In dit onderwerp worden enkele vragen beantwoord IT-beheerders over de instellingen en synchroniseren van app-gegevens hebben kunnen.

## <a name="what-data-roams"></a>Welke gegevens roamt?
**Windows-instellingen**: Hallo PC-instellingen die zijn ingebouwd in Hallo Windows-besturingssysteem. In het algemeen zijn instellingen die uw PC aanpassen en ze Hallo hoofdcategorieën volgende omvatten:

* *Thema*, waaronder functies zoals bureaubladinstellingen thema en de taakbalk.
* *Instellingen van Internet Explorer*, met inbegrip van onlangs geopende tabbladen en Favorieten.
* *Edge-browserinstellingen*, zoals Favorieten en leeslijst zijn vermeld.
* *Wachtwoorden*, zoals wachtwoorden voor Internet-, Wi-Fi-profielen en anderen.
* *Taalvoorkeuren*, waaronder instellingen voor toetsenbordindeling, systeemtaal, datum en tijd en meer.
* *Gebruiksgemak toegangsfuncties*, zoals thema met hoog contrast en Narrator, Vergrootglas.
* *Andere Windows-instellingen*, zoals instellingen voor de opdrachtprompt en de lijst met toepassingen.

**Toepassingsgegevens**: universele Windows-apps instellingen gegevens tooa zwervende kunnen schrijven en geen gegevens geschreven toothis map automatisch worden gesynchroniseerd. Is toohello afzonderlijke Apps developer toodesign app tootake voordeel van deze mogelijkheid. Voor meer informatie over hoe toodevelop een universele Windows-app die gebruikmaakt van roaming, zien Hallo [appdata opslag API](https://msdn.microsoft.com/library/windows/apps/mt299098.aspx) en Hallo [Windows 8 appdata roaming blog developer](http://blogs.msdn.com/b/windowsappdev/archive/2012/07/17/roaming-your-app-data.aspx).

## <a name="what-account-is-used-for-settings-sync"></a>Welk account wordt gebruikt voor synchronisatie van instellingen?
Synchronisatie van instellingen in Windows 8 en Windows 8.1, altijd consumer Microsoft-accounts gebruikt. Zakelijke gebruikers had Hallo mogelijkheid tooconnect een Microsoft-account tootheir Active Directory-domein account toogain toegang toosettings synchroniseren. In Windows 10 verbonden dit Microsoft-account met een account van de primaire en secundaire framework functionaliteit wordt vervangen.

Hallo primaire account is gedefinieerd als Hallo rekening toosign in tooWindows gebruikt. Dit is een Microsoft-account, een account met Azure Active Directory (Azure AD), een lokale Active Directory-account of een lokale account. Windows 10 gebruikers kunnen in toevoeging toohello primaire account, een of meer secundaire cloud accounts tootheir apparaat toevoegen. Een secundaire account wordt doorgaans een Microsoft-account, een Azure AD-account of enige andere account zoals Gmail of Facebook. Deze secundaire accounts toegang tooadditional-services, zoals het eenmalige aanmelding en Hallo Windows Store, maar ze zijn niet geschikt is voor het aansturen van de synchronisatie van instellingen.

In Windows 10 alleen Hallo hoofdaccount voor Hallo apparaat kan worden gebruikt voor synchronisatie van instellingen (Zie [hoe voer ik een upgrade van Microsoft-account instellingen synchroniseren in Windows 8 tooAzure AD instellingen synchronisatie in Windows 10?](active-directory-windows-enterprise-state-roaming-faqs.md#how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-to-azure-ad-settings-sync-in-windows-10)).

Gegevens gemengd is nooit tussen verschillende gebruikersaccounts Hallo op Hallo-apparaat. Er zijn twee regels voor synchronisatie van instellingen:

* Windows-instellingen wordt altijd kunnen worden gebruikt met primaire Hallo-account.
* App-gegevens worden gemarkeerd met Hallo account gebruikt tooacquire Hallo app. Alleen apps die zijn gemarkeerd met het hoofdaccount Hallo worden gesynchroniseerd. App-eigendom tagging wordt bepaald wanneer een app ' side-loaded via Hallo Windows Store of beheer van mobiele apparaten (MDM).

Als de eigenaar van een app kan niet worden geïdentificeerd, wordt deze met de primaire account Hallo kunnen roamen. Als een apparaat is geüpgraded van Windows 8 of Windows 8.1 tooWindows 10, worden alle Hallo apps label dat u hebt aangeschaft door Hallo Microsoft-account. Dit is omdat de meeste gebruikers apps via de Windows Store Hallo verkrijgen en er geen ondersteuning voor Windows Store voor Azure AD-accounts voorafgaande tooWindows 10 is. Als een app is geïnstalleerd via een offline licentie, worden Hallo app gemarkeerd met primaire account Hallo op Hallo-apparaat.

> [!NOTE]
> Windows 10-apparaten die eigendom van het enterprise zijn en verbonden tooAzure AD kunnen niet meer verbinding maken met hun Microsoft-accounts tooa-domeinaccount. Hallo mogelijkheid tooconnect een domeinaccount voor Microsoft-account tooa en synchroniseren van gegevens Hallo van alle gebruikers hebben toohello Microsoft-account (dat wil zeggen, Hallo Microsoft-account roaming via Hallo verbonden Microsoft-account en functionaliteit van Active Directory) wordt verwijderd uit Windows 10-apparaten die gekoppeld tooa zijn verbonden Active Directory of Azure AD-omgeving.
>
>

## <a name="how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-tooazure-ad-settings-sync-in-windows-10"></a>Hoe voer ik een upgrade van Microsoft-account instellingen synchroniseren in Windows 8 tooAzure AD instellingen synchronisatie in Windows 10?
Als u Active Directory-domein gekoppelde toohello met Windows 8 of Windows 8.1 met een Microsoft-account verbonden bent, kunt u instellingen worden gesynchroniseerd via uw Microsoft-account. Na de upgrade tooWindows 10, blijft u gebruikersinstellingen toosync via Microsoft-account als u een gebruiker lid van een domein en Hallo Active Directory-domein geen verbinding met Azure AD maken.

Als Hallo on-premises Active Directory-domein maakt verbinding met Azure AD probeert uw apparaat toosync instellingen met behulp van verbonden hello Azure AD-account. Als hello Azure AD-beheerder niet Enterprise State Roaming, uw verbonden kunnen Azure AD-account wordt stoppen van de synchronisatie van instellingen. Als u een Windows 10-gebruiker bent en u zich met een Azure AD-identiteit aanmeldt, gaat u windows-instellingen worden gesynchroniseerd als uw beheerder instellingen synchroniseren via Azure AD activeert.

Als u geen persoonlijke gegevens op uw zakelijke apparaat opgeslagen, moet u zich bewust zijn dat het Windows-besturingssysteem en toepassingsgegevens begint tooAzure AD synchroniseren. Dit heeft Hallo gevolgen te volgen:

* De instellingen van uw persoonlijke Microsoft-account wordt netjes naast Hallo-instellingen op uw werk of school Azure AD-accounts. Dit komt doordat het Hallo-Microsoft-account en Azure AD-instellingen synchroniseren nu afzonderlijke accounts gebruikt.
* Persoonlijke gegevens, zoals Wi-Fi-wachtwoorden, web-referenties en Favorieten in Internet Explorer die eerder zijn gesynchroniseerd via een gekoppelde Microsoft-account worden via Azure AD gesynchroniseerd.

## <a name="how-do-microsoft-account-and-azure-ad-enterprise-state-roaming-interoperability-work"></a>Hoe Microsoft-account en Azure AD Enterprise status Roaming interoperabiliteit werk?
In Hallo November 2015 of latere versies van Windows 10 wordt Enterprise State Roaming alleen ondersteund voor één account op een tijdstip. Als u zich aanmeldt tooWindows met behulp van een werk- of school Azure AD-account, worden alle gegevens worden gesynchroniseerd via Azure AD. Als u zich aanmeldt tooWindows met behulp van een persoonlijk Microsoft-account, worden alle gegevens worden gesynchroniseerd via Hallo Microsoft-account. Universele appdata wordt roamen gebruik alleen Hallo primaire aanmelden account op Hallo apparaat en wordt deze alleen als het Hallo-app-licentie is eigendom van het hoofdaccount Hallo roamen. Universele appdata voor Hallo-apps die eigendom zijn van een secundaire accounts worden niet gesynchroniseerd.

## <a name="do-settings-sync-for-azure-ad-accounts-from-multiple-tenants"></a>Synchroniseer instellingen voor Azure AD-accounts van meerdere tenants?
Wanneer meerdere Azure AD-accounts van andere Azure AD-tenants, zijn op Hallo hetzelfde apparaat, moet u de Register-toocommunicate Hallo-apparaat bijwerken met Azure Rights Management (Azure RMS) voor elke Azure AD-tenant.  

1. Hallo GUID voor elke Azure AD-tenant zoeken. Hallo klassieke Azure-portal te openen en selecteer een Azure AD-tenant. Hallo GUID voor Hallo tenant wordt Hallo-URL in de adresbalk Hallo van uw browser. Bijvoorbeeld: `https://manage.windowsazure.com/YourAccount.onmicrosoft.com#Workspaces/ActiveDirectoryExtension/Directory/Tenant GUID/directoryQuickStart`
2. Nadat u Hallo GUID hebt, moet u tooadd Hallo registersleutel **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\SettingSync\WinMSIPC\<tenant-ID GUID >**.
   Van Hallo **tenant-ID GUID** sleutel, maakt u een nieuwe waarde met meerdere tekenreeksen (REG-MULTI-SZ) te gebruiken met de naam **AllowedRMSServerUrls**. Geef Hallo distribution point-URL's van Hallo andere Azure-tenants die toegang tot een apparaat Hallo licentieverlening voor de gegevens.
3. U vindt Hallo licentieverlening distribution point-URL's door het uitvoeren van Hallo **Get-AadrmConfiguration** cmdlet. Als het Hallo-waarden voor Hallo **LicensingIntranetDistributionPointUrl** en **LicensingExtranetDistributionPointUrl** verschillend zijn, beide waarden opgeven. Als de waarden zijn Hallo hello dezelfde, slechts één keer Hallo-waarde opgeven.

## <a name="what-are-hello-roaming-settings-options-for-existing-windows-desktop-applications"></a>Wat zijn Hallo zwervende instellingsopties voor bestaande Windows-bureaubladtoepassingen?
Roaming werkt alleen voor universele Windows-apps. Er zijn twee opties beschikbaar voor het inschakelen van roaming op een bestaande Windows desktop-toepassing:

* Hallo [bureaublad Bridge](http://aka.ms/desktopbridge) helpt u uw bestaande Windows desktop-apps toohello universele Windows-Platform. Hier kunt vereist minimale code wijzigingen tootake profiteren van Azure AD app dataroaming. Hallo bureaublad Bridge biedt uw apps met de identiteit van een app, die nodig is tooenable app dataroaming voor bestaande desktop-apps.
* [Gebruiker ervaring Virtualization (UE-V)](https://technet.microsoft.com/library/dn458947.aspx) kunt u een sjabloon aangepaste instellingen voor bestaande Windows desktop-apps maken en zwervende voor Win32-apps inschakelen. Deze optie is niet vereist voor Hallo app developer toochange code van Hallo-app. UE-V is beperkt tooon lokale Active Directory zwervende voor klanten die Microsoft Desktop Optimization Pack Hallo hebt aangeschaft.

Beheerders kunnen UE-V tooroam Windows desktop app-gegevens configureren door het wijzigen van de instellingen van het Windows-besturingssysteem en universele app-gegevens via roaming [UE-V-groepsbeleid](https://technet.microsoft.com/itpro/mdop/uev-v2/configuring-ue-v-2x-with-group-policy-objects-both-uevv2), waaronder:

* Windows-instellingen voor Groepsbeleid kunnen worden gebruikt
* Groepsbeleid voor Windows-Apps niet synchroniseren
* Internet Explorer in de sectie toepassingen Hallo roaming

In toekomstige hello, Microsoft onderzoeken manieren toomake DIE UE-V is nauw geïntegreerd in Windows en UE-V tooroam instellingen via hello Azure AD cloud uitbreiden.

## <a name="can-i-store-synced-settings-and-data-on-premises"></a>Kan ik gesynchroniseerde instellingen en gegevens die on-premises opslaan?
Enterprise State Roaming, worden alle gesynchroniseerde gegevens opgeslagen in hello Azure-cloud. UE-V biedt een on-premises oplossing roaming.

## <a name="who-owns-hello-data-thats-being-roamed"></a>Wie is eigenaar van Hallo-gegevens die wordt wordt zwerven?
Hallo ondernemingen eigen Hallo gegevens via het Enterprise State Roaming zwerven. Gegevens worden opgeslagen in een Azure-datacenter. Alle gebruikersgegevens worden versleuteld onderweg zowel in rust in Hallo cloud met Azure RMS. Dit is een verbetering ten opzichte van tooMicrosoft instellingen op basis van een account sync, waarmee alleen bepaalde gevoelige gegevens, zoals de gebruikersreferenties worden versleuteld voordat u het Hallo-apparaat.

Microsoft is doorgevoerd toosafeguarding klantgegevens. Een enterprise-gebruiker instellingsgegevens worden automatisch versleuteld door Azure RMS voordat u het Windows 10-apparaat, zodat er geen andere gebruiker deze gegevens kan lezen. Als uw organisatie beschikt over een betaald abonnement voor Azure RMS, u kunt gebruiken van andere Azure RMS-functies, zoals bijhouden en intrekken van documenten, automatisch e-mailberichten met gevoelige informatie te beveiligen en uw eigen sleutels beheren (Hallo 'bring your own key'-oplossing ook ook wel BYOK). Zie voor meer informatie over deze functies en hoe Azure RMS werkt [wat is Azure Rights Management](https://technet.microsoft.com/jj585026.aspx).

## <a name="can-i-manage-sync-for-a-specific-app-or-setting"></a>Kan ik synchronisatie voor een specifieke app of -instellingen beheren?
In Windows 10, moet u er geen MDM of Groepsbeleid instelling toodisable roaming voor een afzonderlijke toepassing is. Tenantbeheerders kunnen uitschakelen appdata synchronisatie voor alle apps op een beheerd apparaat, maar er is geen mate van controle op een per-app of in-app-niveau.

## <a name="how-can-i-enable-or-disable-roaming"></a>Hoe kan ik in- of uitschakelen roaming?
In Hallo **instellingen** -app te gaan**Accounts** > **uw instellingen synchroniseren**. Op deze pagina kunt u zien welk account wordt gebruikt tooroam instellingen, en u kunt inschakelen of uitschakelen van afzonderlijke groepen van instellingen toobe zwerven.

## <a name="what-is-microsofts-recommendation-for-enabling-roaming-in-windows-10"></a>Wat is de aanbeveling van Microsoft voor het inschakelen van roaming in Windows 10?
Microsoft heeft een aantal andere instellingen oplossingen beschikbaar zijn, inclusief zwervende gebruikersprofielen, UE-V en Enterprise status zwervende roaming.  Microsoft is doorgevoerd toomaking een investering in Enterprise State Roaming in toekomstige versies van Windows. Als uw organisatie niet gereed of vertrouwd met bewegende gegevens toohello cloud is, vervolgens raden wij u aan UE-V te gebruiken als uw primaire zwervende technologie. Als uw organisatie vereist ondersteuning voor bestaande Windows-bureaubladtoepassingen roaming maar enthousiaste toomove toohello cloud, wordt u aangeraden Enterprise status zwervende en UE-V te gebruiken. Hoewel UE-V- en Enterprise State Roaming zeer soortgelijke technologieën zijn, zijn ze niet sluiten elkaar wederzijds uit. Ze aanvullen elkaar toohelp Zorg ervoor dat uw organisatie Hallo services die uw gebruikers moeten roaming geeft.  

Wanneer u Enterprise State Roaming en UE-V, Hallo volgens de regels van toepassing:

* Enterprise State Roaming is Hallo primaire zwervende-agent op Hallo-apparaat. UE-V wordt gebruikt toosupplement Hallo "Win32 hiaat."
* UE-V voor Windows-instellingen en moderne UWP-app-gegevens voor roaming moet worden uitgeschakeld wanneer Hallo UE-V-groep met van beleidsregels. Deze vallen al Enterprise State Roaming.

## <a name="how-does-enterprise-state-roaming-support-virtual-desktop-infrastructure-vdi"></a>Hoe Enterprise State Roaming ondersteunt virtuele desktopinfrastructuur (VDI)?
Enterprise State Roaming wordt ondersteund op SKU's voor Windows 10-client, maar niet op server SKU's. Als een client virtuele machine wordt gehost op een hypervisor-machine en u zich extern toohello virtuele machine aanmelden, wordt uw gegevens kunnen roamen. Als meerdere gebruikers dezelfde OS en gebruikers zich extern tooa server voor een volledige Bureaubladervaring aanmelden hello delen, roaming werkt mogelijk niet. Hallo laatstgenoemde op basis van sessies scenario wordt niet officieel ondersteund.

## <a name="what-happens-when-my-organization-purchases-azure-rms-after-using-roaming"></a>Wat gebeurt er als mijn organisatie Azure RMS koopt na gebruik van zwervende?
Als uw organisatie al wordt gebruikt in Windows 10-roaming Hello Azure RMS beperkt gebruik gratis abonnement, aanschaffen van een betaald abonnement voor Azure RMS geen invloed op Hallo functie Hallo zwervende en geen configuratiewijzigingen worden vereist door uw IT-beheerder.

## <a name="known-issues"></a>Bekende problemen
Raadpleeg de documentatie in Hallo Hallo [probleemoplossing](active-directory-windows-enterprise-state-roaming-troubleshooting.md) sectie voor een lijst met bekende problemen. 

## <a name="related-topics"></a>Verwante onderwerpen
* [Overzicht van zwervende Enterprise](active-directory-windows-enterprise-state-roaming-overview.md)
* [Enterprise-status roaming in Azure Active Directory inschakelen](active-directory-windows-enterprise-state-roaming-enable.md)
* [Groep beleid en de MDM-instellingen voor synchronisatie van instellingen](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Windows 10 zwervende naslaginformatie](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Problemen oplossen](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
