---
title: aaaConnect tooSQL Database met behulp van SQL Server Management Studio in Azure RemoteApp | Microsoft Docs
description: Gebruik deze zelfstudie toolearn hoe toouse SQL Server Management Studio in Azure RemoteApp voor beveiliging en prestaties bij het verbinden van tooSQL Database
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a>SQL Server Management Studio in Azure RemoteApp tooconnect tooSQL Database gebruiken

> [!IMPORTANT]
> Azure RemoteApp wordt buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
>

## <a name="introduction"></a>Inleiding
Deze zelfstudie leert u hoe toouse SQL Server Management Studio (SSMS) in Azure RemoteApp tooconnect tooSQL Database. Deze begeleidt u bij Hallo-proces voor het instellen van SQL Server Management Studio in Azure RemoteApp, wordt uitgelegd Hallo voordelen en ziet u beveiligingsfuncties die u kunt gebruiken in Azure Active Directory.

**Geschatte tijd toocomplete:** 45 minuten

## <a name="ssms-in-azure-remoteapp"></a>SSMS in Azure RemoteApp
Azure RemoteApp is een RDS-service in Azure die toepassingen levert. Meer informatie over deze hier: [wat is RemoteApp?](../remoteapp/remoteapp-whatis.md)

SSMS uitgevoerd in Azure RemoteApp biedt Hallo u dezelfde ervaring als SSMS lokaal uitgevoerd.

![Schermopname van SSMS uitgevoerd in Azure RemoteApp][1]

## <a name="benefits"></a>Voordelen
Er zijn veel voordelen toousing SSMS in Azure RemoteApp, met inbegrip van:

* Poort 1433 op Azure SQL-server heeft geen toobe blootgesteld extern (buiten Azure).
* Er is geen noodzaak tookeep toevoegen en verwijderen van IP-adressen in de firewall hello Azure SQL server.
* Alle verbindingen met Azure RemoteApp vindt plaats via HTTPS over het gebruik van poort 443 versleuteld Remote Desktop protocol
* Het is van meerdere gebruikers en kan worden geschaald.
* Er is een prestatieverbetering van SSMS in Hallo hebben dezelfde regio bevinden als Hallo SQL-Database.
* U kunt gebruik van Azure RemoteApp met Hallo Premium-editie van Azure Active Directory, die gebruiker activiteit rapporten controleren.
* U kunt multi-factor authentication (MFA) inschakelen.
* Toegang SSMS overal wanneer u een van de Hallo ondersteund Azure RemoteApp-clients, waaronder iOS, Android, Mac, Windows Phone en Windows-PC's.

## <a name="create-hello-azure-remoteapp-collection"></a>Hello Azure RemoteApp-verzameling maken
Hier volgen Hallo stappen toocreate uw Azure RemoteApp-collectie met SSMS:

### <a name="1-create-a-new-windows-vm-from-image"></a>1. Een nieuwe Windows VM vanaf installatiekopie maken
Gebruik Hallo 'Windows Server Remote Desktop Session Host Windows Server 2012 R2' installatiekopie van Hallo galerie toomake uw nieuwe virtuele machine.

### <a name="2-install-ssms-from-sql-express"></a>2. SSMS van SQL Express installeren
Ga op Hallo van nieuwe virtuele machine en ga toothis downloadpagina: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)

Er is een optie tooonly download SSMS. Na het downloaden, gaat u naar de installatiemap Hallo en voer Setup tooinstall SSMS.

U moet ook tooinstall SQL Server 2014 Service Pack 1. U kunt dit hier downloaden: [Microsoft SQL Server 2014 met Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)

SQL Server 2014 Service Pack 1 bevat essentiële functionaliteit voor het werken met Azure SQL Database.

### <a name="3-run-validate-script-and-sysprep"></a>3. Script uitvoeren valideren en Sysprep
Bureaublad Hallo VM is op Hallo een PowerShell-script valideren genoemd. Deze door te dubbelklikken op uitvoeren. Deze controleert dat die Hallo VM is gereed toobe gebruikt voor externe hosting van toepassingen. Als verificatie voltooid is, wordt deze gevraagd toorun sysprep - toorun kiezen deze.

Als sysprep is voltooid, wordt het Hallo VM afsluiten.

toolearn meer informatie over het maken van een Azure RemoteApp-installatiekopie, Zie: [hoe toocreate een sjabloon voor RemoteApp-installatiekopie in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)

### <a name="4-capture-image"></a>4. Installatiekopie vastleggen
Wanneer Hallo VM is gestopt, vinden in de huidige portal Hallo en vastlegt.

toolearn meer informatie over het vastleggen van een afbeelding Zie [een installatiekopie van een Windows Azure virtuele machine gemaakt met het klassieke implementatiemodel Hallo](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="5-add-tooazure-remoteapp-template-images"></a>5. RemoteApp-sjablooninstallatiekopieën tooAzure toevoegen
Hallo Azure RemoteApp-sectie van de huidige portal hello, gaat u toohello Sjablooninstallatiekopieën tabblad en klik op toevoegen. In het pop-vak hello, selecteert u 'Een installatiekopie van het importeren van de bibliotheek van uw virtuele Machines' en kies vervolgens Hallo-installatiekopie die u zojuist hebt gemaakt.

### <a name="6-create-cloud-collection"></a>6. Cloudverzameling maken
In de huidige portal Hallo, maak een nieuwe Azure RemoteApp-Cloudverzameling. Kies Hallo-Sjablooninstallatiekopie die u zojuist hebt geïmporteerd met SSMS is geïnstalleerd.

![Nieuwe cloudverzameling maken][2]

### <a name="7-publish-ssms"></a>7. Publiceren van SSMS
Op het tabblad van de nieuwe cloudverzameling, selecteer publiceren een toepassing wordt publiceren Hallo Hallo Menu Start en kies vervolgens SSMS uit Hallo-lijst.

![App publiceren][5]

### <a name="8-add-users"></a>8. Gebruikers toevoegen
U kunt op Hallo gebruikerstoegang tabblad Hallo-gebruikers die toegang toothis Azure RemoteApp-verzameling waaronder alleen SSMS selecteren.

![Gebruiker toevoegen][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a>9. Toepassing hello Azure RemoteApp-client installeren
U kunt downloaden en installeren van een Azure RemoteApp-client: [downloaden | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)

## <a name="configure-azure-sql-server"></a>Azure SQL-server configureren
Hallo is alleen configuratie is vereist is tooensure dat Azure Services voor Hallo firewall ingeschakeld. Als u deze oplossing gebruikt, hoeft niet u tooadd IP-adressen tooopen Hallo firewall. Hallo-netwerkverkeer dat is toegestaan toohello SQL Server is van andere Azure-services.

![Azure toestaan][4]

## <a name="multi-factor-authentication-mfa"></a>Multi-factor Authentication (MFA)
MFA kan specifiek voor deze toepassing worden ingeschakeld. Ga toohello op het tabblad toepassingen van uw Azure Active Directory. U vindt een vermelding voor Microsoft Azure RemoteApp. Als u deze toepassing op en configureer vervolgens, ziet u Hallo pagina hieronder waar u MFA voor deze toepassing inschakelen kunt.

![Schakel MFA in][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a>Controle van gebruikersactiviteit met Azure Active Directory Premium
Als u nog geen Azure AD Premium, hebt u tooturn Hallo deze op in de sectie licenties van uw directory. Met de Premium is ingeschakeld, kunt u gebruikers toewijzen toohello Premium niveau.

Wanneer u tooa gebruiker in uw Azure Active Directory gaat, kunt u vervolgens toohello activiteit tabblad toosee aanmelding informatie tooAzure RemoteApp gaan.

## <a name="next-steps"></a>Volgende stappen
Na het voltooien van alle Hallo bovenstaande stappen u kunt toorun hello Azure RemoteApp-client en aanmelden met een toegewezen gebruiker. U krijgt SSMS als een van uw toepassingen en u het kunt uitvoeren, zoals u zou doen als deze zijn geïnstalleerd op uw computer met toegang tooAzure SQL server.

Zie voor meer informatie over hoe toomake verbinding tooSQL Database hello, [tooSQL Database verbinding met SQL Server Management Studio en een voorbeeld T-SQL-query uitvoert](sql-database-connect-query-ssms.md).

Dat is alles wat nu. Veel plezier!

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png