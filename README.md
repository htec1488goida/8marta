<!DOCTYPE html>
<html lang="ru">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>С 8 Марта!</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
            background-color: #ffe6f2;
            color: #d63384;
        }

        input {
            padding: 10px;
            font-size: 16px;
            border: 2px solid #d63384;
            border-radius: 5px;
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
            margin-left: 10px;
            cursor: pointer;
            background-color: #d63384;
            color: white;
            border: none;
            border-radius: 5px;
        }

        button:hover {
            background-color: #b82c6c;
        }

        h2 {
            font-size: 24px;
            margin-bottom: 20px;
        }

        #content {
            margin-top: 20px;
            padding: 20px;
            background: white;
            border-radius: 10px;
            display: none;
        }
    </style>
</head>

<body>
    <h2>С Праздником 8 Марта! 🌸</h2>
    <p>Введите код для перехода</p>
    <input type="text" id="codeInput" placeholder="Введите код">
    <button onclick="checkCode()">Перейти</button>

    <div id="content"></div>

    <script>
        let pages = {
            "52": `<h3>Страница 1</h3><p>ДА здраствует Санкт ПИтербург</p>`,
            "5973": `<h3>Страница 1 задачача</h3><p>Как отмечают 8 Марта в разных странах.</p>`,
            "6284": `<h3>ЭТАП ПЕРВЫЙ</h3><p>Альтаир мой</p>`,
            "6640": `<h3>ЭТАП ПЕРВЫЙ</h3><p>подсказка под твоей партой нигер.</p>`,
            "7293": `<h3>ЭТАП ПЕРВЫЙ</h3><p>подсказка под твоей партой.</p>`,
            "3710": `<h3>ЭТАП ПЕРВЫЙ</h3><p>подсказка под твоей партой.</p>`,
            "9263": `<h3>ЭТАП ПЕРВЫЙ</h3><p>подсказка под твоей партой.</p>`,
            "8712": `<h3>ЭТАП ПЕРВЫЙ</h3><p>подсказка под твоей партой.</p>`,
            "8168": `<h3>ЭТАП ПЕРВЫЙ</h3><p>подсказка под твоей партой.</p>`,
            "9872": `<h3>ЭТАП ПЕРВЫЙ</h3><p>подсказка под твоей партой.</p>`,
            "5645": `<h3>ЭТАП ПЕРВЫЙ</h3><p>подсказка под твоей партой.</p>`,
            "1224": `<h3>ЭТАП ПЕРВЫЙ</h3><p>подсказка под твоей партой.</p>`,
            "1246": `<h3>ЭТАП ПЕРВЫЙ</h3><p>подсказка под твоей партой.</p>`,
            "1268": `<h3>ЭТАП ПЕРВЫЙ</h3><p>подсказка под твоей партой.</p>`,
            "1290": `<h3>ЭТАП ПЕРВЫЙ</h3><p>подсказка под твоей партой.</p>`,
            "1303": `<h3>ЭТАП ПЕРВЫЙ</h3><p>подсказка под твоей партой.</p>`,
            "1325": `<h3>ЭТАП ПЕРВЫЙ</h3><p>подсказка под твоей партой.</p>`,
            "1347": `<h3>ЭТАП ВТОРОЙ</h3><p>там где отбрасывают старые подковы и получают новые, присмотрите к вверху входа.</p>`,
            "1369": `<h3>ЭТАП ВТОРОЙ</h3><p>там где отбрасывают старые подковы и получают новые, посмотри на то без чего всё погружается в тьму.</p>`,
            "1391": `<h3>ЭТАП ВТОРОЙ</h3><p>в месте, где работают вместе, на одном из уровней хранится застывший момент. Отыщи его среди стен, что помнят лица.</p>`,
            "1414": `<h3>ЭТАП ВТОРОЙ</h3><p>там, где вверх ведёт последний шаг, перед открытым пространством прячется подсказка.(3 блок, дальняя)</p>`,
            "1436": `<h3>ЭТАП ВТОРОЙ</h3><p>там, где вверх ведёт последний шаг, перед открытым пространством прячется подсказка.(1 блок, дальняя)</p>`,
            "1458": `<h3>ЭТАП ВТОРОЙ</h3><p>там, где вверх ведёт последний шаг, перед открытым пространством прячется подсказка.(3 блок, ближняя)</p>`,
            "1488": `<h3>Страница 24</h3><p>ГОЙДА!!!!!</p>`,
            "1502": `<h3>ЭТАП ВТОРОЙ</h3><p>там, где вверх ведёт последний шаг, перед открытым пространством прячется подсказка.(1 блок, ближняя)</p>`,
            "1524": `<h3>ЭТАП ВТОРОЙ</h3><p>там, где жажда находит утоление, ищи знак рядом с местом творчества.</p>`,
            "1546": `<h3>ЭТАП ВТОРОЙ</h3><p>там, где нарисованные земли хранят тайны былых времён, спрятан ключ к следующему шагу.</p>`,
            "1568": `<h3>ЭТАП ВТОРОЙ</h3><p>кабинет, где оживают события прошлого и стены хранят эхо древних времен, спрятан ключ к разгадке.</p>`,
            "1590": `<h3>ЭТАП ВТОРОЙ</h3><p>там, где когда-то раскрывали секреты живого мира, спрятано нечто, что откроет тебе новый ключ.</p>`,
            "1603": `<h3>ЭТАП ВТОРОЙ</h3><p>там, где рождаются новые мысли, а пламя держат под строгим контролем, ждёт то, что поможет тебе пройти дальше.(4 этаж)</p>`,
            "1625": `<h3>ЭТАП ВТОРОЙ</h3><p>возле танцующей дамы, в месте где роэждаются новые идеи.(4 этаж)</p>`,
            "1647": `<h3>ЭТАП ВТОРОЙ</h3><p>там, где одежка ждут своих хозяев, спрятано то, что поможет тебе сделать следующий шаг.</p>`,
            "1669": `<h3>ФИНИШНАЯ ПРЯМАЯ</h3><p>найдите Большого брата бармена, кодовое слово-"скибиди туалет", после возращайтесь к истокам.</p>`,
            "1691": `<h3>ЭТАП ТРЕТИЙ-КОМАНДНАЯ РАБОТА</h3><p>хорошая работа, ступай туда откуда все начиналось.</p>`,
            "1714": `<h3>ЭТАП ТРЕТИЙ-КОМАНДНАЯ РАБОТА</h3><p>Идеи для фотосессии.</p>`,
            "1736": `<h3>ЭТАП ТРЕТИЙ-КОМАНДНАЯ РАБОТА</h3><p>Праздничный этикет.</p>`,
            "1758": `<h3>ЭТАП ТРЕТИЙ-КОМАНДНАЯ РАБОТА</h3><p>Как расслабиться в этот день.</p>`,
            "1780": `<h3>ФИНИШНАЯ ПРЯМАЯ</h3><p>найдите Мигеля, кодовое слово-"не забывай", после возращайтесь к истокам.</p>`,
            "1802": `<h3>ФИНИШНАЯ ПРЯМАЯ</h3><p>найдите Первую версию Альтаира, кодовое слово-"мятные леденцы", после возращайтесь к истокам</p>`,
            "1824": `<h3>ФИНИШНАЯ ПРЯМАЯ</h3><p>найдите Кудрявого барабанщика, кодовое слово-"лыжник", после возращайтесь к истокам.</p>`
        };

        function checkCode() {
            let code = document.getElementById("codeInput").value;
            let contentDiv = document.getElementById("content");

            if (pages[code]) {
                contentDiv.innerHTML = pages[code];
                contentDiv.style.display = "block";
            } else {
                alert("Неверный код! Попробуйте снова.");
            }
        }
    </script>
</body>

</html>
