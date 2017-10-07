---
title: 'Zelfstudie: Workday configureren voor automatisch gebruikers inrichten met on-premises Active Directory en Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe toouse Workday als bron van identiteitsgegevens voor Active Directory en Azure Active Directory.
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 1a2c375a-1bb1-4a61-8115-5a69972c6ad6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/26/2017
ms.author: asmalser
ms.openlocfilehash: d4eb3237b8fe7614606c58b39fbefcb44f4060fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workday-for-automatic-user-provisioning-with-on-premises-active-directory-and-azure-active-directory"></a>Zelfstudie: Workday voor automatisch gebruikers inrichten met on-premises Active Directory en Azure Active Directory configureren
Hallo-doel van deze zelfstudie is tooshow u stappen die u tooperform tooimport mensen uit Workday in Active Directory en Azure Active Directory, moet met optionele Write-back van enkele kenmerken tooWorkday Hallo. 



## <a name="overview"></a>Overzicht

Hallo [Azure Active Directory-gebruikers inrichten van service](active-directory-saas-app-provisioning.md) kan worden geïntegreerd met Hallo [Workday Human Resources API](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) in volgorde tooprovision gebruikersaccounts. Azure AD maakt gebruik van deze verbinding tooenable Hallo gebruiker inrichting werkstromen te volgen:

* **Inrichting gebruikers tooActive Directory** -geselecteerde sets van gebruikers uit Workday synchroniseren in een of meer Active Directory-forests. 

* **Alleen in de cloud gebruikers tooAzure Active Directory-inrichting** -hybride gebruikers die aanwezig zijn in Active Directory en Azure Active Directory kunnen worden ingericht in het laatste gebruik Hallo [AAD Connect](connect/active-directory-aadconnect.md). Gebruikers die alleen in de cloud kunnen echter worden ingericht rechtstreeks vanuit Workday tooAzure met behulp van Active Directory hello Azure AD-gebruiker-service inricht.

* **Write-back van van e-mailbericht adressen tooWorkday** -service inricht hello Azure AD-gebruiker kunt schrijven Azure AD gebruiker kenmerken back tooWorkday, zoals e-mailadres Hallo geselecteerd.

### <a name="scenarios-covered"></a>Scenario's worden behandeld

Hallo Workday gebruikers inrichten van werkstromen die worden ondersteund door Azure AD-gebruiker Hallo-service inricht maakt gebruik van automatisering van Hallo human resources en identity lifecycle-scenario's voor beheer te volgen:

* **Nieuwe medewerkers inhuren** : wanneer een nieuwe werknemer tooWorkday, wordt toegevoegd een gebruikersaccount wordt automatisch gemaakt in Active Directory, Azure Active Directory en eventueel Office 365 en [andere SaaS-toepassingen die worden ondersteund door Azure AD ](active-directory-saas-app-provisioning.md), met schrijven achterzijde Hallo e-mailadres tooWorkday.

* **Werknemer-kenmerk en het profiel updates** : wanneer een werknemersrecord wordt bijgewerkt in Workday (zoals de naam, titel of manager), wordt hun gebruikersaccount wordt automatisch bijgewerkt in Active Directory, Azure Active Directory en eventueel Office 365 en [andere SaaS-toepassingen die worden ondersteund door Azure AD](active-directory-saas-app-provisioning.md).

* **Werknemer afsluitingen worden** : wanneer een werknemer wordt beëindigd in werkdag, hun gebruikersaccount wordt automatisch uitgeschakeld in Active Directory, Azure Active Directory en eventueel Office 365 en [andere SaaS-toepassingen die worden ondersteund door Azure AD](active-directory-saas-app-provisioning.md).

* **Werknemer opnieuw huurt** : wanneer een werknemer is rehired in werkdag, hun oude account kan opnieuw worden automatisch geactiveerd of opnieuw ingerichte (afhankelijk van uw voorkeur) tooActive Directory, Azure Active Directory, en desgewenst Office 365 en [andere SaaS-toepassingen die worden ondersteund door Azure AD](active-directory-saas-app-provisioning.md).


## <a name="planning-your-solution"></a>Plannen van uw oplossing

Controleer voordat u uw Workday-integratie, Hallo vereisten hieronder en gelezen hello volgen richtlijnen over het toomatch uw huidige Active Directory-architectuur en gebruikers inrichten vereisten met Hallo oplossing(en) verstrekt door Azure Active De map.

### <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

* Een geldig abonnement voor Azure AD Premium-P1 met globale beheerderstoegang
* Een tenant van de implementatie Workday voor test-en-integratie
* Beheerdersmachtigingen in Workday toocreate een systeemgebruiker integratie en controleer wijzigingen tootest werknemersgegevens voor testdoeleinden
* Voor gebruikers inrichten van tooActive Directory, is een domein-server met Windows-Service 2012 of hoger vereist toohost hello [lokale synchronisatie-agent](https://go.microsoft.com/fwlink/?linkid=847801)
* [Azure AD Connect](connect/active-directory-aadconnect.md) voor de synchronisatie tussen Active Directory en Azure AD

> [!NOTE]
> Als uw Azure AD-tenant bevindt zich in Europa, raadpleegt u Hallo [bekende problemen](#known-issues) hieronder.


### <a name="solution-architecture"></a>Oplossingsarchitectuur

Azure AD levert een uitgebreide set voor het leveren van connectors toohelp die u levenscyclusbeheer inrichting en identiteit van Workday tooActive Directory, Azure AD, SaaS-apps, en dan oplossen. Onderdelen die u gebruikt en hoe u Hallo oplossing hebt ingesteld, hangt af van de omgeving en vereisten van uw organisatie. Als een eerste stap rijtje hoeveel van de volgende Hallo aanwezig en geïmplementeerd in uw organisatie zijn:

* Hoeveel Active Directory-Forests worden gebruikt?
* Hoeveel Active Directory-domeinen worden gebruikt?
* Hoeveel Active Directory organisatie-eenheden (OE's) worden gebruikt?
* Hoeveel tenants van Azure Active Directory worden gebruikt?
* Zijn er gebruikers hoeven toobe ingericht tooboth Active Directory en Azure Active Directory (bijvoorbeeld 'hybride' gebruikers)?
* Zijn er gebruikers hoeven toobe ingericht tooAzure Active Directory, maar niet in Active Directory (bijvoorbeeld 'alleen in de cloud' gebruikers)?
* Moeten e-mailadressen gebruiker toobe tooWorkday teruggeschreven?

Zodra u antwoorden toothese vragen hebt, kunt u uw werkdag implementatie inrichten door de volgende richtlijnen voor Hallo onderstaande te plannen.

#### <a name="using-provisioning-connector-apps"></a>Met behulp van de inrichting connector-apps

Azure Active Directory biedt ondersteuning voor vooraf geïntegreerde inrichting connectors voor Workday en een groot aantal andere SaaS-toepassingen. 

Één inrichting connector Hello API van een systeem met één bron-interfaces en helpt inrichten gegevens tooa één doelsysteem. De meeste inrichting connectors die ondersteuning biedt voor Azure AD zijn voor een enkele bron en doelsysteem (bijvoorbeeld Azure AD tooServiceNow) en kunnen worden ingesteld door Hallo app toe te voegen in kwestie van app-galerie (bijvoorbeeld ServiceNow) voor hello Azure AD. 

Er is een-op-een relatie tussen inrichting connector-exemplaren en app-exemplaren in Azure AD:

| Bronsysteem | Doelsysteem |
| ---------- | ---------- | 
| Azure AD-tenant | SaaS-toepassing |


Als u werkt met Workday en Active Directory, zijn er echter meerdere bron- en systemen toobe-beschouwd als:

| Bronsysteem | Doelsysteem | Opmerkingen |
| ---------- | ---------- | ---------- |
| Werkdag | Active Directory-Forest | Elk forest wordt behandeld als een afzonderlijke doelsysteem |
| Werkdag | Azure AD-tenant | Zo vereist zijn voor gebruikers die alleen in de cloud |
| Active Directory-Forest | Azure AD-tenant | Deze stroom wordt verwerkt door de AAD Connect vandaag |
| Azure AD-tenant | Werkdag | Voor write-back van e-mailadressen |

toofacilitate deze meerdere werkstromen toomultiple bron en doel systemen, Azure AD biedt meerdere apps voor inrichting connector die u kunt uit de app-galerie van Azure AD Hallo toevoegen:

![AAD-App-galerie](./media/active-directory-saas-workday-inbound-tutorial/WD_Gallery.PNG)

* **Werkdag tooActive Directory Provisioning** -deze app vereenvoudigt gebruikers account inrichten vanuit Workday tooa één Active Directory-forest. Als u meerdere forests hebt, kunt u één exemplaar van deze app uit de galerie van Azure AD app Hallo voor elk Active Directory-forest moet u tooprovision aan kunt toevoegen.

* **Werkdag tooAzure AD inrichten** -terwijl AAD Connect Hallo-hulpprogramma dat gebruikt toosynchronize Active Directory gebruikers tooAzure Active Directory worden moet, deze app kan worden gebruikt toofacilitate het inrichten van Workday tooa één cloudconfiguratie gebruikers Azure Active Directory-tenant.

* **Write-back van werkdag** -deze app Write-back van e-mailadressen van de gebruiker van Azure Active Directory-tooWorkday vergemakkelijkt.

> [!TIP]
> Hallo reguliere 'Workday' app wordt gebruikt voor het instellen van eenmalige aanmelding tussen Workday en Azure Active Directory. 

Hoe tooset boven en deze speciale configureren inrichting van apps van de connector is Hallo onderwerp Hallo resterende secties van deze zelfstudie. Welke apps u tooconfigure hangen af op welke systemen moet u de tooprovision, en hoeveel Active Directory-Forests en Azure AD zijn tenants in uw omgeving.

![Overzicht](./media/active-directory-saas-workday-inbound-tutorial/WD_Overview.PNG)

## <a name="configure-a-system-integration-user-in-workday"></a>Een systeemgebruiker integratie in Workday configureren
Een algemene eis van alle Hallo Workday inrichting connectors is dat ze referenties nodig voor een werkdag system integratie account tooconnect toohello Workday Human Resources-API. Deze sectie beschrijft hoe een system integrator toocreate in Workday-account.

> [!NOTE]
> Het is mogelijk toobypass deze procedure en in plaats daarvan een globale beheerdersaccount van Workday als Hallo integratie systeemaccount te gebruiken. Dit werkt prima voor demo's, maar wordt niet aanbevolen voor productie-implementaties.

### <a name="create-an-integration-system-user"></a>Maken van een gebruiker van het systeem netwerkintegratie

**toocreate een systeemgebruiker integratie:**

1. Aanmelden bij uw Workday-tenant met een administrator-account. In Hallo **Workday Workbench**, Voer in het zoekvak Hallo gebruiker gemaakt en klik vervolgens op **integratie systeemgebruiker maken**. 
   
    ![Gebruiker maken](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "gebruiker maken")
2. Volledige Hallo **integratie systeemgebruiker maken** taak door het opgeven van een gebruikersnaam en wachtwoord voor een nieuwe gebruiker van de integratie-systeem.  
 * Hallo laat **vereisen nieuwe wachtwoord bij volgende aanmelding** optie is uitgeschakeld, omdat deze gebruiker programmatisch aanmelden. 
 * Hallo laat **minuten voor de time-out sessie** met de standaardwaarde van 0, dit voorkomt dat Hallo gebruikerssessies voortijdig een time-out opgetreden. 
   
    ![Maken van de systeemgebruiker integratie](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "integratie systeemgebruiker maken")

### <a name="create-a-security-group"></a>Maak een beveiligingsgroep
U moet een onbeperkte integratie systeembeveiligingsgroep toocreate en Hallo gebruiker tooit toewijzen.

**toocreate een beveiligingsgroep:**

1. Voer beveiligingsgroep maken in het zoekvak Hallo en klik vervolgens op **beveiligingsgroep maken**. 
   
    ![Groep CreateSecurity](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "CreateSecurity groep")
2. Volledige Hallo **beveiligingsgroep maken** taak.  
3. Selecteer integratie Systeembeveiligingsgroep: een van de Hallo **Type van verpachte beveiligingsgroep** vervolgkeuzelijst.
4. Maak een security group toowhich leden expliciet worden toegevoegd. 
   
    ![Groep CreateSecurity](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "CreateSecurity groep")

### <a name="assign-hello-integration-system-user-toohello-security-group"></a>Hallo-integratie gebruiker toohello systeembeveiligingsgroep toewijzen

**tooassign hello integratie systeemgebruiker:**

1. Voer beveiligingsgroep bewerken in het zoekvak Hallo en klik vervolgens op **beveiligingsgroep bewerken**. 
   
    ![Beveiligingsgroep bewerken](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "beveiligingsgroep bewerken")
2. Zoek en selecteer nieuwe integratie Hallo-beveiligingsgroep met de naam. 
   
    ![Beveiligingsgroep bewerken](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "beveiligingsgroep bewerken")
3. Hallo nieuwe integratie system gebruiker toohello nieuwe beveiligingsgroep toevoegen. 
   
    ![Systeembeveiligingsgroep](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "Systeembeveiligingsgroep")  

### <a name="configure-security-group-options"></a>Configureer de beveiligingsopties voor groep
In deze stap maakt u Verleen toohello nieuwe beveiligingsgroep machtigingen voor **ophalen** en **plaatsen** bewerkingen op Hallo-objecten die zijn beveiligd door Hallo beveiligingsbeleid voor domein te volgen:

* Extern Account inrichten
* Werknemersgegevens: Openbare Worker rapporten
* Werknemersgegevens: Alle posities
* Werknemersgegevens: Huidige bezetting van informatie
* Werknemersgegevens: Functie in werknemersprofiel

**tooconfigure groep beveiligingsopties:**

1. Beveiligingsbeleid voor domein invoeren in het zoekvak Hallo en klik vervolgens op de koppeling Hallo **domein beveiligingsbeleid voor functiegebied**.  
   
    ![Beveiligingsbeleid voor domein](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "beveiligingsbeleid voor domein")  
2. Zoeken naar het systeem en selecteer Hallo **System** functiegebied.  Klik op **OK**.  
   
    ![Beveiligingsbeleid voor domein](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "beveiligingsbeleid voor domein")  
3. Vouw in lijst Hallo van beveiligingsbeleid voor Hallo System functiegebied **beveiligingsbeheer** en selecteer Hallo-beveiligingsbeleid voor domein **extern Account inrichten**.  
   
    ![Beveiligingsbeleid voor domein](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "beveiligingsbeleid voor domein")  
4. Klik op **machtigingen bewerken**, en klik vervolgens op Hallo **machtigingen bewerken**dialoogvenster pagina, het toevoegen van Hallo nieuwe beveiliging groep toohello lijst met beveiligingsgroepen met **ophalen** en **Plaatsen** integratie machtigingen. 
   
    ![Machtigingen bewerken](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "machtigingen bewerken")  
5. Herhaal stap 1 boven tooreturn toohello scherm voor het selecteren van functiegebieden en deze keer zoeken voor bezetting, selecteer Hallo **personeel functiegebied** en klik op **OK**.
   
    ![Beveiligingsbeleid voor domein](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "beveiligingsbeleid voor domein")  
6. Vouw in de lijst Hallo van beveiligingsbeleid voor Hallo functiegebied personeel, **werknemersgegevens: personeel** en Herhaal stap 4 hierboven voor elk van deze resterende beveiligingsbeleid:

   * Werknemersgegevens: Openbare Worker rapporten
   * Werknemersgegevens: Alle posities
   * Werknemersgegevens: Huidige bezetting van informatie
   * Werknemersgegevens: Functie in werknemersprofiel
   
7. Herhaal stap 1, hierboven tooreturn toohello scherm voor functiegebieden te selecteren en deze keer zoeken naar **contactgegevens**, Hallo personeel functiegebied selecteren en op **OK**.

8.  Vouw in de lijst Hallo van beveiligingsbeleid voor Hallo functiegebied personeel, **werknemersgegevens: contactgegevens werk**, en Herhaal stap 4 hierboven voor beveiligingsbeleid Hallo hieronder:

    * Werknemersgegevens: Werke-mailadres

    ![Beveiligingsbeleid voor domein](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "beveiligingsbeleid voor domein")  
    
### <a name="activate-security-policy-changes"></a>Wijzigingen in het beveiligingsbeleid activeren

**wijzigingen in het beveiligingsbeleid tooactivate:**

1. Voer in het zoekvak Hallo activeren en klik vervolgens op Hallo koppeling **activeren in behandeling zijnde wijzigingen in beveiligingsbeleid**. 
   
    ![Activeren](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "activeren") 
2. Begin Hallo wijzigingen in behandeling het beveiligingsbeleid activeren door op te geven van een opmerking voor controledoeleinden, en klik vervolgens op **OK**. 
   
    ![In afwachting van beveiliging activeren](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "activeren in afwachting van beveiliging")   
3. Volledige Hallo-taak op de volgende scherm Hallo door het selectievakje Hallo **bevestigen**, en klik vervolgens op **OK**. 
   
    ![In afwachting van beveiliging activeren](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "activeren in afwachting van beveiliging")  

## <a name="configuring-user-provisioning-from-workday-tooactive-directory"></a>Gebruikers inrichten vanuit Workday tooActive Directory configureren
Volg deze instructies tooconfigure gebruikersaccount inrichten vanuit Workday tooeach Active Directory-forest die u nodig hebt met het inrichten van.

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Deel 1: Hallo inrichting connector app toe te voegen en het Hallo verbinding tooWorkday maken

**tooconfigure Workday tooActive Directory inrichten:**

1.  Ga te<https://portal.azure.com>

2.  Selecteer in de Hallo linkernavigatiebalk **Azure Active Directory**

3.  Selecteer **bedrijfstoepassingen**, klikt u vervolgens **alle toepassingen**.

4.  Selecteer **een toepassing toevoegen**, en selecteer Hallo **alle** categorie.

5.  Zoeken naar **inrichten van Workday tooActive Directory**, en voegt u die app van Hallo-galerie.

6.  Nadat Hallo app is toegevoegd en het welkomstscherm van het app-informatie wordt weergegeven, selecteert u **inrichten**

7.  Wijziging Hallo **inrichten** **modus** te**automatische**

8.  Volledige Hallo **beheerdersreferenties** sectie als volgt:

   * **Admin Username** – Hallo gebruikersnaam Hallo Workday-integratie system-account invoeren met Hallo tenant-domeinnaam is toegevoegd. **Moet als volgt uitzien:username@contoso4**

   * **Beheerderswachtwoord –** Hallo wachtwoord opgeven van Hallo systeemaccount Workday-integratie

   * **Tenant-URL:** Hallo URL toohello Workday web services-eindpunt opgeven voor uw tenant. Dit moet eruitzien als: https://wd3-impl-services1.workday.com/ccx/service/contoso4, waarbij contoso4 is vervangen door de juiste tenantnaam en wd3 impl is vervangen door Hallo juiste omgevingstekenreeks.

   * **Active Directory-Forest -** Hallo 'Name' van uw Active Directory-forest geretourneerd door powershell-commandlet Get-ADForest Hallo. Dit is doorgaans een tekenreeks, zoals: *contoso.com*

   * **Active Directory-Container -** Voer Hallo container tekenreeks zijn met alle gebruikers in uw AD-forest. Voorbeeld: *organisatie-eenheid = standaardgebruikers, OU = Users, DC = contoso, DC = test*

   * **E-mailmelding –** Voer uw e-mailadres in en schakel het selectievakje 'e-mailbericht verzenden als een fout optreedt'.

   * Klik op Hallo **testverbinding** knop. Als het Hallo-verbindingstest is geslaagd, klikt u op Hallo **opslaan** knop Hallo bovenaan. Als dit mislukt, controleer dan dat Hallo Workday-referenties geldig in Workday zijn. 

![Azure Portal](./media/active-directory-saas-workday-inbound-tutorial/WD_1.PNG)

### <a name="part-2-configure-attribute-mappings"></a>Deel 2: Kenmerktoewijzingen configureren 

In deze sectie configureert u hoe gebruikersgegevens uit Workday loopt naar Active Directory.

1.  Op Hallo inrichten tabblad onder **toewijzingen**, klikt u op **synchroniseren Workday werknemers tooOnPremises**.

2.  In Hallo **bron objectbereik** veld, kunt u selecteren welke groepen gebruikers in Workday moet binnen het bereik voor het inrichten van tooAD, door een reeks filters op basis van kenmerken te definiëren. Hallo standaardbereik is 'alle gebruikers in Workday'. Voorbeeld van de filters:

   * Voorbeeld: Bereik toousers met werknemer-id's tussen 1000000 en 2000000

      * Kenmerk: WorkerID

      * Operator: REGEX-overeenkomst

      * Waarde: (1[0-9][0-9][0-9][0-9][0-9][0-9])

   * Voorbeeld: Alleen werknemers en niet contingent werknemers 

      * Kenmerk: werknemer-id

      * Operator: Niet NULL IS

3.  In Hallo **doel Objectacties** veld globaal kunt u filteren welke acties uitvoeren op Active Directory toobe zijn toegestaan. **Maak** en **Update** meest voorkomende zijn.

4.  In Hallo **kenmerktoewijzingen** sectie, kunt u definiëren hoe afzonderlijke Workday kenmerken tooActive directorykenmerken toewijzen.

5. Klik op een bestaand kenmerk toewijzing tooupdate op het **toevoegen van nieuwe toewijzing** Hallo onder Hallo scherm tooadd nieuwe toewijzingen aan. De toewijzing van een individueel kenmerk ondersteunt deze eigenschappen:

      * **Toewijzingstype**

         * **Directe** – schrijft Hallo-waarde van Hallo Workday toohello AD kenmerk, zonder wijzigingen

         * **Constante** -schrijven van een statische, constante string-waarde naar Hallo AD-kenmerk

         * **Expressie** – Hiermee kunt u een aangepaste waarde aan Hallo AD-kenmerk, op basis van een of meer kenmerken van Workday toowrite. [Zie voor meer informatie in dit artikel op expressies](active-directory-saas-writing-expressions-for-attribute-mappings.md).

      * **Bronkenmerk** -Hallo gebruikerskenmerk uit Workday.

      * **Standaardwaarde** : optioneel. Als Hallo bronkenmerk een lege waarde heeft, schrijft Hallo toewijzing deze waarde in plaats daarvan.
            Meest voorkomende configuratie is tooleave dit leeg.

      * **Doelkenmerk** – Hallo gebruikerskenmerk in Active Directory.

      * **Overeen met objecten met behulp van dit kenmerk** : of deze toewijzing moet worden gebruikt of niet toouniquely gebruikers tussen Workday en Active Directory identificeren. Deze wordt meestal ingesteld in het veld ID van de werknemer voor Workday die doorgaans wordt toegewezen aan een van de werknemer-ID-kenmerken Hallo in Active Directory.

      * **Overeenkomende voorrang** – meerdere overeenkomende kenmerken kan worden ingesteld. Wanneer er meerdere, moeten ze worden geëvalueerd in de volgorde gedefinieerd door dit veld. Als een overeenkomst is gevonden, er is geen verdere overeenkomende kenmerken worden geëvalueerd.

      * **Deze toewijzing is van toepassing**
       
         * **Altijd** : deze toewijzing is van toepassing op beide maken van een gebruikersaccount en acties bijwerken

         * **Alleen tijdens het maken van** -deze toewijzing is van toepassing alleen op gebruikersacties maken

6. Klik op toosave uw toewijzingen **opslaan** Hallo boven aan de sectie kenmerk toewijzing.

![Azure Portal](./media/active-directory-saas-workday-inbound-tutorial/WD_2.PNG)

**Hieronder volgen enkele voorbeelden kenmerktoewijzingen tussen Workday en Active Directory met een aantal veelgebruikte expressies**

-   Hallo-expressie die is toegewezen toohello parentDistinguishedName AD-kenmerk kan worden gebruikt tooprovision een gebruiker tooa bepaalde organisatie-eenheid op basis van een of meer Workday bronkenmerken. In dit voorbeeld plaatst gebruikers in verschillende organisatie-eenheden, afhankelijk van hun gegevens plaats in Workday.

-   Hallo-expressie die is toegewezen toohello userPrincipalName AD kenmerk maken een UPN van firstName.LastName@contoso.com. Ook vervangt deze ongeldige tekens.

-   [Er is documentatie over het schrijven van expressies hier](active-directory-saas-writing-expressions-for-attribute-mappings.md)

  
| WERKDAG KENMERK | ACTIVE DIRECTORY-KENMERK |  OVEREENKOMENDE ID? | MAKEN / BIJWERKEN |
| ---------- | ---------- | ---------- | ---------- |
|  **WorkerID**  |  Werknemer-id | **Ja** | Geschreven op alleen maken | 
|  **Gemeente**   |   L   |     | Maken en bijwerken |
|  **Bedrijf**         | Bedrijf   |     |  Maken en bijwerken |
|  **CountryReferenceTwoLetter**      |   CO |     |   Maken en bijwerken |
| **CountryReferenceTwoLetter**    |  C  |     |         Maken en bijwerken |
| **SupervisoryOrganization**  | Afdeling  |     |  Maken en bijwerken |
|  **PreferredNameData**  |  Weergavenaam |     |   Maken en bijwerken |
| **Werknemer-id**    |  algemene naam    |   |   Geschreven op alleen maken |
| **Faxserver**      | facsimileTelephoneNumber     |     |    Maken en bijwerken |
| **Voornaam**   | Voornaam       |     |    Maken en bijwerken |
| **Switch (\[Active\],, '0', 'True', '1')** |  AccountDisabled      |     | Maken en bijwerken |
| **Mobile**  |    mobiele       |     |       Geschreven op alleen maken |
| **EmailAddress**    | E-mail    |     |     Maken en bijwerken |
| **ManagerReference**   | Manager  |     |  Maken en bijwerken |
| **WorkSpaceReference** | physicalDeliveryOfficeName    |     |  Maken en bijwerken |
| **Postcode**  |   Postcode  |     | Maken en bijwerken |
| **LocalReference** |  preferredLanguage  |     |  Maken en bijwerken |
| ** Vervangen (Mid (Vervang (\[werknemer-id\],, ' (\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\|\\\\=\\\\,\\\\+\\\\\*\\\\?\\ \\ &lt; \\ \\ &gt; \]) ', ' ',), 1, 20), ' ([\\\\.) \* \$] (file:///\\.) *$)", , "", , )**      |    SAMAccountName            |     |         Geschreven op alleen maken |
| **Achternaam**   |   SN   |     |  Maken en bijwerken |
| **CountryRegionReference** |  St     |     | Maken en bijwerken |
| **AddressLineData**    |  StreetAddress  |     |   Maken en bijwerken |
| **PrimaryWorkTelephone**  |  telephoneNumber   |     | Geschreven op alleen maken |
| **BusinessTitle**   |  titel     |     |  Maken en bijwerken |
| **Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])" ,, ''M',), '([ñńňÑŃŇN])', "n",), '([öòőõôóÖÒŐÕÔÓO])', "o",), '([P])', 'p',), '([Q])', 'q',), '([řŘR])', 'r',), '([ßšśŠŚS])', "s",), '([TŤť])', "t",), '([üùûúůűÜÙÛÚŮŰU])', "u",), '([V])', 'v',), '([B])', 'w',), '([ýÿýŸÝY])', 'y',), '([źžżŹŽŻZ])', 'z',), ' ',,, ' ',), 'contoso.com')**   | UserPrincipalName     |     | Maken en bijwerken                                                   
| **Switch (\[gemeente\], ' organisatie-eenheid standaardgebruikers, OU = gebruikers, OU = = standaard, organisatie-eenheid locaties, DC = = contoso, DC = com ', 'Dallas' ' organisatie-eenheid standaardgebruikers, OU = gebruikers, OU = Dallas, OU = locaties, DC = = contoso, DC = com ', 'Austin' ' organisatie-eenheid standaardgebruikers, OU = gebruikers, OU = Austin, OU = locaties, DC = = contoso, DC = com ","Seattle"' organisatie-eenheid standaardgebruikers, OU = gebruikers, OU = Seattle, OU = locaties, DC = = contoso, DC = com ', 'Londen', ' organisatie-eenheid standaardgebruikers = OU = Users, organisatie-eenheid Londen, OU = locaties, DC = = contoso, DC = com ")**  | parentDistinguishedName     |     |  Maken en bijwerken |
  
### <a name="part-3-configure-hello-on-premises-synchronization-agent"></a>Deel 3: Hallo lokale synchronisatie-agent configureren

In de volgorde tooprovision tooActive Directory lokaal moet een agent worden geïnstalleerd op een server domein in Hallo desire Active Directory-forest. Domein-(of ondernemingsadministrator-) referenties vereist zijn om Hallo procedure te voltooien.

**[U kunt Hallo lokale synchronisatieagent hier downloaden](https://go.microsoft.com/fwlink/?linkid=847801)**

Voer na de installatie van agent Hallo Powershell-opdrachten hieronder tooconfigure Hallo agent voor uw omgeving.

**Opdracht #1**

> cd C:\\programmabestanden\\Microsoft Azure Active Directory-synchronisatieagent\\Modules\\AADSyncAgent

> AADSyncAgent.psd1 import-module

**Opdracht #2**

> Voeg ADSyncAgentActiveDirectoryConfiguration

* Invoer: Voor 'Mapnaam' hello AD forestnaam invoeren, zoals ingevoerd gedeeltelijk \#2
* Invoer: De gebruikersnaam van de beheerder en het wachtwoord voor Active Directory-forest

**Opdracht #3**

> Voeg ADSyncAgentAzureActiveDirectoryConfiguration

* Invoer: De gebruikersnaam van de globale beheerder en het wachtwoord voor uw Azure AD-tenant

**Opdracht #4**

> Get-AdSyncAgentProvisioningTasks

* Actie: Controleer de gegevens worden geretourneerd. Met deze opdracht detecteert automatisch Workday inrichting van apps in uw Azure AD-tenant. Voorbeelduitvoer:

> Naam: Mijn AD-Forest
>
> Ingeschakeld: True
>
> DirectoryName: mydomain.contoso.com
>
> Bevoegde: False
>
> Identificatie: WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203

**Opdracht #5**

> Start AdSyncAgentSynchronization-automatische

**Opdracht #6**

> net stop aadsyncagent

**Opdracht #7**

> net start aadsyncagent

### <a name="part-4-start-hello-service"></a>Deel 4: Begin Hallo-service
Wanneer onderdelen 1-3 zijn voltooid, kunt u beginnen Hallo terug in Azure Management Portal Hallo-service inricht.

1.  In Hallo **inrichten** tabblad, set Hallo **inrichting Status** naar **op**.

2. Klik op **Opslaan**.

3. Hiermee start u de initiële synchronisatie hello, wat tijd in een variabele aantal uren, afhankelijk van hoeveel gebruikers in Workday zijn kunt nemen.

4. Synchronisatie van afzonderlijke gebeurtenissen, zoals welke gebruikers worden gelezen uit Workday en vervolgens later toegevoegd of bijgewerkt tooActive Directory, kunnen worden weergegeven in Hallo **controlelogboeken** tabblad. **[Zie Hallo inrichting rapportagegids voor gedetailleerde instructies over hoe tooread hello auditlogboeken](active-directory-saas-provisioning-reporting.md)**

5.  Hallo Windows-toepassingslogboek op de agentcomputer Hallo ziet alle bewerkingen die via Hallo-agent wordt uitgevoerd.

6. Een voltooid, wordt er een overzichtsrapport van de audit schrijven in de **inrichten** tabblad, zoals hieronder wordt weergegeven.

![Azure Portal](./media/active-directory-saas-workday-inbound-tutorial/WD_3.PNG)


## <a name="configuring-user-provisioning-tooazure-active-directory"></a>Gebruikers inrichten tooAzure Active Directory configureren
Hoe u inrichting tooAzure Active Directory configureren afhankelijk van uw provisioning vereisten, zoals beschreven in onderstaande tabel voor Hallo.

| Scenario | Oplossing |
| -------- | -------- |
| **Gebruikers moeten toobe ingericht tooActive Directory en Azure AD** | Gebruik  **[AAD Connect](connect/active-directory-aadconnect.md)** |
| **Gebruikers moeten toobe ingericht tooActive Directory alleen** | Gebruik  **[AAD Connect](connect/active-directory-aadconnect.md)** |
| **Gebruikers moeten toobe ingericht tooAzure AD enige (alleen cloud)** | Gebruik Hallo **Workday tooAzure Active Directory provisioning** app in app-galerie Hallo |

Zie voor instructies over het instellen van Azure AD Connect Hallo [documentatie van Azure AD Connect](connect/active-directory-aadconnect.md).

Hallo volgende secties beschrijven instellen van een verbinding tussen Workday en Azure AD tooprovision alleen in de cloud gebruikers.

> [!IMPORTANT]
> Volg Hallo onderstaande procedure alleen als u alleen in de cloud gebruikers dat moet worden ingericht toobe tooAzure AD en niet op de lokale Active Directory.

### <a name="part-1-adding-hello-azure-ad-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Deel 1: Hello Azure AD inrichting connector app toe te voegen en het Hallo verbinding tooWorkday maken

**tooconfigure Workday tooAzure Active Directory-aanbod voor gebruikers alleen in de cloud:**

1.  Ga te<https://portal.azure.com>.

2.  Selecteer in de Hallo linkernavigatiebalk **Azure Active Directory**

3.  Selecteer **bedrijfstoepassingen**, klikt u vervolgens **alle toepassingen**.

4.  Selecteer **een toepassing toevoegen**, en selecteer vervolgens Hallo **alle** categorie.

5.  Zoeken naar **inrichten van Workday tooAzure AD**, en voegt u die app van Hallo-galerie.

6.  Nadat Hallo app is toegevoegd en het welkomstscherm van het app-informatie wordt weergegeven, selecteert u **inrichten**

7.  Wijziging Hallo **inrichten** **modus** te**automatische**

8.  Volledige Hallo **beheerdersreferenties** sectie als volgt:

   * **Admin Username** – Hallo gebruikersnaam Hallo Workday-integratie system-account invoeren met Hallo tenant-domeinnaam is toegevoegd. Moet als volgt uitzien:username@contoso4

   * **Beheerderswachtwoord –** Hallo wachtwoord opgeven van Hallo systeemaccount Workday-integratie

   * **Tenant-URL:** Hallo URL toohello Workday web services-eindpunt opgeven voor uw tenant. Dit moet eruitzien als: https://wd3-impl-services1.workday.com/ccx/service/contoso4, waarbij contoso4 is vervangen door de juiste tenantnaam en wd3 impl is vervangen door Hallo juiste omgevingstekenreeks (indien nodig).

   * **E-mailmelding –** Voer uw e-mailadres in en schakel het selectievakje 'e-mailbericht verzenden als een fout optreedt'.

   * Klik op Hallo **testverbinding** knop.

   * Als het Hallo-verbindingstest is geslaagd, klikt u op Hallo **opslaan** knop Hallo bovenaan. Als dit mislukt, Controleer die Hallo-URL voor Workday en referenties zijn geldig in Workday.


### <a name="part-2-configure-attribute-mappings"></a>Deel 2: Kenmerktoewijzingen configureren 

In deze sectie configureert u hoe de gebruikersgegevens voor gebruikers alleen in de cloud uit Workday wordt loopt met Azure Active Directory.

1.  Op Hallo inrichten tabblad onder **toewijzingen**, klikt u op **synchroniseren werknemers tooAzure AD**.

2.   In Hallo **bron objectbereik** veld, kunt u selecteren welke groepen gebruikers in Workday moet binnen het bereik van de inrichting tooAzure AD, door een reeks filters op basis van kenmerken te definiëren. Hallo standaardbereik is 'alle gebruikers in Workday'. Voorbeeld van de filters:

   * Voorbeeld: Bereik toousers met werknemer-id's tussen 1000000 en 2000000

      * Kenmerk: WorkerID

      * Operator: REGEX-overeenkomst

      * Waarde: (1[0-9][0-9][0-9][0-9][0-9][0-9])

   * Voorbeeld: Alleen contingent werknemers en geen vaste medewerkers

      * Kenmerk: ContingentID

      * Operator: Niet NULL IS

3.  In Hallo **doel Objectacties** veld globaal kunt u filteren welke acties toobe uitgevoerd op Azure AD zijn toegestaan. **Maak** en **Update** meest voorkomende zijn.

4.  In Hallo **kenmerktoewijzingen** sectie, kunt u definiëren hoe afzonderlijke Workday kenmerken tooActive directorykenmerken toewijzen.

5. Klik op een bestaand kenmerk toewijzing tooupdate op het **toevoegen van nieuwe toewijzing** Hallo onder Hallo scherm tooadd nieuwe toewijzingen aan. De toewijzing van een individueel kenmerk ondersteunt deze eigenschappen:

   * **Toewijzingstype**

      * **Directe** – schrijft Hallo-waarde van Hallo Workday toohello AD kenmerk, zonder wijzigingen

      * **Constante** -schrijven van een statische, constante string-waarde naar Hallo AD-kenmerk

      * **Expressie** – Hiermee kunt u een aangepaste waarde aan Hallo AD-kenmerk, op basis van een of meer kenmerken van Workday toowrite. [Zie voor meer informatie in dit artikel op expressies](active-directory-saas-writing-expressions-for-attribute-mappings.md).

   * **Bronkenmerk** -Hallo gebruikerskenmerk uit Workday.

   * **Standaardwaarde** : optioneel. Als Hallo bronkenmerk een lege waarde heeft, schrijft Hallo toewijzing deze waarde in plaats daarvan.
            Meest voorkomende configuratie is tooleave dit leeg.

   * **Doelkenmerk** – Hallo gebruikerskenmerk in Azure AD.

   * **Overeen met objecten met behulp van dit kenmerk** : of deze toewijzing moet worden gebruikt of niet toouniquely Identificeer gebruikers tussen Workday en Azure AD. Deze wordt meestal ingesteld in het veld ID van de werknemer voor Workday die normaal gesproken is toegewezen aan Hallo werknemer-ID-kenmerk (nieuw) of een kenmerk toestelnummer in Azure AD.

   * **Overeenkomende voorrang** – meerdere overeenkomende kenmerken kan worden ingesteld. Wanneer er meerdere, moeten ze worden geëvalueerd in de volgorde gedefinieerd door dit veld. Als een overeenkomst is gevonden, er is geen verdere overeenkomende kenmerken worden geëvalueerd.

   * **Deze toewijzing is van toepassing**

     * **Altijd** : deze toewijzing is van toepassing op beide maken van een gebruikersaccount en acties bijwerken

     * **Alleen tijdens het maken van** -deze toewijzing is van toepassing alleen op gebruikersacties maken

6. Klik op toosave uw toewijzingen **opslaan** Hallo boven aan de sectie kenmerk toewijzing.

### <a name="part-3-start-hello-service"></a>Deel 3: Start Hallo-service
Wanneer onderdelen 1-2 zijn voltooid, kunt u beginnen Hallo-service inricht.

1.  In Hallo **inrichten** tabblad, set Hallo **inrichting Status** naar **op**.

2. Klik op **Opslaan**.

3. Hiermee start u de initiële synchronisatie hello, wat tijd in een variabele aantal uren, afhankelijk van hoeveel gebruikers in Workday zijn kunt nemen.

4. Afzonderlijke sync gebeurtenissen kunnen worden weergegeven in Hallo **controlelogboeken** tabblad. **[Zie Hallo inrichting rapportagegids voor gedetailleerde instructies over hoe tooread hello auditlogboeken](active-directory-saas-provisioning-reporting.md)**

5. Een voltooid, wordt er een overzichtsrapport van de audit schrijven in de **inrichten** tabblad, zoals hieronder wordt weergegeven.


## <a name="configuring-writeback-of-email-addresses-tooworkday"></a>Write-back van e-mailadressen tooWorkday configureren
Volg deze instructies tooconfigure Write-back van gebruiker e-mailadressen van Azure Active Directory-tooWorkday.

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Deel 1: Hallo inrichting connector app toe te voegen en het Hallo verbinding tooWorkday maken

**tooconfigure Workday tooActive Directory inrichten:**

1.  Ga te<https://portal.azure.com>

2.  Selecteer in de Hallo linkernavigatiebalk **Azure Active Directory**

3.  Selecteer **bedrijfstoepassingen**, klikt u vervolgens **alle toepassingen**.

4.  Selecteer **een toepassing toevoegen**, selecteer daarna Hallo **alle** categorie.

5.  Zoeken naar **Write-back van Workday**, en voegt u die app van Hallo-galerie.

6.  Nadat Hallo app is toegevoegd en het welkomstscherm van het app-informatie wordt weergegeven, selecteert u **inrichten**

7.  Wijziging Hallo **inrichten** **modus** te**automatische**

8.  Volledige Hallo **beheerdersreferenties** sectie als volgt:

   * **Admin Username** – Hallo gebruikersnaam Hallo Workday-integratie system-account invoeren met Hallo tenant-domeinnaam is toegevoegd. Moet als volgt uitzien:username@contoso4

   * **Beheerderswachtwoord –** Hallo wachtwoord opgeven van Hallo systeemaccount Workday-integratie

   * **Tenant-URL:** Hallo URL toohello Workday web services-eindpunt opgeven voor uw tenant. Dit moet eruitzien als: https://wd3-impl-services1.workday.com/ccx/service/contoso4, waarbij contoso4 is vervangen door de juiste tenantnaam en wd3 impl is vervangen door Hallo juiste omgevingstekenreeks (indien nodig).

   * **E-mailmelding –** Voer uw e-mailadres in en schakel het selectievakje 'e-mailbericht verzenden als een fout optreedt'.

   * Klik op Hallo **testverbinding** knop. Als het Hallo-verbindingstest is geslaagd, klikt u op Hallo **opslaan** knop Hallo bovenaan. Als dit mislukt, Controleer die Hallo-URL voor Workday en referenties zijn geldig in Workday.


### <a name="part-2-configure-attribute-mappings"></a>Deel 2: Kenmerktoewijzingen configureren 


In deze sectie configureert u hoe gebruikersgegevens uit Workday loopt naar Active Directory.

1.  Op Hallo inrichten tabblad onder **toewijzingen**, klikt u op **synchroniseren Azure AD-gebruikers tooWorkday**.

2.  In Hallo **bron objectbereik** veld, kunt u eventueel filteren welke groepen gebruikers in Azure Active Directory moeten hebben hun e-mailadressen teruggeschreven tooWorkday. Hallo standaardbereik is 'alle gebruikers in Azure AD'. 

3.  In Hallo **kenmerktoewijzingen** sectie, kunt u definiëren hoe afzonderlijke Workday kenmerken tooActive directorykenmerken toewijzen. Er is geen toewijzing voor de e-mailadres Hallo standaard. Hallo die overeenkomt met de ID moet echter bijgewerkte toomatch gebruikers in Azure AD met hun overeenkomstige vermeldingen in Workday. Een populaire overeenkomende methode is toosynchronize hello Workday werknemer-ID of werknemer-ID tooextensionAttribute1 15 in Azure AD en gebruik vervolgens dit kenmerk in Azure AD-toomatch gebruikers weer in Workday.

4.  toosave uw toewijzingen, klikt u op **opslaan** bovenaan Hallo Hallo sectie kenmerk toewijzen.

### <a name="part-3-start-hello-service"></a>Deel 3: Start Hallo-service
Wanneer onderdelen 1-2 zijn voltooid, kunt u beginnen Hallo-service inricht.

1.  In Hallo **inrichten** tabblad, set Hallo **inrichting Status** naar **op**.

2. Klik op **Opslaan**.

3. Hiermee start u de initiële synchronisatie hello, wat tijd in een variabele aantal uren, afhankelijk van hoeveel gebruikers in Workday zijn kunt nemen.

4. Afzonderlijke sync gebeurtenissen kunnen worden weergegeven in Hallo **controlelogboeken** tabblad. **[Zie Hallo inrichting rapportagegids voor gedetailleerde instructies over hoe tooread hello auditlogboeken](active-directory-saas-provisioning-reporting.md)**

5. Een voltooid, wordt er een overzichtsrapport van de audit schrijven in de **inrichten** tabblad, zoals hieronder wordt weergegeven.

## <a name="known-issues"></a>Bekende problemen

* **Controlelogboeken in Europese landen** - zoals van Hallo-release van deze technical preview, een bekend probleem met de Hallo is [controlelogboeken](active-directory-saas-provisioning-reporting.md) voor Hallo Workday connector apps verschijnt niet in Hallo [Azure-portal](https://portal.azure.com) als hello Azure AD-tenant bevindt zich in een Europese Datacenter. Er ontbreekt een oplossing voor dit probleem. Controleer of deze ruimte over Hallo nabije toekomst voor updates opnieuw. 

## <a name="additional-resources"></a>Aanvullende bronnen
* [Zelfstudie: Eenmalige aanmelding tussen Workday en Azure Active Directory configureren](active-directory-saas-workday-tutorial.md)
* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Volgende stappen

* [Informatie over hoe tooreview registreert en het ophalen van rapporten over het inrichten van activiteit](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting)
