---
description: Du bör separera spelarens gränssnittslogik från processen som hanterar och klickar. Ett sätt att göra detta är att implementera flera fragment för en aktivitet.
title: Avgränsa klickbara annonser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Separera den klickbara annonseringsprocessen {#separate-the-clickable-ad-process}

Du bör separera spelarens gränssnittslogik från processen som hanterar och klickar. Ett sätt att göra detta är att implementera flera fragment för en aktivitet.

1. Implementera ett fragment som ska innehålla `MediaPlayer`.

   Detta fragment ska anropa `notifyClick()` och ansvarar för videouppspelning.

   ```java
   public class PlayerFragment extends SherlockFragment { 
       ... 
       public void notifyAdClick () { 
           _mediaPlayer.notifyClick(); 
       } 
       ... 
   } 
   ```

1. Implementera ett annat fragment för att visa ett UI-element som anger att en annons är klickbar, övervaka det UI-elementet och kommunicera användarklickningar till det fragment som innehåller `MediaPlayer`.

   Detta fragment ska deklarera ett gränssnitt för fragmentkommunikation. Fragmentet fångar gränssnittsimplementeringen under sin `onAttach()`-livscykelmetod och kan anropa gränssnittsmetoderna för att kommunicera med aktiviteten.

   ```java
   public class PlayerClickableAdFragment extends SherlockFragment { 
       private ViewGroup viewGroup; 
       private Button button; 
       OnAdUserInteraction callback; 
       @Override 
       public View onCreateView(LayoutInflater inflater,  
                                ViewGroup container,  
                                Bundle savedInstanceState) { 
           // the custom fragment is defined by a custom button 
           viewGroup = (ViewGroup) inflater.inflate(R.layout.fragment_player_clickable_ad,  
                                                    container, false); 
           button = (Button) viewGroup.findViewById(R.id.clickButton); 
   
           // register a click listener to detect user interaction 
           button.setOnClickListener(new View.OnClickListener() { 
               @Override 
               public void onClick(View v) { 
                   // send the event back to the activity 
                   callback.onAdClick(); 
               } 
           }); 
           viewGroup.setVisibility(View.INVISIBLE); 
           return viewGroup; 
       } 
   
       public void hide() { 
           viewGroup.setVisibility(View.INVISIBLE); 
       } 
   
       public void show() { 
           viewGroup.setVisibility(View.VISIBLE);     
       } 
   
       @Override 
       public void onAttach(Activity activity) { 
           super.onAttach(activity); 
           // attaches the interface implementation 
           // if the container activity does not implement the methods  
           // from the interface an exception will be thrown 
           try { 
               callback = (OnAdUserInteraction) activity; 
           } catch (ClassCastException e) { 
               throw new ClassCastException(activity.toString() 
                   + " must implement OnAdUserInteraction"); 
           }     
       } 
   
       // user defined interface that allows fragment communication 
       // must be implemented by the container activity 
       public interface OnAdUserInteraction { 
           public void onAdClick(); 
       } 
   } 
   ```
