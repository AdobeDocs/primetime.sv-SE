---
description: TVSDK ger en TV-liknande upplevelse av att kunna vara med mitt i en annons i liveströmmar.
seo-description: TVSDK ger en TV-liknande upplevelse av att kunna vara med mitt i en annons i liveströmmar.
seo-title: Insättning av delvis annonsbrytning
title: Insättning av delvis annonsbrytning
uuid: b6ee62da-c4d1-42f2-b03d-f73247f8e585
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---


# Insättning av delvis annonsbrytning{#partial-ad-break-insertion}

TVSDK ger en TV-liknande upplevelse av att kunna vara med mitt i en annons i liveströmmar.

Med den partiella infogningsfunktionen kan ni efterlikna en TV-liknande upplevelse, där klienten, om den startar ett direktflöde inuti en mittenrulle, börjar spela upp det i den där mittrullen. Det liknar en övergång till en TV-kanal och reklamen fungerar smidigt.

Om en användare till exempel ansluter sig mitt i en 90-sekunders annonsbrytning (tre 30-sekunders annonser), tio sekunder in i den andra annonsen (d.v.s. 40 sekunder in i annonsbrytningen) spelas den andra annonsen upp under den återstående varaktigheten (20 sekunder) följt av den tredje annonsen.

## Spåra annons {#section_03AFAEAA8DA44399952DC51C5E12951E}

Annonsspårare för annonsen som spelas delvis (den andra annonsen) aktiveras inte. I exemplet ovan aktiveras bara spåraren för den tredje annonsen.

## Beteende med förrullning {#section_7DFBFB12E63343D1A0C614F0CF9F1714}

Funktionen fungerar när en pre-roll-annons spelas upp med livematerial. Direktuppspelningen spelas upp från direktpunkten när pre-roll-annonsen avslutas.

Annonsbrytningshändelser skickas även om det inte finns några fullständiga annonser i den här reklambrytningen. En annons betraktas som delvis annons, om den hoppas över i mer än en sekund. Om ett visningsprogram till exempel tittar på en annons som de hoppat över i 800 ms betraktas den som en fullständig annons.
