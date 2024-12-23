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
¡Claro! A continuación, te proporciono una plantilla en **Markdown** para que puedas completar el informe del **Laboratorio No. 01 - Robótica Industrial**. Incluye secciones para texto, imágenes, figuras, links y cualquier otro material que necesites agregar.

---

# **Laboratorio No. 01 - Robótica Industrial**
## **Trayectorias, Entradas y Salidas Digitales**

---

## **1. Introducción**
El presente informe tiene como objetivo documentar las actividades realizadas en el **Laboratorio No. 01 de Robótica Industrial**, enfocado en el uso de robots ABB IRB 140 y la plataforma RobotStudio. El laboratorio se centra en el diseño y simulación de trayectorias, calibración de herramientas, programación en RAPID y manejo de entradas y salidas digitales.

El contexto de este laboratorio surge de la necesidad de automatizar procesos industriales específicos, como la **decoración de tortas** mediante robots, garantizando precisión, eficiencia y consistencia en las operaciones.


---

## **2. Objetivos**
### **Objetivo General:**
- Desarrollar habilidades prácticas en el diseño, simulación e implementación de trayectorias para un robot ABB IRB 140 mediante RobotStudio y programación RAPID.

### **Objetivos Específicos:**
- Conocer los elementos de un robot industrial.
- Calibrar herramientas tanto en RobotStudio como en el robot real.
- Identificar y aplicar los tipos de movimientos MOVJ y MOVL.
- Diseñar y simular trayectorias específicas.
- Manejar el módulo de entradas y salidas digitales en el controlador IRC5.
- Integrar sensores para la definición de workobjects.

---

## **3. Diseño de la Herramienta**
### **Descripción de la Herramienta Diseñada:**
Se diseñó una herramienta que permite fijar un marcador a la brida del robot ABB IRB 140. Esta herramienta asegura una sujeción estable y permite realizar trayectorias precisas sobre una superficie.

![image](https://github.com/user-attachments/assets/b201da77-73fb-48eb-9e48-b03e7168cb93)

### **Modelo CAD de la Herramienta:**
El diseño se modeló en un software CAD y se exportó en formato `.STL` para su importación en RobotStudio.

### **Parámetros de Diseño:**
- Material: PLC
- Tipo de sujeción: Por friccion al marcador
- Adaptación al flanche: 4 tornillos

![image](https://github.com/user-attachments/assets/7739ee76-a5b7-42cf-ac46-aae5367c6d8d)


### **Calibración de la Herramienta:**
El proceso de calibración se llevó a cabo tanto en **RobotStudio** como en el robot físico, asegurando que las coordenadas del TCP (Tool Center Point) estuvieran correctamente definidas llevando el TCP al mismo punto desde 3 orientaciones distintas y definiendo una direccion de avance.


---

## **4. Desarrollo de las Trayectorias**
### **Descripción de las Trayectorias Diseñadas:**
Se diseñaron trayectorias para escribir las cinco primeras letras de los nombres de los integrantes del grupo y realizar una decoración adicional.

### **Parámetros de Movimiento:**
- **Velocidad:** Entre 100 y 1000.
- **Zona tolerable de errores:** z10.
- **Posición inicial y final:** Home.

### **Workobject:**
Se configuró una superficie inclinada a 30° para replicar la tarea en diferentes cuadrantes.

**Campo de respuesta:**
*(Describe tus trayectorias y agrega imágenes o diagramas)*

**Imagen de la trayectoria en RobotStudio:**
![Agregar Imagen](#)

---

## **5. Programación en RAPID**
### **Código RAPID Utilizado:**
El siguiente ejemplo muestra una estructura básica para las trayectorias:

```RAPID
MODULE Module1
    CONST jointtarget home:=[[0,0,0,0,-45,0],[9E9,9E9,9E9,9E9,9E9,9E9]];
    PROC main()
        TPWrite "Iniciando decoración";
        MoveAbsJ home, v500, fine, tool0;
        ! Añadir más instrucciones aquí
    ENDPROC
ENDMODULE
```

**Campo de respuesta:**
*(Agrega aquí tu código RAPID completo si es diferente al ejemplo proporcionado)*

---

## **6. Entradas y Salidas Digitales**
### **Configuración de Señales Digitales:**
- **Entrada 1:** Inicia la rutina de decorado.
- **Entrada 2:** Posiciona el robot en modo mantenimiento.
- **Salida 1:** Activa la luz de indicación.
- **Salida 2:** Apaga la luz de indicación.

**Campo de respuesta:**
*(Describe tu configuración y agrega diagramas o capturas)*

---

## **7. Implementación del Sensor**
### **Descripción del Sensor:**
Se instaló un sensor en la herramienta para detectar la posición del *workobject*.

### **Calibración y Posicionamiento:**
Se calibró el sensor para garantizar una detección precisa.

**Campo de respuesta:**
*(Agrega texto e imágenes sobre el sensor)*

---

## **8. Diagrama de Flujo**
### **Descripción del Flujo de Operaciones:**
A continuación, se presenta un diagrama de flujo que describe las acciones del robot.

**Diagrama de Flujo:**
![Agregar Imagen](#)

---

## **9. Plano de Ubicación de Elementos**
Se presenta un plano que muestra la ubicación de los elementos clave: herramienta, sensor y superficie de trabajo.

**Plano de Ubicación:**
![Agregar Imagen](#)

---

## **10. Resultados Obtenidos**
- **Simulación en RobotStudio:** *(Describe la simulación)*
- **Implementación en Robot Real:** *(Describe los resultados físicos)*

**Enlace al video de la simulación:**
[Enlace al video](#)

---

## **11. Conclusiones**
Se presentan las conclusiones derivadas del desarrollo del laboratorio, los aprendizajes clave y posibles mejoras para futuras prácticas.

**Campo de respuesta:**
*(Escribe tus conclusiones aquí)*

---

## **12. Repositorio en GitHub**
Se proporciona el enlace al repositorio donde se encuentran los archivos y el código completo.

**Enlace al repositorio:**
[Repositorio GitHub](#)

---

¡Informe completado! 🚀 Si necesitas ajustes adicionales, ¡avísame!

