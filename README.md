# Robotica_lab1
entrega primer laboratorio de robótica de la universidad nacional de Colombia.

Para la realización de la práctica se creó una herramienta para sosstener el marcador cuidando que la herramienta no generae errores de gimbal lock o singularidad en el manipulador del robot.
Luego de dieñar la herramienta e imprimirla en 3D se procedió a crear la trayectoria en forma de líneas y curvas en un software CAD.

Tanto la trayectoria como la herramienta fueron exportadas al software de simulación Robot Studio.
Donde se especificaaron los datos necesarios para la creación del TCP de la herramienta y e creó un workobject para definir la trayectoria

Utilizando las herramientas de creación de rutas, se eligieron los puntos (robtarget) de la trayectoria respecto al workobject creado y luego se procedió a trazar la ruta con los puntos seleccionados.

Una vez hecho esto se sincronizó la ruta con los controladores virtuales del software para generar un código en RAPID y se editó el código de RAPID para evitar colisiones, errores de singularidad y modificar puntos no alcanzables.
utilizando el editor de ruta de RAPID se terminó de configurar las intrucciones de movimiento del módulo, velocidades y zonas.

Una vez se terminó de configurar el módulo de RAPID y de asegurarse que las simulaciones funcionaran, se procedió a probar la ruta en los robots reales definiendo el workobject en la esquina inferior derecha del pastel/papel.
Tomando las precauciones debidas, zona de trabajo despejada y un asistente en el botón de parada de emergencia. Se logró realizar satisfaactoriamente la ruta
