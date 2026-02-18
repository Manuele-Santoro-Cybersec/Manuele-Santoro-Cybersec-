🪟 Study Journal: Windows Command Line & PowerShell
Module Status: Completed ✅ | Platform: HTB Academy | Role Focus: SOC Analyst / DFIR

📌 Executive Summary
Il sistema operativo Windows domina l'ambiente enterprise. Come difensore (Blue Team), non posso affidarmi solo all'interfaccia grafica (GUI), che spesso nasconde i dettagli critici o è inaccessibile durante un incidente.
In questo modulo, sono passato dall'uso base del Command Prompt (CMD) alla potenza di PowerShell, imparando a gestire il sistema tramite oggetti, pipe e script di automazione.

🛠️ Key Technical Concepts Learned
1. Legacy vs. Modern: CMD vs. PowerShell
Ho appreso la distinzione fondamentale tra i due interpreti:

CMD (cmd.exe): Basato sul testo. Utile per compatibilità e comandi rapidi (dir, ipconfig), ma limitato nel filtraggio.

PowerShell (pwsh): Basato sugli Oggetti.NET. Questo è il "game changer".

Insight: In PowerShell, quando eseguo Get-Service, non ottengo una lista di testo, ma una serie di oggetti che posso interrogare, filtrare e manipolare.

2. System Enumeration & Navigation
Prima di difendere (o attaccare) una macchina, bisogna capire "dove siamo".

File System: Navigazione rapida con Set-Location (cd) e Get-ChildItem (ls/dir).

Command Spotlight: Get-ChildItem -Force per rivelare file nascosti (spesso usati per nascondere malware).

System Info: Uso di systeminfo per patch level e OS version, e whoami /priv per verificare i privilegi attuali (fondamentale per capire se c'è stato un Privilege Escalation).

3. Process & Service Management (The SOC View)
Identificare cosa sta girando sulla macchina è il cuore dell'Incident Response.

Tasklist & Get-Process: Ho imparato a visualizzare i processi attivi.

Filtering Malice: La potenza della pipeline | mi permette di isolare processi sospetti.

Esempio: Get-Process | Sort-Object CPU -Descending | Select-Object -First 5 (Per trovare processi che stanno consumando risorse anomale, come un crypto-miner).

Services: Uso di sc query e Get-Service per trovare servizi installati di recente o con nomi strani.

4. Searching with "Findstr" vs "Select-String"
Trovare un ago nel pagliaio (es. una password in un file di config o una stringa in un log).

CMD: findstr /S /I "password" *.txt (Cerca ricorsivamente, case-insensitive).

PowerShell: Select-String -Path "C:\Logs\*.log" -Pattern "Error" (Il grep di Windows, molto più potente).

5. Networking Basics from CLI
Netstat: netstat -ano è il comando re per vedere le connessioni attive.

Use Case: Collegare un PID (Process ID) a una connessione esterna sospetta verso un IP straniero.

Test Connectivity: Test-NetConnection (o tnc) per verificare se una porta specifica è aperta su un server remoto.

🧠 The "Aha!" Moment: The Pipeline (|)
La parte più sfidante ma gratificante è stata comprendere la logica della Pipeline in PowerShell.
A differenza di Linux (dove il pipe passa testo), qui passo l'intero oggetto.

Prima: "Devo formattare il testo per trovare la proprietà Status".

Dopo: Get-Service | Where-Object {$_.Status -eq 'Running'}.
Ho capito che $_ rappresenta l'oggetto corrente nella pipeline. Questa logica è la base per scrivere script di hunting automatici.

🛡️ Relevance to CJCA & SOC Role
Questo modulo è la base per:

Live Response: Quando dovrò collegarmi a un endpoint compromesso per raccogliere prove volatili.

Log Analysis: Capire la sintassi mi aiuterà a leggere meglio i log di PowerShell (Event ID 4104) per vedere cosa ha eseguito un attaccante.

Automation: Le basi di scripting (.ps1) mi permetteranno di automatizzare task ripetitivi nel SOC.

Prossimi passi: Approfondire l'uso di Get-WinEvent per l'analisi specifica dei log di sicurezza.
