1. Inicializamos un proyecto. 

    ```bash
    npm init -y
    ```

2. Instalamos las dependencias.

    ```bash
    npm install --save-dev webpack webpack-cli
    npm i -D webpack webpack-cli
    ```

3. Añadimos nuestro fichero de configuración.

    ```js
    var path = require('path');

    module.exports = {
      entry: './src/main.js',
      output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'main.bundle.js'
      }
    };
    ```

4. Creamos nuestro fichero de entrada `main.js` dentro del directorio `src`

    ```js
    window.load = function() {
        console.log('Hello world')
    }
    ```

5. Añadimos el comando `build` a nuestro proyecto en el fichero `package.json` en la sección `scripts`.

    ```json
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1",
      "build": "webpack"
    },
    ```

6. Ejecutamos el comando para comprobar que funciona correctamente. Deberia generar el fichero 

    ```bash
    npm run build
    ```

7. Instalamos dependenciar para incluir ficheros css.

    ```bash
    npm install --save-dev style-loader css-loader 
    npm i -D style-loader css-loader 
    ```

8. Actualizamos la configuración de webpack

    ```js
    var path = require('path');

    module.exports = {
      entry: './src/main.js',
      output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'main.bundle.js'
      },
      module: {
          rules: [{
            test: /\.css$/,
            use: [ 'style-loader', 'css-loader' ]
        }]
      }
    };
    ```

9. Creamos la hoja de estilos `style.css` en el directorio `src`

    ```css
    body {
        background-color: red;
    }
    ```

10. Incluimos el fichero `style.css` en el fichero `main.js`

    ```js
    require('./style.css')
    ```

11. Ejecutamos de nuevo la paquetización.

    ```bash
    npm run build
    ```

12. Instalamos nuestro primer plugin para nuestra página de entrada.

    ```bash
    npm install --save-dev html-webpack-plugin
    npm i -D html-webpack-plugin
    ```

13. Actualizamos nuestro fichero de configuración de webpack.

    ```js
    var path = require('path');

    var HtmlWebpackPlugin = require('html-webpack-plugin');

    module.exports = {
      entry: './src/main.js',
      output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'main.bundle.js'
      },
      module: {
          rules: [{
            test: /\.css$/,
            use: [ 'style-loader', 'css-loader' ]
        }]
      },
      plugins: [new HtmlWebpackPlugin({template: 'src/index.html'})]
    };
    ```

14. Creamos nuestro primer documento `index.html` en el directorio `src`.

    ```html
    <!DOCTYPE html>

    <html lang="en">
      <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

        <title>Webpack</title>
      </head>
      <body>
        <h1>Webpack</h1>

        <script src="main.bundle.js"></script>
      </body>
    </html>
    ```

15. Ejecutamos de nuevo la paquetización.

    ```bash
    npm run build
    ```

16. Arrancamos un servidor para visualizar nuestra página.

    ```bash
    python -m http.server 3000 --directory ./dist
    ```

17. Instalamos un servidor para desarrollo.

    ```bash
    npm install --save-dev webpack-dev-server
    npm i -D webpack-dev-server
    ```

18. Añadimos el comando `develop` a nuestro proyecto en el fichero `package.json` en la sección `scripts`.

    ```json
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1",
      "build": "webpack",
      "develop": "webpack-dev-server --mode development --port 3000"
    }
    ```

19. Ejecutamos el comando develop.

    ```bash
    npm run develop
    ```

20. Creamos nuestro fichero `.gitignore` para evitar subir ficheros innecesarios al repositorio.

    ```
    dist
    node_modules
    ```

21. Subimos los cambios a nuestro repositorio.

    ```bash
    git add .
    git commit -m "Initial commit"
    git push origin master
    ```