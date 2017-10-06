---
title: 'Azure AD Connect: Ontwerpen concepten | Microsoft Docs'
description: In dit onderwerp beschrijft bepaalde gebieden van implementatie ontwerpen
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4114a6c0-f96a-493c-be74-1153666ce6c9
ms.service: active-directory
ms.custom: azure-ad-connect
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1e5d5c6a716ca653fb14fc059e8155124b433732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-design-concepts"></a>Azure AD Connect: Ontwerpconcepten
Hallo-doel van dit onderwerp is toodescribe gebieden die moeten worden beschouwd door middel van tijdens het Hallo-implementatie ontwerpen van Azure AD Connect. In dit onderwerp is een deep dive op bepaalde gebieden en deze concepten worden kort beschreven in andere onderwerpen ook.

## <a name="sourceanchor"></a>sourceAnchor
Hallo sourceAnchor kenmerk wordt gedefinieerd als *een kenmerk onveranderbaar tijdens de levensduur van een object Hallo*. Een object uniek wordt geïdentificeerd als Hallo dezelfde lokale object en in Azure AD. Hallo-kenmerk is een afkorting **onveranderbare id genoemd** en Hallo twee namen uitwisselbaar worden gebruikt.

Hallo woord onveranderbare, dat is 'kan niet worden gewijzigd', is belangrijk toothis onderwerp. Omdat de waarde van dit kenmerk kan niet worden gewijzigd nadat deze is ingesteld, is het belangrijk toopick een ontwerp dat ondersteuning biedt voor uw scenario.

Hallo-kenmerk wordt gebruikt voor Hallo volgen scenario's:

* Wanneer een nieuwe server van de synchronisatie-engine is gemaakt of opnieuw worden opgebouwd na een noodherstelscenario, koppelt u dit kenmerk bestaande objecten in Azure AD met objecten on-premises.
* Als u van een model alleen in de cloud-identiteit tooa gesynchroniseerde identiteit verplaatsen, wordt dit kenmerk te kan objecten 'harde match' bestaande objecten in Azure AD met lokale objecten.
* Als u gebruikmaakt van Federatie en vervolgens dit kenmerk samen met de Hallo **userPrincipalName** wordt gebruikt in Hallo claim toouniquely identificatie van een gebruiker.

In dit onderwerp alleen wordt gesproken over sourceAnchor als deze zich toousers verhoudt. Hallo gelden dezelfde regels tooall objecttypen, maar dit is alleen bestemd voor gebruikers dat dit probleem is meestal een belangrijk.

### <a name="selecting-a-good-sourceanchor-attribute"></a>Een goede sourceAnchor kenmerk selecteren
Hallo-kenmerkwaarde moet volgens de regels voor Hallo volgen:

* Minder dan 60 tekens bestaan
  * Tekens die niet wordt a-z, A-Z en 0-9 zijn gecodeerd en geteld als 3 tekens
* Speciale tekens niet bevatten: &#92;! # $ % & * + / = ? ^ &#96; { } | ~ < > ( ) ' ; : , [ ] " @ _
* Globaal uniek zijn
* Moet een tekenreeks, geheel getal of binair
* Moet niet zijn gebaseerd op de naam van gebruiker deze wijzigingen
* Niet mogen worden hoofdlettergevoelig en te voorkomen dat de waarden die per aanvraag verschillen kunnen
* Moet worden toegewezen als Hallo-object is gemaakt

Als Hallo geselecteerd sourceAnchor is niet van het type tekenreeks Azure AD Connect Base64Encode Hallo kenmerk waarde tooensure geen speciale tekens verschijnen. Als u een andere federatieserver dan de AD FS gebruikt, controleert u of uw server kunt ook Base64Encode Hallo-kenmerk.

Hallo sourceAnchor kenmerk is hoofdlettergevoelig. Een waarde van 'Jandevries' is niet hetzelfde als 'jandevries' Hallo. Maar u mag geen twee verschillende objecten met alleen een verschil in geval.

Als u één forest is het on-premises vervolgens Hallo-kenmerk moet u **objectGUID**. Dit is ook Hallo-kenmerk dat wordt gebruikt wanneer u expresinstellingen in Azure AD Connect gebruiken en ook Hallo kenmerk dat wordt gebruikt door DirSync.

Als u meerdere forests hebt en niet gebruikers tussen forests en domeinen, klikt u vervolgens verplaatsen **objectGUID** een goed kenmerk toouse zelfs in dit geval is.

Als u gebruikers tussen forests en domeinen verplaatst, moet vervolgens u zoeken een kenmerk dat niet verandert of kan worden verplaatst met Hallo gebruikers tijdens Hallo verplaatsen. Een aanbevolen aanpak is toointroduce een synthetische kenmerk. Een kenmerk kan waarin iets dat op een GUID lijkt zijn geschikt is. Tijdens het maken van het object, een nieuwe GUID gemaakt en op Hallo gebruiker vermeld. Een aangepaste synchronisatieregel kan worden gemaakt in Hallo sync engine server toocreate deze waarde op basis van Hallo **objectGUID** en update Hallo geselecteerde kenmerk in ADDS. Wanneer u Hallo object verplaatsen, moet u ervoor dat tooalso kopie Hallo inhoud van deze waarde.

Een andere oplossing is toopick een bestaand kenmerk weet u niet gewijzigd. Gangbare kenmerken zijn **werknemer-id**. Als u een kenmerk dat letters bevat overweegt, zorg ervoor dat er dat geen kans Hallo geval (hoofdletters en kleine letters) voor de waarde van kenmerk Hallo kunt wijzigen. Ongeldige kenmerken die mag niet worden gebruikt, zijn deze kenmerken met de naam van de gebruiker Hallo Hallo. In een huwelijk of echtscheiding is de naam van de Hallo verwachte toochange, wat niet is toegestaan voor dit kenmerk. Dit is ook een reden waarom kenmerken zoals **userPrincipalName**, **mail**, en **targetAddress** zijn niet zelfs mogelijk tooselect in hello Azure AD Connect-installatie de wizard. Deze kenmerken bevatten ook Hallo ' @ ' is niet toegestaan in Hallo sourceAnchor teken.

### <a name="changing-hello-sourceanchor-attribute"></a>Hallo sourceAnchor kenmerk wijzigen
Hallo sourceAnchor kenmerkwaarde kan niet worden gewijzigd nadat het Hallo-object is gemaakt in Azure AD en het Hallo-identiteit is gesynchroniseerd.

Om deze reden Hallo volgen beperkingen toepassen tooAzure AD Connect:

* Hallo sourceAnchor kenmerk kan alleen worden ingesteld tijdens de eerste installatie. Als u de installatiewizard Hallo opnieuw, wordt deze optie is alleen-lezen. Als u deze instelling toochange moet, moet u verwijderen en opnieuw installeren.
* Moet Selecteer hetzelfde kenmerk voor sourceAnchor zoals eerder is gebruikt in Media Player Hallo als u een andere Azure AD Connect-server, dan hebt u installeert. Als u eerder hebt gebruikt als DirSync en tooAzure AD verplaatsen verbinding te maken met, moet u **objectGUID** omdat dat Hallo-kenmerk dat wordt gebruikt door DirSync.
* Als Hallo-waarde voor sourceAnchor is gewijzigd nadat het Hallo-object is geëxporteerde tooAzure AD, vervolgens Azure AD Connect sync een fout genereert en niet in staat geen wijzigingen meer voor dat object voordat Hallo probleem is opgelost en weer in Hallo Hallo sourceAnchor is gewijzigd bronmap.

## <a name="using-msds-consistencyguid-as-sourceanchor"></a>Met behulp van msDS-ConsistencyGuid als sourceAnchor
Standaard wordt in Azure AD Connect (versie 1.1.486.0 en ouder) objectGUID als Hallo sourceAnchor kenmerk gebruikt. ObjectGUID is door het systeem gegenereerd. U kunt de waarde bij het maken van lokale AD-objecten niet opgeven. Zoals wordt beschreven in de sectie [sourceAnchor](#sourceanchor), zijn er scenario's waar u toospecify hello sourceAnchor waarde nodig. Als Hallo scenario's van toepassing tooyou zijn, moet u een configureerbare AD-kenmerk (bijvoorbeeld msDS-ConsistencyGuid) gebruiken als Hallo sourceAnchor kenmerk.

Azure AD Connect (versie 1.1.524.0 en na) nu Hallo gebruik van msDS-ConsistencyGuid als kenmerk sourceAnchor vergemakkelijkt. Wanneer u deze functie gebruikt, configureert Azure AD Connect automatisch Hallo synchronisatieregels naar:

1. Gebruik msDS-ConsistencyGuid als Hallo sourceAnchor kenmerk voor gebruikersobjecten. ObjectGUID wordt gebruikt voor andere objecttypen.

2. Voor een gegeven on-premises AD-gebruiker object waarvan het kenmerk msDS-ConsistencyGuid niet is ingevuld, Azure AD Connect schrijft het kenmerk objectGUID waarde back toohello msDS-ConsistencyGuid in de lokale Active Directory. Nadat het Hallo msDS-ConsistencyGuid kenmerk is ingevuld, wordt in Azure AD Connect daarna Hallo object tooAzure AD exporteert.

>[!NOTE]
> Eenmaal een on-premises AD-object is geïmporteerd in Azure AD Connect (die is geïmporteerd in AD Connectorruimte Hallo en geprojecteerd in Hallo Metaverse), u kunt de waarde sourceAnchor niet meer wijzigen. toospecify hello sourceAnchor waarde voor een opgegeven lokale AD object, het configureren van het kenmerk msDS-ConsistencyGuid voordat deze wordt geïmporteerd in Azure AD Connect.

### <a name="permission-required"></a>Vereiste machtiging
Voor deze toowork functie moet schrijven machtiging toohello msDS-ConsistencyGuid kenmerk in de lokale Active Directory op Hallo van AD DS-account gebruikt toosynchronize met lokale Active Directory worden toegekend.

### <a name="how-tooenable-hello-consistencyguid-feature---new-installation"></a>Hoe tooenable ConsistencyGuid functie - installatie van nieuwe Hallo
U kunt Hallo gebruik van ConsistencyGuid als sourceAnchor inschakelen tijdens de installatie van nieuwe. Deze sectie worden zowel Express en aangepaste installatie meer informatie.

  >[!NOTE]
  > Alleen nieuwere versies van Azure AD Connect (1.1.524.0 en na) ondersteunt het gebruik van ConsistencyGuid als sourceAnchor Hallo tijdens de installatie van nieuwe.

### <a name="how-tooenable-hello-consistencyguid-feature"></a>Hoe tooenable ConsistencyGuid functie Hallo
Op dit moment kan Hallo-functie alleen worden ingeschakeld tijdens alleen nieuwe Azure AD Connect-installatie.

#### <a name="express-installation"></a>Snelle installatie
Als u Azure AD Connect installeert met de snelle modus, bepaald hello Azure AD Connect-wizard Hallo meest geschikte AD kenmerk toouse automatisch als Hallo sourceAnchor kenmerk met Hallo logica te volgen:

* Eerst Hallo hello Azure AD Connect wizard Query's die uw Azure AD-tenant tooretrieve Hallo AD-kenmerk worden gebruikt als het kenmerk sourceAnchor in Hallo vorige Azure AD Connect-installatie (indien aanwezig). Als deze informatie beschikbaar is, wordt Azure AD Connect Hallo dezelfde AD-kenmerk.

  >[!NOTE]
  > Alleen nieuwere versies van Azure AD Connect (1.1.524.0 en na) slaat gegevens in uw Azure AD-tenant over Hallo sourceAnchor kenmerk worden gebruikt tijdens de installatie. Oudere versies van Azure AD Connect niet.

* Als u informatie over Hallo sourceAnchor kenmerk wordt gebruikt niet beschikbaar is, controleert Hallo wizard Hallo status van kenmerk msDS-ConsistencyGuid op Hallo in uw lokale Active Directory. Als het Hallo-kenmerk is niet geconfigureerd op een object in de directory hello, gebruikt Hallo wizard Hallo msDS-ConsistencyGuid als Hallo sourceAnchor kenmerk. Als het Hallo-kenmerk is geconfigureerd op een of meer objecten in de map hello, concludeert Hallo wizard Hallo kenmerk wordt gebruikt door andere toepassingen en is niet geschikt is als het kenmerk sourceAnchor...

* In dat geval Hallo wizard terugvalt toousing objectGUID als Hallo sourceAnchor kenmerk.

* Zodra de kenmerk sourceAnchor hello, wordt besloten bevat Hallo wizard Hallo gegevens in uw Azure AD-tenant. Hallo-gegevens worden gebruikt door toekomstige installatie van Azure AD Connect.

Wanneer de Express-installatie is voltooid, Hallo wizard laat weten welk kenmerk is opgenomen als Hallo Bronanker kenmerk.

![Wizard informeert AD-kenmerk voor sourceAnchor verzameld](./media/active-directory-aadconnect-design-concepts/consistencyGuid-01.png)

#### <a name="custom-installation"></a>Aangepaste installatie
Als u Azure AD Connect installeert met de aangepaste modus, biedt hello Azure AD Connect-wizard twee opties bij het kenmerk sourceAnchor configureren:

![Aangepaste installatie - sourceAnchor configuratie](./media/active-directory-aadconnect-design-concepts/consistencyGuid-02.png)

| Instelling | Beschrijving |
| --- | --- |
| Azure Hallo bronanker beheren voor mij laten | Selecteer deze optie als u wilt dat Azure AD toopick Hallo kenmerk voor u. Als u deze optie selecteert, Azure AD Connect past wizard dezelfde Hallo [sourceAnchor kenmerk selectie logica wordt gebruikt tijdens de snelle installatie](#express-installation). Vergelijkbare tooExpress installatie Hallo wizard informeert u welk kenmerk is opgenomen als Hallo Bronanker kenmerk nadat aangepaste installatie is voltooid. |
| Een specifiek kenmerk | Selecteer deze optie als u een bestaand AD-kenmerk als Hallo sourceAnchor kenmerk toospecify wenst. |

### <a name="how-tooenable-hello-consistencyguid-feature---existing-deployment"></a>Hoe tooenable Hallo ConsistencyGuid functie - bestaande implementatie
Als u een bestaande implementatie van Azure AD Connect die met behulp van objectGUID als Hallo Bronanker kenmerk hebt, kunt u schakelen deze toousing ConsistencyGuid in plaats daarvan.

>[!NOTE]
> Alleen nieuwere versies van Azure AD Connect (1.1.552.0 en na) ondersteunt overschakelen van tooConsistencyGuid als Hallo Bronanker kenmerk ObjectGuid.

tooswitch van objectGUID tooConsistencyGuid als Hallo Bronanker kenmerk:

1. Hello Azure AD Connect-wizard start en op **configureren** toogo toohello taken scherm.

2. Selecteer Hallo **Bronanker configureren** taak optie en klik op **volgende**.

   ![ConsistencyGuid inschakelen voor bestaande implementatie - stap 2](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment01.png)

3. Voer uw referenties in Azure AD-beheerder en klik op **volgende**.

4. Azure AD Connect-wizard analyseert Hallo status van kenmerk msDS-ConsistencyGuid op Hallo in uw lokale Active Directory. Als Hallo-kenmerk niet is geconfigureerd op een object in de directory, Azure AD Connect vaststelt dat er geen andere toepassing hello kenmerk is momenteel in gebruik en veilige toouse Hallo deze als Hallo Bronanker kenmerk. Klik op **volgende** toocontinue.

   ![ConsistencyGuid inschakelen voor bestaande implementatie - stap 4](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment02.png)

5. In Hallo **gereed tooConfigure** scherm, klikt u op **configureren** toomake Hallo configuratiewijziging.

   ![ConsistencyGuid inschakelen voor bestaande implementatie - stap 5](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment03.png)

6. Zodra het Hallo-configuratie is voltooid, Hallo wizard geeft aan dat msDS-ConsistencyGuid nu als Hallo Bronanker kenmerk wordt gebruikt.

   ![ConsistencyGuid inschakelen voor bestaande implementatie - stap 6](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment04.png)

Tijdens de analyse van hello (stap 4) als Hallo-kenmerk is geconfigureerd op een of meer objecten in de directory Hallo Hallo wizard concludeert de domeincontroller Hallo kenmerk wordt gebruikt door een andere toepassing en een foutmelding zoals geïllustreerd in het onderstaande diagram kunt Hallo. Als u er zeker van bent dat Hallo-kenmerk wordt niet gebruikt door bestaande toepassingen, moet u toocontact ondersteuning voor meer informatie over hoe toosuppress Hallo fout.

![ConsistencyGuid inschakelen voor bestaande implementatie - fout](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeploymenterror.png)

### <a name="impact-on-ad-fs-or-third-party-federation-configuration"></a>Gevolgen voor de AD FS of van derden federation-configuratie
Als u van Azure gebruikmaakt AD Connect toomanage lokaal AD FS-implementatie, hello Azure AD Connect Hallo claim regels toouse Hallo dezelfde AD kenmerk als sourceAnchor automatisch bijgewerkt. Dit zorgt ervoor dat Hallo onveranderbare id genoemd claim die worden gegenereerd door AD FS is consistent met de Hallo sourceAnchor waarden geëxporteerde tooAzure AD.

Als u AD FS buiten Azure AD Connect beheert, of u federatieservers van derden voor verificatie gebruikt, moet u handmatig Hallo claimregels bijwerken voor onveranderbare id genoemd claim toobe consistent zijn met de Hallo sourceAnchor waarden tooAzure AD als geëxporteerd zoals beschreven in artikel gedeelte [wijzigen AD FS claimregels](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-management#modclaims). Hallo wizard retourneert Hallo waarschuwing te volgen nadat de installatie is voltooid:

![Federatieconfiguratie van derden](./media/active-directory-aadconnect-design-concepts/consistencyGuid-03.png)

### <a name="adding-new-directories-tooexisting-deployment"></a>Toevoegen van nieuwe mappen tooexisting implementatie
Stel dat u hebt geïmplementeerd Azure AD Connect Hallo ConsistencyGuid functie is ingeschakeld en nu gewenst tooadd implementatie van een andere directory toohello. Wanneer u tooadd Hallo directory, controleert met Azure AD Connect-wizard Hallo status van Hallo mSDS-ConsistencyGuid kenmerk in Hallo directory. Als het Hallo-kenmerk is geconfigureerd op een of meer objecten in de map hello, Hallo wizard Hallo kenmerk wordt gebruikt door andere toepassingen en een foutmelding zoals geïllustreerd in het onderstaande diagram kunt Hallo wordt afgesloten. Als u er zeker van bent dat Hallo-kenmerk wordt niet gebruikt door bestaande toepassingen, moet u toocontact ondersteuning voor meer informatie over hoe toosuppress Hallo fout.

![Toevoegen van nieuwe mappen tooexisting implementatie](./media/active-directory-aadconnect-design-concepts/consistencyGuid-04.png)

## <a name="azure-ad-sign-in"></a>Azure AD aanmelden
Bij het integreren van uw on-premises directory met Azure AD, is het belangrijk toounderstand Hallo synchronisatie-instellingen kunnen invloed Hallo manier gebruiker wordt geverifieerd. UserPrincipalName (UPN) tooauthenticate Hallo gebruiker maakt gebruik van Azure AD. Wanneer u uw gebruikers synchroniseert, moet u Hallo kenmerk toobe gebruikt voor de waarde van userPrincipalName zorgvuldig kiezen.

### <a name="choosing-hello-attribute-for-userprincipalname"></a>Hallo-kenmerk voor userPrincipalName kiezen
Wanneer het selecteren van Hallo-kenmerk voor het ontwikkelen van Hallo-waarde van de UPN toobe gebruikt in Azure een controleren

* Hallo kenmerkwaarden voldoen toohello UPN-syntaxis (RFC 822), moet van het Hallo-indelingusername@domain
* Hallo-achtervoegsel in Hallo waarden komt overeen met tooone Hallo aangepaste domeinen in Azure AD geverifieerd

In de snelle instellingen uitgegaan Hallo keuze voor Hallo kenmerk userPrincipalName is. Als Hallo userPrincipalName kenmerk bevat geen Hallo waarde u wilt dat uw gebruikers toosign in tooAzure, wordt u moet kiezen **aangepaste installatie**.

### <a name="custom-domain-state-and-upn"></a>Status van het aangepaste domein en UPN
Het is belangrijk tooensure er is een geverifieerde domein voor Hallo UPN-achtervoegsel.

Johan is een gebruiker in contoso.com. U wilt dat Jeroen toouse Hallo lokale UPN john@contoso.com toosign in tooAzure nadat u hebt dus gebruikers tooyour Azure AD-directory contoso.onmicrosoft.com. toodo zijn gesynchroniseerd, u moet tooadd en contoso.com als een aangepast domein in Azure AD voordat u kunt controleren Hallo gebruikers synchroniseren. Als de UPN-achtervoegsel Hallo van Jan, bijvoorbeeld contoso.com is, komt niet overeen met een geverifieerde domeinnaam in Azure AD, vervangt Azure AD Hallo UPN-achtervoegsel door contoso.onmicrosoft.com.

### <a name="non-routable-on-premises-domains-and-upn-for-azure-ad"></a>Niet-routeerbaar on-premises domeinen en UPN voor Azure AD
Sommige organisaties hebben niet-routeerbare domeinen, zoals contoso.local of eenvoudige enkelvoudige domeinen zoals contoso. U bent niet kunnen tooverify een niet-routeerbare domein in Azure AD. Azure AD Connect kunt tooonly een geverifieerde domeinnaam in Azure AD synchroniseren. Wanneer u een Azure Active directory maakt, maakt u een routeerbaar domein dat standaarddomein voor uw Azure AD, bijvoorbeeld: contoso.onmicrosoft.com wordt. Daarom wordt het benodigde tooverify andere routeerbaar domeinen in een dergelijk scenario als u niet dat toosync toohello standaarddomein onmicrosoft.com wilt.

Lees [toevoegen van uw aangepaste domein naam tooAzure Active Directory](../active-directory-add-domain.md) voor meer informatie over het toevoegen en verifiëren van domeinen.

Azure AD Connect detecteert als u in een niet-routeerbare domeinomgeving uitvoert en zou u op de juiste wijze van u wilt doorgaan met expresinstellingen waarschuwen. Als u werkt in een niet-routeerbare domein, dan is het waarschijnlijk dat Hallo UPN van Hallo gebruikers niet-routeerbare achtervoegsels te hebben. Als u worden uitgevoerd onder contoso.local, Azure AD Connect wordt voorgesteld u toouse aangepaste instellingen in plaats van met expresinstellingen is. Met aangepaste instellingen voor zijn u kan toospecify Hallo kenmerk op dat moet worden gebruikt als de UPN toosign in tooAzure nadat Hallo gebruikers gesynchroniseerd tooAzure AD zijn.

## <a name="next-steps"></a>Volgende stappen
Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory](active-directory-aadconnect.md).
