---
title: aaaHPC Pack cluster met Azure Active Directory | Microsoft Docs
description: Meer informatie over hoe een HPC Pack 2016 toointegrate-cluster in Azure met Azure Active Directory
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a>Een HPC Pack cluster in Azure met Azure Active Directory beheren
[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) ondersteunt de integratie met [Azure Active Directory](../../active-directory/index.md) (Azure AD) voor beheerders die een HPC Pack cluster in Azure implementeren.



Hallo stappen in dit artikel voor Hallo taken op hoog niveau volgen: 
* Uw cluster HPC Pack handmatig te integreren met uw Azure AD-tenant
* Beheren en plannen van taken in uw cluster HPC Pack in Azure 

Een clusteroplossing HPC Pack integreren met Azure AD volgt toointegrate standaard stappen, andere toepassingen en services. In dit artikel wordt ervan uitgegaan dat u bekend bent met basisgebruiker management in Azure AD. Zie voor meer informatie en achtergrond Hallo [Azure Active Directory-documentatie](../../active-directory/index.md) en Hallo de volgende sectie.

## <a name="benefits-of-integration"></a>Voordelen van de integratie


Azure Active Directory (Azure AD) is een multitenant cloud-gebaseerde directory en identity management-service die toocloud oplossingen voor eenmalige aanmelding (SSO) toegang biedt.

Integratie van een cluster HPC Pack met Azure AD kunt u Hallo volgende doelstellingen te bereiken:

* Hallo traditionele Active Directory-domeincontroller uit Hallo HPC Pack cluster verwijderen. Dit kan helpen om kosten te verlagen Hallo van onderhouden Hallo cluster als dit niet nodig zijn voor uw bedrijf en versnellen Hallo-implementatieproces is.
* Gebruikmaken van Hallo volgende voordelen die worden uitgevoerd door Azure AD:
    *   Eenmalige aanmelding 
    *   Met behulp van een lokale AD-identiteit voor Hallo HPC Pack cluster in Azure 

    ![Azure Active Directory-omgeving](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a>Vereisten
* **HPC Pack 2016 cluster is geïmplementeerd in virtuele machines in Azure** - voor de stappen, Zie [een HPC Pack 2016-cluster in Azure implementeren](hpcpack-2016-cluster.md). U moet Hallo DNS-naam van het hoofdknooppunt Hallo en Hallo referenties van een Clusterbeheerder Hallo stappen in dit artikel uit te voeren.

  > [!NOTE]
  > Azure Active Directory-integratie wordt niet ondersteund in versies van HPC Pack vóór HPC Pack 2016.



* **Clientcomputer** -moet u een Windows- of Windows Server client computer te worden uitgevoerd HPC Pack client hulpprogramma's. Als u alleen toouse Hallo HPC Pack web-portal of REST-API toosubmit taken wilt, kunt u elke clientcomputer van uw keuze.

* **Hulpprogramma's voor HPC Pack client** -Hallo HPC Pack client hulpprogramma's installeren op Hallo van de clientcomputer, met behulp van Hallo gratis installatiepakket beschikbaar is via Hallo Microsoft Download Center.


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a>Stap 1: Hallo HPC clusterserver registreren met uw Azure AD-tenant
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Klik op **Active Directory** in Hallo linkermenu en klik op de gewenste map Hallo in uw abonnement. In de map Hallo moet u de machtiging tooaccess resources hebben.
3. Klik op **gebruikers**, en controleer of er gebruikersaccounts al gemaakt of geconfigureerd.
4. Klik op **toepassingen** > **toevoegen**, en klik vervolgens op **mijn organisatie ontwikkelt toepassing toevoegen**. Voer de volgende informatie in de wizard Hallo Hallo:
    * **Naam** -HPCPackClusterServer
    * **Type** : Selecteer **Web-toepassing en/of Web-API**
    * **Eenmalige aanmelding URL**- hello basis-URL voor hello, die standaard is`https://hpcserver`
    * **App ID URI** - `https://<Directory_name>/<application_name>`. Vervang `<Directory_name`> Hello volledige naam van uw Azure AD-tenant, bijvoorbeeld `hpclocal.onmicrosoft.com`, en vervang `<application_name>` met Hallo-naam die u eerder hebt gekozen.

5. Nadat het Hallo-app wordt toegevoegd, klikt u op **configureren**. Configureer Hallo volgende eigenschappen:
    * Selecteer **Ja** voor **toepassing multitenant is**
    * Selecteer **Ja** voor **gebruiker toewijzing vereist tooaccess app**.

6. Klik op **Opslaan**. Wanneer opslaan is voltooid, klikt u op **beheren Manifest**. Deze actie downloadt van uw toepassing JavaScript object notation (JSON) manifestbestand. Hallo gedownload-manifest bewerken door het zoeken naar Hallo `appRoles` instellen en het toevoegen van Hallo toepassingsrol te volgen:
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. Hallo-bestand opslaan. Klik in het Hallo-portal **beheren Manifest** > **uploaden Manifest**. U kunt vervolgens Hallo bewerkte manifest uploaden.
8. Klik op **gebruikers**, selecteert u een gebruiker en klik vervolgens op **toewijzen**. Een Hallo beschikbare rollen (HpcUsers of HpcAdminMirror) toohello gebruiker toewijzen. Herhaal deze stap met extra gebruikers in het Hallo-directory. Zie voor achtergrondinformatie over cluster gebruikers, [Cluster gebruikers beheren](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).

   > [!NOTE] 
   > toomanage gebruikers, wordt u aangeraden hello Azure Active Directory preview blade in Hallo [Azure-portal](https://portal.azure.com).
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a>Stap 2: Hallo HPC cluster client registreren bij uw Azure AD-tenant

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Klik op **Active Directory** in Hallo linkermenu en klik op de gewenste map Hallo in uw abonnement. In de map Hallo moet u de machtiging tooaccess resources hebben.
3. Klik op **toepassingen** > **toevoegen**, en klik vervolgens op **mijn organisatie ontwikkelt toepassing toevoegen**. Voer de volgende informatie in de wizard Hallo Hallo:

    * **Naam** -HPCPackClusterClient
    * **Type** : Selecteer **Native Client-toepassing**
    * **Omleidings-URI** - `http://hpcclient`

4. Nadat het Hallo-app wordt toegevoegd, klikt u op **configureren**. Kopiëren Hallo **Client-ID** waarde en op te slaan. U nodig dit later bij het configureren van uw toepassing.

5. In **machtigingen tooother toepassingen**, klikt u op **toepassing toevoegen**. Zoeken en Hallo HpcPackClusterServer toepassing is (gemaakt in stap 1) toe te voegen.

6. In Hallo **gedelegeerde machtigingen** vervolgkeuzelijst **toegang HpcClusterServer**. Klik vervolgens op **Opslaan**.


## <a name="step-3-configure-hello-hpc-cluster"></a>Stap 3: Hallo HPC-cluster configureren

1. Verbinding maken met het hoofdknooppunt toohello HPC Pack 2016 in Azure.

2. Start HPC PowerShell.

3. Hallo volgende opdracht uitvoeren:

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    waar

    * `AADTenant`Hiermee geeft u hello Azure AD-tenantnaam, zoals`hpclocal.onmicrosoft.com`
    * `AADClientAppId`Hiermee geeft u Hallo client-ID voor Hallo-app gemaakt in stap 2.

4. Hallo HpcSchedulerStateful service opnieuw starten.

    In een cluster met meerdere hoofdknooppunten, kunt u de volgende PowerShell-opdrachten op Hallo hoofdknooppunt tooswitch Hallo primaire replica voor Hallo HpcSchedulerStateful service Hallo uitvoeren:

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a>Stap 4: Beheren en verzenden van taken van Hallo-client

de HPC Pack 2016 setup-bestanden (volledige installatie) downloaden tooinstall Hallo HPC Pack client hulpprogramma's op uw computer vanaf Microsoft Download Center Hallo. Wanneer u Hallo installatie begint, selecteer de installatieoptie Hallo voor Hallo **HPC Pack client utilities**.

tooprepare Hallo-clientcomputer installeren Hallo certificaat dat wordt gebruikt tijdens [HPC cluster setup](hpcpack-2016-cluster.md) op Hallo-clientcomputer. Gebruik standaard Windows certificate management procedures tooinstall Hallo openbaar certificaat toohello **certificaten-huidige gebruiker** > **Trusted Root Certification Authorities** opslaan. 

U kunt nu Hallo HPC Pack opdrachten uitvoeren of Hallo HPC Pack Job manager GUI toosubmit gebruiken en cluster taken beheren met behulp van hello Azure AD-account. Zie voor de opties voor het indienen van taak [HPC verzenden taken tooan HPC Pack-cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).

> [!NOTE]
> Wanneer u probeert eerst tooconnect toohello HPC Pack cluster in Azure voor hello, verschijnt een pop-upvensters. Voer uw Azure AD-referenties toolog in. Hallo-token wordt vervolgens in de cache opgeslagen. Token in cache opgeslagen hoger verbindingen toohello cluster in Azure gebruik Hallo tenzij verificatie wijzigingen of Hallo in cache is uitgeschakeld.
>
  
Bijvoorbeeld, na het voltooien van de vorige stappen hello, u kunt een query voor de taken van een on-premises client als volgt:

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a>Handig cmdlets taak te verzenden met Azure AD-integratie 

### <a name="manage-hello-local-token-cache"></a>Hallo lokale tokencache beheren

HPC Pack 2016 biedt twee nieuwe HPC PowerShell-cmdlets toomanage Hallo lokale tokencache. Deze cmdlets zijn handig voor het verzenden van taken niet-interactief. Zie Hallo voorbeeld te volgen:

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a>Hallo-referenties voor het indienen van taken met hello Azure AD-account instellen 

U kunt toorun Hallo taak onder Hallo HPC cluster gebruiker soms (voor een domein HPC-cluster moet uitvoeren als een domeingebruiker; voor een niet-domein HPC-cluster moet uitvoeren als een lokale gebruiker op het hoofdknooppunt Hallo).

1. Gebruik Hallo opdrachten tooset Hallo referenties te volgen:

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. Vervolgens dient als volgt Hallo-taak. Hallo-taak taak wordt uitgevoerd onder $localUser op Hallo rekenknooppunten.

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   Als `–Credential` niet wordt opgegeven met `Submit-HpcJob`, Hallo- taak wordt uitgevoerd onder een lokale gebruikersaccount toegewezen als hello Azure AD-account. (Hallo HPC-cluster maakt een lokale gebruiker met dezelfde naam als hello Azure AD-account toorun Hallo taak Hallo.)
    
3. Uitgebreide gegevens voor hello Azure AD-account instellen. Dit is handig wanneer een MPI-taak wordt uitgevoerd op Linux-knooppunten met hello Azure AD-account.

   * Uitgebreide gegevens voor Azure AD-account zelf Hallo instellen

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * Uitgebreide gegevens instellen en uitvoeren als gebruiker met HPC-cluster
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

