# Publicera FriendZone på webben

Då får ni en vanlig länk som fungerar i Safari, Chrome, Edge, Firefox, på iPhone, iPad, Android och dator.

## 1. Bygg webbversionen
I Unity: menyn **FriendZone → Bygg WebGL**. Resultatet hamnar i mappen `Builds/WebGL`.
Första bygget tar ungefär 20 minuter, därefter går det snabbare.

## 2. Ladda upp (välj ett alternativ)

### A. Firebase Hosting (rekommenderas, ni har redan projektet)
Länken blir `https://friendzone-7fd80.web.app`. Gratis.

1. I Firebase-konsolen: **Build → Hosting → Get started**, klicka igenom guiden (den gör inget annat än att slå på Hosting).
2. Installera Node.js (LTS) från https://nodejs.org om ni inte har det.
3. Öppna en terminal i projektmappen `FriendZone` och kör, en rad i taget:

```bash
npm install -g firebase-tools
```
```bash
firebase login
```
```bash
firebase deploy --only hosting
```

Filerna `firebase.json` och `.firebaserc` är redan ifyllda. Efter sista kommandot skriver terminalen ut länken ("Hosting URL").
För att uppdatera sidan senare: bygg igen och kör sista kommandot igen.

### B. Netlify Drop (snabbast, ingen installation)
1. Gå till https://app.netlify.com/drop och logga in.
2. Dra mappen `Builds/WebGL` till sidan. Du får en länk direkt som du kan byta namn på.

## Bra att veta
- Appen pratar med er Firebase-databas, så alla som öppnar länken delar vänner, chatt och poäng.
- Första gången laddar sidan ungefär 12 MB, sedan sparas den i webbläsaren.
- På iPhone: öppna länken i Safari, tryck på dela-ikonen och välj **Lägg till på hemskärmen** så beter den sig som en app.
- Lägg inte länken eller koden publikt om ni inte vill att okända kan skapa konton i er databas.
