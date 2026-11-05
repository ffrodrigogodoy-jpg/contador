<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>¿Volvemos a ser mejores amigos?</title>
    <style>
        body {
            margin: 0;
            padding: 15px;
            background: linear-gradient(135deg, #e8f5e9, #c8e6c9);
            font-family: 'Arial', sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            min-height: 100vh;
            overflow-y: auto;
            text-align: center;
            box-sizing: border-box;
            position: relative;
        }

        .container {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            width: 100%;
            max-width: 380px;
            margin: auto;
        }

        img {
            width: 220px;
            height: 220px;
            object-fit: cover;
            border-radius: 15px;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
            margin-bottom: 15px;
            border: 4px solid #fff;
        }

        h1 {
            font-size: 22px;
            color: #2e7d32;
            margin-bottom: 20px;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.1);
        }

        .buttons {
            display: flex;
            gap: 15px;
            align-items: center;
            justify-content: center;
            flex-wrap: wrap;
            position: relative;
            width: 100%;
            min-height: 80px;
        }

        #btn-si {
            background-color: #2e7d32;
            color: white;
            border: none;
            padding: 12px 30px;
            font-size: 18px;
            font-weight: bold;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 4px 10px rgba(46, 125, 50, 0.3);
            z-index: 10;
            max-width: 90%;
        }

        #btn-no {
            background-color: #c62828;
            color: white;
            border: none;
            padding: 10px 20px;
            font-size: 16px;
            border-radius: 12px;
            cursor: pointer;
            box-shadow: 0 4px 10px rgba(198, 40, 40, 0.3);
            transition: all 0.2s ease;
            position: relative;
        }

        .btn-mensaje {
            background-color: #388e3c;
            color: white;
            border: none;
            padding: 12px 25px;
            font-size: 16px;
            font-weight: bold;
            border-radius: 12px;
            cursor: pointer;
            margin-top: 15px;
            box-shadow: 0 4px 10px rgba(56, 142, 60, 0.3);
            animation: latido 1.5s infinite;
        }

        @keyframes latido {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        .mensaje-card {
            display: none;
            background: #ffffff;
            padding: 15px;
            border-radius: 15px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.15);
            margin-top: 15px;
            margin-bottom: 30px;
            text-align: left;
            color: #1b5e20;
            font-size: 13px;
            line-height: 1.5;
            max-height: 280px;
            overflow-y: auto;
            border: 2px solid #a5d6a7;
            width: 100%;
            box-sizing: border-box;
        }
    </style>
</head>
<body>

    <div class="container" id="main-container">
        <!-- Imagen inicial -->
        <img id="imagen-actual" src="https://i.ibb.co/5hJxvGVK/651f14c3ef17a4f36a88ee508d20e52a.jpg" alt="¿Volvemos a ser mejores amigos?">
        
        <h1 id="pregunta">¿Volvemos a ser mejores amigos? 🥺</h1>
        
        <div class="buttons" id="contenedor-botones">
            <button id="btn-si" onclick="aceptar()">Sí</button>
            <button id="btn-no" onclick="rechazar()">No</button>
        </div>
    </div>

    <script>
        // Secuencia exclusiva con imágenes tristes, de perritos y de ruego
        const pasosNo = [
            { texto: "¿En serio me vas a decir que no? 😿", imagen: "https://i.ibb.co/spFm40VY/bb6911504517465307913ab96692fadb.jpg" },
            { texto: "Prometo portarme bien ✋", imagen: "https://i.ibb.co/ZpJHYnkG/920411313b11c51ada64af360ddd19e3.jpg" },
            { texto: "¡No seas así de malita conmigo! 😭", imagen: "https://i.ibb.co/PGNfM4Rq/7450c0679decbae9c9bcdbabd5623c0c.jpg" },
            { texto: "Te invito lo que quieras de comer 🍕", imagen: "https://i.ibb.co/Fb0PJ0F7/9894277bc2cb84fa101077aa088e0c55.jpg" },
            { texto: "El botón verde se ve mucho mejor ✨", imagen: "https://i.ibb.co/m5TV60pY/73f372065ba118ebe1501dda7ff43898.jpg" },
            { texto: "Mira qué carita te pongo 🥺", imagen: "https://i.ibb.co/j9kgBCCd/c2fd7634c8f170a78a4a5fabf4b47bb6.jpg" },
            { texto: "Prohibido decir que no 😌", imagen: "https://i.ibb.co/NgHVJ7bJ/a8f6275b8e2fa68c929aafd02c102d12.jpg" },
            { texto: "Ya ríndete y di que sí porfis 💚", imagen: "https://i.ibb.co/spFm40VY/bb6911504517465307913ab96692fadb.jpg" }
        ];

        let contadorClicks = 0;
        let escalaSi = 1;
        let escalaNo = 1;

        function rechazar() {
            const btnNo = document.getElementById('btn-no');
            const btnSi = document.getElementById('btn-si');
            const imgActual = document.getElementById('imagen-actual');

            const pasoActual = pasosNo[contadorClicks % pasosNo.length];
            
            btnNo.innerText = pasoActual.texto;
            imgActual.src = pasoActual.imagen;

            if (escalaSi < 1.8) {
                escalaSi += 0.15;
            }
            btnSi.style.transform = `scale(${escalaSi})`;

            if (escalaNo > 0.4) {
                escalaNo -= 0.08;
            }
            btnNo.style.transform = `scale(${escalaNo})`;

            const randomX = (Math.random() - 0.5) * 120;
            const randomY = (Math.random() - 0.5) * 80;
            btnNo.style.position = 'relative';
            btnNo.style.left = randomX + 'px';
            btnNo.style.top = randomY + 'px';

            contadorClicks++;
        }

        function aceptar() {
            const container = document.getElementById('main-container');
            
            container.innerHTML = `
                <h1 id="titulo-principal" style="color: #2e7d32; font-size: 20px; margin-bottom: 5px;">¡Gracias por decir que sí! 🥹</h1>
                <p style="font-size: 13px; color: #1b5e20; font-weight: bold; margin-bottom: 10px; line-height: 1.4;">Y por nada del mundo se movía el botón, JAJAJA. 🫠<br>También quería darte las gracias por volver a darme la oportunidad de que seamos mejores amigos otra vez. :D</p>
                <img src="https://i.ibb.co/XfJVVhJ8/49efb97ab8054f6032da0a36e526ff7c.jpg" alt="Amigos" style="width: 180px; height: 180px; margin-bottom: 10px;">
                <button class="btn-mensaje" onclick="toggleMensaje()">💌 Leer Carta de Perdón</button>
                <div class="mensaje-card" id="card-mensaje">
                    💚 Bueno ahora volvemos a ser mejores amigos y ya sé que no te tengo que hacer enojar más, pero ya entendí y prometo no hacerte enojar más, y no sé qué más decir :D ✨
                </div>
            `;
        }

        function toggleMensaje() {
            const card = document.getElementById('card-mensaje');
            const titulo = document.getElementById('titulo-principal');
            
            if (card.style.display === 'block') {
                card.style.display = 'none';
            } else {
                card.style.display = 'block';
                titulo.innerText = "¡Ahora Dime en Chat :D!";
                card.scrollIntoView({ behavior: 'smooth' });
            }
        }
    </script>
</body>
</html>
