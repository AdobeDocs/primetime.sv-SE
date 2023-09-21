---
description: Du kan välja att använda standardbeteenden för annonser.
title: Använd standardbeteendet för uppspelning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Använd standardbeteendet för uppspelning {#use-the-default-playback-behavior}

Du kan välja att använda standardbeteenden för annonser.

1. Gör något av följande om du vill använda standardbeteenden:

   * Om du implementerar en egen `AdvertisingFactory` klass, returnera null för `createAdPolicySelector`.

   * Om du inte har någon anpassad implementering för `AdvertisingFactory` klassen TVSDK använder en standardväljare för annonsprinciper.

## Konfigurera anpassad uppspelning {#set-up-customized-playback}

Du kan anpassa eller åsidosätta annonsbeteenden.

Innan du kan anpassa eller åsidosätta annonsbeteenden måste du registrera annonsprincipinstansen med .
Gör något av följande om du vill anpassa annonsbeteenden:

* Implementera `AdPolicySelector` -gränssnittet och alla dess metoder.

  Det här alternativet rekommenderas om du behöver åsidosätta **alla** standardbeteenden för annonser.

* Utöka `DefaultAdPolicySelector` och bara implementera beteenden som kräver anpassning.

  Det här alternativet rekommenderas om du bara behöver åsidosätta **några** standardbeteenden.

Så här anpassar du annonsbeteenden:

1. Implementera `AdPolicySelector` -gränssnittet och alla dess metoder.
1. Tilldela principinstansen som ska användas av TVSDK via reklamfabriken.

   >[!NOTE]
   >
   >Klassen CustomContentFactory utökar ContentFactory&amp;lbrace;
   >...
   >@Åsidosätt
   >public AdPolicySelector retrieveAdPolicySelector>(MediaPlayerItem mediaPlayerItem) &amp;lbrace;
   >return new CustomAdPolicySelector(mediaPlayerItem);
   >&amp;rankning;
   >...
   >&amp;rankning;
   >// registrera den anpassade innehållsfabriken med mediespelaren
   >MediaPlayerItemConfig config = new MediaPlayerItemConfig();
   >config.setAdvertisingFactory(new CustomContentFactory());
   >// den här konfigurationen skickas senare när >resursen läses in
   >mediaPlayer.replaceCurrentResource(resource, config);

1. Implementera dina anpassningar.
