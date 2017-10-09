---
title: aaaGet slag met Opslagverkenner (Preview) | Microsoft Docs
description: Azure Storage-resources beheren met Opslagverkenner (Preview)
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a>Aan de slag met Opslagverkenner (Preview)
## <a name="overview"></a>Overzicht
Azure Opslagverkenner (Preview) is een zelfstandige app waardoor u tooeasily werken met Azure Storage-gegevens op Windows-, Mac OS- en Linux. In dit artikel leert u Hallo verschillende manieren van het verbinden van uw Azure storage-accounts beheren tooand.

![Microsoft Azure Storage Explorer (voorbeeld)][15]

## <a name="prerequisites"></a>Vereisten
* [Opslagverkenner (Preview) downloaden en installeren](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a>Verbinding maken met tooa storage-account of -service
Opslagverkenner (Preview) biedt verschillende manieren tooconnect toostorage accounts. U kunt bijvoorbeeld:
* Verbinding maken met toostorage accounts die zijn gekoppeld aan uw Azure-abonnementen.
* Sluit toostorage accounts en -services die worden gedeeld van andere Azure-abonnementen.
* Verbinding maken met tooand lokale opslag beheren met behulp van hello Azure-Opslagemulator. 

Bovendien kunt u wereldwijd en nationaal werken met opslagaccounts in Azure:

* [Verbinding maken met Azure-abonnement tooan](#connect-to-an-azure-subscription): beheer opslagresources die deel uitmaken van tooyour Azure-abonnement.
* [Werken met lokale ontwikkeling storage](#work-with-local-development-storage): beheer lokale opslag met behulp van hello Azure-Opslagemulator.
* [Koppel tooexternal opslag](#attach-or-detach-an-external-storage-account): beheer opslagresources die deel uitmaken van tooanother Azure-abonnement of die onder nationale clouds voor Azure met behulp van de naam, de sleutel en de eindpunten Hallo van het opslagaccount.
* [Koppelen van een opslagaccount met behulp van een SAS](#attach-storage-account-using-sas): beheer opslagresources die deel uitmaken van tooanother Azure-abonnement met behulp van een shared access signature (SAS).
* [Een service koppelen via een SAS](#attach-service-using-sas): een specifieke opslagservice (blobcontainer, wachtrij of tabel) die deel uitmaakt van tooanother Azure-abonnement met behulp van een SAS te beheren.

## <a name="connect-tooan-azure-subscription"></a>Verbinding maken met tooan Azure-abonnement
> [!NOTE]
> Als u geen Azure-account hebt, kunt u zich [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) of [gebruikmaken van uw voordelen als Visual Studio-abonnee](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
>
>

1. Selecteer in Storage Explorer (voorbeeld) **Azure-accountinstellingen**.

    ![Azure-accountinstellingen][0]

2. Hallo linkerdeelvenster geeft alle Hallo Microsoft-accounts die hebt aangemeld bij. tooconnect tooanother account, selecteer **account toevoegen**, en volg Hallo instructies toosign met een Microsoft-account dat is gekoppeld aan ten minste één actief Azure-abonnement.

    >[!NOTE]
    >Verbinding maken met toonational Azure (zoals Duitse Azure, Azure Government en Azure voor China via aanmelden) is momenteel niet ondersteund. Zie Hallo ' koppelen of ontkoppelen van een extern opslagaccount ' sectie voor informatie over het tooconnect toonational Azure storage-accounts.

3. Nadat u hebt aangemeld met een Microsoft-account Hallo links deelvenster is gevuld met hello Azure-abonnementen die zijn gekoppeld aan dat account. Selecteer hello Azure-abonnementen die u wilt toowork met en selecteer vervolgens **toepassen**. (Selecteren **alle abonnementen** Schakelknoppen selecteren alle of geen hello Azure-abonnementen weergegeven.)

    ![Selecteer Azure-abonnementen][3]  
    Hallo linkerdeelvenster geeft Hallo storage-accounts die zijn gekoppeld aan Azure-abonnementen Hallo geselecteerd.

    ![Geselecteerde Azure-abonnementen][4]

## <a name="connect-tooan-azure-stack-subscription"></a>Verbinding maken met tooan Stack Azure-abonnement

Zie voor informatie over verbinding tooan Stack Azure-abonnement [Opslagverkenner verbinding tooan Stack Azure-abonnement](azure-stack/azure-stack-storage-connect-se.md).

## <a name="work-with-local-development-storage"></a>Werken met lokale ontwikkelingsopslag
Met Opslagverkenner (Preview) kunt u werken met lokale opslag met behulp van hello Azure-Opslagemulator. Deze aanpak kunt u code schrijven tegen en test opslag schrijven zonder dat hiervoor een opslagaccount dat is geïmplementeerd in Azure, omdat het Hallo-opslagaccount wordt gesimuleerd door hello Azure-Opslagemulator.

> [!NOTE]
> Hello Azure-Opslagemulator wordt momenteel alleen ondersteund voor Windows.
>
>

1. Vouw in het linkerdeelvenster van Opslagverkenner (Preview) hello, Hallo **(lokaal en Attached)** > **Opslagaccounts** > **(ontwikkeling)** knooppunt.

    ![Node lokale ontwikkeling][21]

2. Als u hello Azure-Opslagemulator nog niet hebt geïnstalleerd, bent u na vragen aan gebruiker toodo geval via de informatiebalk. Als Hallo informatiebalk wordt weergegeven, selecteert u **downloaden Hallo meest recente versie**, en installeer vervolgens Hallo-emulator.

    ![Azure Storage-emulator prompt downloaden][22]

3. Nadat het Hallo-emulator is geïnstalleerd, kunt u maken en werken met lokale blobs, wachtrijen en tabellen. toolearn hoe toowork met elk opslagaccount typt, Zie een van de volgende Hallo:

    * [Resources voor Azure Blob Storage beheren](vs-azure-tools-storage-explorer-blobs.md)
    * Opslagresources voor het delen van Azure-bestanden beheren: *binnenkort beschikbaar*
    * Resources voor Azure Queue Storage beheren: *binnenkort beschikbaar*
    * Resources voor Azure Table Storage beheren: *binnenkort beschikbaar*

## <a name="attach-or-detach-an-external-storage-account"></a>Koppelen aan een extern opslagaccount of de koppeling opheffen
Met Opslagverkenner (Preview) kunt u tooexternal storage-accounts koppelen zodat storage-accounts kunnen eenvoudig worden gedeeld. Deze sectie wordt uitgelegd hoe tooattach too(and detach from) externe opslagaccounts.

### <a name="get-hello-storage-account-credentials"></a>Hallo opslagaccountreferenties ophalen
tooshare een extern opslagaccount, Hallo eigenaar van het account moet zich eerst Hallo referenties (accountnaam en -sleutel) niet ophalen voor Hallo-account en daarna die informatie delen met Hallo persoon die wil tooattach toothat (externe) account. Hallo opslagaccountreferenties via hello Azure-portal kunt u verkrijgen door Hallo volgende te doen:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).

2. Selecteer **Bladeren**.

3. Selecteer **Opslagaccounts**.

4. Op Hallo **Opslagaccounts** blade, selecteer Hallo gewenst storage-account.

5. Op Hallo **instellingen** blade voor Hallo storage-account geselecteerd, selecteert u **toegangssleutels**.

    ![Optie Toegangssleutels][5]

6. Op Hallo **toegangssleutels** blade, kopie Hallo **opslagaccountnaam** en **key1** waarden voor gebruik bij het toohello storage-account koppelen.

    ![Toegangssleutels][6]

### <a name="attach-tooan-external-storage-account"></a>Het externe opslagaccount tooan koppelen
tooattach tooan externe storage-account, moet u de naam en sleutel van het Hallo-account. Hallo 'Get Hallo opslagaccountreferenties' sectie wordt uitgelegd hoe deze waarden van tooobtain hello Azure-portal. Echter Hallo accountsleutel in Hallo-portal wordt aangeroepen **key1**. Dus wanneer Opslagverkenner (Preview) om een accountsleutel wordt gevraagd, u Voer Hallo **key1** waarde.

1. Selecteer in Opslagverkenner (Preview) **tooAzure opslag koppelt**.

    ![Verbinding maken met de opslagoptie tooAzure][23]

2. In Hallo **tooAzure opslag verbinding** dialoogvenster geeft u de accountsleutel hello (Hallo **key1** waarde van hello Azure-portal), en selecteer vervolgens **volgende**.

    > [!NOTE]
    > U kunt Hallo-verbindingsreeks voor opslag van een opslagaccount op nationale Azure invoeren. Bijvoorbeeld, voer tooconnect tooAzure Duitsland storage-accounts, verbinding tekenreeksen vergelijkbare toohello volgende in: 
    >
    >* DefaultEndpointsProtocol=https
    >* AccountName=cawatest03
    >* AccountKey=<storage_account_key>
    >* EndpointSuffix=core.cloudapi.de
    
    >U kunt Hallo-verbindingsreeks ophalen van hello Azure portal in Hallo dezelfde manier zoals beschreven in Hallo sectie 'Hello opslagaccountreferenties ophalen'.

    ![Verbinding maken in het dialoogvenster tooAzure-opslag][24]

3. In Hallo **externe opslag koppelen** dialoogvenster in Hallo **accountnaam** vak, voer opslagaccountnaam hello, geef de gewenste instellingen en selecteer vervolgens **volgende**.

    ![Dialoogvenster Externe opslag koppelen][8]

4. In Hallo **verbinding samenvatting** dialoogvenster of Hallo informatie. Als u alles toochange wilt, schakelt u **terug** en voer deze opnieuw Hallo gewenste instellingen. 

5. Selecteer **Verbinden**.

6. Nadat deze is verbonden, Hallo externe opslagaccount weergegeven met **(extern)** toohello opslagaccountnaam toegevoegd.

    ![Resultaat van het verbinden van externe tooan-opslagaccount][9]

### <a name="detach-from-an-external-storage-account"></a>De koppeling met een extern opslagaccount opheffen
1. Met de rechtermuisknop op het externe opslagaccount hello wilt toodetach en selecteer vervolgens **Detach**.

    ![Loskoppelen van de opslagoptie][10]

2. Selecteer in het bevestigingsbericht hello, **Ja** tooconfirm Hallo loskoppelen van het externe opslagaccount Hallo.

## <a name="attach-a-storage-account-by-using-an-sas"></a>Een opslagaccount koppelen met behulp van een SAS
Een [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) kunt Hallo beheerder van een Azure-abonnement tijdelijke toegang tooa opslagaccount verlenen zonder tooprovide Azure-abonnementsreferenties.

tooillustrate dit scenario, laten we zeggen dat GebruikerA is een beheerder van een Azure-abonnement en gebruiker a wil tooallow gebruiker b tooaccess een opslag-account voor een beperkte tijd met bepaalde machtigingen:

1. Gebruiker a genereert een SAS (bestaande uit Hallo-verbindingsreeks voor Hallo storage-account) voor een bepaald tijdstip en met Hallo gewenst machtigingen.

2. Gebruiker a shares Hallo SAS met Hallo persoon (in ons voorbeeld gebruiker b) die toegang toohello storage-account willen.  

3. Gebruiker b gebruikt Opslagverkenner (Preview) tooattach toohello account die deel uitmaakt van tooUserA met behulp van Hallo opgegeven SAS.

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a>Een SAS ophalen voor de gewenste tooshare Hallo-account
1. In Opslagverkenner (Preview) met de rechtermuisknop op Hallo storage-account u wilt delen, en selecteer vervolgens **Shared Access Signature ophalen**.

    ![Optie SAS-contextmenu ophalen][13]

2. In Hallo **Shared Access Signature** dialoogvenster geeft u de Hallo tijdsbestek en machtigingen die u wilt voor Hallo-account en selecteer vervolgens **maken**.

    ![Dialoogvenster SAS ophalen][14]  
    Hallo **Shared Access Signature** in het dialoogvenster wordt geopend en Hallo SAS.

3. Volgende toohello **verbindingsreeks**, selecteer **kopie** toocopy het toohello Klembord, en selecteer vervolgens **sluiten**.

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a>Toohello gedeeld account koppelen via SAS Hallo
1. Selecteer in Opslagverkenner (Preview) **tooAzure opslag koppelt**.

    ![Verbinding maken met de opslagoptie tooAzure][23]

2. In Hallo **tooAzure opslag verbinding** in het dialoogvenster verbindingsreeks Hallo opgeven en selecteer vervolgens **volgende**.

    ![Verbinding maken in het dialoogvenster tooAzure-opslag][24]

3. In Hallo **verbinding samenvatting** dialoogvenster of Hallo informatie. toomake gewijzigd, schakelt u **terug**, en voer vervolgens de gewenste Hallo-instellingen. 

4. Selecteer **Verbinden**.

5. Nadat deze is gekoppeld, Hallo opslagaccount weergegeven met **(SAS)** toegevoegd toohello accountnaam op die u hebt opgegeven.

    ![Resultaat van het account van de gekoppelde tooan via SAS][17]

## <a name="attach-a-service-by-using-an-sas"></a>Een service koppelen met behulp van een SAS
Hallo 'Storage-account koppelen via een SAS' sectie wordt uitgelegd hoe de beheerder van een Azure-abonnement tijdelijke toegang tooa storage-account kunt verlenen door te genereren en delen van een SAS voor Hallo storage-account. Op deze manier kunt u ook een SAS genereren voor een bepaalde service (blobcontainer, wachtrij of tabel) binnen een opslagaccount.  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a>Een SAS voor Hallo-service die u wilt dat tooshare genereren
In deze context is een service een blobcontainer, een wachtrij of een tabel. toogenerate hello SAS voor een vermelde service, Zie:

* [Hallo SAS ophalen voor een blob-container](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* Hallo SAS ophalen voor een bestandsshare: *binnenkort beschikbaar*
* Hallo SAS ophalen voor een wachtrij: *binnenkort beschikbaar*
* Hallo SAS ophalen voor een tabel: *binnenkort beschikbaar*

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a>Service met behulp van Hallo SAS toohello gedeeld-account koppelen
1. Selecteer in Opslagverkenner (Preview) **tooAzure opslag koppelt**.

    ![Verbinding maken met de opslagoptie tooAzure][23]

2. In Hallo **tooAzure opslag verbinding** in het dialoogvenster Hallo SAS-URI opgeven en selecteer vervolgens **volgende**.

    ![Verbinding maken in het dialoogvenster tooAzure-opslag][24]

3. In Hallo **verbinding samenvatting** dialoogvenster of Hallo informatie. toomake gewijzigd, schakelt u **terug**, en voer vervolgens de gewenste Hallo-instellingen. 

4. Selecteer **Verbinden**.

5. Nadat deze is gekoppeld, hello zojuist gekoppelde service wordt weergegeven onder Hallo **(Service-SAS)** knooppunt.

    ![Resultaat van het koppelen van tooa shared service met behulp van een SAS][20]

## <a name="search-for-storage-accounts"></a>Zoeken naar opslagaccounts
Als u een lange lijst met opslagaccounts hebt, is een toolocate snel bepaalde opslagaccounts toouse Hallo zoekvak Hallo boven aan het linkerdeelvenster Hallo.

Terwijl u in het zoekvak hello typt, linkerdeelvenster Hallo geeft Hallo storage-accounts die overeenkomen met de Hallo zoekwaarde die u hebt ingevoerd toothat punt. Bijvoorbeeld, een zoekopdracht voor alle opslagaccounts waarvan de naam bevat **tarcher** wordt weergegeven in de volgende schermafbeelding Hallo:

![Zoeken naar Storage-account][11]

## <a name="next-steps"></a>Volgende stappen
* [Azure Blob Storage-resources beheren met Opslagverkenner (Preview)](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
