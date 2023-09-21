---
title: Lista över principuppdateringar
description: Lista över principuppdateringar
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Lista över principuppdateringar {#policy-update-list}

Du kan använda principuppdateringslistor för att kommunicera principändringar till en licensserver. Om en profil ändras efter att den har använts för att paketera innehåll är det önskvärt att licensservern är medveten om den senaste versionen av profilen, så att den versionen kan användas för att utfärda en licens.

Om du vill skapa en principuppdateringslista för första gången klickar du på **[!UICONTROL Add policies]** om du vill visa alla tillgängliga principer på servern. För profiler som har uppdaterats sedan de användes för att paketera innehåll väljer du **[!UICONTROL update]** alternativknapp.

Om du inte längre vill använda en profil för att utfärda licenser och profilen redan har använts för att paketera innehåll, kan du återkalla profilen. Om du vill göra det väljer du **[!UICONTROL revoke]** alternativknapp. När du har valt profiler väljer du **[!UICONTROL Create Policy Update List]**. En fil som kallas [!DNL PolicyUpdateList.dat] sparas i [!DNL Resources] Katalog.

Om du vill ändra en befintlig principuppdateringslista klickar du på **[!UICONTROL Add policies]** om du vill visa alla tillgängliga principer på servern. Välj de ytterligare profiler som ska läggas till eller återkallas. Befintliga poster i listan över principuppdateringar kan ändras i skärmens övre del. Profiler som är markerade **[!UICONTROL updated]** kan ändras till **[!UICONTROL revoked]**, men när en policy väl är **[!UICONTROL revoked]** går det inte att ändra tillbaka till **[!UICONTROL updated]**.

När du har gjort ändringarna väljer du **[!UICONTROL Create Policy Update List]** och [!DNL PolicyUpdateList.dat] filen genereras om. Om en princip redan finns i principuppdateringslistan och har uppdaterats sedan den senaste gången listan skapades, kommer den senaste versionen av principen att användas när principuppdateringslistan genereras igen.
