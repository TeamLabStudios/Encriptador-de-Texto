# Encriptador de Texto

Este proyecto es una aplicación web simple que permite encriptar y desencriptar texto utilizando el algoritmo AES (Advanced Encryption Standard) de la biblioteca CryptoJS.

## Características

- Encriptar texto ingresado por el usuario.
- Desencriptar texto encriptado utilizando la misma clave de encriptación.
- Interfaz de usuario amigable y fácil de usar.

## Tecnologías Utilizadas

- HTML
- CSS
- JavaScript
- [CryptoJS](https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.1.1/crypto-js.min.js)

## Cómo Usar

1. Clona este repositorio en tu máquina local.
2. Abre el archivo `index.html` en tu navegador web favorito.
3. Ingresa el texto que deseas encriptar en el campo "Texto a encriptar".
4. Ingresa una clave de encriptación en el campo "Clave de encriptación".
5. Haz clic en el botón "Encriptar" para encriptar el texto.
6. El texto encriptado aparecerá en la sección de resultados.
7. Para desencriptar el texto, ingresa el texto encriptado y la misma clave de encriptación, luego haz clic en el botón "Desencriptar".

## Ejemplo

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Encriptador de Texto</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.1.1/crypto-js.min.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        .container {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        .input-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        textarea, input[type="text"] {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            margin-bottom: 10px;
        }
        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            margin-right: 10px;
        }
        button:hover {
            background-color: #45a049;
        }
        .result {
            margin-top: 20px;
            padding: 15px;
            background-color: #f8f9fa;
            border-radius: 4px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Encriptador de Texto</h1>

        <div class="input-group">
            <label for="inputText">Texto a encriptar:</label>
            <textarea id="inputText" rows="4" placeholder="Escribe aquí el texto que deseas encriptar..."></textarea>
        </div>

        <div class="input-group">
            <label for="key">Clave de encriptación:</label>
            <input type="text" id="key" placeholder="Ingresa tu clave secreta">
        </div>

        <div>
            <button onclick="encrypt()">Encriptar</button>
            <button onclick="decrypt()">Desencriptar</button>
        </div>

        <div class="result">
            <h3>Resultado:</h3>
            <p id="output"></p>
        </div>
    </div>

    <script>
        function encrypt() {
            const text = document.getElementById('inputText').value;
            const key = document.getElementById('key').value;

            if (!text || !key) {
                alert('Por favor, ingresa tanto el texto como la clave');
                return;
            }

            try {
                const encrypted = CryptoJS.AES.encrypt(text, key).toString();
                document.getElementById('output').textContent = encrypted;
            } catch (error) {
                alert('Error al encriptar: ' + error.message);
            }
        }

        function decrypt() {
            const encryptedText = document.getElementById('inputText').value;
            const key = document.getElementById('key').value;

            if (!encryptedText || !key) {
                alert('Por favor, ingresa tanto el texto encriptado como la clave');
                return;
            }

            try {
                const decrypted = CryptoJS.AES.decrypt(encryptedText, key);
                const originalText = decrypted.toString(CryptoJS.enc.Utf8);

                if (originalText) {
                    document.getElementById('output').textContent = originalText;
                } else {
                    alert('Clave incorrecta o texto no válido');
                }
            } catch (error) {
                alert('Error al desencriptar: ' + error.message);
            }
        }
    </script>
</body>
</html>
