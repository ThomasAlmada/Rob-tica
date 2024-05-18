<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aplicación de Asistencia</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f7f6;
            margin: 0;
            padding: 0;
            color: #333;
        }
        .container {
            width: 80%;
            max-width: 800px;
            margin: 50px auto;
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h1, h2 {
            text-align: center;
            color: #4CAF50;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            color: #555;
        }
        input[type="text"], input[type="password"], select {
            width: 100%;
            padding: 10px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 16px;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #45a049;
        }
        .menu {
            display: none;
            margin-top: 20px;
            text-align: center;
        }
        .menu a {
            display: block;
            padding: 10px;
            margin-bottom: 10px;
            background-color: #4CAF50;
            color: white;
            text-align: center;
            text-decoration: none;
            border-radius: 4px;
        }
        .menu a:hover {
            background-color: #45a049;
        }
        .section {
            display: none;
            margin-top: 20px;
        }
        .result {
            background-color: #e9f7ef;
            padding: 10px;
            border-radius: 4px;
            margin-top: 10px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
        }
        th, td {
            padding: 10px;
            border: 1px solid #ddd;
            text-align: left;
        }
        th {
            background-color: #4CAF50;
            color: white;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Inicio de Sesión</h1>
        <div id="login-form" class="form-group">
            <label for="username">Usuario</label>
            <input type="text" id="username" placeholder="Usuario">
            <label for="password">Contraseña</label>
            <input type="password" id="password" placeholder="Contraseña">
            <button onclick="login()">Iniciar Sesión</button>
        </div>

        <div id="menu" class="menu">
            <a href="#" onclick="showSection('marca-asistencia')">Marca Ingreso-Asistencia</a>
            <a href="#" onclick="showSection('matriculados-presencia')">Matriculados Presencia</a>
            <a href="#" onclick="showSection('base-datos')">Base de datos de asistencias</a>
            <a href="#" onclick="logout()">Salir</a>
        </div>

        <div id="marca-asistencia" class="section">
            <h2>Marca Ingreso-Asistencia</h2>
            <div class="form-group">
                <label for="dni">D.N.I</label>
                <input type="text" id="dni" placeholder="Ingrese D.N.I del alumno">
                <button onclick="buscarEstudiante()">Buscar Estudiante</button>
            </div>
            <div id="resultado-busqueda" class="result">
                <h3>RESULTADO DE BÚSQUEDA</h3>
                <p>Nombre: <span id="nombre-alumno"></span></p>
                <p>DNI: <span id="dni-alumno"></span></p>
                <h4>ULTIMAS ASISTENCIAS</h4>
                <table id="asistencias-alumno">
                    <thead>
                        <tr>
                            <th>DNI</th>
                            <th>Semana</th>
                            <th>Asiste en la fecha</th>
                        </tr>
                    </thead>
                    <tbody>
                        <!-- Aquí se llenarán las últimas asistencias -->
                    </tbody>
                </table>
            </div>
        </div>

        <div id="matriculados-presencia" class="section">
            <h2>Listado de Estudiantes Matriculados Modalidad Presencial</h2>
            <div class="form-group">
                <label for="dni-matriculado">D.N.I</label>
                <input type="text" id="dni-matriculado" placeholder="Ingrese D.N.I del alumno">
                <label for="apellido-matriculado">Apellido</label>
                <input type="text" id="apellido-matriculado" placeholder="Ingrese apellido del alumno">
                <label for="nombre-matriculado">Nombre</label>
                <input type="text" id="nombre-matriculado" placeholder="Ingrese nombre del alumno">
                <label for="horario-matriculado">Horario para Cursado</label>
                <input type="text" id="horario-matriculado" placeholder="Ingrese día y hora">
                <button onclick="buscarMatriculado()">Buscar</button>
            </div>
            <div id="resultado-matriculado" class="result">
                <h3>Días de Asistencia</h3>
                <ul id="dias-asistencia">
                    <!-- Aquí se llenarán los días de asistencia -->
                </ul>
            </div>
        </div>

        <div id="base-datos" class="section">
            <h2>Listado de Asistencias e Ingreso a clases de los Estudiantes</h2>
            <div class="form-group">
                <label for="semana">Semana N°</label>
                <select id="semana">
                    <!-- Opciones de la semana del 0 al 100 -->
                    <script>
                        for (let i = 0; i <= 100; i++) {
                            document.write(`<option value="${i}">${i}</option>`);
                        }
                    </script>
                </select>
                <label for="dia">Día</label>
                <select id="dia">
                    <option value="Lunes">Lunes</option>
                    <option value="Martes">Martes</option>
                    <option value="Miércoles">Miércoles</option>
                    <option value="Jueves">Jueves</option>
                    <option value="Viernes">Viernes</option>
                    <option value="Sábado">Sábado</option>
                    <option value="Domingo">Domingo</option>
                </select>
                <label for="hora-inicio">Hora Inicio</label>
                <input type="text" id="hora-inicio" placeholder="Ingrese la hora de inicio">
                <button onclick="buscarAsistencias()">Buscar</button>
            </div>
            <div id="resultado-asistencias" class="result">
                <h3>Resultados de Asistencia</h3>
                <ul id="lista-asistencias">
                    <!-- Aquí se llenarán las asistencias -->
                </ul>
            </div>
        </div>
    </div>

    <script>
        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            if (username === 'Thomas Almada' && password === '2002') {
                document.getElementById('login-form').style.display = 'none';
                document.getElementById('menu').style.display = 'block';
            } else {
                alert('Usuario o contraseña incorrectos');
            }
        }

        function logout() {
            document.getElementById('menu').style.display = 'none';
            document.getElementById('login-form').style.display = 'block';
            document.querySelectorAll('.section').forEach(section => {
                section.style.display = 'none';
            });
        }

        function showSection(sectionId) {
            document.querySelectorAll('.section').forEach(section => {
                section.style.display = 'none';
            });
            document.getElementById(sectionId).style.display = 'block';
        }

        function buscarEstudiante() {
            // Simulación de búsqueda
            document.getElementById('nombre-alumno').innerText = 'Juan Pérez';
            document.getElementById('dni-alumno').innerText = document.getElementById('dni').value;
            document.getElementById('asistencias-alumno').querySelector('tbody').innerHTML = `
                <tr><td>12345678</td><td>12</td><td>202
