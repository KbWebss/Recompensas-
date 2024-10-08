
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Página de Recompensas</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f0f0f0;
            padding: 50px;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .container {
            text-align: center;
        }

        h1 {
            margin-top: -20px;
        }

        button {
            display: block;
            margin: 10px auto;
            padding: 15px 30px;
            font-size: 18px;
            cursor: pointer;
            background-color: #81D8D0;
            color: white;
            border: none;
            border-radius: 5px;
        }

        button:hover {
            background-color: #76C7C0;
        }

        button.disabled {
            background-color: #d3d3d3;
            cursor: not-allowed;
        }

        #mensaje {
            margin-top: 30px;
            font-size: 28px;
            color: #333;
            font-weight: bold;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
            opacity: 0;
            transition: opacity 0.5s ease-in-out;
        }

        #mensaje.fade-in {
            opacity: 1;
        }

        #error {
            color: #ff0000;
            font-size: 20px;
            font-weight: bold;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Pulsa los botones para descubrir tus recompensas</h1>
        
        <button id="btn1" onclick="mostrarMensaje(1)" aria-label="Recompensa 1">Recompensa 1</button>
        <button id="btn2" class="disabled" onclick="mostrarMensaje(2)" aria-label="Recompensa 2">Recompensa 2</button>
        <button id="btn3" class="disabled" onclick="mostrarMensaje(3)" aria-label="Recompensa 3">Recompensa 3</button>
        <button id="btn4" class="disabled" onclick="mostrarMensaje(4)" aria-label="Recompensa 4">Recompensa 4</button>
        <button id="btn5" class="disabled" onclick="mostrarMensaje(5)" aria-label="Recompensa 5">Recompensa 5</button>

        <p id="mensaje"></p>
        <p id="error"></p>
    </div>

    <script>
        let siguienteBoton = 1;

        function mostrarMensaje(num) {
            const mensajes = [
                "🎉 Enhorabuena, has ganado un batido de oreo!! 🍪",
                "💐 Enhorabuena, has ganado un ramo de flores!!! 🌹",
                "🍭 Enhorabuena, has ganado unas chuches!!! 🍬",
                "🍣 Enhorabuena, has ganado una cena en el Shibuya!!! 🍽️",
                "💇 Enhorabuena, has ganado un aceite para el pelo!!! 🌟"
            ];

            const mensajeElement = document.getElementById("mensaje");
            const errorElement = document.getElementById("error");

            mensajeElement.classList.remove("fade-in");
            mensajeElement.textContent = "";
            errorElement.textContent = "";

            if (num === siguienteBoton) {
                setTimeout(() => {
                    mensajeElement.textContent = mensajes[num - 1];
                    mensajeElement.classList.add("fade-in");

                    // Desaparecer el mensaje después de 13 segundos
                    setTimeout(() => {
                        mensajeElement.classList.remove("fade-in");
                        mensajeElement.textContent = "";
                    }, 13000); // Tiempo en milisegundos
                }, 500);

                siguienteBoton++;
                actualizarBotones();
            } else if (num < siguienteBoton) {
                errorElement.textContent = "Ya has reclamado esta recompensa amor";
            } else {
                errorElement.textContent = "Aún no puedes saber esta recompensa chiquita >:(";
            }
        }

        function actualizarBotones() {
            for (let i = 1; i <= 5; i++) {
                const boton = document.getElementById("btn" + i);
                if (i < siguienteBoton) {
                    boton.classList.add("disabled");
                } else if (i === siguienteBoton) {
                    boton.classList.remove("disabled");
                } else {
                    boton.classList.add("disabled");
                }
            }
        }
    </script>
</body>
</html>
