---
title: aaaRun een Windows-app op elk apparaat met Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe tooshare een Windows-app met uw gebruikers met behulp van Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 961d40ca-9673-4977-aa54-d6b22fc61ce1
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 750f3b881e0cb671ff6e8f3e851bccdf2262d156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-any-windows-app-on-any-device-with-azure-remoteapp"></a>Een Windows-app op elk apparaat uitvoeren met Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

U kunt een Windows-toepassing overal en op elk apparaat uitvoeren, gewoon met Azure RemoteApp. Of een aangepaste toepassing die tien jaar geleden geschreven of een Office-app, wordt niet langer gebonden toobe tooa specifiek besturingssysteem (zoals Windows XP) voor die paar toepassingen in uw gebruikers hebben.

Met Azure RemoteApp kunnen uw gebruikers kunnen ook hun eigen Android gebruiken of Apple-apparaten en get Hallo dezelfde ervaring krijgen als op Windows (of op een Windows Phone). Dit wordt bereikt door het hosten van uw Windows-toepassing in een verzameling van virtuele machines in Windows Azure: uw gebruikers hebben toegang vanaf elke locatie waar ze een internetverbinding hebben. 

Lees verder voor een voorbeeld van precies hoe toodo dit.

In dit artikel gaan we tooshare toegang met alle gebruikers. U kunt echter ELKE willekeurige app gebruiken. Als u uw app op een computer met Windows Server 2012 R2 installeren kunt, kunt u met behulp van de onderstaande stappen voor Hallo delen. U kunt bekijken Hallo [appvereisten](remoteapp-appreqs.md) toomake ervoor dat uw app werkt.

Neem notitie dat omdat toegang een database is en we willen dat die database toobe nuttig, we gaan doen een paar extra stappen toolet gebruikers toegang krijgen tot Hallo toegang tot gegevens delen. Als uw app geen database, of u niet uw gebruikers toobe kunnen tooaccess een bestandsshare hoeft, kunt u deze stappen in deze zelfstudie overslaan

> [!NOTE]
> <a name="note"></a>U moet een Azure-account toocomplete in deze zelfstudie:
> 
> * U kunt [gratis een Azure-account openen](https://azure.microsoft.com/free/?WT.mc_id=A261C142F): U ontvangt tegoed kunt u tootry uit betaalde Azure-services en zelfs nadat ze allemaal hebt gebruikt kunt u maximaal Hallo account houden en gebruik gratis Azure-services, zoals Websites. Uw creditcard wordt nooit worden in rekening gebracht, tenzij u expliciet de instellingen wijzigen en vraag toobe in rekening gebracht.
> * U kunt [de voordelen voor MSDN-abonnees activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): via uw MSDN-abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.
> 
> 

## <a name="create-a-collection-in-remoteapp"></a>Een verzameling maken in RemoteApp
Eerst maakt u een verzameling. Hallo verzameling fungeert als een container voor uw apps en gebruikers. Elke verzameling is gebaseerd op een installatiekopie: u kunt uw eigen installatiekopie maken of de installatiekopie gebruiken die deel uitmaakt van uw abonnement. We maken gebruik van Hallo Office 2013-proefabonnement installatiekopie - Hallo app willen we tooshare bevat voor deze zelfstudie.

1. In hello Azure-portal, schuif omlaag in de navigatiestructuur aan de linkerkant Hallo tot u RemoteApp ziet. Open die pagina.
2. Klik op **Een RemoteApp-verzameling maken**.
3. Klik op **Snelle invoer** en voer een naam in voor uw verzameling.
4. Selecteer Hallo regio toouse toocreate uw verzameling. Selecteer voor de beste ervaring Hallo Hallo regio die het dichtst geografisch toohello locatie waar uw gebruikers toegang hebben tot Hallo-app. Bijvoorbeeld: in deze zelfstudie Hallo gebruikers worden bevindt zich in Redmond, Washington. Hallo dichtstbijzijnde Azure-regio is **VS-West**.
5. Hallo-abonnement dat u toouse wilt selecteren. Hallo een basisabonnement omvat 16 gebruikers op een grote virtuele machine van Azure, terwijl het standaardabonnement Hallo 10 gebruikers op een grote virtuele machine in Azure heeft. Hallo-basisabonnement zeer als voorbeeld van een algemene geschikt voor gegevens invoertype werkstroom. Voor een productiviteits-app, zoals Office, kunt u Hallo standaard-plan.
6. Ten slotte selecteert Hallo Office 2013 Professional installatiekopie. Deze installatiekopie bevat Office 2013-apps. Vergeet echter niet dat deze installatiekopie alleen geschikt is voor proefverzamelingen en POC’s. U kunt deze installatiekopie niet gebruiken in een productieverzameling.
7. Klik nu op **Een RemoteApp-verzameling maken**.

![Een cloudverzameling maken in RemoteApp](./media/remoteapp-anyapp/ra-anyappcreatecollection.png)

Hiermee wordt gestart met het maken van de verzameling, maar het tooan uur kan duren.

Nu u bent klaar tooadd uw gebruikers.

## <a name="share-hello-app-with-users"></a>Hallo-app voor delen met gebruikers
Zodra uw verzameling is gemaakt, is de tijd toopublish toegang toousers en Hallo gebruikers toevoegen die tooit toegang moeten hebben.

Als u weggegaan hello Azure RemoteApp-knooppunt terwijl Hallo verzameling werd gemaakt, start u door het maken van uw back-tooit vanaf de startpagina van Azure Hallo manier.

1. Klik op Hallo-verzameling die u hebt de aanvullende opties voor eerdere tooaccess gemaakt en Hallo verzameling configureren.
   ![Een nieuwe RemoteApp-cloudverzameling](./media/remoteapp-anyapp/ra-anyappcollection.png)
2. Op Hallo **Publishing** tabblad **publiceren** onderin Hallo Hallo scherm en klik vervolgens op **programma's van het menu Start publiceren**.
   ![Een RemoteApp-programma publiceren](./media/remoteapp-anyapp/ra-anyapppublish.png)
3. Hallo-apps die u toopublish uit de lijst hello wilt selecteren. In dit geval kiest u Access. Klik op **Voltooien**. Wachten op Hallo apps toofinish publiceren.
   ![Access publiceren in RemoteApp](./media/remoteapp-anyapp/ra-anyapppublishaccess.png)
4. Zodra het Hallo-app is gepubliceerd, Ga toohello **gebruikerstoegang** tabblad tooadd alle Hallo-gebruikers die toegang moeten hebben tot tooyour apps. Voer gebruikersnamen (e-mailadressen) voor uw gebruikers in en klik vervolgens op **Opslaan**.

![Gebruikers tooRemoteApp toevoegen](./media/remoteapp-anyapp/ra-anyappaddusers.png)

1. Nu is tijd tootell uw gebruikers over deze nieuwe apps en hoe tooaccess ze. toodo, uw gebruikers een e-mail te sturen toohello extern bureaublad-client download-URL te sturen.
   ![Hallo clientdownload-URL voor RemoteApp](./media/remoteapp-anyapp/ra-anyappurl.png)

## <a name="configure-access-tooaccess"></a>Toegang tooAccess configureren
Sommige apps hebben nog extra configuratie nodig nadat u ze via RemoteApp hebt geïmplementeerd. In het bijzonder voor toegang tot we continu toocreate een bestandsshare op Azure waartoe een gebruiker toegang heeft. (Als u toodo niet wilt, kunt u een [hybride verzameling](remoteapp-create-hybrid-deployment.md) [in plaats van onze cloudverzameling waarmee uw gebruikers toegang tot bestanden en gegevens op uw lokale netwerk.) Vervolgens moet u tootell onze gebruikers toomap een lokaal station op hun computer toohello Azure-bestandssysteem.

Hallo eerste deel u als Hallo beheerder doet. Vervolgens hebben we een aantal stappen voor uw gebruikers.

1. Start publishing Hallo opdrachtregelinterface (cmd.exe). In Hallo **Publishing** tabblad **cmd**, en klik vervolgens op **publiceren > programma publiceren met behulp van pad**.
2. Voer Hallo-naam van het Hallo-app en het Hallo-pad. Gebruik 'Verkenner' als Hallo naam en '% SYSTEMDRIVE%\windows\explorer.exe' als Hallo pad voor onze doel.
   ![Hallo cmd.exe bestand publiceren.](./media/remoteapp-anyapp/ra-publishcmd.png)
3. Nu u een Azure toocreate moet [opslagaccount](../storage/common/storage-create-storage-account.md). We hebben die van ons 'accessstorage ' genoemd, met de naam dus kies een naam die zinvol tooyou. (toomisquote Highlander, kunnen er slechts één 'accessstorage.') ![Ons Azure storage-account](./media/remoteapp-anyapp/ra-anyappazurestorage.png)
4. Nu gaat u terug tooyour dashboard zodat u Hallo pad tooyour opslag (eindpuntlocatie krijgt). U gaat dit straks gebruiken, dus kopieer het ergens.
   ![Hallo-opslagpad account](./media/remoteapp-anyapp/ra-anyappstoragelocation.png)
5. Als Hallo storage-account is gemaakt, moet u vervolgens de primaire toegangssleutel Hallo. Klik op **toegangssleutels beheren**, en vervolgens kopiëren Hallo primaire toegangssleutel.
6. Nu Hallo context van Hallo storage-account instellen en een nieuwe bestandsshare maken om toegang te krijgen. Voer Hallo na cmdlets in een Windows PowerShell-venster met verhoogde bevoegdheid:
   
        $ctx=New-AzureStorageContext <account name> <account key>
        $s = New-AzureStorageShare <share name> -Context $ctx
   
    Voor onze share zijn deze dus Hallo cmdlets uitgevoerd:
   
        $ctx=New-AzureStorageContext accessstorage <key>
        $s = New-AzureStorageShare <share name> -Context $ctx

Nu het Hallo gebruiker aan zet's. Laat uw gebruikers eerst een [RemoteApp-client](remoteapp-clients.md) installeren. Vervolgens Hallo gebruikers moeten toomap een station van hun account toothat Azure-bestand delen dat u hebt gemaakt en hun Access-bestanden toevoegen. Dit doen ze als volgt:

1. Hallo RemoteApp-client toegang Hallo gepubliceerde apps. Start Hallo cmd.exe programma.
2. Voer Hallo opdracht toomap na een station vanaf uw computer toohello-bestandsshare:
   
        net use z: \\<accountname>.file.core.windows.net\<share name> /u:<user name> <account key>
   
    Als u Hallo instelt **/ persistent** parameter tooyes, hello toegewezen station wordt behouden over de sessies.
3. Start nu Hallo Verkenner-app vanuit RemoteApp. Toegang tot bestanden die u toouse in Hallo gedeelde app toohello bestandsshare wilt kopiëren.
   ![Access-bestanden in een Azure-share zetten](./media/remoteapp-anyapp/ra-anyappuseraccess.png)
4. Tot slot opent u Access en open vervolgens Hallo-database die u zojuist hebt gedeeld. Hier ziet u uw gegevens in Access uitgevoerd vanuit de cloud Hallo.
   ![Een echte Access-database uit Hallo cloud](./media/remoteapp-anyapp/ra-anyapprunningaccess.png)

Nu kunt u Access op al uw apparaten gebruiken, maar zorg er wel voor dat u een RemoteApp-client installeert.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Volgende stappen
Nu u hebt geleerd hoe een verzameling maakt, kunt u proberen een [verzameling te maken die gebruikmaakt van Office 365](remoteapp-tutorial-o365anywhere.md). U kunt ook een [hybride verzameling](remoteapp-create-hybrid-deployment.md) maken die toegang heeft tot uw lokale netwerk.

<!--Image references-->

