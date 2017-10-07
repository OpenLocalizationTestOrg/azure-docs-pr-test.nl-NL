---
title: aaaAzure opslag beveiligingshandleiding | Microsoft Docs
description: Details Hallo veel methoden van het beveiligen van Azure Storage, met inbegrip van maar niet beperkt tooRBAC, versleuteling van opslag-, Client-side-versleuteling, SMB 3.0 en Azure Disk Encryption.
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 6f931d94-ef5a-44c6-b1d9-8a3c9c327fb2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: d406ff0d6b45c6107d0276ad9e65c331078ce792
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-guide"></a>Azure Storage-beveiligingshandleiding
## <a name="overview"></a>Overzicht
Azure Storage biedt een uitgebreide reeks beveiligingsmogelijkheden die samen ontwikkelaars kunnen toobuild beveiligde toepassingen. Hallo storage-account zelf kan worden beveiligd met op rollen gebaseerde toegangsbeheer en Azure Active Directory. Gegevens onderweg tussen een toepassing en Azure kunnen worden beveiligd met behulp van [versleuteling van de Client-Side](storage-client-side-encryption.md), HTTPS- of SMB 3.0. Gegevens kunnen worden ingesteld op automatisch versleuteld wanneer geschreven toobe tooAzure opslag met behulp van [opslag Service versleuteling (SSE)](storage-service-encryption.md). Besturingssysteem en gegevensschijven die worden gebruikt door virtuele machines kunnen worden ingesteld op toobe versleuteld met [Azure Disk Encryption](../security/azure-security-disk-encryption.md). Gedelegeerde toegang toohello gegevensobjecten in Azure Storage kunnen worden verleend met behulp van [Shared Access Signatures](storage-dotnet-shared-access-signature-part-1.md).

In dit artikel biedt een overzicht van elk van deze beveiligingsfuncties die kunnen worden gebruikt met Azure Storage. Koppelingen vindt u tooarticles waarmee details van elke functie wordt uitgevoerd, zodat u eenvoudig kunt doen nader onderzoek op elk onderwerp.

Hier volgen Hallo onderwerpen toobe die in dit artikel:

* [Beveiliging van Management vlak](#management-plane-security) – voor het beveiligen van uw Storage-Account

  Hallo management vlak bestaat uit Hallo gebruikte resources toomanage uw storage-account. In deze sectie bespreken we hello Azure Resource Manager-implementatiemodel en hoe toouse op rollen gebaseerde toegangsbeheer (RBAC) toocontrol toegang krijgen tot tooyour storage-accounts. We zullen ook hebben over het beheren van uw toegangscodes voor opslag en hoe tooregenerate ze.
* [Beveiliging van gegevens vlak](#data-plane-security) – tooYour toegang beveiligen van gegevens

  In deze sectie zullen we toegang toe te staan toohello actuele gegevensobjecten in uw opslagaccount, zoals blobs, bestanden, wachtrijen en tabellen, met behulp van handtekeningen voor gedeelde toegang en toegangsbeleid opgeslagen. Zowel serviceniveau-SAS en account niveau SAS wordt uitgelegd. Ook bekijken we hoe toolimit toegang krijgen tot tooa specifiek IP-adres (of een bereik van IP-adressen), hoe toolimit Hallo protocol tooHTTPS gebruikt en hoe toorevoke een Shared Access Signature zonder te wachten op het tooexpire.
* [Versleuteling 'in transit'](#encryption-in-transit)

  Deze sectie wordt beschreven hoe u gegevens toosecure wanneer u het overbrengen van of naar Azure Storage. Bespreken we Hallo aanbevolen gebruik van HTTPS en Hallo versleuteling door SMB 3.0 gebruikt voor de Azure-bestandsshares. Er wordt ook rekening houden met kijken clientzijde versleuteling, waarmee u tooencrypt Hallo gegevens voordat deze worden overgedragen naar de opslag in een clienttoepassing en toodecrypt Hallo gegevens nadat deze zijn overgebracht buiten opslag.
* [Versleuteling 'at rest'](#encryption-at-rest)

  We zullen hebben over opslag Service versleuteling (SSE) en hoe u kunt inschakelen voor een opslagaccount, wat resulteert in uw blok-blobs, pagina-blobs en toevoeg-blobs worden automatisch versleuteld wanneer geschreven tooAzure opslag. Ook kijken we hoe u Azure Disk Encryption gebruiken en verkennen Hallo basic verschillen en aanvragen van schijfversleuteling versus SSE ten opzichte van de Client-Side-versleuteling. Kort kijken we FIPS-naleving voor VS Computers van de overheid.
* Met behulp van [Opslaganalyse](#storage-analytics) tooaudit toegang van Azure Storage

  Deze sectie wordt beschreven hoe toofind informatie in Hallo storage analytics registreert voor een aanvraag. We eens kijken echte opslaganalyse logboekgegevens en Zie hoe toodiscern of een aanvraag wordt gedaan met Hallo opslag sleutel, met een Shared Access signature, account of anoniem en of deze is geslaagd of mislukt.
* [Browser gebaseerde Clients met behulp van CORS inschakelen](#Cross-Origin-Resource-Sharing-CORS)

  Deze sectie wordt gesproken over het tooallow cross-origin-resource delen (CORS). Bespreken we domeintoegang en hoe toohandle met Hallo CORS mogelijkheden ingebouwd in Azure Storage.

## <a name="management-plane-security"></a>Beveiliging van de vlak Management
Hallo management vlak bestaat uit de bewerkingen die invloed hebben op Hallo storage-account zelf. Bijvoorbeeld, kunt u maken of een opslagaccount verwijderen, een lijst met storage-accounts in een abonnement ophalen, Hallo opslagaccountsleutels ophalen of Hallo sleutels van opslagaccount opnieuw genereren.

Als u een nieuw opslagaccount maakt, selecteert u een implementatiemodel van klassieke of Resource Manager. Hallo klassieke model van het maken van resources in Azure kunt alleen ofwel volledig, ofwel toegang toohello abonnement en op zijn beurt Hallo storage-account.

Deze handleiding is gericht op Hallo Resource Manager-model dat Hallo aanbevolen manier voor het maken van opslagaccounts. Met Resource Manager-opslagaccounts hello, in plaats van die toegang toohello hele abonnement, u kunt de toegang op een meer beperkte niveau toohello management vlak met behulp van op rollen gebaseerde toegangsbeheer (RBAC).

### <a name="how-toosecure-your-storage-account-with-role-based-access-control-rbac"></a>Hoe toosecure uw storage-account met op rollen gebaseerde toegangsbeheer (RBAC)
We wat RBAC is en hoe u deze kunt gebruiken. Elk Azure-abonnement heeft een Azure Active Directory. Toegang tot toomanage bronnen in hello Azure-abonnement met Resource Manager-implementatiemodel Hallo kunnen verleend aan gebruikers, groepen en toepassingen van die map. Dit is bedoeld tooas op rollen gebaseerde toegangsbeheer (RBAC). toomanage dit openen, kunt u Hallo [Azure-portal](https://portal.azure.com/), Hallo [Azure CLI-hulpprogramma's](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), of Hallo [Azure Storage Resource Provider REST-API's ](https://msdn.microsoft.com/library/azure/mt163683.aspx).

Met Resource Manager-model hello plaatst u Hallo storage-account in een resource group en beheer toegang toohello management vlak van het specifieke storage-account met Azure Active Directory. Bijvoorbeeld, kunt u specifieke gebruikers geven Hallo mogelijkheid tooaccess Hallo toegangscodes voor opslag, terwijl andere gebruikers informatie over Hallo storage-account weergeven kunnen, maar heeft geen toegang de opslagaccountsleutels Hallo tot.

#### <a name="granting-access"></a>Het verlenen van toegang
Toegang is verleend door toe te wijzen Hallo juiste RBAC-rol toousers, groepen en toepassingen op het juiste bereik Hallo. toogrant toegang toohello hele abonnement, dat u een rol op het abonnementsniveau Hallo toewijzen. Verleent machtigingen toohello resourcegroep zelf kunt u tooall van resources in een resourcegroep Hallo toegang verlenen. U kunt specifieke rollen ook toospecific resources, zoals de storage-accounts toewijzen.

Hier volgen de belangrijkste punten Hallo moet u tooknow over het gebruik van RBAC tooaccess Hallo beheerbewerkingen van een Azure Storage-account:

* Wanneer u toegang toewijst, worden in feite een rol toohello-account dat u toohave toegang wilt toewijzen. U kunt toegang toohello operations gebruikt toomanage te beheren die storage-account, maar niet toohello-gegevensobjecten in Hallo-account. Bijvoorbeeld, kunt u toestemming geven tooretrieve Hallo eigenschappen van Hallo storage-account (zoals redundantie), maar niet tooa container of -gegevens binnen een container in Blob Storage.
* Voor iemand toohave machtiging tooaccess Hallo gegevensobjecten in Hallo storage-account, krijgt deze machtiging tooread hello opslagaccountsleutels en die gebruiker kan vervolgens worden gebruikt die sleutels tooaccess Hallo blobs, wachtrijen, tabellen en bestanden.
* Rollen kunnen worden toegewezen tooa specifiek gebruikersaccount, een groep gebruikers of tooa specifieke toepassing.
* Elke functie heeft een lijst van acties en geen acties. Rol van de virtuele Machine Inzender Hallo heeft bijvoorbeeld een actie van het 'listKeys' waarmee Hallo storage account sleutels toobe lezen. Hallo Inzender heeft 'Geen acties' zoals Hallo-toegang voor gebruikers in Hallo Active Directory bijwerken.
* Rollen voor opslag bevatten (maar niet beperkt tot) Hallo volgende:

  * Eigenaar: ze kunnen alles beheren, inclusief toegang.
  * Inzender – ze alles kunnen doen Hallo eigenaar kunt behalve toegang toewijzen. Iemand met deze functie kunt weergeven en opnieuw genereren van sleutels van opslagaccount Hallo. Met de Hallo toegangscodes voor opslag, toegang te krijgen tot Hallo-gegevensobjecten.
  * Lezer – kunnen ze informatie over opslagaccount hello, met uitzondering van geheimen bekijken. Bijvoorbeeld als u een rol met de Lezersmachtigingen op Hallo storage account toosomeone toewijst, kunnen ze Hallo eigenschappen van het opslagaccount Hallo bekijken, maar mag niet aanbrengen van wijzigingen toohello eigenschappen of Hallo toegangscodes voor opslag weergeven.
  * Storage-Account Inzender – kunnen ze Hallo storage-account beheren: kan worden gelezen Hallo van abonnement resourcegroepen en resources, en maken en beheren van resourcegroepimplementaties abonnement. Ze kunnen ook toegang tot Hallo toegangscodes voor opslag, wat betekent dat op zijn beurt toegang te krijgen tot Hallo gegevens vlak.
  * Beheerder voor gebruikerstoegang – kunnen ze gebruiker toegang toohello storage-account beheren. Ze kunnen bijvoorbeeld lezer toegang tooa specifieke gebruiker verlenen.
  * Virtuele Machine Inzender – kunnen ze virtuele machines, maar niet Hallo storage account toowhich die ze zijn verbonden beheren. Deze rol kunt aanbieden Hallo toegangscodes voor opslag, wat betekent dat de gebruiker toowhom u deze rol toewijzen Hallo Hallo gegevens vlak kunt bijwerken.

    Om een gebruiker toocreate een virtuele machine hebben ze toobe kunnen toocreate Hallo bijbehorende VHD-bestand in een opslagaccount. toodo dat ze nodig hebben toobe kunnen tooretrieve Hallo storage account sleutel en geef dit toohello API Hallo VM maken. Daarom moeten ze deze machtiging hebben, zodat ze Hallo opslagaccountsleutels kunnen weergeven.
* Hallo mogelijkheid toodefine aangepaste rollen is een functie waarmee u toocompose een reeks acties in een lijst met beschikbare acties die kunnen worden uitgevoerd op Azure-resources.
* Hallo gebruiker heeft toobe in uw Azure Active Directory instellen voordat u een toothem rol kunt toewijzen.
* U kunt een rapport maken van die verleend/ingetrokken wat voor soort toegang naar/van wie en op welke bereik met PowerShell of Azure CLI Hallo.

#### <a name="resources"></a>Resources
* [Toegangsbeheer op basis van rollen in Azure Active Directory](../active-directory/role-based-access-control-configure.md)

  Dit artikel wordt uitgelegd Hallo toegangsbeheer op basis van een functie van Azure Active Directory en hoe het werkt.
* [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md)

  In dit artikel beschrijft alle Hallo ingebouwde rollen beschikbaar in RBAC.
* [Resource Manager-implementatie en klassieke implementatie begrijpen](../azure-resource-manager/resource-manager-deployment-model.md)

  Dit artikel wordt uitgelegd Hallo Resource Manager-implementatie en klassieke implementatiemodellen en Hallo voordelen van het gebruik van het Resource Manager en resource groepen Hallo uitgelegd. Hierin wordt uitgelegd hoe hello Azure Compute, Network en Storage Providers onder Hallo Resource Manager-model werken.
* [Toegangsbeheer op basis van rollen met Hallo REST-API beheren](../active-directory/role-based-access-control-manage-access-rest.md)

  Dit artikel laat zien hoe toouse Hallo REST-API toomanage RBAC.
* [Azure Storage Resource Provider REST API-verwijzing](https://msdn.microsoft.com/library/azure/mt163683.aspx)

  Dit is Hallo-verwijzing voor Hallo API's kunt u toomanage uw storage-account via een programma.
* [Developer's guide tooauth met Azure Resource Manager-API](http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/)

  Dit artikel laat zien hoe met behulp van tooauthenticate Hallo Resource Manager-API's.
* [Toegangsbeheer op basis van rollen voor Microsoft Azure vanuit Ignite](https://channel9.msdn.com/events/Ignite/2015/BRK2707)

  Dit is een koppeling tooa video op Channel 9 Hallo 2015 MS Ignite conferentie. In deze sessie, hebben ze over toegang tot beheer- en rapportagefuncties in Azure en bekijk de aanbevolen procedures om de toegang beveiligen tooAzure abonnementen met Azure Active Directory.

### <a name="managing-your-storage-account-keys"></a>Het beheren van uw toegangscodes voor opslag
Storage-account zijn gemaakt door Azure 512-bits-tekenreeksen die samen met de Hallo opslag accountnaam, sleutels kan worden gebruikt tooaccess Hallo gegevensobjecten die zijn opgeslagen in Hallo storage-account, zoals blobs, entiteiten in een tabel, Wachtrijberichten en bestanden op een bestandsshare in Azure. Beheren toohello storage account sleutels toegangsbeheer toegang tot toohello gegevens vlak voor dat opslagaccount.

Elk opslagaccount heeft twee sleutels bedoelde tooas 'Sleutel 1' en "Sleutel 2" in hello [Azure-portal](http://portal.azure.com/) en in Hallo PowerShell-cmdlets. Deze kunnen worden hersteld handmatig met behulp van een van de verschillende methoden, inclusief, maar niet beperkt toousing hello [Azure-portal](https://portal.azure.com/), PowerShell, hello Azure CLI of programmatisch met behulp van Storage-clientbibliotheek voor .NET Hallo of hello Azure Opslagservices REST-API.

Er zijn een aantal redenen tooregenerate uw toegangscodes voor opslag.

* U kunt ze opnieuw genereren uit veiligheidsoverwegingen regelmatig.
* Als iemand toohack beheerd in een toepassing en Hallo sleutel ophalen die is vastgelegd of opgeslagen in een configuratiebestand, zodat ze tooyour storage-account volledige toegang, zou u uw sleutels van opslagaccount opnieuw genereren.
* Een andere wordt voor sessiesleutels als uw team met behulp van een toepassing Opslagverkenner die Hallo opslagaccountsleutel behoudt en een van de teamleden Hallo verlaat. Hallo toepassing zou toowork, zodat ze toegang tooyour storage-account nadat ze verdwenen zijn voortgezet. Dit is daadwerkelijk Hallo primaire reden die ze account niveau Shared Access Signatures gemaakt: u kunt een SAS niveau gebruiken in plaats van de toegangssleutels Hallo opslaan in een configuratiebestand.

#### <a name="key-regeneration-plan"></a>Plan toegangssleutel wordt opnieuw gegenereerd
Wilt u toojust opnieuw genereren Hallo sleutel u zonder enige planning werkt niet. Als u dat doet, kan u alle toegang toothat storage-account, wat leiden onderbreking van de primaire tot kan afgekapt. Daarom zijn er twee sleutels. U moet één sleutel opnieuw genereren tegelijk.

Voordat u uw sleutels genereren, moet u er een lijst met alle toepassingen die afhankelijk zijn van Hallo storage-account, evenals andere services die u gebruikt in Azure. Bijvoorbeeld, als u Azure Media Services die afhankelijk van uw storage-account zijn gebruikt, moet u opnieuw synchroniseren Hallo toegangstoetsen met uw mediaservice nadat u Hallo-sleutel opnieuw genereren. Als u alle toepassingen, zoals een Opslagverkenner gebruikt, moet u tooprovide Hallo nieuwe sleutels toothose toepassingen ook. Houd er rekening mee dat als u virtuele machines waarvan VHD-bestanden worden opgeslagen in Hallo storage-account hebt, ze niet worden beïnvloed door Hallo sleutels van opslagaccount opnieuw genereren.

U kunt uw sleutels in hello Azure-portal opnieuw genereren. Zodra de sleutels opnieuw worden gegenereerd deze too10 kunnen nemen minuten toobe synchroniseren tussen de Storage-Services.

Wanneer u klaar bent, is het hier Hallo algemene proces met gedetailleerde informatie over hoe u uw sleutel moet wijzigen. In dit geval Hallo verondersteld wordt dat u momenteel Key 1 gebruikt en u toochange Alles gaat toouse sleutel 2 in plaats daarvan.

1. Opnieuw genereren sleutel 2 tooensure dat beveiligd is. U kunt dit doen in hello Azure-portal.
2. Wijzig in alle Hallo toepassingen waar Hallo-opslagsleutel is opgeslagen, Hallo opslag sleutel toouse sleutel 2 van nieuwe waarde. Testen en publiceren van de toepassing hello.
3. Nadat alle Hallo toepassingen en services actief zijn en kon worden voltooid, Key 1 genereren. Dit zorgt ervoor dat iedereen u niet expliciet hebben de nieuwe sleutel Hallo toowhom niet langer hoeft toegang tot het opslagaccount toohello.

Als u momenteel sleutel 2 gebruikt, kunt u dezelfde, maar de sleutelnamen omgekeerde Hallo verwerken Hallo gebruiken.

U kunt migreren via een paar dagen, het wijzigen van elke toepassing toouse Hallo nieuwe sleutel en publiceren. Nadat ze allemaal zijn voltooid, moet u vervolgens gaat u terug en Hallo oude sleutel opnieuw genereren zodat deze niet meer werkt.

Een andere optie is tooput hello opslagaccountsleutel in een [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) als een geheim en de sleutel van uw toepassingen ophalen Hallo van daaruit hebben. Wanneer u Hallo-sleutel opnieuw genereren en hello Azure Key Vault bijwerkt, moet Hallo toepassingen niet toobe omdat ze Hallo nieuwe sleutel opgehaald uit Azure Key Vault Hallo automatisch geïmplementeerd. Houd er rekening mee dat er Hallo toepassing hello sleutel lezen. elke keer dat u nodig hebt, of u kunt deze in de cache in het geheugen en als dit mislukt wanneer u deze ophalen Hallo sleutel opnieuw hello Azure Sleutelkluis.

Een ander niveau van beveiliging voor de opslagsleutels met Azure Key Vault ook worden toegevoegd. Als u deze methode gebruikt, hebt u nooit Hallo opslag sleutel vastgelegd in een configuratiebestand, waardoor deze doorverwezen iemand toohello sleutels zonder specifieke machtiging wordt de toegang wordt verwijderd.

Een ander voordeel van het gebruik van Azure Sleutelkluis is dat tooyour toegangstoetsen met Azure Active Directory kunt u ook bepalen. Dit betekent dat u kunt toegang toohello handvol toepassingen die moeten tooretrieve Hallo sleutels van Azure Sleutelkluis, en andere toepassingen worden niet kunnen tooaccess Hallo sleutels zonder deze machtiging verlenen om precies weet verlenen.

Opmerking: het verdient aanbeveling toouse alleen een Hallo-codes in al uw toepassingen op Hallo dezelfde tijd. Als u sleutel 1 op bepaalde plaatsen en sleutel 2 in andere gevallen gebruikt, wordt u niet kunt toorotate worden uw sleutels zonder een toepassing toegang verliezen.

#### <a name="resources"></a>Resources
* [Over Azure Storage-Accounts](storage-create-storage-account.md#regenerate-storage-access-keys)

  Dit artikel biedt een overzicht van de storage-accounts en weergeven, kopiëren en opnieuw genereren van de toegangssleutels voor opslag.
* [Azure Storage Resource Provider REST API-verwijzing](https://msdn.microsoft.com/library/mt163683.aspx)

  Dit artikel bevat koppelingen toospecific artikelen over ophalen Hallo-toegangscodes voor opslag en opnieuw genereren Hallo-toegangscodes voor opslag voor een Azure-Account met behulp van Hallo REST-API. Opmerking: Dit is voor Resource Manager-opslagaccounts.
* [Bewerkingen voor opslagaccounts](https://msdn.microsoft.com/library/ee460790.aspx)

  Dit artikel in Hallo Storage Service Manager REST API Reference bevat koppelingen toospecific artikelen op te halen en opnieuw genereren van Hallo toegangscodes voor opslag met behulp van Hallo REST-API. Opmerking: Dit is voor Hallo klassieke opslagaccounts.
* [Zeg goodbye tookey management – toegang tooAzure Storage-gegevens met behulp van Azure AD beheren](http://www.dushyantgill.com/blog/2015/04/26/say-goodbye-to-key-management-manage-access-to-azure-storage-data-using-azure-ad/)

  Dit artikel laat zien hoe toouse Active Directory toocontrol toegangstoetsen tooyour Azure Storage in Azure Sleutelkluis. Ook ziet u hoe een Azure Automation toouse tooregenerate Hallo sleutels op uurbasis taak.

## <a name="data-plane-security"></a>Beveiliging van gegevens vlak
Beveiliging van gegevens vlak verwijst toohello methoden gebruikte toosecure Hallo-gegevensobjecten in Azure Storage-Hallo blobs, wachtrijen, tabellen en bestanden opgeslagen. We methoden tooencrypt Hallo gegevens en beveiliging tijdens de overdracht van gegevens Hallo hebt gezien, maar hoe moet u doen over het toestaan van toegang toohello objecten?

Er zijn in principe twee methoden voor het beheren toegang toohello gegevensobjecten zelf. Hallo is eerst door beheren toegang toohello toegangscodes voor opslag en Hallo tweede gebruikt Shared Access Signatures toogrant toegang toospecific-gegevensobjecten voor een specifieke hoeveelheid tijd.

Een uitzondering toonote is kunt u openbare toegang tooyour blobs door in te stellen Hallo toegangsniveau voor Hallo-container met Hallo blobs dienovereenkomstig toestaan. Als u toegang voor een tooBlob container of de Container hebt ingesteld, is het toegestaan openbare leestoegang voor Hallo blobs in de container. Dit betekent dat iedereen met een URL die verwijst tooa blob in de container kunt openen in een browser zonder met behulp van een Shared Access Signature of het Hallo-opslagaccountsleutels hebben.

### <a name="storage-account-keys"></a>Opslagaccountsleutels
Toegangscodes voor opslag zijn 512-bits-tekenreeksen die door Azure die samen met de naam opslagaccount hello, gebruikte tooaccess Hallo gegevensobjecten die zijn opgeslagen in Hallo storage-account kan worden gemaakt.

U kunt bijvoorbeeld BLOB's lezen, schrijven tooqueues, tabellen maken en wijzigen. Veel van deze acties kunnen worden uitgevoerd via hello Azure portal of met behulp van een van de vele Opslagverkenner toepassingen. U kunt ook schrijven code toouse Hallo REST-API of een van de Hallo Opslagclientbibliotheken tooperform deze bewerkingen.

Zoals beschreven in de sectie Hallo op Hallo [Management vlak beveiliging](#management-plane-security), toegangssleutels toohello opslag voor een opslagaccount van klassiek kan worden verleend door middel van een volledige toegang toohello Azure-abonnement. Toohello opslag toegangstoetsen voor een opslagaccount met hello Azure Resource Manager-model kunnen worden beheerd via op rollen gebaseerde toegangsbeheer (RBAC).

### <a name="how-toodelegate-access-tooobjects-in-your-account-using-shared-access-signatures-and-stored-access-policies"></a>Hoe toodelegate toegang krijgen tot tooobjects in uw account met handtekeningen voor gedeelde toegang en toegangsbeleid opgeslagen
Een Shared Access Signature is een tekenreeks met een beveiligingstoken dat kan worden gekoppeld tooa URI waarmee u toodelegate access toostorage-objecten en beperkingen zoals Hallo machtigingen en Hallo datum/tijd-bereik van toegang opgeven.

U kunt verlenen toegang tooblobs, containers, Wachtrijberichten, bestanden en tabellen. Met tabellen, kunt u daadwerkelijk verlenen machtiging tooaccess een bereik van entiteiten in de tabel Hallo Hallo partitie en rij sleutelbereiken toowhich gewenste Hallo toohave gebruikerstoegang geven. Bijvoorbeeld, als u gegevens opgeslagen met een partitiesleutel van geografische staat hebt, kan geeft u iemand toegang tot toojust Hallo gegevens voor Californië.

In een ander voorbeeld kan u een webtoepassing geven een SAS-token dat deze toowrite vermeldingen tooa wachtrij kan en geef een werknemer rol toepassing een SAS-token tooget-berichten van Hallo wachtrij en deze te verwerken. Of u een klant een SAS-token ze tooupload afbeeldingen tooa container in Blob Storage gebruiken en een tooread web toepassing toestemming geven deze afbeeldingen kan geven. In beide gevallen is er een scheiding van zorgen – elke toepassing kunt die toegang moet krijgen alleen Hallo die ze nodig hebben in volgorde tooperform hun taak. Dit is mogelijk door het Hallo-gebruik van handtekeningen voor gedeelde toegang.

#### <a name="why-you-want-toouse-shared-access-signatures"></a>Waarom het gewenste toouse Shared Access Signatures
Waarom zou u toouse een SAS in plaats van alleen de opslagaccountsleutel veel eenvoudiger is dat? Geven van de sleutel van uw opslagaccount is vergelijkbaar met het Hallo-sleutels van uw opslag Koninkrijk delen. Deze verleent volledige toegang. Iemand anders uw sleutels te gebruiken en hun gehele muziek bibliotheek tooyour storage-account uploaden. Ze kunnen ook uw bestanden vervangen door versies geïnfecteerde of uw gegevens worden gestolen. Vrijgeven van onbeperkte toegang tooyour storage-account, is er iets niet licht moet worden gehouden.

Met handtekeningen voor gedeelde toegang kunt u een client NET Hallo machtigingen vereist voor een beperkte hoeveelheid tijd geven. Bijvoorbeeld als iemand anders een blob tooyour account uploaden wordt, verleent u hen schrijftoegang voor net voldoende tijd tooupload Hallo-blob (afhankelijk van de grootte van de Hallo Hallo BLOB, natuurlijk). En als u van gedachten verandert, kunt u die toegang intrekken.

Daarnaast kunt u opgeven dat aanvragen met een SAS beperkte tooa bepaalde IP-adres of IP-bereik externe tooAzure zijn. U kunt ook vereisen dat aanvragen worden gedaan met een bepaald protocol (HTTPS of HTTP/HTTPS). Dit betekent dat als u wilt dat alleen tooallow HTTPS-verkeer, u alleen Hallo vereist protocol tooHTTPS instellen kunt en HTTP-verkeer wordt geblokkeerd.

#### <a name="definition-of-a-shared-access-signature"></a>Definitie van een Shared Access Signature
Een Shared Access Signature is dat een set van queryparameters toegevoegd toohello URL Hallo bron wijzen

die biedt informatie over Hallo toegang toegestaan en Hallo tijdsduur voor welke Hallo toegang is toegestaan. Hier volgt een voorbeeld; Deze URI bevat leestoegang tooa blob gedurende vijf minuten. Opmerking SAS queryparameters moet gecodeerde URL, zoals % 3A voor dubbele punt (:) of 20% van een spatie.

```
http://mystorage.blob.core.windows.net/mycontainer/myblob.txt (URL toohello blob)
?sv=2015-04-05 (storage service version)
&st=2015-12-10T22%3A18%3A26Z (start time, in UTC time and URL encoded)
&se=2015-12-10T22%3A23%3A26Z (end time, in UTC time and URL encoded)
&sr=b (resource is a blob)
&sp=r (read access)
&sip=168.1.5.60-168.1.5.70 (requests can only come from this range of IP addresses)
&spr=https (only allow HTTPS requests)
&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D (signature used for hello authentication of hello SAS)
```

#### <a name="how-hello-shared-access-signature-is-authenticated-by-hello-azure-storage-service"></a>Hoe Hallo Shared Access Signature wordt geverifieerd door Azure-opslagservice Hallo
Wanneer opslagservice Hallo Hallo aanvraag ontvangt, wordt het Hallo-invoer voor de query-parameters zijn vereist en een handtekening gemaakt met behulp van dezelfde methode Hallo zoals Hallo aanroepende programma. Hallo twee handtekeningen worden vervolgens vergeleken. Als ze akkoord gaat, wordt Hallo kunt storage-service controleren Hallo opslag service versie toomake of dat deze geldig is, Controleer of hello huidige datum en tijd vallen binnen het opgegeven venster hello, zorg ervoor dat Hallo toegang aangevraagd overeenkomt met toohello aanvraag is ingediend, enzovoort.

Bijvoorbeeld, met onze URL mislukken als het Hallo-URL is tooa-bestand in plaats van een blob verwijst deze aanvraag omdat hiermee die Hallo die Shared Access Signature voor een blob is. Als Hallo REST-opdracht wordt aangeroepen tooupdate een blob is, zou deze mislukken omdat hello Shared Access Signature geeft aan dat alleen lezen-toegang is toegestaan.

#### <a name="types-of-shared-access-signatures"></a>Typen handtekeningen voor gedeelde toegang
* Een SAS serviceniveau mag gebruikte tooaccess specifieke bronnen in een opslagaccount. Enkele voorbeelden van deze zijn bij het ophalen van een lijst met blobs in een container, downloaden van een blob, bijwerken van een entiteit in een tabel, toe te voegen berichten tooa wachtrij of een bestandsshare tooa-bestand uploaden.
* Een SAS niveau kan gebruikte tooaccess van alles zijn die een SAS serviceniveau voor kan worden gebruikt. Bovendien kan deze opties tooresources die niet zijn toegestaan met een SAS serviceniveau zoals Hallo mogelijkheid toocreate containers, tabellen, wachtrijen en bestandsshares geven. U kunt ook toegang tot toomultiple services in één keer opgeven. Bijvoorbeeld, u mogelijk geven iemand toegang tot tooboth blobs en bestanden in uw opslagaccount.

#### <a name="creating-an-sas-uri"></a>Maken van een SAS-URI
1. U kunt een ad-hoc URI maken op aanvraag alle Hallo queryparameters telkens definiëren.

   Dit echt flexibel is, maar als er een logische set parameters die vergelijkbaar telkens zijn, een beter idee krijgen met behulp van een toegangsbeleid opgeslagen is.
2. U kunt een toegangsbeleid opgeslagen voor een volledige container, een bestandsshare, een tabel of een wachtrij maken. Vervolgens kunt u dit als Hallo basis voor Hallo SAS-URI's die u maakt. Machtigingen op basis van opgeslagen-beleidsregels kunnen gemakkelijk worden ingetrokken. U kunt hebben omhoog too5 beleid gedefinieerd voor elke container, queue, table of bestandsshare.

   Bijvoorbeeld, als u toohave ging veel mensen lezen Hallo blobs in een specifieke container, kunt u een toegangsbeleid opgeslagen met de tekst 'leestoegang geven' en andere instellingen die worden Hallo gelijk elke keer. Vervolgens kunt u een SAS-URI met behulp van de instellingen Hallo Hallo toegangsbeleid opgeslagen en Hallo verlopen datum/tijd te geven. Hallo voordeel hiervan is dat er geen toospecify alle Hallo queryparameters elke keer.

#### <a name="revocation"></a>Intrekken
Stel dat uw SAS is aangetast, of het gewenste toochange deze vanwege het beveiligingsbeleid van het bedrijf of naleving van regelgeving vereisten. Hoe u de toegang tooa resource met die SAS intrekken? Dit is afhankelijk van hoe u Hallo SAS-URI hebt gemaakt.

Als u van ad-hoc URI gebruikmaakt, hebt u drie opties. U kunt de SAS-tokens uitgeven met korte verloopbeleid en te wachten op Hallo SAS tooexpire. U kunt wijzigen of verwijderen van Hallo-resource (ervan uitgaande dat Hallo-token is één object binnen het bereik tooa). U kunt toegangscodes voor opslag Hallo wijzigen. Deze laatste optie kan een grote invloed, afhankelijk van hoeveel services met behulp van dit opslagaccount en is waarschijnlijk niet iets gewenste toodo zonder enige planning.

Als u van een SAS afgeleid van een toegangsbeleid opgeslagen gebruikmaakt, kunt u toegang verwijderen door het Hallo opgeslagen toegangsbeleid intrekken – u kunt deze alleen wijzigen zodat deze al is verlopen, of kunt u deze helemaal verwijderen. Dit wordt direct van kracht en elke SAS gemaakt met behulp van dat beleid opgeslagen toegang wordt ongeldig gemaakt. Bijwerken of verwijderen van Hallo personen met toegang tot die specifieke container, een bestandsshare, een tabel of een wachtrij via SAS mogelijk van invloed op toegangsbeleid opgeslagen, maar als hello clients worden geschreven, zodat ze een nieuw SAS vragen wanneer Hallo oude ongeldig dit goed werkt.

Omdat met behulp van een SAS afgeleid van een toegangsbeleid opgeslagen, kunt u gebruiken Hallo mogelijkheid toorevoke SAS onmiddellijk, is het Hallo aanbevolen best practice tooalways toegangsbeleid opgeslagen indien mogelijk.

#### <a name="resources"></a>Resources
Raadpleeg voor meer gedetailleerde informatie over het gebruik van handtekeningen voor gedeelde toegang en opgeslagen toegangsbeleid, met voorbeelden voltooid toohello volgende artikelen:

* Dit zijn Hallo verwijzing artikelen.

  * [Service-SAS](https://msdn.microsoft.com/library/dn140256.aspx)

    Dit artikel vindt voorbeelden van het gebruik van een SAS serviceniveau met blobs, Wachtrijberichten, tabel bereiken en bestanden.
  * [Maken van een service-SAS](https://msdn.microsoft.com/library/dn140255.aspx)
  * [Een SAS-account maken](https://msdn.microsoft.com/library/mt584140.aspx)
* Deze zijn zelfstudies voor het gebruik van Hallo .NET client bibliotheek toocreate handtekeningen voor gedeelde toegang en toegangsbeleid opgeslagen.

  * [Met behulp van Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md)
  * [Shared Access Signatures, deel 2: Maken en gebruiken van een SAS met Hallo Blob-Service](storage-dotnet-shared-access-signature-part-2.md)

    Dit artikel bevat een uitleg van Hallo SAS-model, voorbeelden van handtekeningen voor gedeelde toegang en aanbevelingen voor de beste Hallo gebruik van SAS. Ook besproken is Hallo intrekking van Hallo zijn gemachtigd om.
* Toegang beperken op basis van IP-adres (IP-ACL's)

  * [Wat is er een eindpunt toegangsbeheerlijst (ACL's)?](../virtual-network/virtual-networks-acl.md)
  * [Maken van een Service-SAS](https://msdn.microsoft.com/library/azure/dn140255.aspx)

    Dit is Hallo verwijzingsartikel voor serviceniveau SAS; het bevat een voorbeeld van een IP-ACLing.
  * [Een SAS-Account maken](https://msdn.microsoft.com/library/azure/mt584140.aspx)

    Dit is Hallo verwijzingsartikel voor account-niveau SAS; het bevat een voorbeeld van een IP-ACLing.
* Authentication

  * [Verificatie voor hello Azure Storage-Services](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* Shared Access Signatures aan de slag zelfstudie

  * [Aan de slag zelfstudie SAS](https://github.com/Azure-Samples/storage-dotnet-sas-getting-started)

## <a name="encryption-in-transit"></a>Codering in Transit
### <a name="transport-level-encryption--using-https"></a>Transportniveau codering – via HTTPS
Een andere stap moet u rekening houden met tooensure Hallo beveiliging van uw Azure Storage-gegevens is tooencrypt Hallo gegevens tussen Hallo-client en Azure Storage. Hallo eerste aanbeveling is tooalways gebruiken Hallo [HTTPS](https://en.wikipedia.org/wiki/HTTPS) protocol, waardoor beveiligde communicatie via openbaar Internet Hallo.

een beveiligd communicatiekanaal toohave, moet u altijd gebruiken HTTPS tijdens het aanroepen van Hallo REST-API's of toegang tot in de opslag objecten. Bovendien **Shared Access Signatures**, wat kan gebruikte toodelegate zijn tooAzure opslagobjecten krijgen, bevatten een optie toospecify die alleen Hallo HTTPS-protocol kan worden gebruikt bij het gebruik van handtekeningen voor gedeelde toegang, ervoor te zorgen dat iedereen koppelingen met SAS-tokens verstuurt het juiste protocol Hallo gebruikt.

Kunt u gebruik van HTTPS Hallo afdwingen bij het aanroepen van Hallo REST-API's tooaccess objecten in opslagaccounts doordat [vereiste gegevensoverdracht Secure](storage-require-secure-transfer.md) voor Hallo storage-account. Verbindingen met HTTP geweigerd als deze optie is ingeschakeld.

### <a name="using-encryption-during-transit-with-azure-file-shares"></a>Met behulp van versleuteling tijdens de overdracht met Azure-bestandsshares
Azure File storage ondersteunt HTTPS wanneer Hallo REST-API gebruiken, maar is veelgebruikte als een SMB-bestandsshare tooa VM gekoppelde. SMB 2.1 biedt geen ondersteuning voor versleuteling, zodat de verbindingen zijn alleen toegestaan binnen Hallo dezelfde regio in Azure. Echter, SMB 3.0 ondersteunt versleuteling, en is beschikbaar in Windows Server 2012 R2, Windows 8, Windows 8.1 en Windows 10, zodat de regio-overschrijdende toegang en zelfs toegang op Hallo bureaublad.

Houd er rekening mee dat hoewel Azure-bestandsshares kunnen worden gebruikt voor Unix, Hallo Linux SMB-client nog geen versleuteling, ondersteunt zodat toegang is alleen toegestaan binnen een Azure-regio. Ondersteuning voor Linux codering is op Hallo roadmap van Linux-ontwikkelaars die verantwoordelijk is voor SMB-functionaliteit. Wanneer ze versleuteling toevoegen, hebt u dezelfde mogelijkheid voor het openen van een Azure-bestandsshare op Linux, zoals u zou voor Windows doen hello.

U kunt Hallo gebruik van versleuteling Hello Azure Files service afdwingen door in te schakelen [vereiste gegevensoverdracht Secure](storage-require-secure-transfer.md) voor Hallo storage-account. Als met behulp van REST-API's hello, HTTPs is vereist. Voor SMB, wordt SMB alleen verbindingen die ondersteuning bieden voor versleuteling verbinding gemaakt.

#### <a name="resources"></a>Resources
* [Hoe toouse Azure File storage met Linux](storage-how-to-use-files-linux.md)

  Dit artikel laat zien hoe toomount een Azure-bestand delen op een Linux-systeem en uploaden/downloaden van bestanden.
* [Aan de slag met Azure File Storage in Windows](storage-dotnet-how-to-use-files.md)

  In dit artikel biedt een overzicht van Azure-bestandsshares en hoe toomount en deze gebruiken met behulp van PowerShell en .NET.
* [Inside Azure File Storage (Een kijkje achter de schermen van Azure File Storage)](https://azure.microsoft.com/blog/inside-azure-file-storage/)

  Dit artikel kondigt Hallo algemene beschikbaarheid van Azure File storage en biedt technische gegevens over Hallo SMB 3.0-versleuteling.

### <a name="using-client-side-encryption-toosecure-data-that-you-send-toostorage"></a>Met behulp van de Client-side toosecure Versleutelingsgegevens toostorage te sturen
Een andere optie waarmee u ervoor te zorgen dat uw gegevens beveiligd is terwijl ze worden overgebracht tussen een clienttoepassing en -opslag is versleuteling aan de clientzijde. Hallo-gegevens worden versleuteld voordat ze worden overgedragen naar de Azure-opslag. Bij het Hallo-gegevens ophalen uit Azure Storage, worden de Hallo gegevens worden ontsleuteld nadat het is ontvangen op Hallo-client. Hoewel Hallo gecodeerde gegevens gaat over de kabel hello wordt aangeraden dat u ook gebruik van HTTPS, omdat deze gegevens integriteitscontroles ingebouwd die verminderen die invloed hebben op Hallo integriteit van gegevens van de Hallo netwerkfouten.

Client-side '-versleuteling is ook een methode voor het versleutelen van uw gegevens in rust, zoals Hallo gegevens worden opgeslagen in de versleutelde vorm. Bespreken we dit nader beschreven in de sectie Hallo op [versleuteling in rust](#encryption-at-rest).

## <a name="encryption-at-rest"></a>Codering in rust
Er zijn drie Azure-functies die at-rest versleuteling wilt gebruiken een. Azure Disk Encryption is gebruikte tooencrypt hello OS- en gegevensschijven in IaaS virtuele Machines. Hallo andere twee – clientzijde versleuteling en SSE – zijn beide gebruikte tooencrypt gegevens in Azure Storage. Laten we kijken naar elk van deze, en vervolgens Doe een vergelijking en Zie wanneer elk ervan kan worden gebruikt.

Terwijl het onderweg (dit wordt ook opgeslagen in de versleutelde vorm in de opslag) kunt u gegevens van clientzijde versleuteling tooencrypt hello, kunt u toosimply gebruik HTTPS liever tijdens de overdracht van Hallo en hebben enkele manier voor Hallo gegevens toobe automatisch versleuteld wanneer het opgeslagen. Er zijn twee manieren toodo deze--Azure Disk Encryption en SSE. Een wordt gebruikt toodirectly Hallo-gegevens op het besturingssysteem en gegevensschijven die wordt gebruikt door virtuele machines worden versleuteld en andere Hallo gebruikte tooencrypt gegevens tooAzure Blob-opslag geschreven.

### <a name="storage-service-encryption-sse"></a>Versleuteling van opslag-Service (SSE)
SSE kunt u toorequest dat opslagservice Hallo Hallo gegevens automatisch coderen bij het schrijven van tooAzure opslag. Wanneer u Hallo gegevens uit Azure Storage leest, wordt deze door Hallo storage-service worden ontsleuteld voordat het wordt geretourneerd. Hiermee kunt u toosecure uw gegevens zonder toomodify code of code tooany toepassingen toe te voegen.

Dit is een instelling die van toepassing toohello hele storage-account is. U kunt inschakelen en uitschakelen van deze functie door Hallo-waarde van Hallo-instelling te wijzigen. toodo dit hello Azure-portal, PowerShell hello Azure CLI gebruiken, REST-API van Storage Resource Provider Hallo of Hallo Storage-clientbibliotheek voor .NET. SSE is standaard uitgeschakeld.

Op dit moment worden Hallo sleutels gebruikt voor versleuteling Hallo beheerd door Microsoft. We oorspronkelijk Hallo sleutels genereren en veilige opslag Hallo Hallo-sleutels, evenals Hallo reguliere rotatie van beheren zoals gedefinieerd door intern beleid van Microsoft. In toekomstige hello, wordt u Hallo mogelijkheid toomanage uw eigen versleutelingssleutels ophalen en bieden een migratiepad van door Microsoft beheerde sleutels toocustomer beheerde sleutels.

Deze functie is beschikbaar voor Standard en Premium-opslag accounts die zijn gemaakt met Hallo Resource Manager-implementatiemodel. SSE geldt alleen tooblock blobs, pagina-blobs en toevoeg-blobs. Hallo wordt andere typen gegevens, waaronder tabellen, wachtrijen en -bestanden niet versleuteld.

Gegevens worden alleen versleuteld als SSE is ingeschakeld en Hallo gegevens tooBlob opslag worden geschreven. In- of uitschakelen van SSE heeft geen gevolgen voor bestaande gegevens. Met andere woorden, wanneer u deze versleuteling inschakelt, wordt deze niet teruggaan en gegevens versleutelen die al bestaat; ook worden gedecodeerd Hallo-gegevens die al voorkomen wanneer u SSE uitschakelt.

Als u deze functie met een opslagaccount van klassiek toouse wilt, kunt u een nieuw opslagaccount voor de Resource Manager maken en gebruiken van AzCopy toocopy Hallo gegevens toohello nieuwe account.

### <a name="client-side-encryption"></a>Client-side-versleuteling
We bij het bespreken van Hallo versleuteling van gegevens die onderweg Hallo versleuteling aan clientzijde worden vermeld. Deze functie kunt u tooprogrammatically versleutelen van uw gegevens in een clienttoepassing voordat het wordt verzonden via Hallo kabel toobe tooAzure opslag geschreven en tooprogrammatically ontsleutelen van uw gegevens bij het ophalen van het uit Azure Storage.

Dit biedt versleuteling onderweg, maar biedt ook de functie Hallo van versleuteling in rust. Houd er rekening mee dat hoewel Hallo gegevens onderweg zijn versleuteld, nog steeds aangeraden HTTPS tootake profiteren van Hallo ingebouwde gegevens integriteitscontroles die netwerkfouten die invloed hebben op Hallo integriteit van gegevens van de Hallo verminderen.

Een voorbeeld van waar u dit kunt gebruiken is als u een webtoepassing die blobs opgeslagen en opgehaald van BLOB's hebt en u Hallo-toepassing en gegevens toobe zo veilig mogelijk wilt. In dat geval gebruikt u versleuteling aan clientzijde. Hallo-verkeer tussen Hallo-client en hello Azure Blob-Service bevat Hallo versleuteld resource en niemand kan interpreteren Hallo gegevens tijdens de overdracht en het opnieuw samenstellen in uw persoonlijke blobs.

Versleuteling aan clientzijde is ingebouwd in Hallo Java en Hallo .NET opslagclientbibliotheken, dat op zijn beurt hello Azure Key Vault-API's, zodat u heel eenvoudig u tooimplement gebruiken. Hallo-proces voor het versleutelen en ontsleutelen van gegevens Hallo Hallo envelop techniek gebruikt en slaat metagegevens die door elke opslagobject Hallo-versleuteling gebruikt. Bijvoorbeeld: voor blobs, het opgeslagen in de metagegevens van de blob hello, terwijl voor wachtrijen, wordt toegevoegd het tooeach wachtrijbericht.

U kunt voor de versleuteling Hallo zelf, genereren en beheren van uw eigen versleutelingssleutels. U kunt ook sleutels die zijn gegenereerd door hello Azure Storage-clientbibliotheek gebruiken, of u kunt laten hello Azure Key Vault Hallo sleutels genereren. U kunt uw versleutelingssleutels opslaan in de opslag van uw lokale sleutels of kunt u ze opslaan in een Azure Sleutelkluis. Azure Sleutelkluis kunt u toogrant toegang toohello geheimen in Azure Key Vault toospecific gebruikers met Azure Active Directory. Dit betekent dat niet alleen iedereen kunt hello Azure Sleutelkluis lezen sleutels en ophalen hello die wordt gebruikt voor versleuteling aan clientzijde.

#### <a name="resources"></a>Resources
* [Blobs in Microsoft Azure Storage met Azure Key Vault versleutelen en ontsleutelen](storage-encrypt-decrypt-blobs-key-vault.md)

  Dit artikel laat zien hoe toouse clientzijde versleuteling met Azure Sleutelkluis, met inbegrip van hoe toocreate KEK Hallo en sla deze op Hallo kluis met behulp van PowerShell.
* [Client-Side-versleuteling en Azure Sleutelkluis voor Microsoft Azure Storage](storage-client-side-encryption.md)

  Dit artikel geeft een uitleg van client-side '-versleuteling en vindt u voorbeelden van het gebruik van Hallo opslag client tooencrypt en ontsleutelen bibliotheekbronnen van Hallo vier storage-services. Het is ook wordt gesproken over Azure Sleutelkluis.

### <a name="using-azure-disk-encryption-tooencrypt-disks-used-by-your-virtual-machines"></a>Met behulp van Azure Disk Encryption tooencrypt schijven gebruikt door uw virtuele machines
Azure Disk Encryption is een nieuwe functie. Deze functie kunt u tooencrypt Hallo OS schijven en gegevensschijven die wordt gebruikt door een virtuele Machine voor IaaS. Hallo stations zijn versleuteld met behulp van standaard-BitLocker-versleuteling technologie voor Windows. Hallo-schijven zijn versleuteld met behulp van technologie Hallo DM-Crypt voor Linux. Dit is geïntegreerd met Azure Key Vault tooallow u toocontrol en beheren van versleutelingssleutels Hallo-schijf.

Hallo-oplossing ondersteunt Hallo volgen scenario's voor IaaS VM's wanneer ze zijn ingeschakeld in Microsoft Azure:

* Integratie met Azure Sleutelkluis
* Standard-laag VMs: [A, D, DS, G, GS en enzovoort reeks IaaS VM's](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Codering voor Windows en Linux IaaS VM's inschakelen
* Het uitschakelen van versleuteling op besturingssysteem en schijven voor Windows IaaS VM 's
* Codering op gegevensstations voor Linux IaaS VM's uitschakelen
* IaaS VM's waarop Windows client-OS-codering inschakelen
* Versleuteling voor volumes met koppelpunten paden inschakelen
* Op Linux-virtuele machines die zijn geconfigureerd met de schijf (RAID) te verwijderen met behulp van mdadm-codering inschakelen
* Inschakelen van versleuteling op Linux VM's met behulp van LVM voor gegevensschijven
* Op Windows-virtuele machines die zijn geconfigureerd met behulp van opslagruimten-codering inschakelen
* Alle openbare Azure-regio worden ondersteund

Hallo-oplossing biedt geen ondersteuning voor Hallo volgen scenario's, functies en -technologie in Hallo release:

* Basisstaffel IaaS VM 's
* Het uitschakelen van Linux IaaS VM's op een station OS versleuteling
* IaaS VM's die zijn gemaakt met behulp van Hallo-methode voor het maken van klassieke VM
* Integratie met uw on-premises Key Management Service
* Azure File storage (gedeelde bestandssysteem), Network File System (NFS), dynamische volumes en virtuele machines van Windows die zijn geconfigureerd met software gebaseerde RAID-systemen


> [!NOTE]
> Schijfversleuteling Linux-besturingssysteem wordt momenteel ondersteund in de volgende Linux-distributies Hallo: RHEL 7.2, CentOS 7.2n en Ubuntu 16.04.
>
>

Deze functie zorgt ervoor dat alle gegevens voor de virtuele machine-schijven is versleuteld in rust in Azure Storage.

#### <a name="resources"></a>Resources
* [Azure Disk Encryption for Windows and Linux IaaS VM 's](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)

### <a name="comparison-of-azure-disk-encryption-sse-and-client-side-encryption"></a>Vergelijking van Azure Disk Encryption, SSE en Client-Side-versleuteling
#### <a name="iaas-vms-and-their-vhd-files"></a>IaaS VM's en hun VHD-bestanden
Voor schijven die door IaaS VM's gebruikt, wordt u aangeraden Azure Disk Encryption. U kunt inschakelen SSE tooencrypt Hallo VHD-bestanden die gebruikt tooback zijn deze schijven in Azure Storage, maar alleen nieuw geschreven gegevens worden versleuteld. Dit betekent dat als u een virtuele machine maken en schakel vervolgens SSE op Hallo storage-account van de VHD-bestand hello, alleen Hallo wijzigingen, worden versleuteld, niet Hallo oorspronkelijke VHD-bestand.

Als u een virtuele machine met een installatiekopie van hello Azure Marketplace maken, Azure voert een [recente kopie](https://en.wikipedia.org/wiki/Object_copying) van Hallo installatiekopie tooyour storage-account in Azure Storage, maar niet versleuteld zelfs als er SSE ingeschakeld. Nadat het Hallo VM maakt en begint met het bijwerken van de installatiekopie hello, start SSE Hallo gegevens te coderen. Daarom is het beste toouse die Azure Disk Encryption op virtuele machines gemaakt op basis van installatiekopieën in hello Azure Marketplace als u wilt dat ze volledig versleuteld.

Als u een vooraf zijn versleuteld virtuele machine in Azure van on-premises brengt, gaat u kunnen tooupload Hallo versleuteling sleutels tooAzure Sleutelkluis en blijven Hallo versleuteling gebruiken voor die dat u waren met on-premises VM. Azure Disk Encryption is ingeschakeld toohandle dit scenario.

Als u niet-versleutelde VHD on-premises hebt, kunt u uploaden naar de galerie Hallo als een aangepaste installatiekopie en inrichten van een virtuele machine uit. Als u dit met Hallo Resource Manager-sjablonen doen, kunt u vragen het tooturn op Azure Disk Encryption wanneer het Hallo VM wordt opgestart.

Wanneer u een gegevensschijf toevoegen en op Hallo VM te koppelen, kunt u Azure Disk Encryption inschakelen op de gegevensschijf. De gegevensschijf van die lokaal eerst zal worden versleuteld en vervolgens Hallo service management-laag wordt hiervoor een vertraagde schrijven tegen opslag Hallo opslag inhoud is versleuteld.

#### <a name="client-side-encryption"></a>Clientversleuteling
Versleuteling aan clientzijde is de veiligste methode Hallo van het versleutelen van uw gegevens, omdat het versleutelt voordat de doorvoer en Hallo-gegevens in rust versleuteld. Het is echter vereist dat u code tooyour toepassingen met behulp van opslag, waarmee u niet wilt toevoegen toodo. In deze gevallen kunt u HTTPs gebruiken voor uw gegevens onderweg en SSE tooencrypt Hallo gegevens in rust.

U kunt tabelentiteiten, Wachtrijberichten en blobs versleutelen met client-side '-versleuteling. U kunt alleen blobs versleutelen met SSE. Als u table en queue gegevens toobe versleuteld moet, moet u versleuteling aan clientzijde.

Versleuteling aan clientzijde wordt volledig beheerd door de toepassing hello. Dit is de veiligste benadering hello, maar toomake programmatische wijzigingen tooyour toepassing, moet u en opgezet Sleutelbeheer processen. U zou deze gebruiken als u wilt dat Hallo extra beveiliging tijdens de overdracht en u wilt dat uw opgeslagen gegevens toobe versleuteld.

Versleuteling aan clientzijde meer belasting op het Hallo-client, en u hebt tooaccount voor dit in uw plannen voor schaalbaarheid, met name als u versleutelen en overdracht van grote hoeveelheden gegevens.

#### <a name="storage-service-encryption-sse"></a>Versleuteling van opslag-Service (SSE)
SSE wordt beheerd door Azure Storage. Met behulp van SSE biedt geen voor Hallo beveiliging van gegevens die onderweg hello, maar deze Hallo-gegevens versleutelen, zoals het tooAzure opslag is geschreven. Er zijn geen gevolgen op Hallo prestaties bij gebruik van deze functie.

U kunt alleen versleutelen blok-blobs, toevoeg-blobs en pagina-blobs SSE gebruiken. Als u tooencrypt tabelgegevens of wachtrijgegevens moet, moet u rekening houden met behulp van versleuteling aan clientzijde.

Als u een archiveren of bibliotheek van VHD-bestanden die u als basis gebruikt voor het maken van nieuwe virtuele machines hebt, kunt u een nieuw opslagaccount maken, SSE inschakelen en vervolgens uploaden Hallo VHD-bestanden toothat account. De VHD-bestanden wordt versleuteld door Azure Storage.

Als u Azure Disk Encryption is ingeschakeld voor Hallo-schijven in een virtuele machine en de SSE ingeschakeld op Hallo Hallo VHD-bestanden met storage-account hebt, werkt deze goed; Dit leidt ertoe dat geen nieuw geschreven gegevens tweemaal wordt versleuteld.

## <a name="storage-analytics"></a>Storage Analytics
### <a name="using-storage-analytics-toomonitor-authorization-type"></a>Met behulp van Storage Analytics toomonitor autorisatie type
U kunt voor elke storage-account Azure Storage Analytics tooperform logboekregistratie inschakelen en metrische gegevens opslaan. Dit is een uitstekend hulpprogramma toouse wanneer toocheck Hallo maatstaven voor prestaties van een opslagaccount, moet of wilt u een opslagaccount tootroubleshoot omdat u problemen met de prestaties ondervindt.

Een andere gegevenseenheid u in Hallo storage analytics logboeken ziet is Hallo verificatiemethode door iemand wordt gebruikt wanneer ze toegang hebben tot opslag. Bijvoorbeeld, met Blob Storage ziet u als ze een Shared Access Signature of Hallo opslagaccountsleutels gebruikt of als Hallo blob toegankelijk openbaar is.

Dit is heel nuttig als u toegang toostorage nauw zijn beveiligen. Bijvoorbeeld in Blob Storage kunt u alle Hallo containers tooprivate instellen en implementeren van Hallo gebruik van een SAS-service in uw toepassingen. U kunt vervolgens controleren Hallo Logboeken regelmatig toosee als uw blobs worden geopend met behulp van Hallo toegangscodes voor opslag, dit kunnen duiden op een schending van beveiliging, of als Hallo blobs openbaar zijn, maar ze mag niet.

#### <a name="what-do-hello-logs-look-like"></a>Wat hello logboeken eruit?
Nadat u metrische gegevens Hallo storage account inschakelen en aan te melden via hello Azure-portal, analytische gegevens wordt tooaccumulate snel starten. Hallo-logboekregistratie en metrische gegevens voor elke service is gescheiden; Hallo-logboekregistratie is alleen geschreven wanneer er activiteiten in die storage-account, terwijl Hallo metrische gegevens worden geregistreerd elke minuut of elk uur per dag uit, afhankelijk van hoe u configureert.

Hallo-logboeken worden opgeslagen in een blok-blobs in een container met de naam $logs in Hallo storage-account. Deze container wordt automatisch gemaakt wanneer Opslaganalyse is ingeschakeld. Zodra deze container is gemaakt, verwijderen u niet, maar u kunt de inhoud ervan verwijderen.

Er is een map voor elke service onder Hallo $logs-container en submappen er voor Hallo jaar per maand/dag, uur te zijn. Hallo logboeken zijn gewoon genummerd onder uur. Dit is wat Hallo directory-structuur ziet er als volgt:

![Weergave van logboekbestanden](./media/storage-security-guide/image1.png)

Elke aanvraag tooAzure opslag wordt vastgelegd. Hier volgt een momentopname van een logboekbestand, met Hallo eerste weinig velden.

![Momentopname van een logboekbestand](./media/storage-security-guide/image2.png)

U kunt zien die u Hallo logboeken tootrack elk soort aanroepen tooa storage-account gebruiken kunt.

#### <a name="what-are-all-of-those-fields-for"></a>Wat zijn alle die velden voor?
Er is een artikel die worden vermeld in de onderstaande resources voor Hallo waarmee Hallo lijst Hallo veel velden in het Hallo-logboeken en wat ze worden gebruikt. Hier volgt de lijst Hallo van velden in de volgorde:

![Momentopname van de velden in een logboekbestand](./media/storage-security-guide/image3.png)

We geïnteresseerd bent in het Hallo-vermeldingen voor GetBlob en hoe ze zijn geverifieerd, dus we toolook voor vermeldingen met 'Get-Blob' type-bewerking nodig hebt en controleer Hallo aanvraagstatus (4<sup>th</sup> kolom) en het Hallo-autorisatie-type (8<sup>th</sup> kolom).

Bijvoorbeeld in Hallo eerst paar rijen in Hallo aanbieding hierboven, Hallo aanvraagstatus is 'Geslaagd' en Hallo autorisatie-type 'geverifieerd'. Dit betekent dat het Hallo-aanvraag is gevalideerd met behulp van de opslagaccountsleutel Hallo.

#### <a name="how-are-my-blobs-being-authenticated"></a>Hoe worden mijn blobs geverifieerd?
We hebben drie gevallen waarin we geïnteresseerd bent.

1. Hallo blob openbaar is en toegankelijk is via een URL zonder een Shared Access Signature. In dit geval Hallo aanvraag-status is 'AnonymousSuccess' en Hallo autorisatie-type is 'anonymous'.

   1.0; 2015-11-17T02:01:29.0488963Z; GetBlob; **AnonymousSuccess**; 200; 124; 37; **anonieme**; mystorage...
2. Hallo-blob is persoonlijk en is gebruikt met een Shared Access Signature. In dit geval Hallo aanvraag-status is 'SASSuccess' en Hallo autorisatie-type is 'sas'.

   1.0; 2015-11-16T18:30:05.6556115Z; GetBlob; **SASSuccess**; 200; 416; 64; **SAS**; mystorage...
3. Hallo-blob is persoonlijk en Hallo-opslagsleutel is gebruikte tooaccess deze. In dit geval Hallo aanvraagstatus is '**geslaagd**'en Hallo autorisatie-type is'**geverifieerde**'.

   1.0; 2015-11-16T18:32:24.3174537Z; GetBlob; **Geslaagd**; 206 59; 22; **geverifieerde**; mystorage...

U kunt Hallo Microsoft Message Analyzer tooview gebruiken en analyseren van deze logboeken. Het bevat de mogelijkheden van zoeken en filteren. U kunt bijvoorbeeld toosearch voor exemplaren van GetBlob toosee als Hallo gebruik verwacht, dat wil zeggen toomake zeker van te zijn dat iemand anders wordt uw storage-account niet verkeerd opent.

#### <a name="resources"></a>Resources
* [Storage Analytics](storage-analytics.md)

  In dit artikel wordt een overzicht van storage analytics en hoe tooenable ze.
* [Storage Analytics logboekindeling](https://msdn.microsoft.com/library/azure/hh343259.aspx)

  In dit artikel ziet u Hallo Storage Analytics logboekindeling en details Hallo beschikbare velden, met inbegrip van verificatie van het type, waarmee wordt aangegeven Hallo type verificatie Hallo aanvraag gebruikt.
* [Een Opslagaccount in hello Azure-portal bewaken](storage-monitor-storage-account.md)

  Dit artikel laat zien hoe tooconfigure maatstaven voor controle en logboekregistratie voor een opslagaccount.
* [End-to-End-problemen oplossen met metrische gegevens van Azure Storage en logboekregistratie, AzCopy en Message Analyzer](storage-e2e-troubleshooting.md)

  Dit artikel wordt gesproken over het oplossen van problemen met behulp van Hallo Storage Analytics en ziet u hoe toouse Hallo Microsoft Message Analyzer.
* [Microsoft Message Analyzer besturingssysteem handleiding](https://technet.microsoft.com/library/jj649776.aspx)

  In dit artikel is Hallo-verwijzing voor Hallo Microsoft Message Analyzer en bevat koppelingen tooa zelfstudie snel aan de slag en overzicht van de functies.

## <a name="cross-origin-resource-sharing-cors"></a>CORS (Cross-Origin Resource Sharing)
### <a name="cross-domain-access-of-resources"></a>Domeintoegang van resources
Wanneer een webbrowser in één domein met een HTTP-aanvraag voor een resource van een ander domein, is dit een cross-origin-HTTP-aanvraag genoemd. Een HTML-pagina aangeboden via contoso.com maakt bijvoorbeeld een aanvraag voor een jpeg gehost op fabrikam.blob.core.windows.net. Uit veiligheidsoverwegingen beperken browsers cross-origin HTTP-aanvragen is gestart vanaf in scripts, zoals JavaScript. Dit betekent dat wanneer wat JavaScript-code op een webpagina op contoso.com die jpeg op fabrikam.blob.core.windows.net aanvraagt, Hallo browser wordt niet toestaan Hallo-aanvraag.

Wat doet deze hebben toodo met Azure Storage? Ook als u statische activa zoals JSON of XML-gegevensbestanden zijn opgeslagen in Blob Storage met behulp van een opslagaccount Fabrikam genoemd, Hallo domein voor Hallo activa zijn fabrikam.blob.core.windows.net en Hallo contoso.com webtoepassing tooaccess kunnen niet worden ze met behulp van JavaScript omdat Hallo domeinen verschillend zijn. Dit geldt ook als u probeert toocall een hello Azure Storage-Services – zoals Table Storage – die JSON gegevens toobe verwerkt door Hallo JavaScript client retourneren.

#### <a name="possible-solutions"></a>Mogelijke oplossingen
Eenzijdige tooresolve dit is een aangepast domein, zoals 'storage.contoso.com' toofabrikam.blob.core.windows.net tooassign. Hallo-probleem is dat u dit opslagaccount van het aangepaste domein tooone alleen kunt toewijzen. Wat gebeurt er als Hallo activa zijn opgeslagen in meerdere opslagaccounts?

Een andere manier tooresolve dit toohave Hallo web application act is als proxy voor Hallo storage aanroepen. Dit betekent dat als u een bestand tooBlob Storage uploadt, Hallo webtoepassing zou lokaal schrijven en vervolgens kopiëren tooBlob opslag of zou alle ervan worden gelezen in het geheugen en schrijf vervolgens tooBlob opslag. U kunt ook een specifieke webtoepassing (zoals een Web-API) die bestanden lokaal Hallo uploadt en schrijft deze tooBlob opslag schrijven. In beide gevallen moet u tooaccount voor die functie hebben als bepalende Hallo schaalbaarheid moet.

#### <a name="how-can-cors-help"></a>Hoe kunt CORS
Azure-opslag kunt u tooenable CORS – Cross-Origin-resources delen. Voor elke storage-account, kunt u domeinen die toegang bronnen in het opslagaccount Hallo tot opgeven. Bijvoorbeeld: in ons geval die hierboven worden beschreven, kunnen we CORS inschakelen in Hallo fabrikam.blob.core.windows.net storage-account en configureer deze tooallow toegang toocontoso.com. Hallo web application contoso.com kan vervolgens rechtstreeks toegang tot bronnen in fabrikam.blob.core.windows.net Hallo.

Een ding toonote is dat CORS toegang toestaat, maar biedt geen verificatie is vereist voor alle niet-openbare toegang tot storage-resources. Dit betekent dat u hebt alleen toegang tot blobs als ze openbaar zijn nemen of u een Shared Access Signature zodat u de benodigde machtiging Hallo. Tabellen, wachtrijen en -bestanden hebben geen openbare toegang en een SAS vereisen.

CORS is standaard uitgeschakeld op alle services. U kunt CORS inschakelen met behulp van Hallo REST-API of Hallo opslag client bibliotheek toocall een Hallo methoden tooset Hallo beleid. Wanneer u dat doet, kunt u een regel CORS, dat zich in XML bevindt opnemen. Hier volgt een voorbeeld van een CORS-regel die is ingesteld met behulp van de bewerking van de Hallo Service-eigenschappen instellen voor Hallo Blob-Service voor een opslagaccount. U kunt uitvoeren die voor deze bewerking met behulp van het storage-clientbibliotheek Hallo Hallo REST-API's voor Azure Storage.

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

Dit is wat elke rij betekent:

* **AllowedOrigins** dit geeft aan welke domeinen niet-overeenkomend kunnen aanvragen en gegevens ontvangen van Hallo storage-service. Dit staat dat contoso.com en fabrikam.com gegevens uit Blob-opslag voor een specifieke storage-account aanvragen kunnen. U kunt ook deze jokertekens tooa instellen (\*) tooallow alle domeinen tooaccess aanvragen.
* **AllowedMethods** dit Hallo lijst met methoden (HTTP-aanvraag woorden) die kunnen worden gebruikt wanneer Hallo-aanvraag is. In dit voorbeeld worden alleen PUT en GET toegestaan. U kunt deze jokertekens tooa instellen (\*) tooallow alle methoden toobe gebruikt.
* **AllowedHeaders** dit headers die Hallo brondomein opgeven kunnen wanneer de aanvraag Hallo Hallo-aanvraag is. In dit voorbeeld zijn alle metagegevens headers beginnen met x-ms-meta-data x-ms-meta-doel en de x-ms-meta-abc toegestaan. Hallo jokerteken (\*) geeft aan dat een koptekst die begint met de Hallo opgegeven voorvoegsel is toegestaan.
* **ExposedHeaders** Zo weet welke antwoordheaders door Hallo browser toohello aanvraag verlener worden blootgesteld. In dit voorbeeld wordt een koptekst die beginnen met ' x-ms - meta-' zichtbaar.
* **MaxAgeInSeconds** dit Hallo maximale tijdsduur dat een browser opgeslagen in de cache Hallo voorbereidende opties aanvraag is. (Raadpleeg Hallo eerste artikel hieronder voor meer informatie over Hallo voorbereidende aanvraag).

#### <a name="resources"></a>Resources
Voor meer informatie over CORS en hoe tooenable, Controleer of deze bronnen.

* [Cross-Origin-Resource delen (CORS) ondersteuning voor hello Azure Storage-Services op Azure.com](storage-cors-support.md)

  Dit artikel bevat een overzicht van CORS en hoe tooset Hallo regels voor Hallo verschillende storage-services.
* [Cross-Origin-Resource delen (CORS) ondersteuning voor hello Azure Storage-Services op MSDN](https://msdn.microsoft.com/library/azure/dn535601.aspx)

  Dit is Hallo-naslagdocumentatie voor CORS-ondersteuning voor hello Azure Storage-Services. Dit heeft koppelingen tooarticles tooeach storage-service, toepassing en toont een voorbeeld en wordt uitgelegd voor elk element in Hallo CORS-bestand.
* [Microsoft Azure Storage: Introducing CORS](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/02/03/windows-azure-storage-introducing-cors.aspx)

  Dit is een koppeling toohello initiële blog artikel aangekondigd CORS en wordt weergegeven hoe toouse deze.

## <a name="frequently-asked-questions-about-azure-storage-security"></a>Veelgestelde vragen over Azure Storage-beveiliging
1. **Hoe kan ik Hallo integriteit van Hallo blobs die ik van of naar Azure Storage brengen ben als ik Hallo HTTPS-protocol niet gebruiken controleren?**

   Als voor een of andere reden moet u toouse HTTP in plaats van HTTPS en u werkt met blok-blobs, kunt u MD5 controleren controleren toohelp Hallo integriteit van Hallo blobs worden overgebracht. Dit helpt met bescherming tegen netwerk/transport layer fouten, maar niet noodzakelijkerwijs met tussenliggende aanvallen.

   Als u HTTPS, waardoor transport level security, dan is het gebruik van MD5 controleren redundante en onnodige gebruiken kunt.

   Voor meer informatie raadpleegt Hallo [overzicht van Azure Blob-MD5](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/02/18/windows-azure-blob-md5-overview.aspx).
2. **Hoe zit het met FIPS-naleving voor Hallo VS Government?**

   Hallo Verenigde Staten Federal Information Processing Standard (FIPS) definieert cryptografische algoritmen die zijn goedgekeurd voor gebruik door het Amerikaanse Computersystemen overheid voor Hallo bescherming van gevoelige gegevens. Inschakelen van FIPS vertelt-modus op een WindowsServer of het bureaublad Hallo OS dat alleen FIPS-gevalideerde cryptografische algoritmen moeten worden gebruikt. Als een toepassing gebruikt een niet-compatibele algoritmen, wordt Hallo toepassingen verbroken. Versies van With.NET Framework 4.5.2 of hoger, Hallo toepassing automatisch activeren algoritmen Hallo-toouse FIPS-compatibele cryptografiealgoritmen wanneer Hallo computer zich in de FIPS-modus.

   Microsoft blijft deze up tooeach klant toodecide of tooenable FIPS-modus. We zijn ervan overtuigd dat er geen dwingende redenen voor klanten die geen onderwerp toogovernment voorschriften tooenable FIPS-modus standaard.

   **Resources**

* [Waarom We je niet aanbevelen 'FIPS-modus' meer](http://blogs.technet.com/b/secguide/archive/2014/04/07/why-we-re-not-recommending-fips-mode-anymore.aspx)

  In dit artikel blog geeft een overzicht van FIPS en wordt uitgelegd waarom ze niet standaard ingeschakeld in de FIPS-modus.
* [FIPS 140 validatie](https://technet.microsoft.com/library/cc750357.aspx)

  In dit artikel bevat informatie over hoe Microsoft-producten en cryptografiemodules aan de FIPS-standaard Hallo voor Hallo VS voldoet Federale overheid.
* [' Systeemcryptografie: gebruik FIPS-compatibele algoritmen voor versleuteling, hashing en ondertekening ' beveiligingsrisico van instellingen in Windows XP en latere versies van Windows](https://support.microsoft.com/kb/811833)

  In dit artikel wordt gesproken over Hallo gebruik van FIPS-modus in oudere Windows-computers.
