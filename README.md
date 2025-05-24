Rețetar Culinar


Nume: Postolache Anaid-Maria 
Grupa: 1034 SIMPRE
•	 Link video prezentare proiect: https://youtu.be/GE-v3eCxYuA?feature=shared
•	Link publicare aplicație: https://proiect-2rod.vercel.app/
•	Link GitHub: https://github.com/AnaidP/Proiect


1. Introducere
Rețetar Culinar este o aplicație web destinată organizării rețetelor culinare într-un mod simplu, intuitiv și eficient. Într-o eră în care digitalizarea este esențială în toate aspectele vieții noastre, inclusiv în bucătărie, această aplicație răspunde nevoii de a centraliza și gestiona colecțiile personale de rețete într-un spațiu sigur și accesibil de pe orice dispozitiv. Proiectul a fost conceput pentru a înlocui metodele clasice de notare a rețetelor – de la carnețelele fizice, greu de întreținut și predispose la deteriorare, până la notițele disparate din telefon sau fișierele nestructurate din calculator.
Utilizatorii pot adăuga rețete noi, le pot modifica în timp real și le pot șterge atunci când acestea nu mai sunt relevante. Aplicația oferă o interfață prietenoasă și responsivă, adaptabilă tuturor ecranelor, astfel încât experiența utilizatorului să fie una plăcută indiferent dacă accesează platforma de pe un laptop sau un telefon mobil. Din punct de vedere tehnologic, aplicația este dezvoltată cu Next.js, un framework modern bazat pe React, care permite atât redare server-side cât și generare statică. Pentru stocarea persistentă a datelor se utilizează MongoDB, o bază de date NoSQL recunoscută pentru flexibilitatea și performanțele sale în gestionarea documentelor JSON-like, făcând-o ideală pentru structuri de date variabile, așa cum sunt rețetele culinare.

2. Descrierea problemei
În mod tradițional, pasionații de gătit sau chiar profesioniștii din domeniu își arhivează rețetele în carnețele fizice, caiete vechi sau fișiere digitale nestructurate. Aceste metode nu doar că sunt ineficiente în ceea ce privește căutarea și organizarea informațiilor, dar și riscante: se pot pierde, pot deveni ilizibile sau pot fi accesate greu în momentele cheie ale procesului de gătit. Mai mult decât atât, în lipsa unei soluții digitale moderne, devine complicat să împărtășești rețetele cu prietenii sau familia într-un mod elegant și rapid.
Aplicația Rețetar Culinar a fost gândită tocmai pentru a elimina aceste inconveniente. Printr-o abordare web-centrică, ușor de utilizat și accesibilă online, ea devine un substitut perfect pentru metodele arhaice de stocare a rețetelor. Utilizatorul are control complet asupra conținutului: poate crea, edita și șterge rețete într-o manieră naturală, cu salvare automată în baza de date, astfel încât nimic important să nu se piardă.
3. Descriere API
API-ul care susține aplicația de Rețetar Culinar este construit în cadrul arhitecturii serverless a framework-ului Next.js și este localizat în fișierul /pages/api/records.js. Acesta este proiectat pentru a asigura toate operațiunile esențiale asupra datelor, utilizând paradigma REST pentru manipularea colecției de rețete stocate într-o bază de date MongoDB. Funcționând ca intermediar între interfața client și baza de date, API-ul permite crearea, preluarea, actualizarea și ștergerea rețetelor prin metode HTTP standard. Acest mecanism oferă o separare clară a responsabilităților, contribuind la menținerea unui cod curat, scalabil și ușor de întreținut.
Toate interacțiunile cu resursele se realizează printr-un singur endpoint: /api/records. Acest endpoint este configurat să răspundă la patru metode principale: GET, POST, PUT și DELETE, fiecare corespunzând unei operațiuni specifice. Cererile de tip GET sunt utilizate pentru a extrage date, iar comportamentul lor variază în funcție de prezența unui parametru de tip id. Dacă se furnizează un id, API-ul returnează un singur obiect cu informațiile rețetei corespunzătoare; dacă acest parametru lipsește, răspunsul va conține întreaga colecție de rețete disponibile în baza de date.
Pentru adăugarea de noi rețete, se utilizează metoda POST, care preia obiectul transmis în corpul cererii și îl inserează ca document nou în colecția MongoDB. Fiecare rețetă este compusă din patru câmpuri esențiale: title (titlul rețetei), description (descrierea detaliată a modului de preparare), mealType (tipul mesei – de exemplu, „Mic dejun”, „Prânz”, „Cină” sau „Desert”) și _id (generat automat de MongoDB). Este important de menționat că toate cererile de acest tip trebuie să aibă antetul Content-Type: application/json pentru a fi procesate corect.
Actualizarea unei rețete existente se face prin metoda PUT. În acest caz, corpul cererii trebuie să includă întregul obiect, inclusiv identificatorul unic _id, alături de noile valori ce trebuie înlocuite în baza de date. Procesul presupune identificarea documentului pe baza identificatorului și înlocuirea câmpurilor sale cu cele noi, fără a afecta restul datelor.
Ștergerea unei rețete se realizează prin metoda DELETE, care necesită transmiterea parametrului id în URL. Odată identificat, documentul este eliminat definitiv din colecție, iar răspunsul confirmă succesul operațiunii printr-un obiect JSON cu câmpuri acknowledged și deletedCount.
API-ul este construit fără autentificare, ceea ce înseamnă că toate operațiunile sunt accesibile oricărui utilizator care interacționează cu interfața aplicației. Deși această alegere simplifică utilizarea și testarea în mediul de dezvoltare, pentru un mediu de producție se recomandă ferm introducerea unui sistem de autentificare și autorizare, cum ar fi integrarea next-auth pentru protejarea endpointurilor sau utilizarea de tokenuri JWT pentru acces controlat la resurse.
Structura datelor este simplă și clar definită, ceea ce permite o integrare ușoară cu componentele de interfață. Fiecare rețetă este un obiect ce include titlul rețetei, descrierea detaliată a procesului de gătire și al ingredientelor, tipul mesei pentru care este recomandată (de exemplu, „Mic dejun” sau „Desert”) și un identificator unic. Această structură permite o flexibilitate mare în filtrarea sau sortarea datelor pe interfața client, oferind totodată o bază solidă pentru extinderea aplicației cu funcționalități precum căutare, etichetare sau categorii complexe.
Prin intermediul acestui API, aplicația reușește să îmbine simplitatea utilizării cu funcționalitatea completă necesară gestionării unei colecții de rețete într-un mod dinamic, intuitiv și eficient.

4. Fluxul de date
Fluxul de date din cadrul aplicației „Rețetar Culinar” urmează un model bidirecțional clasic, în care componenta client (frontend-ul dezvoltat în React/Next.js) comunică constant cu backend-ul API construit tot în Next.js, iar backend-ul la rândul său interacționează direct cu baza de date MongoDB. Această structură oferă o separare clară între logica de prezentare, logica de business și persistarea datelor, contribuind la un cod modular și ușor de extins.
La inițializarea aplicației, pagina principală declanșează o cerere HTTP de tip GET către endpointul /api/records. Acest apel este procesat de server, care accesează colecția records din baza de date și returnează un array cu toate rețetele disponibile. Aceste date sunt mapate în componenta de afișare într-un layout vizual sub formă de listă sau grilă, oferind utilizatorului o privire de ansamblu asupra întregii colecții de rețete.

![image](https://github.com/user-attachments/assets/d8927f8a-4424-45dd-a70d-5db4a5accedb)

Atunci când utilizatorul decide să adauge o rețetă nouă, acesta este direcționat către pagina de creare, unde este prezentat un formular interactiv. Formularul conține câmpuri pentru titlu, descriere și tipul mesei (mealType) – de exemplu, Mic dejun, Prânz, Cină sau Desert. După completarea acestor câmpuri și trimiterea formularului, datele sunt trimise sub forma unui JSON către server printr-un request POST la același endpoint. Serverul inserează noile date în colecția MongoDB, iar utilizatorul este redirecționat înapoi către pagina principală, unde rețeta nou adăugată este afișată imediat, într-un mod complet dinamic, fără a fi necesară reîncărcarea paginii. 
![image](https://github.com/user-attachments/assets/7db64c2b-08e3-4dc3-9b38-f6371e2bc498) 
![image](https://github.com/user-attachments/assets/19a83177-93ca-46b3-a35d-06612d005a2d)
![image](https://github.com/user-attachments/assets/bbd5c58a-f67a-4326-a5f9-8d6edfa9e3fa)
 
Pentru modificarea unei rețete existente, utilizatorul accesează formularul de editare, care este prepopulat automat cu datele rețetei selectate. Aceasta se realizează printr-o cerere GET care conține parametrul id, ce permite identificarea unică a rețetei. După ce utilizatorul efectuează modificările necesare și trimite formularul, este inițiat un request PUT care transmite către server noua versiune a obiectului, înlocuind valorile din documentul original în baza de date. Interfața reflectă instant aceste modificări prin reîmprospătarea locală a stării aplicației. 
![image](https://github.com/user-attachments/assets/76183b9b-e7a4-41b0-9ed3-beccb7b099c4)


Ștergerea unei rețete se realizează tot printr-o interacțiune simplă și intuitivă. Utilizatorul apasă butonul de ștergere asociat unei rețete, iar aplicația trimite o cerere de tip DELETE care conține id-ul documentului ce trebuie eliminat. Serverul identifică acest document în baza de date și îl șterge definitiv, confirmând succesul operațiunii printr-un răspuns JSON care conține un indicator de tip acknowledged. În interfață, rețeta este eliminată în timp real.
Acest flux de date asigură o experiență fluidă pentru utilizator, iar utilizarea metodelor HTTP standard contribuie la claritatea și predictibilitatea comportamentului aplicației. Nu sunt utilizate servicii externe de autentificare sau autorizare, întrucât aplicația este gândită ca un prototip didactic. Cu toate acestea, arhitectura este suficient de flexibilă pentru a permite integrarea ulterioară a unui mecanism de autentificare, de exemplu prin NextAuth.js sau JWT, în cazul în care aplicația ar urma să fie extinsă pentru a include funcționalități multi-utilizator sau restricții de acces.
Astfel, fluxul de date este clar definit, eficient, scalabil și centrat pe o interacțiune rapidă între client și server, cu răspunsuri rapide din partea bazei de date.
 

6. Referințe
Dezvoltarea aplicației „Rețetar Culinar” a fost realizată pe baza unui set extins de resurse tehnice, biblioteci și documentații oficiale, menite să asigure un cadru modern, robust și scalabil pentru aplicațiile web. În continuare sunt listate principalele surse utilizate în cadrul proiectului:
•	Next.js Documentation
Documentația oficială pentru framework-ul Next.js, utilizată pentru routing, server-side rendering, API routes și configurare generală a aplicației.
https://nextjs.org/docs
•	MongoDB Manual
Ghid complet utilizat pentru operarea asupra bazei de date NoSQL, inclusiv pentru gestionarea colecțiilor și interogărilor.
https://www.mongodb.com/docs/manual/
•	Vercel Deployment Documentation
Informații esențiale despre publicarea și configurarea aplicației pe platforma Vercel, inclusiv gestionarea erorilor de runtime și routing.
https://vercel.com/docs
•	Tailwind CSS Documentation
Framework CSS folosit pentru stilizarea componentelor în mod rapid și eficient, cu suport pentru teme dark/light.
https://tailwindcss.com/docs
•	GitHub
Platformă de versionare și colaborare pe cod sursă, utilizată pentru gestionarea proiectului și publicarea codului.
https://github.com/



This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/pages/api-reference/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `pages/index.js`. The page auto-updates as you edit the file.

[API routes](https://nextjs.org/docs/pages/building-your-application/routing/api-routes) can be accessed on [http://localhost:3000/api/hello](http://localhost:3000/api/hello). This endpoint can be edited in `pages/api/hello.js`.

The `pages/api` directory is mapped to `/api/*`. Files in this directory are treated as [API routes](https://nextjs.org/docs/pages/building-your-application/routing/api-routes) instead of React pages.

This project uses [`next/font`](https://nextjs.org/docs/pages/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn-pages-router) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/pages/building-your-application/deploying) for more details.
