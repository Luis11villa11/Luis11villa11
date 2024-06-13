<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Juego del Ahorcado</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f7f7f7;
            text-align: center;
            padding: 20px;
        }
        #palabra-en-ingles, #casillas-por-llenar, #intento, button {
            margin: 10px 0;
        }
        #casillas-por-llenar {
            letter-spacing: 2px;
        }
        input, button {
            padding: 10px;
            font-size: 16px;
        }
        button {
            cursor: pointer;
            background-color: #008CBA;
            color: white;
            border: none;
        }
    </style>
</head>
<body>
    <h1>Juego del Ahorcado</h1>
    <div id="palabra-en-ingles">Palabra: <span id="palabra"></span></div>
    <div id="casillas-por-llenar"></div>
    <input type="text" id="intento" placeholder="Escribe tu intento aquí" maxlength="1">
    <button onclick="verificarIntento()">Intentar</button>
</body>
</html>
<script>
    const palabras = [
        { ingles: "Apple", espanol: "manzana" },
        { ingles: "Tree", espanol: "arbol" },
{ ingles: "Table", espanol: "meza" },
{ ingles: "Few", espanol: "pocos" },
{ ingles: "How", espanol: "como" },
{ ingles: "should", espanol: "deber" },
{ ingles: "Advice", espanol: "consejo" },
{ ingles: "Quick", espanol: "rapido" },
{ ingles: "Wrong", espanol: "equivocado " },
    ];
    let palabraActual = palabras[Math.floor(Math.random() * palabras.length)];
    let palabraEspanol = palabraActual.espanol;
    let palabraIngles = palabraActual.ingles;
    let intentos = []; 
    let aciertos = 0;
    let casillas = Array(palabraEspanol.length).fill('_');
   {
        document.getElementById('palabra-en-ingles').innerText = `Word: ${palabraIngles}`;
      
        document.getElementById('casillas-por-llenar').innerText = casillas.join(' ');
    }
    function verificarIntento() {
        let intento = document.getElementById('intento').value.toLowerCase();
        document.getElementById('intento').value = '';
      
        if (intentos.includes(intento)) {
            alert('Ya has intentado esa letra.');
            return;
        }
      
        intentos.push(intento);
      
        let acierto = false;
        for (let i = 0; i < palabraEspanol.length; i++) {
            if (palabraEspanol[i] === intento) {
                casillas[i] = intento;
                acierto = true;
                aciertos++;
            }
        }
      
        document.getElementById('casillas-por-llenar').innerText = casillas.join(' ');

        // Verificar si el usuario ha ganado
        if (aciertos === palabraEspanol.length) {
            alert('¡Felicidades! Has adivinado la palabra.');
        } else if (!acierto) {
            alert('Intento incorrecto. ¡Inténtalo de nuevo!');
        }
    }
  
    window.onload = iniciarJuego;
</script>
