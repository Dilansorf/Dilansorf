<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Registro de Autos Nuevos</title>
    <style>
        /* Estilos del formulario (los mismos que en el ejemplo HTML) */
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        
        /* Estilos del formulario (los mismos que en el ejemplo HTML) */
        /* ... (Resto del código CSS) */
    </style>
</head>
<body>
    <form method="post" action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]); ?>">
        <h2>Registro de Autos Nuevos</h2>
        <label for="idAuto">IdAuto:</label>
        <input type="text" id="idAuto" name="idAuto" required>

        <label for="marca">Marca:</label>
        <input type="text" id="marca" name="marca" required>

        <label for="modelo">Modelo:</label>
        <input type="text" id="modelo" name="modelo" required>

        <label for="anio">Año:</label>
        <input type="number" id="anio" name="anio" min="1900" max="2024" required>

        <label for="color">Color:</label>
        <input type="text" id="color" name="color" required>

        <label for="precio">Precio:</label>
        <input type="number" id="precio" name="precio" min="0" required>

        <button type="submit">Registrar Auto</button>
    </form>
</body>
</html>

<?php
session_start();

function conectar ($dbname){
    $servername = 'localhost';
    $username = 'root';
    $password = 'root';
    $port = 3306;
    // Crear conexión
    $conn = new mysqli($servername, $username, $password, $dbname, $port);
    // Comprobar la conexión
    if ($conn->connect_error) {
        die("Conexión a base de datos fallo: " . $conn->connect_error);
        }
    return $conn;
    }
if($_SERVER["REQUEST_METHOD"] == "POST") {
    $idauto = $_POST["idAuto"]
    $marca = $_POST["marca"];
    $modelo = $_POST["modelo"];
    $anio = $_POST["anio"];
    $color = $_POST["color"];
    $precio = $_POST["precio"];

    // Conectarse al servidor y abrir la base de datos  
    $conn = conectar ("mydb_progtools");

    // Consultar si el Usuario existe en la tabla de usuarios
    $sql = "Select * from usuarios WHERE username='$idAuto';";
    $query = $conn->query($sql); // Query the users table

    if ($query->num_rows > 0) {     // Comprobar si existe el nombre de usuario 
        $user == $row['idAuto'];  // la primera fila de nombre de usuario
                                    
        Print '<script>alert("Carro ya registrado!");</script>';            // Prompts al usuario
        Print '<script>window.location.assign("register.php");</script>';     // redirige a página register.php
        }
    else { // usuario no existe ingresarlo
        // Ingresar en Persons
        $sql = "INSERT INTO autos (marca, modelo, anio, color. precio)
                VALUES ('$idauto', '$marca', '$modelo', '$anio','$color', '$precio');";

        $sql2 = "INSERT INTO usuarios (username, contraseña, email, personid) 
        VALUES ('$username', '$password', '$correo','$idpersona');";

        if ($conn->query($sql) == TRUE && $conn->query($sql2) === TRUE) {
            Print '<script>alert("Registrado exitosamente!");</script>';      // Prompts al usuario
            Print '<script>window.location.assign("index.php");</script>'; // redirige a página index.php
            } 
        else {
            Print '<script>alert(Error:'.$conn->error.');</script>';          // Prompts al usuario
            Print '<script>window.location.assign("register.php");</script>';  // redirige a página register.php
            }
        }
    $conn->close();
    }            
?>
