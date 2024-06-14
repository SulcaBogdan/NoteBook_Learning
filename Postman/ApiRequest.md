# Api Request

## Ce este un api request?

Un API request (cerere API) este o solicitare trimisă de un client către un server pentru a accesa sau a manipula resursele oferite de API (Application Programming Interface). API-urile sunt interfețe care permit aplicațiilor software să comunice între ele. O cerere API specifică tipul de operațiune pe care clientul dorește să o efectueze și este formată din mai multe componente esențiale.

### Componentele unei cereri API

1. **Endpoint**: URL-ul sau adresa web a serverului unde este găzduit API-ul. Endpoint-ul specifică locația resursei pe care clientul dorește să o acceseze. De exemplu: `https://api.example.com/users`.

2. **Metoda HTTP**: Tipul de operațiune pe care clientul dorește să o efectueze. Cele mai comune metode HTTP sunt:
   - **GET**: Obține date de la server (de exemplu, obține o listă de utilizatori).
   - **POST**: Trimite date către server pentru a crea o nouă resursă (de exemplu, creează un utilizator nou).
   - **PUT**: Trimite date către server pentru a actualiza o resursă existentă (de exemplu, actualizează detaliile unui utilizator).
   - **DELETE**: Șterge o resursă de pe server (de exemplu, șterge un utilizator).

3. **Header-e**: Informații suplimentare trimise împreună cu cererea, cum ar fi tipul de conținut (Content-Type), informații de autentificare (Authorization), și altele. De exemplu:
   ```json
   {
     "Content-Type": "application/json",
     "Authorization": "Bearer <token>"
   }
   ```

4. **Parametri**: Informații adiționale incluse în cerere. Aceștia pot fi:
   - **Parametri de interogare (Query parameters)**: Atașați la URL, specificați după semnul `?`. De exemplu: `https://api.example.com/users?limit=10&page=2`.
   - **Parametri de cale (Path parameters)**: Inserți direct în URL pentru a specifica resurse particulare. De exemplu: `https://api.example.com/users/123`, unde `123` este un ID de utilizator.

5. **Corpul cererii (Request Body)**: Datele trimise către server în cadrul unei cereri POST, PUT, PATCH. Acesta este de obicei formatat ca JSON, XML sau alte formate de date. De exemplu:
   ```json
   {
     "name": "John Doe",
     "email": "john.doe@example.com"
   }
   ```

### Exemplu de cerere API

Să presupunem că dorim să creăm un nou utilizator pe un server. Cererea API ar putea arăta astfel:

- **Endpoint**: `https://api.example.com/users`
- **Metoda HTTP**: `POST`
- **Header-e**:
  ```json
  {
    "Content-Type": "application/json",
    "Authorization": "Bearer abc123token"
  }
  ```
- **Corpul cererii**:
  ```json
  {
    "name": "Jane Doe",
    "email": "jane.doe@example.com"
  }
  ```

### Răspunsul API

După trimiterea cererii, serverul va răspunde cu un răspuns API, care include:
- **Codul de stare HTTP (HTTP Status Code)**: Indică succesul sau eșecul cererii (ex. 200 OK, 201 Created, 404 Not Found).
- **Header-e**: Informații suplimentare despre răspuns (ex. tipul de conținut, lungimea conținutului).
- **Corpul răspunsului (Response Body)**: Datele returnate de server, de obicei în format JSON sau XML.

### Concluzie

Un API request este o componentă fundamentală în interacțiunea între aplicații și servere, permițând accesarea și manipularea resurselor prin intermediul metodelor HTTP și a structurilor de date standardizate.