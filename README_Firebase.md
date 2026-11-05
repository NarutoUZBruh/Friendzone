# FriendZone i molnet (Firebase)

Utan inställningar körs FriendZone lokalt: all data sparas på den enhet man kör på.
För att alla enheter (dator, mobil, iPad) ska dela vänner, chatt, spel och liga behövs en gratis Firebase-databas.
Det tar ungefär 5 minuter och kräver inget kreditkort.

## 1. Skapa projektet
1. Gå till https://console.firebase.google.com och logga in med ett Google-konto.
2. **Add project** → välj ett namn, t.ex. `friendzone` → stäng av Google Analytics (behövs inte) → **Create project**.

## 2. Slå på inloggning
1. Menyn **Build → Authentication → Get started**.
2. Fliken **Sign-in method** → **Email/Password** → slå på **Enable** → **Save**.

## 3. Skapa databasen
1. Menyn **Build → Realtime Database → Create database**.
2. Välj en plats nära er (t.ex. `europe-west1`) och starta i **locked mode**.
3. Reglerna ligger i filen `database.rules.json` i projektmappen. Publicera dem med `firebase deploy --only database`
   (eller klistra in innehållet under fliken **Rules** och tryck **Publish**).

Reglerna gör att man bara kan skriva som sig själv: ingen kan ändra någon annans profil, skicka chattmeddelanden i någon annans namn,
skicka vänförfrågningar åt någon annan eller lägga in resultat åt någon annan. Obehöriga (ej inloggade) kommer inte åt något alls.
## 4. Hämta de två värdena
- **Databasadressen** hittar du högst upp på fliken **Data** i Realtime Database,
  t.ex. `https://friendzone-12345-default-rtdb.europe-west1.firebasedatabase.app`.
- **Web API Key** hittar du under kugghjulet → **Project settings → General → Web API Key**.

## 5. Klistra in dem
Öppna `Assets/Scripts/Data/CloudConfig.cs` och fyll i:

```csharp
public static string ApiKey = "din-web-api-key";
public static string DatabaseUrl = "https://friendzone-12345-default-rtdb....firebasedatabase.app";
```

Tryck Play. På inloggningsskärmen står nu "Delat via molnet". Skapa konton på olika enheter, lägg till varandra som vänner och spela.

## Bra att veta
- Användarnamn blir en påhittad e-postadress (`namn@friendzone.app`) i Firebase Authentication. Lösenorden hanteras av Firebase, appen sparar dem aldrig. Minst 6 tecken.
- Reglerna skyddar mot att man låtsas vara någon annan, men en inloggad användare kan fortfarande läsa all data i databasen (även privata chattar) om hen vet hur. Skulle man vilja ändra det behöver chatten och poängen flyttas till en server (Cloud Functions). Läs mer i Firebase-konsolen under Realtime Database → Rules.
- Gratisnivån (Spark) räcker gott för en klass. Appen frågar bara efter en liten räknare var 1,5 sekund och hämtar all data först när något har ändrats.
- Appen kollar ändringar med jämna mellanrum i stället för en öppen anslutning. Det gör att den fungerar likadant i WebGL, på mobil och på dator.

