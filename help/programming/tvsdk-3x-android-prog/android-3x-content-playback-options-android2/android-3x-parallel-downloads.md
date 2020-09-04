---
description: Att hämta video och ljud parallellt, i stället för i en serie, minskar startfördröjningarna.
seo-description: Att hämta video och ljud parallellt, i stället för i en serie, minskar startfördröjningarna.
seo-title: Parallella nedladdningar
title: Parallella nedladdningar
uuid: 11d37a39-391d-4127-9aa7-c94eb8a6a6a8
translation-type: tm+mt
source-git-commit: 51b3713e04fcb4adeaa7a8d1b700372b1dba7cf6
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# Parallella nedladdningar {#parallel-downloads}

Att hämta video och ljud parallellt, i stället för i en serie, minskar startfördröjningarna.

Parallella nedladdningar gör det möjligt att spela upp VOD-filer (video on demand), optimerar den tillgängliga bandbreddsanvändningen från en server, minskar sannolikheten för att hamna i buffertläge under körning och minimerar fördröjningen mellan hämtning och uppspelning.

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

Utan parallella hämtningar skickar TVSDK en begäran för videosegmentet och när videosegmentet har lästs in begär det ett eller två ljudsegment. Vid parallella nedladdningar laddas ljud- och videosegmenten ned samtidigt, inte sekventiellt. Eftersom det finns två anslutningar och två HTTP-begäranden per segment parallellt når data dessutom skärmen snabbare.

>[!NOTE]
>
>Den här funktionen gäller bara innehåll där ljud och video kodas till olika filer (omultiplicerat innehåll) och inte för MP4-innehåll, som alltid är multiplexat. HLS-innehåll är ofta omultiplicerat, särskilt med alternativt ljud.

<!-- 

See comment above (DASH use case removed).

  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
-->

HTTP-anslutningen kan fördröjas i följande steg:

* När TCP/IP-anslutningen till servern upprättas

   Även om klienten och servern har gått med på att kommunicera, har ingen HTTP-kommunikation utförts ännu. Den här typen av fördröjning beror på infrastrukturen mellan klienten och servern. Den här processen kräver att du hittar en sökväg via Internet mellan klienten och servern och ser till att alla enheter, som routrar och brandväggar, på vägen accepterar dataöverföringen.
* När en HTTP-begäran skickas för ett segment eller ett manifest via TCP/IP-anslutningen.

   Servern tar emot begäran, bearbetar den och börjar skicka data tillbaka till klienten. Hur lång tid det tar beror på belastningen och komplexiteten hos programvaran på servern och något på överföringshastigheten när klienten skickar begäran.