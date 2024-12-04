Este código utiliza OpenCV y GPIO en una Raspberry Pi para controlar un motor mediante el driver L298N, en función de la posición de un rectángulo rojo detectado en la imagen capturada por la cámara.

IN3 y IN4: Pines de control para determinar la dirección del motor.
ENB: Pin de habilitación que utiliza PWM para controlar la velocidad del motor.
Raspberry Pi GPIO

Se usa para enviar señales al L298N y controlar el motor.
Cámara

Captura la imagen en tiempo real para procesar.
Flujo del Programa
1. Configuración Inicial
GPIO: Los pines se configuran como salidas.
PWM: Se inicializa en el pin ENB con una frecuencia de 50 Hz y un ciclo de trabajo del 50%.
OpenCV: Se configura la cámara para capturar imágenes.
2. Procesamiento de Imagen
Convertir el fotograma de BGR a HSV.
Crear dos máscaras para detectar el color rojo:
Rojo claro (lower_red1 a upper_red1).
Rojo oscuro (lower_red2 a upper_red2).
Unir ambas máscaras para identificar todos los tonos de rojo.
Encontrar contornos en la máscara combinada.
Dibujar rectángulos alrededor de los contornos detectados que superen un área mínima de 1000 píxeles.
3. Control del Motor
Se calcula el centroide del contorno (posición X).
Comparar la posición X del rectángulo con el centro del marco:
Si está a la izquierda, el motor gira en una dirección.
Si está a la derecha, gira en la dirección opuesta.
Esto se logra configurando los pines IN3 y IN4.
4. Bucle Principal
Captura continuamente fotogramas de la cámara.
Procesa el fotograma para detectar rectángulos rojos.
Controla el motor en función de la posición detectada.
Muestra el fotograma procesado con rectángulos dibujados.
5. Finalización
Se liberan los recursos de la cámara.
Se detiene el PWM y se limpian los pines GPIO.
Detalles Técnicos
Configuración del L298N
IN3 y IN4 controlan la dirección:
IN3 = HIGH, IN4 = LOW: Gira en una dirección.
IN3 = LOW, IN4 = HIGH: Gira en la dirección opuesta.
Máscaras de Color
Tonos de rojo:
Rojo claro: [0, 40, 40] a [20, 255, 255].
Rojo oscuro: [150, 40, 40] a [180, 255, 255].
Estas máscaras permiten detectar colores en el rango completo de tonos de rojo.



