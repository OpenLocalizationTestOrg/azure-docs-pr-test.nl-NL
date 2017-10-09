---
title: aaaHow toouse uw Office 365-abonnement met Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe u uw Office 365-abonnement in Azure RemoteApp tooshare Office-apps kunt gebruiken.
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: f82b6e23-2b71-47be-846d-fd93f2652f3c
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2648868dd28cbcd93e38461ae6dce25eaa5d5e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-your-office-365-subscription-with-azure-remoteapp"></a>Hoe toouse uw Office 365-abonnement met Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Wist u dat u kunt uw bestaande Office 365-abonnement in Azure RemoteApp tooshare Office-apps vanuit de cloud hello gebruiken? Lees verder voor meer informatie over uw Office 365 + Azure RemoteApp-opties, inclusief koppelingen tooarticles over Office 365 die u helpen ervoor meest Hallo van uw abonnement.

## <a name="how-do-i-use-office-365-accounts-for-azure-remoteapp"></a>Hoe gebruik ik Office 365-accounts voor Azure RemoteApp?
Bekijk Peter van nieuw artikel voor alle informatie Hallo: [hoe toouse Azure RemoteApp met Office 365-gebruikersaccounts](remoteapp-o365user.md)

## <a name="can-i-use-my-office-365-subscription-toorun-office-applications-in-azure-remoteapp"></a>Kan ik mijn Office-toepassingen van Office 365-abonnement toorun gebruiken in Azure RemoteApp?
Ja. In feite is met behulp van uw Office 365-abonnement Hallo alleen manier toobring uw Office-toepassingen tooAzure RemoteApp.

(Opmerking: als uw Azure RemoteApp-implementatie wordt geleverd door een partner hosting, ze mogelijk kunnen tooprovide u met Office-licenties op basis van een [Service Provider Licensing Agreement](http://www.microsoft.com/en-us/Licensing/licensing-programs/spla-program.aspx))

Hallo aardige van uw Office 365-abonnement is dat deze kunt u gebruiken Hallo dezelfde gebruikerslicentie op tal van verschillende platforms en omgevingen, inclusief hello Azure-cloud. Als u Office-toepassingen in Azure RemoteApp gebruikt geen u toopurchase extra licenties nodig of uw licenties te configureren op een speciale manier. Hoeft u een Office 365-abonnement inclusief [Office 365 ProPlus](https://technet.microsoft.com/library/Gg702619.aspx).

Office 365 ProPlus schakelt [gedeelde computeractivering](https://technet.microsoft.com/library/Dn782860.aspx) - met deze functie kunt u tijdelijk op basis van gebruikers activering voor Office in virtuele en cloudomgevingen zoals Azure RemoteApp (en extern bureaublad-Services).

Welke Office 365-abonnementen Office 365 ProPlus opnemen? Bekijk Hallo [Service-beschikbaarheid binnen elk plan](https://technet.microsoft.com/library/office-365-plan-options.aspx) tabel. Houd er rekening mee dat niet alle abonnementen Office 365 ProPlus (bijvoorbeeld Hallo Office 365 Business plan) bevatten. Als uw plan niet ondersteunt, kunt u overwegen tooa-plan dat (bijvoorbeeld Office 365 Education E3 is).

## <a name="ok-so-how-are-my-office-365-proplus-licenses-used-with-azure-remoteapp"></a>OK hoe worden mijn Office 365 ProPlus licenties die worden gebruikt met Azure RemoteApp?
Elke gebruikerslicentie voor Office 365 ProPlus kunt één gebruiker Office-toepassingen op up too5 computers plus tablets en telefoons activeren. Elke activering is geregistreerd bij Hallo gebruiker totdat ze Office op Hallo-apparaat deactiveren. (Gebruikers kunnen hun apparaten in Hallo beheren [Office 365-portal](https://portal.office365.com/).)

Met Azure RemoteApp één gebruiker kan zich aanmelden bij verschillende computers op Hallo dezelfde dag gerust. Dat komt doordat het Hallo-service automatisch beheert en bronnen in de cloud hello, schaalt terwijl Hallo gebruiker ziet alleen Hallo apps en programma's die u hebt gedeeld. Voor dit scenario Office 365 ProPlus een gedeelde computer activering modus biedt: dit betekent dat gebruikers niet toodo moet een licentie management tooaccess die bronnen en dat afzonderlijke computers Hallo niet meegeteld activeringslimiet Hallo 5-computer.

Als u (Hallo beheerder) Office 365 ProPlus licenties tooyour gebruikers toewijst, kunnen ze Office gebruiken op hun persoonlijke apparaten, evenals via uw Azure RemoteApp-collectie.

## <a name="which-office-applications-can-i-use-with-office-365-and-azure-remoteapp"></a>Welke Office-toepassingen kan ik gebruiken met Office 365 en Azure RemoteApp?
U kunt uw Office 365-abonnement tooactivate gebruiken en delen van Office 2013 in Azure RemoteApp-implementaties. We ondersteunen momenteel geen Hallo gebruik van andere versies van Office met Azure RemoteApp. Dit omvat Office 2003, Office 2007, Office 2010 en Office 2016.

## <a name="what-about-visio-pro-or-project-pro"></a>Wat over Visio Pro en Project Pro?
Hallo Office 365 ProPlus-installatiekopie opnemen in uw RemoteApp-abonnement omvat zowel Visio Pro en Project Pro. Maar u deze programma's niet gebruiken voor uw Office 365 ProPlus-abonnement tooactivate - deze hebben elk een eigen licentie. U kunt deze activeren in Hallo [Office 365-portal](https://portal.office365.com/). 

U hebt geen toolicense deze programma's als u niet toouse wilt ze. Alleen activeren Hallo programma's die u wilt dat toouse - overslaan Hallo anderen. Nog steeds ziet u ze in Hallo-installatiekopie, maar u deze niet gebruiken. 

## <a name="how-do-i-get-started-with-office-365-and-azure-remoteapp"></a>Hoe ga ik aan de slag met Office 365 en Azure RemoteApp?
Nu dat u Hallo details weet van het Office 365-licentieverlening, krijgen we u aan de slag met Azure RemoteApp - het is heel eenvoudig:

Wanneer u uw Azure RemoteApp-collectie maakt, gebruikt u Hallo **Office 365 ProPlus (abonnement vereist)** installatiekopie.

![Azure RemoteApp-installatiekopie met de Office 365 Pro Plus](./media/remoteapp-officesubscription/remoteapp-officeimage.png)

Deze installatiekopie bevat de meest recente versie van Windows Server en Office 365 ProPlus Hallo. Nadat u uw verzameling (inclusief publishing apps), uw gebruikers gewoon configureren Meld u aan bij Azure RemoteApp (met behulp van de RemoteApp-client) en hun Office 365-referenties opgeven voor alle Office-apps. Licenties worden automatisch geleverd zonder een set up of management is vereist.

## <a name="can-i-create-a-custom-image-with-office-365-proplus"></a>Kan ik een aangepaste installatiekopie maken met Office 365 ProPlus?
U kunt een aangepaste installatiekopie maken voor uw verzameling met Office 365 ProPlus. Er zijn 2 keuzes: gebruik hello Azure-galerie installatiekopie we bieden of u kunt uw eigen aangepaste installatiekopie maken en er Office 365 ProPlus installeren.

### <a name="use-hello-azure-gallery-image"></a>Installatiekopie van een Azure-galerie hello gebruiken
Hallo gemakkelijkste manier toodeploy Office 365 ProPlus tooa verzameling is te[beginnen met een van de installatiekopieën van het Azure-galerie Hallo](remoteapp-image-on-azurevm.md) opgenomen in uw Azure RemoteApp-abonnement. Zorg ervoor dat u kiest Hallo **Windows Server Remote Desktop Session Host met Office 365 ProPlus vooraf geïnstalleerde** installatiekopie. Installeer alle andere apps die u wilt dat op die installatiekopie en u kunt toogo.

### <a name="use-a-custom-image"></a>Een aangepaste installatiekopie gebruiken
U kunt altijd een aangepaste installatiekopie maken - kunt u een [Azure VM](remoteapp-image-on-azurevm.md) of [lokaal Hallo installatiekopie maken](remoteapp-create-custom-image.md) en upload het tooAzure. In beide gevallen moet dat u Office 365 ProPlus met behulp van gedeelde computerknooppunt activering Hallo installeren. Gebruik Hallo [Office Deployment Tool](http://blogs.technet.com/b/odsupport/archive/2014/07/11/using-the-office-deployment-tool.aspx) en volg Hallo [instructies](https://technet.microsoft.com/library/Dn782858.aspx) voor installatie.  

### <a name="disable-automatic-updates-for-office-365-proplus-in-your-custom-image---important"></a>Het uitschakelen van automatische updates voor Office 365 ProPlus in uw aangepaste installatiekopie - belangrijk
Uw aangepaste installatiekopie wordt gebruikt door Azure RemoteApp als een sjabloon voor het toevoegen van aanvullende bronnen als Hallo vraag uit uw gebruikers toeneemt. tooprevent vertragingen en verbindingsproblemen, automatische updates niet uitschakelen voor Office in Hallo-installatiekopie. Als u dit niet doet, wordt klikt u vervolgens elke bron met die sjabloon gemaakt automatisch bijgewerkt wanneer deze wordt gestart. Gebruik in plaats daarvan Hallo standaard Azure RemoteApp-proces voor het bijwerken van uw aangepaste installatiekopie. Op die manier Hallo Office-toepassingen eenmaal op Hallo-sjablooninstallatiekopie bijwerken en vervolgens laat u Azure RemoteApp zorgt voor het ophalen van Hallo updates tooyour gebruikers.

toodisable automatische updates, toevoegen Hallo toohello Office Deployment Tool-configuratiebestand te volgen:

        <Updates Enabled="FALSE" />

Het configuratiebestand moet nu deze regels bevatten:

        <Display Level="NONE" AcceptEULA="TRUE" />
        <Property Name="SharedComputerLicensing" Value="1" />
        <Updates Enabled="FALSE" />

## <a name="so-how-can-i-update-an-image-with-office-365-proplus"></a>Hoe kan ik een afbeelding met Office 365 ProPlus bijwerken?
Er zijn veel redenen tooupdate Hallo installatiekopie in uw verzameling. Hier volgen een paar:

* Hallo laatste Windows-updates downloaden 
* Hallo laatste Office 365 ProPlus toepassingsupdates downloaden
* Uw aangepaste app bijwerken
* Andere configuratie-instellingen voor de installatiekopie van de Hallo zelf wijzigen

Hallo end-to-end-stappen voor het bijwerken van uw verzameling toouse Hallo installatiekopie u bijgewerkt, gaat u [hier](remoteapp-update.md). Maar voor informatie over hoe tooupdate installatiekopie en Office 365 ProPlus Hallo, bekijk Hallo informatie te volgen.

U hebt twee opties voor het bijwerken van uw installatiekopie - vervangt de afbeelding met een volledig nieuw of handmatig bijwerken van uw bestaande installatiekopie.

### <a name="replace-your-image-with-hello-latest-azure-gallery-image--add-customizations"></a>Vervang uw installatiekopie met de nieuwste Azure-galerie installatiekopie Hallo + aanpassingen toevoegen
Met deze optie kunt u Microsoft behandelen Hallo Windows Server- en Office 365 ProPlus-updates. In plaats van uw bestaande installatiekopie wordt bijgewerkt, gaat u een volledig nieuwe installatiekopie op basis van Hallo nieuwste afbeelding maken. Herhaal vervolgens de stappen die u voorheen toocustomize Hallo afbeelding - aangepaste apps installeren, wijzigt u Hallo image-configuratie, enzovoort.

Hallo-afbeeldingen regelmatig worden bijgewerkt, zodat u eenvoudig, kan er weten dat uw apps voor Windows Server en Office 365 ProPlus toodate zijn. Hallo nadeel is natuurlijk dat u tooapply uw aanpassingen hebt telkens wanneer u een nieuwe installatiekopie ophalen. U kunt scripts tooautomate instellen van uw aanpassingen kunt maken.

### <a name="manually-update-your-existing-image"></a>Uw bestaande installatiekopie handmatig bijwerken
Met deze optie kunt u Windows extra tooapply updates toohello standaardinstallatiekopie gebruiken. Voor Office 365 ProPlus, Hallo Office Deployment tool toodownload gebruik en de meest recente updates Hallo of versies van Office 365 ProPlus installeren.

> [!IMPORTANT]
> Houd er rekening mee - Hallo Office 365 ProPlus automatische updates niet uitschakelen.
> 
> 

Meer informatie over het gebruik van de Office Deployment Tool Hallo voor updates nodig?

* [Klik en klaar voor Office 365-producten implementeren met behulp van Hallo Office Deployment Tool](https://technet.microsoft.com/library/JJ219423.aspx)
* [Implementeren en bijwerken van Office 365 ProPlus met behulp van de Office Deployment Tool Hallo](https://channel9.msdn.com/Events/Ignite/2015/BRK3168) (video)
* [Instellingen voor Office 365 ProPlus-updates configureren](https://technet.microsoft.com/library/dn761708.aspx)

