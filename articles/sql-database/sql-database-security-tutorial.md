---
title: aaaSecure uw Azure SQL database | Microsoft Docs
description: Meer informatie over technieken en functies toosecure uw Azure SQL database.
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a>Beveiligen van uw Azure SQL Database

SQL-Database beveiligt uw gegevens door te beperken van toegang tooyour database met behulp van firewallregels, verificatiemechanismen vereisen tooprove gebruikers hun identiteit en autorisatie toodata via lidmaatschappen op basis van rollen en machtigingen, evenals via beveiliging en dynamische gegevensmaskering.

U kunt de beveiliging van uw database tegen kwaadwillende gebruikers of onbevoegde toegang met een paar eenvoudige stappen Hallo verbeteren. In deze zelfstudie leert u naar: 

> [!div class="checklist"]
> * Niveau van de server firewallregels voor uw server in hello Azure-portal instellen
> * Regels voor uw database met behulp van SSMS firewallregel op databaseniveau instellen
> * Verbinding maken met behulp van een beveiligde verbindingsreeks tooyour-database
> * Gebruikerstoegang beheren
> * Uw gegevens beschermen met versleuteling
> * Inschakelen van controle voor SQL-Database
> * Detectie van dreigingen SQL-Database inschakelen

Als u een Azure-abonnement geen [een gratis account maken](https://azure.microsoft.com/free/) voordat u begint.

## <a name="prerequisites"></a>Vereisten

toocomplete deze zelfstudie, zorg ervoor dat u hebt hello te volgen:

- Meest recente versie van geïnstalleerde Hallo [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). 
- Geïnstalleerde Microsoft Excel
- Zie gemaakt van een Azure SQL-server en database - [maken van een Azure SQL database in Azure-portal Hallo](sql-database-get-started-portal.md), [maken van één Azure SQL database met behulp van Azure CLI Hallo](sql-database-get-started-cli.md), en [maken van een enkele Azure SQL de database met behulp van PowerShell](sql-database-get-started-powershell.md). 

## <a name="log-in-toohello-azure-portal"></a>Meld u bij toohello Azure-portal

Meld u bij toohello [Azure-portal](https://portal.azure.com/).

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Maken van een firewallregel op serverniveau in hello Azure-portal

SQL-databases worden beveiligd door een firewall in Azure. Standaard worden alle verbindingen toohello server- en Hallo databases binnen Hallo server geweigerd, met uitzondering van verbindingen met andere Azure-services. Zie voor meer informatie [Azure SQL Database server- en databaseniveau firewallregels](sql-database-firewall-configure.md).

de veiligste configuratie Hallo is tooset 'Toestaan dat toegang tot services tooAzure' tooOFF. Als u nodig hebt tooconnect toohello-database van een virtuele machine in Azure of cloud-service, moet u een [gereserveerde IP-adres](../virtual-network/virtual-networks-reserved-public-ip.md) en alleen Hallo gereserveerd IP-adres toegang toestaan via Hallo firewall. 

Volg deze stappen toocreate een [SQL-Database firewallregel op serverniveau](sql-database-firewall-configure.md) voor uw server tooallow verbindingen van een specifiek IP-adres. 

> [!NOTE]
> Als u een voorbeelddatabase hebt gemaakt in Azure met behulp van een van de vorige zelfstudies Hallo of snelstartgidsen en zijn de u deze zelfstudie op een computer met de Hallo dezelfde IP, dat het adres had toen u deze zelfstudie hebt doorlopen, kunt u deze stap overslaan als u een firewallregel op serverniveau al gemaakt.
>

1. Klik op **SQL-databases** uit Hallo links en klik op Hallo database gewenst tooconfigure Hallo firewallregel voor op Hallo **SQL-databases** pagina. Hallo overzichtspagina voor uw database wordt geopend, waarin u Hallo volledig gekwalificeerde servernaam (zoals **mynewserver 20170313.database.windows.net**) en biedt opties voor verdere configuratie.

      ![serverfirewallregel](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. Klik op **serverfirewall ingesteld** op Hallo werkbalk zoals weergegeven in de vorige afbeelding Hallo. Hallo **Firewall-instellingen** pagina voor Hallo SQL Database-server wordt geopend. 

3. Klik op **client-IP toevoegen** op Hallo werkbalk tooadd Hallo openbaar IP-adres van Hallo computer verbonden toohello portal met of Hallo firewallregel handmatig invoeren en klik vervolgens op **opslaan**.

      ![serverfirewallregel instellen](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. Klik op **OK** en klik vervolgens op Hallo **X** tooclose hello **Firewall-instellingen** pagina.

U kunt nu verbinding maken met de database tooany in Hallo server Hello opgegeven IP-adres of IP-adresbereik.

> [!NOTE]
> SQL Database communiceert via poort 1433. Als u tooconnect van binnen een bedrijfsnetwerk probeert, kan uitgaand verkeer via poort 1433 niet worden toegestaan door de firewall van uw netwerk. Zo ja, zich u niet kunnen tooconnect tooyour Azure SQL Database-server tenzij uw IT-afdeling poort 1433 wordt geopend.
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a>Een firewallregel op databaseniveau met behulp van SSMS maken

Firewallregel op databaseniveau regels kunt u toocreate verschillende firewall-instellingen voor de verschillende databases binnen dezelfde logische server en toocreate firewallregels die zijn draagbare - wat betekent dat ze Hallo database tijdens volgen Hallo een [failover ](sql-database-geo-replication-overview.md) in plaats van op Hallo SQL server worden opgeslagen. Firewallregels databaseniveau kunnen alleen worden geconfigureerd met behulp van Transact-SQL-instructies en alleen nadat u het eerste niveau van de server firewallregel Hallo hebt geconfigureerd. Zie voor meer informatie [Azure SQL Database server- en databaseniveau firewallregels](sql-database-firewall-configure.md).

Deze stappen toocreate een database-specifieke firewallregel volgt.

1. Verbinding maken met tooyour-database, bijvoorbeeld met behulp van [SQL Server Management Studio](./sql-database-connect-query-ssms.md).

2. In Object Explorer met de rechtermuisknop op de gewenste tooadd een firewall voor regel en klik op Hallo-database **nieuwe Query**. Een lege queryvenster wordt geopend die verbonden tooyour database.

3. In het queryvenster hello, Hallo IP-adres tooyour openbaar IP-adres wijzigen en vervolgens Hallo volgende query wordt uitgevoerd:

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. Op de werkbalk Hallo **Execute** toocreate Hallo firewallregel.

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a>Hoe een toepassing tooyour tooconnect database met behulp van een beveiligde verbindingsreeks weergeven

tooensure een beveiligde, gecodeerde verbinding tussen een client-toepassing en de SQL-Database, Hallo-verbindingsreeks heeft toobe geconfigureerd:

- Aanvragen van een versleutelde verbinding, en
- toonot vertrouwensrelatie Hallo-servercertificaat. 

Dit maakt een verbinding met behulp van Transport Layer Security (TLS) en Hallo risico van man-in-the-middle-aanvallen vermindert. U kunt ophalen met juist geconfigureerde verbindingsreeksen voor uw SQL-Database voor ondersteunde client stuurprogramma's hello Azure-portal zoals weergegeven voor ADO.net in deze schermafbeelding.

1. Selecteer **SQL-databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina.

2. Op Hallo **overzicht** pagina voor uw database, klikt u op **databaseverbindingsreeksen tonen**.

3. Bekijk Hallo voltooid **ADO.NET** verbindingsreeks.

    ![ADO.NET-verbindingsreeks](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a>Databasegebruikers te maken

Voordat u alle gebruikers, moet u eerst kiezen uit twee soorten verificatie wordt ondersteund door Azure SQL Database: 

**SQL-verificatie**, die gebruikmaakt van gebruikersnaam en wachtwoord voor aanmeldingen en gebruikers die geldig zijn alleen in de context van een bepaalde database binnen een logische server Hallo. 

**Azure Active Directory-verificatie**, waarbij identiteiten die worden beheerd door Azure Active Directory wordt gebruikt. 

Als u wilt dat toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate op SQL-Database ingevuld Azure Active Directory moet bestaan voordat u verder kunt gaan.

Volg deze stappen toocreate een gebruiker via SQL-verificatie:

1. Verbinding maken met tooyour-database, bijvoorbeeld met behulp van [SQL Server Management Studio](./sql-database-connect-query-ssms.md) met uw beheerdersreferenties voor de server.

2. In Object Explorer met de rechtermuisknop op Hallo database tooadd een nieuwe gebruiker op en klik op **nieuwe Query**. Een lege queryvenster wordt geopend dat de geselecteerde database verbonden toohello.

3. Voer in het queryvenster hello, Hallo query te volgen:

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. Op de werkbalk Hallo **Execute** toocreate Hallo gebruiker.

5. Standaard Hallo gebruiker verbinding kan maken van toohello database, maar heeft geen machtigingen tooread of schrijven gegevens. toogrant deze machtigingen toohello nieuw aangemaakte gebruiker, het uitvoeren van de volgende twee opdrachten in een nieuwe queryvenster Hallo

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

Het is best practice toocreate deze accounts niet-beheerders op Hallo database niveau tooconnect tooyour database tenzij u tooexecute beheerderstaken, zoals het maken van nieuwe gebruikers wordt gevraagd. Controleer op Hallo [Azure Active Directory-zelfstudie](./sql-database-aad-authentication-configure.md) over het tooauthenticate met Azure Active Directory.


## <a name="protect-your-data-with-encryption"></a>Uw gegevens beschermen met versleuteling

Azure SQL Database transparante gegevensversleuteling (TDE) versleutelt automatisch uw gegevens in rust, zonder eventuele wijzigingen toohello toepassing toegang tot Hallo versleutelde database. Voor nieuwe databases is TDE standaard ingeschakeld. tooenable TDE voor uw database of tooverify die TDE ingeschakeld is, als volgt te werk:

1. Selecteer **SQL-databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina. 

2. Klik op **transparante gegevensversleuteling** tooopen Hallo-configuratiepagina voor TDE.

    ![Transparante gegevensversleuteling](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. Indien nodig stelt **gegevensversleuteling** tooON en klik op **opslaan**.

Hallo-versleutelingsproces op Hallo achtergrond gestart. U kunt Hallo voortgang via verbindende tooSQL Database [SQL Server Management Studio](./sql-database-connect-query-ssms.md) door het uitvoeren van query's Hallo encryption_state kolom Hallo `sys.dm_database_encryption_keys` weergeven.

## <a name="enable-sql-database-auditing-if-necessary"></a>Controle in te schakelen SQL-Database, indien nodig

Azure SQL Database Auditing houdt databasegebeurtenissen bij en schrijft deze tooan controlelogboek in uw Azure Storage-account. Controle, kunt u de naleving van regelgeving onderhouden, de activiteit in een database begrijpen en meer inzicht krijgen in discrepanties en afwijkingen die kunnen wijzen op mogelijke schendingen van de beveiliging. Volg deze stappen toocreate een controle standaardbeleid voor uw SQL-database:

1. Selecteer **SQL-databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina. 

2. Selecteer in de blade beleidinstellingen Hallo **controle en detectie van dreigingen**. Kennisgeving serverniveaus controle is uitgeschakeld en of er een **serverinstellingen weergeven** koppeling kunt u tooview of wijzigen van Hallo server controle-instellingen in deze context.

    ![Controle-Blade](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. Als u liever tooenable een Audit type (of locatie?) verschilt van Hallo opgegeven op het serverniveau hello, schakelt u **ON** controle, en kies Hallo **Blob** controletype. Als server Auditingfunctie voor blobs is ingeschakeld, wordt naast Hallo server Blob audit Hallo geconfigureerd databaseaudit bestaan.

    ![Controle inschakelen](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. Selecteer **opslaggroep** tooopen Hallo Audit logboeken opslag Blade. Selecteer hello Azure storage-account waarin de logboeken worden opgeslagen en de bewaarperiode hello, als u welke Hallo oude logboeken worden verwijderd, klikt u **OK** Hallo onderaan. 

   > [!TIP]
   > Gebruik dezelfde Hallo opslagaccount voor alle gecontroleerde databases tooget Hallo optimaal gebruik van Hallo controle rapporteert sjablonen.
   > 

5. Klik op **Opslaan**.

> [!IMPORTANT]
> Als u toocustomize Hallo gecontroleerd gebeurtenissen wilt, u kunt dit doen via PowerShell of REST-API - Zie Hallo [Automation (PowerShell / REST-API)](sql-database-auditing.md#subheading-7) sectie voor meer informatie.
>

## <a name="enable-sql-database-threat-detection"></a>Detectie van dreigingen SQL-Database inschakelen

Detectie van dreigingen biedt een nieuwe laag van beveiliging, waarbij kan klanten toodetect en hierop reageren toopotential bedreigingen wanneer deze zich voordoen doordat beveiligingswaarschuwingen op vreemde activiteiten worden gedetecteerd. Gebruikers kunnen Hallo verdachte gebeurtenissen met SQL Database Auditing toodetermine als ze het gevolg zijn van een poging tooaccess, inbreuk of misbruik van gegevens in Hallo database verkennen. Detectie van dreigingen maakt het eenvoudig tooaddress potentiële bedreigingen toohello database zonder Hallo nodig toobe een expert beveiliging of systemen bewaking van de geavanceerde beveiliging te beheren.
Detectie van dreigingen detecteert bijvoorbeeld bepaalde afwijkende databaseactiviteiten potentiële SQL-injectie pogingen die aangeeft. SQL-injectie is een van de Hallo algemene Web application beveiligingsproblemen op Hallo Internet, gebruikte tooattack gegevensgestuurde toepassingen. Aanvallers te profiteren van de toepassing beveiligingslekken tooinject schadelijke SQL-instructies in de invoervelden toepassing voor schendingen veroorzaken of wijzigen van gegevens in de database Hallo.

1. Navigeer toohello configuratie blade Hallo gewenste toomonitor SQL-database. Selecteer in de blade beleidinstellingen Hallo **controle en detectie van dreigingen**.

    ![Navigatiedeelvenster](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. In Hallo **controle en detectie van dreigingen** configuratie blade Schakel **ON** controle, wordt die Hallo threat detectie-instellingen weergegeven.

3. Schakel **ON** bedreigingendetectie.

4. Hallo lijst configureren van e-mailberichten die beveiligingswaarschuwingen na detectie van afwijkende databaseactiviteiten ontvangt.

5. Klik op **opslaan** in Hallo **controle en detectie van bedreigingen** blade toosave Hallo nieuwe of bijgewerkte controle en threat beleid.

    ![Navigatiedeelvenster](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    Als er worden afwijkende databaseactiviteiten gedetecteerd, ontvangt u een e-mailmelding na detectie van afwijkende databaseactiviteiten. Hallo e bevatten informatie over verdachte beveiligingslogboek Hallo Hallo aard van Hallo afwijkende activiteiten, databasenaam, server-naam en het Hallo gebeurtenistijd inclusief. Bovendien bevatten informatie over mogelijke oorzaken en aanbevolen acties tooinvestigate en Hallo mogelijke bedreiging toohello database beperken. Hallo volgende stappen walk via welke toodo moet u deze een e-mail ontvangen:

    ![Threat detectie e](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. Hallo e-mail, klik op Hallo **Azure SQL-controle logboek** koppeling waarmee u hello Azure-portal te starten en relevante Hallo controle records rond de tijd Hallo van Hallo verdachte activiteit weer te geven.

    ![AuditRecords](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. Klik op Hallo audit records tooview meer informatie over Hallo database verdachte activiteiten zoals SQL-instructie is mislukt reden en client-IP.

    ![Details van de records](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. Klik op Hallo controle Records blade **openen in Excel** tooopen een vooraf geconfigureerde excel sjabloon tooimport en uitvoeren diepgaande analyse van Hallo controlelogboek rond de tijd Hallo van verdachte Hallo-gebeurtenis.

    > [!NOTE]
    > In Excel 2010 of hoger, Power Query en Hallo **snel combineren** instelling is vereist.

    ![Open records in Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. Hallo tooconfigure **snel combineren** instelling - In Hallo **POWER QUERY** linttabblad, selecteer **opties** dialoogvenster toodisplay Hallo-opties. Selecteer Hallo privacysectie en kies Hallo tweede optie - 'Negeren Hallo privacyniveaus en mogelijk verbeterde prestaties':

    ![Excel snel combineren](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. controlelogboeken tooload SQL, zorg ervoor dat Hallo-parameters in tabblad Hallo-instellingen juist zijn ingesteld en selecteer Hallo 'Data' lint en klikt u op Hallo Alles vernieuwen.

    ![Excel-parameters](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. Hallo resultaten worden weergegeven in Hallo **SQL controlelogboeken** blad waarmee u toorun diepgaande analyse van Hallo afwijkende activiteiten die zijn gedetecteerd en verhelpen van Hallo gevolgen van het beveiligingslogboek Hallo in uw toepassing.


## <a name="next-steps"></a>Volgende stappen
U kunt de beveiliging van uw database tegen kwaadwillende gebruikers of onbevoegde toegang met een paar eenvoudige stappen Hallo verbeteren. In deze zelfstudie leert u naar: 

> [!div class="checklist"]
> * Firewallregels voor de server en of de database instellen
> * Verbinding maken met behulp van een beveiligde verbindingsreeks tooyour-database
> * Gebruikerstoegang beheren
> * Uw gegevens beschermen met versleuteling
> * Inschakelen van controle voor SQL-Database
> * Detectie van dreigingen SQL-Database inschakelen

> [!div class="nextstepaction"]
>[De prestaties van uw SQL-database verbeteren](sql-database-performance-tutorial.md)

