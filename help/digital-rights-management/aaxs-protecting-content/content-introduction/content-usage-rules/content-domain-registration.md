---
title: Domänregistrering för enhetsgrupp
description: Domänregistrering för enhetsgrupp
copied-description: true
exl-id: 1f3e9d26-c185-4d12-accf-aa74a313f890
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Domänregistrering för enhetsgrupp{#device-group-domain-registration}

Som ett alternativ till att binda en licens till en viss enhet har Adobe Access 3.0 och senare stöd för att binda licenser till en enhetsdomän. Flera enheter kan ansluta till en domän och ta emot domäntoken. När en enhet i domänen har skaffat en licens kan licensen överföras till vilken annan enhet som helst i domänen, och dessa enheter kan spela upp innehållet utan att hämta en licens direkt från licensservern.

För att ge stöd åt domänbundna licenser måste principen ange den domänserver som klienten måste registrera sig hos. Principen anger även autentiseringskraven för domänservern (om anonym åtkomst tillåts eller om servern kräver användarnamn/lösenord eller anpassad autentisering).

Domänregistrering och domänbundna licenser stöds av Adobe Access-klienter version 3.0 och senare. Om en äldre klient eller en Adobe Access 3.0-klient i Flash Player begär en licens för innehåll som stöder domänregistrering, kan licensservern utfärda en licens med en alternativ princip som stöder bindning till en viss enhet.
