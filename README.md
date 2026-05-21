# Tablou de Bord Interactiv: Utilizarea AI Generative în Educația din Republica Moldova

Studiu național privind percepția, competențele și barierele cadrelor didactice. Un instrument analitic modern conceput ca o aplicație web **Single-Page Application (SPA)** pentru interpretarea cantitativă și calitativă a datelor din chestionar.

# Link: https://nudoarmetudor.github.io/perceptia-profesori-ai-in-edu/

---

# Structura Interfeței și Meniul de Navigare

Aplicația este organizată modular pentru a asigura o navigare fluidă și intuitivă, fiind structurată în trei mari zone de interacțiune:

## Antetul (Header)

Conține:

* titlul studiului;
* contorul dinamic al eșantionului curent;
* indicatorul stării conexiunii;
* butonul pentru încărcarea unui alt fișier CSV.

## Panoul Lateral de Filtrare (Sidebar)

Permite segmentarea instantanee a datelor pe baza profilului demografic al respondenților:

* Gen
* Mediu
* Nivel
* Categorie curriculară
* Vechime

## Zona Centrală de Lucru

Afișează rezultatele prelucrate în funcție de tab-ul selectat din meniul de navigare superior.

---

# Detalierea Funcționalităților pe Tab-uri

## 1. Tab-ul „Demografie și Profil”

Acest tab oferă o imagine de ansamblu imediată asupra structurii eșantionului selectat prin intermediul indicatorilor cantitativi principali.

### Carduri KPI Dinamice

* **Cadre Didactice**
  Numărul total de chestionare active (recalculat în funcție de filtre).

* **Predomină în Mediul**
  Afișează mediul majoritar (Urban/Rural) și ponderea acestuia în eșantionul curent.

* **Nivel Principal de Predare**
  Indică treapta de învățământ cel mai des întâlnită printre respondenți.

* **Vechime Majoritară**
  Identifică intervalul de experiență didactică cel mai frecvent.

### Module de Grafice (Chart.js)

#### Distribuție Gen și Mediu

Diagrame:

* Pie (Gen)
* Doughnut (Mediu)

poziționate comparativ.

#### Vechime în Învățământ

Diagramă pe coloane reprezentând experiența în ani.

#### Niveluri de Învățământ

Grafic pe bare orizontale care separă:

* Primar
* Gimnazial
* Liceal

#### Arii Curriculare și Discipline

Grafic pe bare orizontale care listează Top 10 discipline predate.

Funcționalități suplimentare:

* tooltip-uri inteligente;
* afișarea numelui complet al disciplinelor lungi la hover.

---

## 2. Tab-ul „Competențe și Percepții”

O zonă critică ce analizează răspunsurile de opinie exprimate pe scara Likert de la:

* **1** = Dezacord total
* **7** = Acord total

corespunzătoare competențelor digitale și metodologice TPACK-AI.

### Indicele Global de Autoevaluare

Un algoritm calculează media generală a tuturor competențelor evaluate, generând un calificativ dinamic însoțit de un cod de culori:

* 🟢 **Nivel Ridicat de Pregătire**
  *(Medie ≥ 5.5)*

* 🟡 **Nivel Moderat de Pregătire**
  *(Medie între 4.0 și 5.4)*

* 🔴 **Pregătire Precara / Nevoie de Formare**
  *(Medie < 4.0)*

### Clasamentul Competențelor (Sidebar-ul Tab-ului)

Ordonează descrescător cele 13 abilități evaluate, evidențiind:

* bara de progres colorată;
* badge procentual;
* nivelul de acord pozitiv (note de 5, 6 și 7).

### Fișa Analitică Detaliată (Panelul Drept)

La selectarea oricărei competențe din clasament, sistemul calculează în timp real:

* **Scor Mediu**
  Nivelul mediu pe scara 1–7.

* **Acord Total (6–7)**
  Procentul profesorilor care sunt în total acord cu afirmația.

* **Mediană**
  Valoarea centrală a eșantionului.

* **Deviația Standard**
  Indicator care arată dacă opiniile sunt:

  * grupate (consens);
  * dispersate/polarizate (dezacord intern).

### Grafic de Distribuție (7 culori)

Reprezintă frecvența fiecărui nivel de răspuns:

* roșu = dezacord;
* verde = acord deplin.

---

## 3. Tab-ul „Analiza Comparativă”

Un instrument puternic de corelare statistică menit să identifice decalajele de:

* mediu;
* gen;
* experiență;

în pregătirea profesorilor.

### Selectare Criteriu

Permite compararea mediilor pe cele 13 competențe în funcție de:

* Mediul rezidențial;
* Gen;
* Vechime.

### Grafic de Bare Grupate

Generează automat:

* bare suprapuse;
* bare alăturate;

pentru fiecare grup comparat.

Exemplu:

> evidențierea faptului că profesorii din licee pot avea abilități de promptare superioare celor din învățământul primar.

---

## 4. Tab-ul „Feedback și Text Liber”

Panoul calitativ care oferă acces direct la vocea profesorilor, transformând textul liber în date explorabile.

### Selector de Întrebare

Permite trecerea rapidă între:

* analiza textelor privind pregătirea lecțiilor;
* analiza neconcordanțelor AI observate în clasă.

### Motor de Căutare Avansată

Caută cuvinte-cheie în timp real în timpul tastării.

### Evidențiere Vizuală (Highlighting)

Toate cuvintele-cheie identificate sunt marcate automat pentru scanare vizuală rapidă.

### Carduri Demografice Anonime

Fiecare citat este asociat cu profilul respondentului, de exemplu:

> „Masculin, Rural, Experiență > 10 ani”

pentru a oferi context sociologic răspunsurilor calitative.

---

# Logica Tehnică Internă

## Parser de Înaltă Performanță

Utilizarea bibliotecii **PapaParse.js** asigură:

* citirea foarte rapidă a fișierelor CSV;
* suport pentru mii de înregistrări;
* funcționare fără blocarea browserului.

## Curățarea Datelor (Sanitization Engine)

Aplicația include un sistem robust bazat pe expresii regulate (Regex) care:

* detectează caractere deteriorate;
* repară automat erorile de codare;
* păstrează intact textul deja corect.

Exemple de erori reparate:

* `preda?i`
* `înv??mânt`

Dacă este încărcat fișierul curat `DateChestionar.csv`, algoritmul detectează automat absența erorilor și nu modifică textul.

## Găzduire Statică și Securitate

Aplicația rulează **100% în browserul clientului**.

Avantaje:

* datele nu sunt trimise către servere externe;
* confidențialitate completă;
* conformitate GDPR.

---

# Tehnologii Utilizate

Proiectul utilizează tehnologii web moderne de tip „zero-install”.

## Stack Tehnologic

* **HTML5 & CSS3**
  Layout semantic și adaptiv.

* **Tailwind CSS**
  Framework utilitar pentru design modern și responsive.

* **Chart.js**
  Bibliotecă performantă pentru grafice interactive Canvas.

* **PapaParse.js**
  Parser rapid și robust pentru fișiere CSV.

* **Inter Font Family**
  Tipografie premium optimizată pentru ecrane moderne.

---

# Structura Fișierelor pe GitHub

```text
├── index.html          # Interfața aplicației (HTML, Tailwind, structură)
├── DateChestionar.csv  # Setul de date exportat din Google Forms
└── README.md           # Ghidul de documentare
```

> **Notă:**
> Codul poate fi separat modular în:
>
> * `style.css`
> * `app.js`
>
> Comentariile din `index.html` delimitează clar aceste secțiuni.

---

# Cum se utilizează local

1. Descărcați sau clonați depozitul.
2. Asigurați-vă că:

   * `index.html`
   * `DateChestionar.csv`

   se află în același folder.
3. Deschideți `index.html` într-un browser modern:

   * Chrome
   * Firefox
   * Edge
   * Safari

## Dacă apare eroarea CORS

Trageți fișierul `DateChestionar.csv` peste zona:

> „Drag & Drop”

din interfață.

---

# Publicarea pe GitHub Pages (Gratuit)

Pentru a publica aplicația online:

1. Deschideți repository-ul pe GitHub.
2. Accesați:

   * `Settings`
3. Din meniul lateral:

   * `Pages`
4. La:

   * `Build and deployment → Source`

   selectați:

   * `Deploy from a branch`
5. Selectați:

   * branch-ul `main` sau `master`
   * folderul `/ (root)`
6. Apăsați:

   * `Save`
7. Așteptați 1–2 minute.

GitHub va genera automat un link public de forma:

```text
https://numeutilizator.github.io/nume-depozit/
```

unde aplicația va funcționa instantaneu și va încărca automat datele.

---

# Licență și Drepturi de Autor

Acest depozit utilizează un model de licențiere de tip **Split Licensing**.

## Codul Sursă

Fișiere:

* HTML
* CSS
* JavaScript

Licență:

* **GNU General Public License v3.0 (GPL-3.0)**

Permisiuni:

* copiere;
* modificare;
* distribuire;

cu condiția păstrării licenței GPLv3 pentru lucrările derivate.

## Conținutul, Datele și Documentația

Include:

* README;
* materiale didactice;
* seturi de date;
* analize științifice.

Licență:

* **Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)**

---

# Atribuire obligatorie

**Tudor Lapp**
Formator, CNIDE „Clasa Viitorului”
