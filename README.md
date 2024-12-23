# **Laboratorio No. 01 - Robótica Industrial**
## **Trayectorias, Entradas y Salidas Digitales**

---

## **1. Objetivos**
### **Objetivo General:**
- Desarrollar habilidades prácticas en el diseño, simulación e implementación de trayectorias para un robot ABB IRB 140 mediante RobotStudio y programación RAPID.

### **Objetivos Específicos:**
- Conocer los elementos de un robot industrial.
- Calibrar herramientas tanto en RobotStudio como en el robot real.
- Identificar y aplicar los tipos de movimientos MOVJ y MOVL.
- Diseñar y simular trayectorias específicas.
- Manejar el módulo de entradas y salidas digitales en el controlador IRC5.
- Integrar sensores para la definición de workobjects.

Para la realización de la práctica se creó una herramienta para sostener el marcador cuidando que la herramienta no generara errores de *gimbal lock* o singularidad en el manipulador del robot.

---

## **2. Diseño de la Herramienta**
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

![image](https://github.com/user-attachments/assets/6a214994-eee2-4a2b-8f8d-916e800cae65)

---

## **3. Desarrollo de las Trayectorias**
### **Descripción de las Trayectorias Diseñadas:**
Se diseñaron trayectorias para escribir las cinco primeras letras de los nombres de los integrantes del grupo y realizar una decoración adicional.
Mediante Autocad se diseñaron las geometrias de cada una de las letras y la torta a decorar, luego se exportó en formato .SAT y se importó como una geometria en robot studio:

![image](https://github.com/user-attachments/assets/b11e2636-41ca-49a9-b437-922122466578)

Utilizando las herramientas de creación de rutas, se eligieron los puntos (*robtarget*) de la trayectoria respecto al *workobject* creado:

![image](https://github.com/user-attachments/assets/9878254d-2dce-4c6e-89b4-b302611d895d)

Luego se procedió a trazar la ruta con los puntos seleccionados:

![image](https://github.com/user-attachments/assets/6341238c-257b-44ed-a8b8-6d0756cf17e4)

### **Parámetros de Movimiento:**
- **Velocidad:** Entre 100 y 1000.
- **Zona tolerable de errores:** z10.
- **Posición inicial y final:** Home.

### **Workobject:**
Se configuró una superficie inclinada a 30° para replicar la tarea en diferentes cuadrantes.

Una vez hecho esto, se sincronizó la ruta con los controladores virtuales del software para generar un código en RAPID. Se editó el código RAPID para evitar colisiones, errores de singularidad y modificar puntos no alcanzables.


https://github.com/user-attachments/assets/afbffb6b-02c6-4d95-a072-a3922f04cfd2


---

## **4. Programación en RAPID**
### **Código RAPID Utilizado:**
El siguiente ejemplo muestra la estructura básica para la trayectoria:

```RAPID
MODULE Module1
        PERS tooldata MyNewTool:=[TRUE,[[25.289,0,191.739],[0.923879533,0,0.382683432,0]],[0.5,[-37.543,-11.677,118.601],[1,0,0,0],0,0,0]];
    TASK PERS wobjdata Workobject_1:=[FALSE,TRUE,"",[[615,-85,200],[0.965925826,0,-0.258819045,0]],[[0,0,0],[1,0,0,0]]];
    CONST robtarget Target_10:=[[149.241,70.858,24],[0.130526196,0,0.991444861,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_20:=[[149.241,70.858,0],[0.130526196,0,0.991444861,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_30:=[[135.099,85,0],[0.130526196,0,0.991444861,0],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_40:=[[149.241,99.142,0],[0.130526196,0,0.991444861,0],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_50:=[[163.384,85,0],[0.130526196,0,0.991444861,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_60:=[[149.241,70.858,0],[0.130526196,0,0.991444861,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_70:=[[149.241,70.858,24],[0.130526196,0,0.991444861,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_80:=[[99.757,120.09,24],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_90:=[[99.757,120.09,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_100:=[[99.757,117.868,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_110:=[[101.05812907,114.725008652,0.000349024],[0.130526181,-0.000000019,0.991444863,0.000000016],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_120:=[[104.201,113.423,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_130:=[[119.757,113.423,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_140:=[[119.757,113.423,24],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_150:=[[114.201,106.757,24],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_160:=[[114.201,106.757,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_170:=[[119.757,101.201,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_180:=[[114.201,95.645,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_190:=[[105.312,95.645,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_200:=[[99.757,101.201,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_210:=[[105.312,106.757,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_220:=[[114.201,106.757,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_230:=[[114.201,106.757,24],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_240:=[[100.868,88.979,24],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_250:=[[100.868,88.979,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_260:=[[99.766,86.31,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_270:=[[99.757,83.423,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_280:=[[103.37,78.987,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_290:=[[108.646,81.201,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_300:=[[110.312,83.979,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_310:=[[111.979,86.757,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_320:=[[115.054,88.861,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_330:=[[118.646,87.868,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_340:=[[119.766,83.423,0],[0.130526201,0,0.99144486,-0.000000003],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_350:=[[118.646,78.979,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_360:=[[118.646,78.979,24],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_370:=[[99.757,63.423,24],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_380:=[[99.757,63.423,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_390:=[[99.757,72.312,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_400:=[[110.868,72.312,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_410:=[[110.868,65.645,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_420:=[[110.868,72.312,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_430:=[[119.757,72.312,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_440:=[[119.757,63.423,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_450:=[[119.757,63.423,24],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_460:=[[99.757,56.757,24],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_470:=[[99.757,56.757,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_480:=[[119.757,50.09,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_490:=[[99.757,43.423,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_500:=[[105.312,45.645,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_510:=[[105.312,54.534,0],[0.130526201,0,0.99144486,-0.000000003],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_520:=[[61.026,117.682,24],[0.130526198,0,0.991444861,-0.000000001],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_530:=[[61.026,117.682,0],[0.130526198,0,0.991444861,-0.000000001],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_540:=[[81.026,111.016,0],[0.130526198,0,0.991444861,-0.000000001],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_550:=[[61.026,104.349,0],[0.130526198,0,0.991444861,-0.000000001],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_560:=[[66.582,106.571,0],[0.130526198,0,0.991444861,-0.000000001],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_570:=[[66.582,115.46,0],[0.130526198,0,0.991444861,-0.000000001],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_580:=[[66.582,115.46,24],[0.130526198,0,0.991444861,-0.000000001],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_590:=[[61.026,88.794,24],[0.130526198,0,0.991444861,-0.000000001],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_600:=[[61.026,88.794,0],[0.130526198,0,0.991444861,-0.000000001],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_610:=[[61.026,97.682,0],[0.130526198,0,0.991444861,-0.000000001],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_620:=[[81.026,97.682,0],[0.130526198,0,0.991444861,-0.000000001],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_630:=[[81.026,97.682,24],[0.130526198,0,0.991444861,-0.000000001],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_640:=[[61.026,73.238,24],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_650:=[[61.026,73.238,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_660:=[[61.026,82.127,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_670:=[[72.137,82.127,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_680:=[[72.137,75.46,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_690:=[[72.137,82.127,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_700:=[[81.026,82.127,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_710:=[[81.026,73.238,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_720:=[[81.026,73.238,24],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_730:=[[61.026,66.571,24],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_740:=[[61.026,66.571,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_750:=[[61.026,64.349,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_760:=[[62.328,61.206,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_770:=[[65.471,59.905,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_780:=[[81.026,59.905,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_790:=[[81.026,59.905,24],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_800:=[[61.026,53.238,24],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_810:=[[61.026,53.238,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_820:=[[81.026,46.571,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_830:=[[61.026,39.905,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_840:=[[66.582,42.127,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_850:=[[66.582,51.016,0],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_860:=[[66.582,51.016,24],[0.130526198,0,0.991444861,-0.000000001],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_870:=[[26.922,119.639,24],[0.130526152,0,0.991444867,0],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_880:=[[26.922,119.639,0],[0.130526152,0,0.991444867,0],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_890:=[[46.922,112.972,0],[0.130526152,0,0.991444867,0],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_900:=[[26.922,106.305,0],[0.130526152,0,0.991444867,0],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_910:=[[32.478,108.527,0],[0.130526152,0,0.991444867,0],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_920:=[[32.478,117.416,0],[0.130526152,0,0.991444867,0],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_930:=[[32.478,117.416,24],[0.130526152,0,0.991444867,0],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_940:=[[26.922,90.75,24],[0.130526152,0,0.991444867,0],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_950:=[[26.922,90.75,0],[0.130526152,0,0.991444867,0],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_960:=[[26.922,99.639,0],[0.130526152,0,0.991444867,0],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_970:=[[46.922,99.639,0],[0.130526152,0,0.991444867,0],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_980:=[[46.922,99.639,24],[0.130526152,0,0.991444867,0],[0,2,-3,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_990:=[[26.922,75.194,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1000:=[[26.922,84.083,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1010:=[[38.033,84.083,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1020:=[[38.033,77.416,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1030:=[[38.033,84.083,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1040:=[[46.922,84.083,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1050:=[[46.922,75.194,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1060:=[[46.922,75.194,24],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1070:=[[26.922,68.527,24],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1080:=[[26.922,68.527,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1090:=[[26.922,66.305,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1100:=[[28.224,63.163,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1110:=[[31.367,61.861,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1120:=[[46.922,61.861,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1130:=[[46.922,61.861,24],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1140:=[[26.922,55.194,24],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1150:=[[26.922,55.194,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1160:=[[46.922,48.527,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1170:=[[26.922,41.861,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1180:=[[32.478,44.083,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1190:=[[32.478,52.972,0],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_1200:=[[32.478,52.972,24],[0.130526152,0,0.991444867,0],[-1,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];

    PROC main()
        !Add your code here
    ENDPROC
    PROC Path_10()
        MoveJ Target_10,v100,fine,MyNewTool\WObj:=Workobject_1;
        MoveL Target_20,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_30,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_40,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_50,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_60,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_70,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_80,v100,fine,MyNewTool\WObj:=Workobject_1;
        MoveL Target_90,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_100,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveC Target_110,Target_120,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_130,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_140,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_150,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_160,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveC Target_170,Target_180,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_190,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveC Target_200,Target_210,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_220,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_230,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_240,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_250,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_260,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_270,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveC Target_280,Target_290,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_300,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_310,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveC Target_320,Target_330,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveC Target_340,Target_350,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_360,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_370,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_380,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_390,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_400,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_410,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_420,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_430,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_440,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_450,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_460,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_470,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_480,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_490,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_500,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_510,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_520,v100,fine,MyNewTool\WObj:=Workobject_1;
        MoveL Target_530,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_540,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_550,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_560,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_570,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_580,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_590,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_600,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_610,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_620,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_630,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_640,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_650,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_660,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_670,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_680,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_690,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_700,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_710,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_720,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_730,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_740,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_750,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveC Target_760,Target_770,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_780,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_790,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_800,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_810,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_820,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_830,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_840,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_850,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_860,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_870,v100,fine,MyNewTool\WObj:=Workobject_1;
        MoveL Target_880,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_890,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_900,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_910,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_920,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_930,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_940,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_950,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_960,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_970,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_980,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_990,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1000,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1010,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1020,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1030,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1040,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1050,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1060,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1070,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1080,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1090,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveC Target_1100,Target_1110,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1120,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1130,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1140,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1150,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1160,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1170,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1180,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1190,v100,z10,MyNewTool\WObj:=Workobject_1;
        MoveL Target_1200,v100,z10,MyNewTool\WObj:=Workobject_1;
    ENDPROC
ENDMODULE
```

Utilizando el editor de ruta de RAPID se terminó de configurar las instrucciones de movimiento del módulo, velocidades y zonas.

---

## **5. Implementación en el Robot Real**
Una vez se terminó de configurar el módulo de RAPID y de asegurarse que las simulaciones funcionaran, se procedió a probar la ruta en los robots reales definiendo el *workobject* en la esquina inferior derecha del pastel/papel.
Tomando las precauciones debidas, zona de trabajo despejada y un asistente en el botón de parada de emergencia, se logró realizar satisfactoriamente la ruta.


---

## **6. Entradas y Salidas Digitales**
### **Configuración de Señales Digitales:**

# Explicación Conceptual del Programa RAPID

El programa controla un **robot industrial** con dos modos principales de funcionamiento: **Operación normal** y **Modo de mantenimiento**.

---

##  *1. Operación Normal**  
- El robot **espera una señal de inicio** (entrada digital) para comenzar su tarea principal.  
- Al recibir esta señal:  
   - El robot **realiza una trayectoria predefinida**, moviéndose entre puntos específicos.  
   - Se **activa una salida digital** (por ejemplo, una luz) para indicar que está en operación.  
- Una vez finalizada la trayectoria:  
   - La **salida digital se apaga**.  
   - El robot **regresa a su estado de espera**, listo para recibir una nueva señal de inicio.

---

##  *2. Modo de Mantenimiento**  
- Si el robot recibe una **señal específica para mantenimiento** (segunda entrada digital):  
   - **Interrumpe cualquier acción en curso.**  
   - Se **desplaza a una posición segura predefinida** para mantenimiento.  
   - Se **activa una segunda salida digital** para indicar que está en modo mantenimiento.  
- El robot **permanece en esta posición** hasta recibir una nueva señal de inicio:  
   - Al recibir la señal, la **salida digital de mantenimiento se apaga**.  
   - El robot **vuelve al estado de espera**, listo para operar nuevamente.

---

##  *Resumen del Comportamiento**  
- **Operación normal:** El robot realiza su tarea y enciende una señal de operación.  
- **Modo mantenimiento:** El robot se mueve a una posición segura y activa una señal de mantenimiento.  
- El sistema es **cíclico** y siempre espera nuevas órdenes para cambiar su estado.
```
MODULE MainModule

    ! Declaración de señales
    VAR signaldi diStart := di1;           ! Entrada digital para iniciar trayectoria
    VAR signaldo doTrajActive := do1;      ! Salida digital activa durante la trayectoria
    VAR signaldi diMaintenance := di2;     ! Entrada digital para mantenimiento
    VAR signaldo doMaintenanceMode := do2; ! Salida digital activa en modo mantenimiento

    ! Puntos de trayectoria
    CONST robtarget pStart:=[[500,0,500],[1,0,0,0],[-1,0,0,0],[0,0,0,0]];
    CONST robtarget pEnd:=[[1000,0,500],[1,0,0,0],[-1,0,0,0],[0,0,0,0]];
    CONST robtarget pMaintenance:=[[0,500,500],[1,0,0,0],[-1,0,0,0],[0,0,0,0]];

    ! Rutina principal
    PROC main()
        WHILE TRUE DO
            IF diMaintenance = 1 THEN
                MaintenanceMode();
            ELSEIF diStart = 1 THEN
                Trajectory();
            ENDIF
            WaitTime 0.1; ! Pequeño retraso para evitar sobrecarga del sistema
        ENDWHILE
    ENDPROC

    ! Rutina para la trayectoria
    PROC Trajectory()
        Set doTrajActive;    ! Encender salida digital para indicar trayectoria activa
        MoveJ pStart, v100, fine, tool0;
        MoveL pEnd, v200, fine, tool0;
        MoveJ pStart, v100, fine, tool0;
        Reset doTrajActive;  ! Apagar salida digital al finalizar
        WaitUntil diStart = 0; ! Esperar a que la entrada se apague antes de continuar
    ENDPROC

    ! Rutina para mantenimiento
    PROC MaintenanceMode()
        Set doMaintenanceMode; ! Encender salida digital para modo mantenimiento
        MoveJ pMaintenance, v100, fine, tool0;
        WaitUntil diMaintenance = 0; ! Esperar a que la entrada se apague
        Reset doMaintenanceMode; ! Apagar salida digital de mantenimiento
    ENDPROC

ENDMODULE
```

Este enfoque asegura que el robot **trabaje de manera eficiente** en su tarea principal y pueda **realizar mantenimiento de forma segura** cuando sea necesario.


---

## **8. Diagrama de Flujo**
### **Descripción del Flujo de Operaciones:**
A continuación, se presenta un diagrama de flujo que describe las acciones del robot.

```plaintext
                 +-------------------------+
                 |      INICIO             |
                 +-----------+-------------+
                             |
                             v
                 +-------------------------+
                 | ¿Entrada Digital 1 ON?  |
                 +-----------+-------------+
                      No |        | Sí
                         |        v
                         | +----------------+
                         | | Activar Salida |
                         | | Realizar       |
                         | | Trayectoria    |
                         | +----------------+
                         |        |
                         |        v
                         | +----------------+
                         | | Desactivar     |
                         | | Salida         |
                         | +----------------+
                         |        |
                         v        |
                 +-------------------------+
                 | ¿Entrada Digital 2 ON?  |
                 +-----------+-------------+
                      No |        | Sí
                         |        v
                         | +----------------+
                         | | Ir a Posición  |
                         | | de Mantenimiento|
                         | | Activar Salida |
                         | +----------------+
                         |        |
                         |        v
                         | +----------------+
                         | | ¿Entrada Digital|
                         | | 1 ON?          |
                         | +----------------+
                         |        |
                         |   Sí   |
                         |        v
                         | +----------------+
                         | | Desactivar     |
                         | | Salida         |
                         | +----------------+
                         |        |
                         v        |
                 +-------------------------+
                 |       ESPERAR           |
                 | Nueva señal de entrada  |
                 +-------------------------+

```

---

## **9. Plano de Ubicación de Elementos**
Se presenta un plano que muestra la ubicación de los elementos clave: herramienta, sensor y superficie de trabajo.

**Plano de Ubicación:**
![Agregar Imagen](#)

---

## **10. Resultados Obtenidos**

En esta sección se presentan los logros alcanzados durante el desarrollo del proyecto. Se logró con éxito la escritura de las primeras cinco letras de cada nombre, demostrando la precisión y funcionalidad del sistema implementado. Sin embargo, debido a la disponibilidad limitada del laboratorio, no fue posible llevar a cabo la calibración final de las entradas y salidas digitales. A pesar de esta limitación, la trayectoria programada fue probada en un plano horizontal, para lo cual se creó un nuevo workobject. Estos resultados reflejan el correcto desempeño del sistema en diferentes condiciones de operación, validando así su robustez y adaptabilidad.

https://github.com/user-attachments/assets/7687df32-6a72-4f66-b5e6-19027e26dfc2


---

## **11. Conclusiones**

-Limitaciones Operativas: La falta de disponibilidad del laboratorio impidió una calibración completa de las señales digitales, lo que restringió la validación de algunos aspectos del sistema automatizado.

-Aplicación en Diferentes Entornos: El sistema demostró ser versátil y adaptable a diferentes configuraciones de trabajo, lo que facilita su implementación en diversas aplicaciones industriales.

-Aprendizaje y Mejora Continua: El desarrollo del laboratorio permitió fortalecer conocimientos en programación de robots industriales, configuración de trayectorias y manejo de workobjects, sentando una base sólida para futuros proyectos y mejoras en el sistema.

---

## **12. Repositorio en GitHub**
Se proporciona el enlace al repositorio donde se encuentran los archivos y el código completo.

**Enlace al repositorio:**
[Repositorio GitHub](#https://github.com/JoseAlejandroRosero/Robotica_lab1/tree/main)

---

