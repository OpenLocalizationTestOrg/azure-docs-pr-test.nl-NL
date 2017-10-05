---
title: Verbinding maken met SQL Database met SQL Server Management Studio in Azure RemoteApp | Microsoft Docs
description: Gebruik deze handleiding om meer informatie over het SQL Server Management Studio in Azure RemoteApp voor beveiliging en prestaties wordt gebruikt om verbinding te maken met SQL-Database
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
ms.openlocfilehash: ae1f2fa38d38fe6c10bc7960fddb07ae330d1eeb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-to-connect-to-sql-database"></a>SQL Server Management Studio in Azure RemoteApp gebruiken voor verbinding met SQL-Database

> [!IMPORTANT]
> Azure RemoteApp wordt buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
>

## <a name="introduction"></a>Inleiding
Deze zelfstudie laat zien hoe u verbinding maken met SQL Database met SQL Server Management Studio (SSMS) in Azure RemoteApp. Deze begeleidt u bij het proces voor het instellen van SQL Server Management Studio in Azure RemoteApp, worden de voordelen en toont beveiligingsfuncties die u kunt gebruiken in Azure Active Directory.

**Geschatte duur:** 45 minuten

## <a name="ssms-in-azure-remoteapp"></a>SSMS in Azure RemoteApp
Azure RemoteApp is een RDS-service in Azure die toepassingen levert. Meer informatie over deze hier: [wat is RemoteApp?](../remoteapp/remoteapp-whatis.md)

SSMS uitgevoerd in Azure RemoteApp biedt u dezelfde ervaring als SSMS lokaal uitgevoerd.

![Schermopname van SSMS uitgevoerd in Azure RemoteApp][1]

## <a name="benefits"></a>Voordelen
Er zijn veel voordelen voor het gebruik van SSMS in Azure RemoteApp, met inbegrip van:

* Poort 1433 op Azure SQL-server heeft geen extern (buiten Azure) worden weergegeven.
* U hoeft te houden toevoegen en verwijderen van IP-adressen in de Azure SQL server-firewall.
* Alle verbindingen met Azure RemoteApp vindt plaats via HTTPS over het gebruik van poort 443 versleuteld Remote Desktop protocol
* Het is van meerdere gebruikers en kan worden geschaald.
* Er is een prestatieverbetering van SSMS hebben in dezelfde regio bevinden als de SQL-Database.
* U kunt gebruik van Azure RemoteApp met de Premium-editie van Azure Active Directory, die gebruiker activiteit rapporten controleren.
* U kunt multi-factor authentication (MFA) inschakelen.
* Toegang SSMS overal wanneer u een van de ondersteunde Azure RemoteApp-clients, waaronder iOS, Android, Mac, Windows Phone en Windows-PC's.

## <a name="create-the-azure-remoteapp-collection"></a>De Azure RemoteApp-verzameling maken
Hier volgen de stappen voor het maken van uw Azure RemoteApp-collectie met SSMS:

### <a name="1-create-a-new-windows-vm-from-image"></a>1. Een nieuwe Windows VM vanaf installatiekopie maken
De installatiekopie van het 'Windows Server Remote Desktop Session Host Windows Server 2012 R2' uit de galerie gebruiken om uw nieuwe virtuele machine.

### <a name="2-install-ssms-from-sql-express"></a>2. SSMS van SQL Express installeren
Ga naar de nieuwe virtuele machine en navigeer naar deze downloadpagina: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)

Er is een optie voor het downloaden van alleen SSMS. Na het downloaden, gaat u naar de installatiemap en voer Setup voor de installatie van SSMS.

U moet ook SQL Server 2014 Service Pack 1 installeert. U kunt dit hier downloaden: [Microsoft SQL Server 2014 met Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)

SQL Server 2014 Service Pack 1 bevat essentiële functionaliteit voor het werken met Azure SQL Database.

### <a name="3-run-validate-script-and-sysprep"></a>3. Script uitvoeren valideren en Sysprep
Op het bureaublad van de virtuele machine wordt een PowerShell-script valideren genoemd. Deze door te dubbelklikken op uitvoeren. Er wordt gecontroleerd dat de virtuele machine gereed om te worden gebruikt is voor externe hosting van toepassingen. Als verificatie voltooid is, wordt u gevraagd naar voert u sysprep - kiezen uit te voeren.

Wanneer sysprep is voltooid, wordt deze de virtuele machine afgesloten.

Zie voor meer informatie over het maken van een Azure RemoteApp-installatiekopie: [een RemoteApp-sjablooninstallatiekopie maken in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)

### <a name="4-capture-image"></a>4. Installatiekopie vastleggen
Wanneer de virtuele machine is gestopt, vindt het in de huidige portal en vastlegt.

Zie voor meer informatie over het vastleggen van een installatiekopie, [een installatiekopie van een Windows Azure virtuele machine gemaakt met het klassieke implementatiemodel](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="5-add-to-azure-remoteapp-template-images"></a>5. Toevoegen aan Azure RemoteApp-sjablooninstallatiekopieën
In de Azure RemoteApp-sectie van de huidige portal, gaat u naar het tabblad installatiekopieën van de sjabloon en klikt u op toevoegen. Selecteer 'Een afbeelding van uw virtuele Machines bibliotheek importeren' in het pop- en kies vervolgens de installatiekopie die u zojuist hebt gemaakt.

### <a name="6-create-cloud-collection"></a>6. Cloudverzameling maken
Maak een nieuwe Azure RemoteApp-Cloudverzameling in de huidige portal. Kies de Sjablooninstallatiekopie die u zojuist hebt geïmporteerd met SSMS is geïnstalleerd.

![Nieuwe cloudverzameling maken][2]

### <a name="7-publish-ssms"></a>7. Publiceren van SSMS
Op de publicatie tabblad van uw nieuwe cloudverzameling, selecteer een toepassing in het Menu Start publiceren en kies vervolgens SSMS in de lijst.

![App publiceren][5]

### <a name="8-add-users"></a>8. Gebruikers toevoegen
U kunt de gebruikers die toegang hebben tot deze Azure RemoteApp-collectie waaronder alleen SSMS selecteren op het tabblad gebruikerstoegang.

![Gebruiker toevoegen][6]

### <a name="9-install-the-azure-remoteapp-client-application"></a>9. De toepassing Azure RemoteApp-client installeren
U kunt downloaden en installeren van een Azure RemoteApp-client: [downloaden | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)

## <a name="configure-azure-sql-server"></a>Azure SQL-server configureren
De enige configuratie nodig is om ervoor te zorgen dat Azure Services voor de firewall is ingeschakeld. Als u deze oplossing gebruikt, vervolgens hoeft niet u voor het toevoegen van IP-adressen om de firewall te openen. Het netwerkverkeer dat is toegestaan voor de SQL Server is van andere Azure-services.

![Azure toestaan][4]

## <a name="multi-factor-authentication-mfa"></a>Multi-factor Authentication (MFA)
MFA kan specifiek voor deze toepassing worden ingeschakeld. Ga naar het tabblad toepassingen van uw Azure Active Directory. U vindt een vermelding voor Microsoft Azure RemoteApp. Als u deze toepassing op en configureer vervolgens, ziet u de pagina waar u MFA voor deze toepassing inschakelen kunt.

![Schakel MFA in][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a>Controle van gebruikersactiviteit met Azure Active Directory Premium
Als u geen Azure AD Premium, hebt u inschakelen in de sectie licenties van uw directory. Met Premium is ingeschakeld, kunt u gebruikers toewijzen aan het Premium-niveau.

Wanneer u naar een gebruiker in uw Azure Active Directory gaat, kunt u vervolgens naar het tabblad activiteit om te zien van aanmeldingsgegevens naar Azure RemoteApp gaan.

## <a name="next-steps"></a>Volgende stappen
Na het voltooien van de bovenstaande stappen, zult u de Azure RemoteApp-client uitvoeren en het aanmelden met een toegewezen gebruiker. U krijgt SSMS als een van uw toepassingen en u het kunt uitvoeren, zoals u zou doen als deze zijn geïnstalleerd op uw computer met toegang tot Azure SQL-server.

Zie voor meer informatie over het maken van de verbinding met SQL Database [verbinding maken met SQL Database met SQL Server Management Studio en een voorbeeld T-SQL-query uit te voeren](sql-database-connect-query-ssms.md).

Dat is alles wat nu. Veel plezier!

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png