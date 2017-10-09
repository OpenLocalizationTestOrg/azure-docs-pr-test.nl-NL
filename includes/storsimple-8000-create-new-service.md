<!--author=alkohli last changed:02/10/2017-->


#### <a name="toocreate-a-new-service"></a>een nieuwe service toocreate

1. Gebruik uw Microsoft-account referenties toolog op toohello [Azure-portal](https://portal.azure.com/).

2. In hello Azure-portal, klikt u op  **+**  en klikt u in de marketplace hello, **alle**.

    ![StorSimple-apparaatbeheerfunctie maken](./media/storsimple-8000-create-new-service/createssdevman1.png)

    Zoek naar _Fysieke StorSimple_. Selecteer en klik op **Serie met fysieke StorSimple-apparaten** en klik vervolgens op **Maken**. U kunt ook in hello Azure-portal op  **+**  en klik vervolgens onder **opslag**, klikt u op **StorSimple fysieke apparaat reeks**.

    ![StorSimple-apparaatbeheerfunctie maken](./media/storsimple-8000-create-new-service/createssdevman11.png)

3. In Hallo **StorSimple Apparaatbeheer** blade Hallo volgende stappen:
   
   1. Geef een unieke **resourcenaam** voor uw service op. Deze naam is een beschrijvende naam die kan worden gebruikt tooidentify Hallo-service. Hallo-naam kan tussen 2 en 50 tekens die letters, cijfers en afbreekstreepjes worden kunnen hebben. Hallo-naam moet beginnen en eindigen met een letter of cijfer.

   2. Kies een **abonnement** uit de vervolgkeuzelijst Hallo. Hallo-abonnement is gekoppeld tooyour account facturering. Dit veld wordt niet weergegeven als u slechts één abonnement hebt.

   3. Gebruik voor **Resourcegroep** de optie **Bestaande groep gebruiken** of **Nieuwe groep maken**. Zie [Azure-resourcegroepen](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/) voor meer informatie.
   
   4. Geef een **locatie** voor uw service op. Kies een locatie die het dichtst toohello geografische regio waar u toodeploy in het algemeen uw apparaat. U kunt ook toofactor in Hallo overwegingen te volgen: 
      
      * Als u bestaande workloads in Azure die u ook van plan toodeploy met uw StorSimple-apparaat bent hebt, moet u dat datacenter gebruiken.
      * Uw StorSimple Manager-apparaatbeheerfunctie en Azure Storage kunnen zich op twee verschillende locaties bevinden. In dat geval moet zijn u vereiste toocreate hello StorSimple Apparaatbeheer en Azure storage-account afzonderlijk. toocreate Azure storage-account, gaat u toohello Azure Storage-service in hello Azure-portal en volg de stappen Hallo in [maken van een Azure Storage-account](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account). Nadat u dit account hebt gemaakt, het toohello StorSimple Apparaatbeheer service toevoegen door Hallo stappen in [configureren van een nieuw opslagaccount voor Hallo service](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service).

   5. Selecteer **maken van een nieuw opslagaccount** tooautomatically een opslagaccount maken met de Hallo-service. Geef een naam op voor dit opslagaccount. Als u een andere locatie voor uw gegevens wilt kiezen, schakelt u dit vakje uit.

   6. Controleer **pincode toodashboard** als u wilt dat een snelle link toothis-service op uw dashboard.
      
   7. Klik op **maken** toocreate hello StorSimple Apparaatbeheer.

       ![StorSimple-apparaatbeheerfunctie maken](./media/storsimple-8000-create-new-service/createssdevman2.png)
   
maken van de service Hallo duurt een paar minuten. Nadat het Hallo-service is gemaakt, ziet u een melding en Hallo nieuwe service-blade wordt geopend.
   
![StorSimple-apparaatbeheerfunctie maken](./media/storsimple-8000-create-new-service/createssdevman5.png)


