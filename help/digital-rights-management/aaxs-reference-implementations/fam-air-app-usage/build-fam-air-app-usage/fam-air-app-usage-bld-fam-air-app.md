---
seo-title: Bygga AIR-programmet för Flash Access Manager
title: Bygga AIR-programmet för Flash Access Manager
uuid: 00927eb3-b8eb-4dd4-b528-91b70760c8cd
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Bygga AIR-programmet för Flash Access Manager {#building-the-flash-access-manager-air-application}

Om du vill skapa Flash Access Manager AIR-filen från källkoden måste du ha Flex och AIR SDK installerade på datorn. Innan du kan paketera och köra programmet måste du kompilera MXML-koden till en SWF-fil med hjälp av [!DNL amxmlc] kompilatorn. Kompilatorn finns [!DNL amxmlc] i katalogen [!DNL bin] för Flex 4 eller senare SDK. Om du vill kan du ställa in systemvariabeln path så att den inkluderar bin-katalogen för Flex SDK så att det blir enklare att köra verktygen på kommandoraden.

Gör så här för att skapa AIR-filen för Flash Access Manager:

1. Öppna ett kommandoskal eller en terminal och navigera till projektmappen för Flash Access Manager AIR-programmet ( [!DNL UI Tools\Flash Access Manager] i referensimplementeringskatalogen).
1. Ange följande kommando:

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   Körning [!DNL amxmlc] skapar [!DNL FlashAccessManager.swf]som innehåller den kompilerade koden för programmet.

Adobe AIR SDK innehåller ADT-verktyget (AIR Developer Tool) för att paketera AIR-program och generera certifikat. AIR-applikationer bör signeras digitalt. får användarna en varning när de installerar program som inte är korrekt signerade eller som inte är signerade alls. Om du vill generera ett certifikat med kommandoraden öppnar du ett konsolfönster i samma mapp som AIR-programmet och skriver följande:

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

Ersätt *some_password* med ett lösenord som du väljer. Efter några sekunder bör ADT slutföra certifikatgenereringsprocessen och du bör ha en ny [!DNL testCert.pfx] fil i programkatalogen.

Använd sedan ADT för att paketera programmet i en [!DNL .air] fil med kommandot:

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

Det här kommandot anger för ADT att paketera programmet med hjälp av nyckelfilen i [!DNL testCert.pfx]. På raden ovan konfigurerar du ADT att paketera hela programmet i en fil med namnet [!DNL FlashAccessManager.air]och att inkludera filerna [!DNL FlashAccessManager-app.xml] och [!DNL FlashAccessManager.swf] bilderna från resurskatalogen.

Som en del av den här processen uppmanas du att ange lösenordet som du anger för den nya certifikatfilen. Ange det, vänta en stund och en [!DNL FlashAccessManager.air] fil ska visas i samma katalog som dina projektfiler.
