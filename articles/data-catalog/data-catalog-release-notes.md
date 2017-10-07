---
title: Releaseopmerkingen voor Data Catalog aaaAzure | Microsoft Docs
description: Releaseopmerkingen voor Azure Data Catalog.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 661826f66020ba72a885c6b14522b53c8b469d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-release-notes"></a>Azure Data Catalog release-opmerkingen
## <a name="notes-for-hello-november-20-2015-release-of-azure-data-catalog"></a>Opmerkingen voor Hallo 20 November 2015-release van Azure Data Catalog
### <a name="opening-data-sources-in-power-bi-desktop"></a>De gegevensbronnen openen in Power BI Desktop
Bij gebruik van Hallo 'Openen in Power BI Desktop' optie van Hallo **Azure Data Catalog** portal gebruikers kunnen ondervinden een van twee problemen in Power BI Desktop toepassing hello:

* Een dialoogvenster met Hallo titel 'Kan geen tooOpen Document' wordt weergegeven
* Hallo Power BI Desktop-toepassing wordt geopend, maar het Hallo-bestand weergegeven toobe leeg

Voor elke situatie Hallo probleem worden opgelost door downloaden en installeren van de meest recente versie van Power BI Desktop van Hallo [PowerBI.com](https://powerbi.com).

## <a name="notes-for-hello-november-13-2015-release-of-azure-data-catalog"></a>Opmerkingen voor Hallo 13 November 2015-release van Azure Data Catalog
### <a name="registering-and-connecting-tooteradata"></a>Registreren en te verbinden tooTeradata
Wanneer u verbinding maakt tooTeradata gegevensbronnen gebruikers moeten de juiste Teradata ODBC-stuurprogramma Hallo hebben geïnstalleerd die overeenkomen met de Hallo bitness (32-bits of 64-bits) van Hallo software wordt gebruikt.

Vanaf deze ADC releasedatum, de meest recente Hallo [Teradata ODBC-stuurprogramma voor windows (versie 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) is compatibel met Office 2013, maar niet met Office 2016.

## <a name="notes-for-hello-july-13-2015-release-of-azure-data-catalog"></a>Opmerkingen voor Hallo 13 juli 2015-release van Azure Data Catalog
### <a name="registering-and-connecting-toooracle-database"></a>Registreren en te verbinden tooOracle Database
Wanneer gegevens tooOracle-bronnen databasegebruikers verbinding moet hebben geïnstalleerd Hallo juiste Oracle stuurprogramma's die overeenkomen met de Hallo bitness (32-bits of 64-bits) van Hallo software wordt gebruikt.

* Bij het registreren van Oracle-gegevensbronnen op een computer met 32-bits Windows wordt hello 32-bits Oracle-stuurprogramma's gebruikt
* Bij het registreren van Oracle-gegevensbronnen op een computer met 64-bits Windows wordt hello 64-bits Oracle-stuurprogramma's gebruikt
* Wanneer u verbinding maakt tooOracle gegevensbronnen met Excel op een computer met Hallo 32-bits versie van Microsoft Office, wordt inclusief op 64-bits Windows hello 32-bits Oracle-stuurprogramma's gebruikt
* Wanneer u verbinding maakt met gegevensbronnen tooOracle met Excel op een computer met Hallo 64-bits versie van Microsoft Office, worden Hallo 64-bits Oracle-stuurprogramma's gebruikt

### <a name="registering-and-connecting-toosql-server-reporting-services"></a>Registreren en te verbinden tooSQL Server Reporting Services
Ondersteuning voor gegevensbronnen van SQL Server Reporting Services (SSRS) is momenteel beperkt tooNative modus alleen servers. Ondersteuning voor SQL Server Reporting Services in de modus SharePoint wordt uitgevoerd wordt in een latere versie toegevoegd.

### <a name="opening-data-assets-in-excel"></a>Gegevensassets openen in Excel
Wanneer u gegevensassets in Microsoft Excel opent vanuit Hallo **Azure Data Catalog** portal gebruikers mogelijk gevraagd met een **beveiligingsbericht Microsoft Excel** in het dialoogvenster. Dit is standaard, verwacht gedrag en gebruikers kunnen selecteren **inschakelen** toocontinue.

Zie voor meer informatie [in- of uitschakelen van beveiligingswaarschuwingen over koppelingen en bestanden van verdachte websites](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a>Proxy- en beleid voor configuratie en gegevens registratie van gegevensbron
Gebruikers kunnen ondervinden een situatie waarin ze zich aanmelden kunnen op toohello Azure Data Catalog-portal, maar als ze proberen toolog op toohello hulpprogramma voor registratie die een foutbericht weergegeven dat voorkomt ze dat zich aanmelden optreden.

Er zijn twee mogelijke oorzaken voor dit probleem gedrag:

**1 oorzaak: Active Directory Federation Services configuration** hulpprogramma voor registratie van gegevensbronnen Hallo formulierverificatie toovalidate gebruikersaanmeldingen op basis van Active Directory wordt gebruikt. Voor geslaagde aanmelding moet formulierverificatie zijn ingeschakeld in Hallo Global Authentication Policy door een Active Directory-beheerder.

In sommige gevallen is kan deze fout gebeuren wanneer Hallo gebruiker op het bedrijfsnetwerk hello, of alleen wanneer Hallo gebruiker verbinding maakt vanaf externe Hallo-netwerk van bedrijf. Hallo algemeen verificatiebeleid kunt verificatie methoden toobe afzonderlijk ingeschakeld voor intranet en extranet-verbindingen. Aanmeldingsfouten kunnen optreden als formulierverificatie niet is ingeschakeld voor het Hallo-netwerk van welke Hallo gebruiker verbinding maakt.

Zie voor meer informatie [Authenticatiebeleid configureren](https://technet.microsoft.com/library/dn486781.aspx).

**Oorzaak 2: Proxy netwerkconfiguratie** als Hallo bedrijfsnetwerk gebruikmaakt van een proxyserver, Hallo-hulpprogramma voor registratie kunnen tooconnect tooAzure Active Directory via Hallo proxy niet mogelijk. Gebruikers kunnen ervoor zorgen dat Hallo-hulpprogramma voor registratie door te bewerken van het hulpprogramma Hallo-configuratiebestand, deze sectie toohello-bestand toe te voegen:

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


toolocate hello RegistrationTool.exe.config bestand Hallo-hulpprogramma voor registratie starten en open vervolgens Hallo Windows Taakbeheer hulpprogramma. Op tabblad met Details Hallo in Taakbeheer, met de rechtermuisknop op RegistrationTool.exe en kies bestandslocatie openen Hallo pop-upmenu.
