Projekt för höghus och krisberedskap
I en värld där cyberattacker, naturkatastrofer och geopolitiska spänningar ökar, står svenska höghus inför en kritisk utmaning: Hur kommunicerar 100+ boende med varandra när all extern kommunikation bryts?
Vi har utvecklat ett Open Source-system som gör höghus till själv-försörjande kommunikationsnav – helt utan beroende av internet eller mobilnät.

Dagens verklighet:
- 89% av svenskar förlitar sig på internet för kriskommunikation
- Höghus saknar lokala kommunikationssystem
- Våningsansvariga kan inte koordinera utan sociala medier
- MSB:s beredskapsinformation når inte fram vid systemkollaps

Vad händer vid:
- Cyberattacker mot teleoperatörer
- Strömavbrott över flera dagar
- Naturkatastrofer som skadar infrastruktur
- Krigssituationer med kommunikationsblockad

Vi har skapat en prototyp på världens första lokala krisberedskapssystem specifikt designat för höghus. Systemet fungerar helt utan internet och integrerar officiell svensk beredskapsinformation från MSB. Om internet fungerar kan den hämta information från Supabase och ladda ner lokalt för hybrid funktionalitet.


Läs mer på:
https://itsäkerhet.com//smart-hoghus/
https://expandtalk.se


Teknisk dokumentation

Hybrid Cloud + Offline System
🔄 Smart Sync-funktionalitet:

Offline-first: Fungerar helt utan internet
Auto-sync: Synkar data när internet kommer tillbaka
Real-time status: Visar online/offline + senaste sync-tid
Pending uploads: Sparar meddelanden lokalt och laddar upp senare

💾 Data Management:

localStorage backup: All data sparas lokalt permanent
Intelligent merging: Undviker dubbletter när data synkas
Graceful degradation: Fungerar perfekt även om Supabase är nere

📊 Supabase Database Schema:
Du behöver skapa dessa tabeller i Supabase:
sql-- Messages table
CREATE TABLE building_messages (
    id BIGSERIAL PRIMARY KEY,
    type TEXT NOT NULL,
    sender TEXT NOT NULL,
    target TEXT NOT NULL,
    text TEXT NOT NULL,
    building_id TEXT DEFAULT 'sandfjardsgatan42',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Floors table  
CREATE TABLE building_floors (
    id BIGSERIAL PRIMARY KEY,
    floor_number INTEGER NOT NULL,
    active_devices INTEGER DEFAULT 0,
    contact_person TEXT,
    status TEXT DEFAULT 'ok',
    building_id TEXT DEFAULT 'sandfjardsgatan42',
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Emergency updates table
CREATE TABLE emergency_updates (
    id BIGSERIAL PRIMARY KEY,
    message TEXT NOT NULL,
    priority TEXT DEFAULT 'info',
    building_id TEXT DEFAULT 'sandfjardsgatan42',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
⚙️ Setup Instructions:

Skapa Supabase-projekt på supabase.com
Kopiera URL och API-nyckel
Ersätt i koden:
javascriptconst SUPABASE_URL = 'https://your-project.supabase.co';
const SUPABASE_ANON_KEY = 'your-anon-key-here';

Skapa tabellerna med SQL ovan
Aktivera Row Level Security för säkerhet

🚀 Funktioner:
När Online:

Synkar meddelanden från andra byggnader/användare
Laddar upp lokala meddelanden till molnet
Hämtar emergencyuppdateringar från MSB
Uppdaterar våningsinformation real-time

När Offline:

Fungerar helt normalt lokalt
Sparar alla meddelanden för senare upload
Visar tydligt offline-status
Behåller all funktionalitet

Smart Features:

Auto-reconnect: Kontrollerar internet var 30:e sekund
Visual feedback: Tydlig status för online/offline/syncing
Conflict resolution: Intelligent merge av data
Performance: Bara synkar när det behövs

Detta ger dig det bästa av två världar - komplett offline-funktionalitet MEN även molnbaserad koordinering mellan flera byggnader när internet fungerar!
