### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>Verleen Mobile Engagement toegang tooyour GCM-API-sleutel
tooallow Mobile Engagement toosend pushmeldingen namens u, moet u deze toegang hebben tot tooyour API-sleutel toogrant. Dit wordt gedaan door te configureren en u uw sleutel in de Mobile Engagement-portal Hallo invoert.

1. Zorg ervoor dat Hallo-App wordt gebruikt voor dit project en klik vervolgens op Hallo van de klassieke Azure-Portal **Engage** knop Hallo onderaan:
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. Klik vervolgens op Hallo **instellingen** -> **Native Pushbericht** sectie tooenter uw GCM-sleutel:
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. Klik op Hallo **bewerken** pictogram vóór **API-sleutel** in Hallo **GCM-instellingen** sectie zoals hieronder wordt weergegeven:
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. In het pop-upvenster Hallo plakken Hallo GCM-serversleutel die u eerder hebt verkregen en klik vervolgens op **Ok**.
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <a id="send"></a>Een melding tooyour app verzenden
We gaan nu een eenvoudige pushmeldingcampagne die een push notification tooour-app stuurt maken.

1. Navigeer toohello **bereiken** tabblad in uw Mobile Engagement-portal.
2. Klik op **nieuwe aankondiging** toocreate uw pushmeldingcampagne.
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. Instellen van de eerste veld Hallo van uw campagne in via Hallo stappen te volgen:
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    a. Geef uw campagne een naam.
   
    b. Selecteer Hallo **bezorgingstype** als *Systeemmelding -> eenvoudig*: dit is Hallo eenvoudige Android-pushmeldingentype met een titel en een korte tekstregel.
   
    c. Selecteer **leveringstijd** als *elk gewenst moment* tooallow Hallo app tooreceive een melding of Hallo-app wordt gestart of niet.
   
    d. In Hallo melding tekst type Hallo **titel** die worden weergegeven in vet weergegeven in het Hallo-push.
   
    e. Typ vervolgens uw **bericht**
4. Schuif omlaag en in Hallo **inhoud** sectie **alleen melding**.
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. Instelling Hallo meest elementaire campagne mogelijk kunt u klaar bent. Nu Blader nogmaals naar beneden en klik op Hallo **maken** knop toosave uw campagne.
6. Laatste stap: klik op **activeren** tooactivate uw campagne toosend-pushmeldingen.
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

