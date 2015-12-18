#PyBossa Ablauf

##userID
    Tasks mit ID 1 und 2 sind dummy tasks zum ermitteln der userID.
    Sie erhalten Priorität 0. Alle anderen Tasks Priorität 1.
    Durch das speichern einer antwort bekommt man die userID zurück. 
    Diese wird dann im local storage hinterlegt.
    Da jedoch nur eine Antwort pro User und Task gespeichert werden kann,
    muss die Antwort danach wieder gelöscht werden um die ID erneut erhalten zu können.
    Dieser Fall tritt auf, wenn der local storage gelöscht wurde.
    Da das löschen einer Antwort seitens PyBossa nicht direkt erkannt wird (Cache) braucht man einen zweiten Task um die ID zu ermitteln, falls der erste gerade nicht verfügbar ist.
    
    
    Im task presenter wird bei jedem Aufruf geprüft ob die ID im local storage ist.
    ID vorhanden: bearbeite Task ganz normal.
    Wenn nicht: leite um zu Task 1 oder 2 und kehre danach zurück.
    

##Worker
    Folgende Informationen müssen über Worker gespeichert werden:
    Id
    Email
    Kalibrierungsfragen -> führt zu einem plattform-globalen Worker-Profil.
 
##Experimente
    Entsprechen genau einem Task bei PyBossa.
    Ein Experiment hat folgenden Ablauf:
    1.a ID bekannt? (Siehe oben)
    1.b Email Adresse bekannt?
        Nein? -> Abfragen. TODO lösungsansatz um nicht immer durchlaufen zu müssen.
    2. Benötigte Kalibrierung erfüllt? 
        Wenn nicht alle bekannt: Erst kalibrierungsfragen beantworten.
        Wenn nicht alle erfüllt: Blockieren.
    3. Kontrollfragen:
        Anzeigen der Aufgabenstellung mit Verständnisfragen.
        Kontrolle ok? 
    4. Echte Fragen bearbeiten
    5. Alle echten Fragen bearbeitet?
        Task in PyBossa für Worker  als beantwortet markieren
 

##Projekt
    In PyBossa muss einmal angelegt werden und dient als Container für alle Experimente.

##CreativeTask
    ajax an Worker-Service next. 
    Parameter
        userID, expID, plattform, [assignmentID]
    
##CreativeAnswer
    ajax an Worker-Service
    - submitCreative
    - submitRating
    - submitCalibration
    - submitControl
    - submitEmail
