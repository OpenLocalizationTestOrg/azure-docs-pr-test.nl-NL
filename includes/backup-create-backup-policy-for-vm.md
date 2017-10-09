## <a name="defining-a-backup-policy"></a>Een back-upbeleid definiëren
Een back-upbeleid definieert een matrix met wanneer Hallo momentopnamen worden gemaakt en hoe lang deze momentopnamen worden bewaard. Bij het definiëren van een beleid voor het maken van een back-up van een virtuele machine, kunt u ervoor zorgen dat er *eenmaal per dag* een back-uptaak wordt uitgevoerd. Wanneer u een nieuw beleid maakt, is het toegepaste toohello kluis. Hallo-interface voor back-upbeleid ziet er als volgt:

![Back-upbeleid](./media/backup-create-policy-for-vms/backup-policy.png)

een beleid toocreate:

1. Voer een naam voor Hallo **beleidsnaam**.
2. Momentopnamen van uw gegevens kunnen met tussenpozen van een dag of een week worden gemaakt. Gebruik Hallo **back-upfrequentie** vervolgkeuzelijst toochoose of gegevens momentopnamen worden dagelijks of wekelijks.
   
   * Als u een dagelijks interval kiest, moet u Hallo gemarkeerd besturingselement tooselect Hallo tijd van de dag hello gebruiken voor Hallo momentopname. toochange hello uur, schakelt u Hallo uur en selecteert u Hallo nieuwe tijdstip.
     
     ![Dagelijks back-upbeleid](./media/backup-create-policy-for-vms/backup-policy-daily.png) <br/>
   * Als u een wekelijkse interval kiest, gebruik Hallo besturingselementen gemarkeerde tooselect Hallo dag(en) van Hallo week en Hallo-tijd van dag tootake Hallo momentopname. Selecteer een of meer dagen in Hallo dag menu. Selecteer één uur in Hallo uur menu. toochange hello uur, schakelt u het huidige tijdstip Hallo en selecteert u Hallo nieuwe tijdstip.
     
     ![Wekelijks back-upbeleid](./media/backup-create-policy-for-vms/backup-policy-weekly.png)
3. Standaard zijn alle opties voor een **bewaartermijn** geselecteerd. Schakelt u niet wilt dat toouse limieten voor de bewaartermijnen. Geef vervolgens Hallo interval(s) toouse.
   
    Maandelijkse en jaarlijkse bewaartermijnen kunnen u toospecify Hallo momentopnamen op basis van een wekelijks of dagelijks interval.
   
   > [!NOTE]
   > Als u een virtuele machine beveiligt, wordt één keer per dag een back-uptaak uitgevoerd. Hallo tijd wanneer Hallo back-up wordt uitgevoerd is Hallo dezelfde voor elke bewaartermijn.
   > 
   > 
4. Na het instellen van alle opties voor Hallo beleid boven Hallo in Hallo-blade op **opslaan**.
   
    Hallo nieuwe beleid wordt onmiddellijk toegepaste toohello kluis.

