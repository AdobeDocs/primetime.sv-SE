---
seo-title: Lista över principuppdateringar
title: Lista över principuppdateringar
uuid: ecc74b66-5b53-4ec3-9641-8b78929e2932
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Lista över principuppdateringar {#policy-update-list}

Du kan använda principuppdateringslistor för att kommunicera principändringar till en licensserver. Om en profil ändras efter att den har använts för att paketera innehåll är det önskvärt att licensservern är medveten om den senaste versionen av profilen, så att den versionen kan användas för att utfärda en licens.

Om du vill skapa en principuppdateringslista för första gången klickar du **[!UICONTROL Add policies]** för att visa alla tillgängliga principer på servern. Om det finns profiler som har uppdaterats sedan de användes för att paketera innehåll markerar du **[!UICONTROL update]** alternativknappen.

Om du inte längre vill använda en profil för att utfärda licenser och profilen redan har använts för att paketera innehåll kan du återkalla profilen. Det gör du genom att markera **[!UICONTROL revoke]** alternativknappen. Välj **[!UICONTROL Create Policy Update List]** profiler när de önskade profilerna har valts. En fil som anropas [!DNL PolicyUpdateList.dat] sparas i [!DNL Resources] katalogen.

Om du vill ändra en befintlig principuppdateringslista klickar du **[!UICONTROL Add policies]** för att visa alla tillgängliga principer på servern. Välj de ytterligare profiler som ska läggas till eller återkallas. Befintliga poster i listan över principuppdateringar kan ändras i skärmens övre del. Principer som är markerade **[!UICONTROL updated]** kan ändras till **[!UICONTROL revoked]**, men när en princip är markerad kan den inte ändras tillbaka **[!UICONTROL revoked]** till **[!UICONTROL updated]**.

När du har gjort önskade ändringar väljer du **[!UICONTROL Create Policy Update List]** och [!DNL PolicyUpdateList.dat] filen genereras om. Om en princip redan finns i principuppdateringslistan och har uppdaterats sedan den senaste gången listan skapades, kommer den senaste versionen av principen att användas när principuppdateringslistan genereras igen.
