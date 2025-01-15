<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Giercowanie</title>
    <link href="https://fonts.googleapis.com/css2?family=Pacifico&display=swap" rel="stylesheet"> <!-- Dodana czcionka -->
    <style>
        body {
            font-family: 'Pacifico', sans-serif; /* Zmiana czcionki na Pacifico */
            text-align: center;
            background-color: #ffe6f2;
            color: #333;
            position: relative; /* Dodane, aby kotki były w dolnych rogach */
        }
        button {
            padding: 10px 20px;
            font-size: 18px;
            color: #fff;
            background-color: #ff66a3;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #ff3399;
        }
        .container {
            margin-top: 50px;
        }
        .hidden {
            display: none;
        }
        .activity-option {
            display: inline-block;
            margin: 20px;
        }
        img {
            width: 150px;
            border-radius: 10px;
        }
        .activity-option img {
            width: 150px;
            height: 150px;
            object-fit: cover;
            margin-bottom: 10px;
        }
        .activity-option p {
            font-weight: bold;
        }
        .goodbye-message {
            font-family: 'Pacifico', sans-serif;
            color: #ff66a3;
            font-size: 30px;
        }
        /* Stylizacja kotów w dolnych rogach */
        .kot-left, .kot-right {
            position: absolute;
            bottom: 10px;
            width: 200px;
        }
        .kot-left {
            left: 10px;
        }
        .kot-right {
            right: 10px;
        }
    </style>
</head>
<body>

    <div class="container" id="homePage">
        <h1>Witam piękną panią!!</h1>
        <img src="https://malowanieponumerach.com/wp-content/uploads/2023/05/kot-z-roza-1.jpg" alt="Kot z różą" style="width: 100px; margin-bottom: 20px;">
        <br><br>
        <button onclick="showActivitySelection()">Giercowanie?</button>
    </div>

    <div class="container hidden" id="activitySelectionPage">
        <h1>Co chcesz robić?</h1>
        <div class="activity-option">
            <img src="https://www.pngimg.com/uploads/fortnite/fortnite_PNG60.png" alt="Fortnite">
            <p>Fortnite</p>
            <button onclick="showSetTimePage('fortnite')">Wybierz</button>
        </div>
        <div class="activity-option">
            <img src="https://ferko.pl/wp-content/uploads/2022/01/fivem-4.png" alt="Fivem">
            <p>Fivem</p>
            <button onclick="showSetTimePage('fivem')">Wybierz</button>
        </div>
        <div class="activity-option">
            <img src="https://doladowania.pl/wp-content/uploads/2023/05/roblox.jpg" alt="Roblox">
            <p>Roblox</p>
            <button onclick="showSetTimePage('roblox')">Wybierz</button>
        </div>
    </div>

    <div class="container hidden" id="setTimePage">
        <h1>Ustal godzinkę jaka ci pasuje</h1>
        <h2>W co gramy: <span id="activityName"></span></h2>
        <label for="date">Wybierz datę:</label>
        <input type="date" id="date">
        <br><br>
        <label for="time">Wybierz godzinę:</label>
        <input type="time" id="time">
        <br><br>
        <button onclick="setTime()">Zatwierdź</button>
    </div>

    <div class="container hidden" id="goodbyePage">
        <h1 class="goodbye-message">Super, Do Zobaczenia Wikusia!!</h1> <!-- Zmieniony tekst na różowy i ładną czcionkę -->
        <img src="https://malowanieponumerach.com/wp-content/uploads/2023/05/kot-z-roza-1.jpg" alt="Kot z różą">
    </div>

    <script type="text/javascript" src="https://cdn.emailjs.com/dist/email.min.js"></script>

    <script>
        // Inicjalizacja EmailJS (użyj swojego User ID)
        emailjs.init("gSc6bXW3kPyQrHegV");  // Zastąp "gSc6bXW3kPyQrHegV" swoim ID

        // Funkcja do przejścia na stronę z wyborem aktywności
        function showActivitySelection() {
            document.getElementById('homePage').classList.add('hidden');
            document.getElementById('activitySelectionPage').classList.remove('hidden');
        }

        // Funkcja do przejścia na stronę do ustalania godziny
        function showSetTimePage(activity) {
            document.getElementById('activitySelectionPage').classList.add('hidden');
            document.getElementById('setTimePage').classList.remove('hidden');
            document.getElementById('activityName').textContent = activity.charAt(0).toUpperCase() + activity.slice(1);
        }

        // Funkcja do zapisania daty i godziny oraz przejścia do strony pożegnania
        function setTime() {
            const date = document.getElementById('date').value;
            const time = document.getElementById('time').value;

            if (date && time) {
                document.getElementById('setTimePage').classList.add('hidden');
                document.getElementById('goodbyePage').classList.remove('hidden');

                // Funkcja do wysyłania wiadomości
                const activity = document.getElementById('activityName').textContent;
                const data = {
                    activity: activity,
                    date: date,
                    time: time
                };

                // Wysyłamy dane za pomocą EmailJS
                emailjs.send("lk5azkm", "5rltk6x", data) // Zastąp "lk5azkm" i "5rltk6x"
                    .then((response) => {
                        console.log('Wiadomość wysłana!', response);
                        alert('Wiadomość wysłana na Twój e-mail!');
                    }, (error) => {
                        console.log('Błąd wysyłania wiadomości', error);
                        alert('Wystąpił błąd podczas wysyłania wiadomości!');
                    });
            } else {
                alert("Proszę wybrać datę i godzinę!");
            }
        }
    </script>

    <!-- Kotki w dolnym lewym i prawym rogu -->
    <img src="https://i.pinimg.com/236x/b0/40/e7/b040e76ad3b62145df9c938f4c96e5b8.jpg" alt="Kot" class="kot-left">
    <img src="https://i.pinimg.com/236x/b0/40/e7/b040e76ad3b62145df9c938f4c96e5b8.jpg" alt="Kot" class="kot-right">

</body>
</html>
