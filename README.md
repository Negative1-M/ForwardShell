# ForwardShell

**ForwardShell** es una herramienta de shell interactivo que permite la ejecución remota de comandos en un servidor a través de peticiones HTTP. Utiliza codificación Base64 para enviar los comandos y puede iniciar una pseudo-terminal o ejecutar comandos predefinidos como la enumeración de binarios con SUID.

## Requisitos

- Python 3.x
- Biblioteca `requests` (puede instalarse con `pip install requests`)
- Acceso a un servidor que ejecute un script vulnerable en `index.php` o similar que permita ejecutar comandos a través de peticiones HTTP.

## Uso

1. Inicia el programa:
    ```bash
    python3 ForwardShell.py
    ```

2. Ingresa los comandos que deseas ejecutar en el servidor remoto. Por ejemplo:
    ```bash
    > ls -la
    ```

3. Opciones especiales:
    - **Pseudo-terminal**: Inicia una pseudo-terminal ingresando:
      ```bash
      > script /dev/null -c bash
      ```
    - **Enumeración de SUID**: Ejecuta el comando para listar archivos con el bit SUID activado:
      ```bash
      > enum suid
      ```

4. Para salir del shell, usa el comando:
    ```bash
    > exit
    ```

## Explicación del Código

- **run_command(command)**: Envía el comando codificado en Base64 al servidor remoto y ejecuta `/bin/sh` para procesarlo.
- **write_stdin(command)** y **read_stdout()**: Utilizan archivos FIFO ubicados en `/dev/shm/` para enviar comandos y leer su salida.
- **setup_shell()**: Crea un entorno shell básico usando FIFO para manejar la entrada y salida de comandos.
- **remove_data()**: Elimina los archivos temporales creados en `/dev/shm/`.
- **clear_stdout()**: Limpia el contenido del archivo de salida para evitar acumulación de datos.

## Notas

- El programa requiere que el servidor de destino esté vulnerable a la ejecución remota de comandos a través de peticiones HTTP.
- El uso de este tipo de herramientas sin autorización en servidores ajenos es ilegal y puede tener consecuencias legales graves.

## Advertencia Legal

El uso de esta herramienta debe ser únicamente con fines educativos y en sistemas en los que tienes permiso para realizar pruebas de seguridad.
