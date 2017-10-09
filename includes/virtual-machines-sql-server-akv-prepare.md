## <a name="prepare-for-akv-integration"></a>Voorbereiden voor Azure Sleutelkluis-integratie
Integratie van Azure Sleutelkluis-tooconfigure toouse uw virtuele machine van SQL Server zijn er verschillende vereisten: 

1. [Azure Powershell installeren](#install-azure-powershell)
2. [Maak een Azure Active Directory](#create-an-azure-active-directory)
3. [Een sleutelkluis maken](#create-a-key-vault)

Hallo volgende secties worden deze vereisten en het Hallo-informatie die u nodig hebt toocollect toolater uitvoeren Hallo PowerShell-cmdlets.

### <a name="install-azure-powershell"></a>Azure PowerShell installeren
Zorg ervoor dat u hebt geïnstalleerd Hallo nieuwste Azure PowerShell SDK. Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="create-an-azure-active-directory"></a>Maak een Azure Active Directory
U moet eerst toohave een [Azure Active Directory](https://azure.microsoft.com/trial/get-started-active-directory/) (AAD) in uw abonnement. Tussen veel voordelen kunt hiermee u toogrant machtiging tooyour sleutelkluis voor bepaalde gebruikers en toepassingen.

Vervolgens moet u een toepassing registreren met AAD. Hierdoor krijgt u een Service-Principal-account dat toegang tooyour sleutelkluis die uw virtuele machine nodig heeft. In hello Azure Key Vault artikel vindt u deze stappen in Hallo [een toepassing registreren met Azure Active Directory](../articles/key-vault/key-vault-get-started.md#register) sectie, of u kunt zien Hallo stappen met schermopnamen in Hallo **een identiteit voor de toepassing hello ophalen sectie** van [dit blogbericht](http://blogs.technet.com/b/kv/archive/2015/01/09/azure-key-vault-step-by-step.aspx). Voordat u deze stappen uitvoert, houd er rekening mee dat u nodig hebt toocollect Hallo informatie tijdens deze registratie die later nodig wanneer u Azure Sleutelkluis-integratie op uw SQL-VM inschakelt te volgen.

* Nadat de toepassing hello is toegevoegd, Hallo zoeken **CLIENT-ID** op Hallo **configureren** tabblad.   ![Azure Active Directory-Client-ID](./media/virtual-machines-sql-server-akv-prepare/aad-client-id.png)
  
    Hallo client-ID wordt toegewezen hoger toohello **$spName** parameter in Hallo PowerShell script tooenable Azure Sleutelkluis-integratie (Service Principal name). 
* Ook tijdens deze stappen bij het maken van uw sleutel Hallo-geheim niet kopiëren voor uw sleutel wordt weergegeven in de volgende schermafbeelding Hallo. Deze sleutel geheim hoger toohello is toegewezen **$spSecret** (Service Principal-geheim)-parameter in Hallo PowerShell-script.  
    ![Azure Active Directory-geheim](./media/virtual-machines-sql-server-akv-prepare/aad-sp-secret.png)
* U moet deze nieuwe toohave Hallo van client-ID volgende toegangsmachtigingen toestaan: **versleutelen**, **ontsleutelen**, **wrapKey**, **unwrapKey**, **aanmelding**, en **controleren**. Dit wordt gedaan met Hallo [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/azure/mt603625.aspx) cmdlet. Zie voor meer informatie [autoriseren hello toepassing toouse Hallo sleutel of geheim](../articles/key-vault/key-vault-get-started.md#authorize).

### <a name="create-a-key-vault"></a>Een sleutelkluis maken
In de volgorde toouse Azure Key Vault toostore Hallo sleutels die u voor versleuteling in uw virtuele machine gebruikt, moet u toegang tooa sleutelkluis. Als u de sleutelkluis al geen hebt ingesteld, maken door de stappen te volgen Hallo in Hallo [aan de slag met Azure Key Vault](../articles/key-vault/key-vault-get-started.md) onderwerp. Voordat u deze stappen uitvoert, houd er rekening mee dat er enige informatie die u toocollect nodig tijdens deze instellen hoger is vereist is wanneer u Azure Sleutelkluis-integratie op de SQL-VM inschakelen.

Als u krijgt maken toohello een stap sleutelkluis Opmerking Hallo geretourneerd **vaultUri** eigenschap, die Hallo sleutelkluis-URL. Sleutelkluisnaam Hallo is ContosoKeyVault, daarom Hallo sleutelkluis-URL https://contosokeyvault.vault.azure.net/ zou worden in Hallo voorbeeld in deze stap, die hieronder worden weergegeven.

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

Hallo sleutelkluis-URL is toegewezen hoger toohello **$akvURL** parameter in Hallo PowerShell script tooenable Azure Sleutelkluis-integratie.

