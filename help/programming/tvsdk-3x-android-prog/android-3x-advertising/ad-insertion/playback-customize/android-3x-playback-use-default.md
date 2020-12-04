---
description: Du kan välja att använda standardbeteenden för annonser.
seo-description: Du kan välja att använda standardbeteenden för annonser.
seo-title: Använd standardbeteendet för uppspelning
title: Använd standardbeteendet för uppspelning
uuid: 36f76c42-4c6c-4620-9b47-ec97519a642a
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Använd standardbeteendet för uppspelning {#use-the-default-playback-behavior}

Du kan välja att använda standardbeteenden för annonser.

1. Gör något av följande om du vill använda standardbeteenden:

   * Om du implementerar en egen `AdvertisingFactory`-klass returnerar du null för `createAdPolicySelector`.

   * Om du inte har någon anpassad implementering för klassen `AdvertisingFactory` använder TVSDK en standardväljare för annonspolicy.

## Konfigurera anpassad uppspelning {#set-up-customized-playback}

Du kan anpassa eller åsidosätta annonsbeteenden.

Innan du kan anpassa eller åsidosätta annonsbeteenden måste du registrera annonsprincipinstansen med .
Gör något av följande om du vill anpassa annonsbeteenden:

* Implementera gränssnittet `AdPolicySelector` och alla dess metoder.

   Det här alternativet rekommenderas om du behöver åsidosätta **alla** standardbeteendena för annonser.

* Utöka klassen `DefaultAdPolicySelector` och tillhandahåll implementeringar för endast de beteenden som kräver anpassning.

   Det här alternativet rekommenderas om du bara behöver åsidosätta **vissa** av standardbeteendena.

Så här anpassar du annonsbeteenden:

1. Implementera gränssnittet `AdPolicySelector` och alla dess metoder.
1. Tilldela principinstansen som ska användas av TVSDK via reklamfabriken.

   >[!NOTE]
   >
   >Klassen CustomContentFactory utökar ContentFactory &amp;lbrace;
   >...
   >@Åsidosätt
   >public AdPolicySelector retrieveAdPolicySelector>(MediaPlayerItem mediaPlayerItem) &amp;lbrace;
   >return new CustomAdPolicySelector(mediaPlayerItem);
   >&amp;rbrace;
   >...
   >&amp;rbrace;
   >// registrera den anpassade innehållsfabriken med mediespelaren
   >MediaPlayerItemConfig config = new MediaPlayerItemConfig();
   >config.setAdvertisingFactory(new CustomContentFactory());
   >// den här konfigurationen skickas senare när >resursen läses in
   >mediaPlayer.replaceCurrentResource(resource, config);

1. Implementera dina anpassningar.
