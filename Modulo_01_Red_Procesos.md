# 📘 Ficha Técnica — Módulo 1: Red de Procesos del Sistema Experto

## 1. Propósito del componente
Este módulo presenta el **diagrama de flujo del sistema experto**, elaborado en Miro, que representa visualmente el recorrido lógico que sigue EduDB desde que recibe un esquema hasta que determina si cumple una Forma Normal (1FN, 2FN o 3FN).

El objetivo es **explicar de manera gráfica** la secuencia de decisiones y verificaciones, sin entrar aún en la representación conceptual (red semántica) ni en el modelo lógico (frames).  
Es una pieza de diseño, **no un componente ejecutable**.



## 2. Entradas
El diagrama conceptualiza las entradas que el sistema recibirá más adelante:

- Esquema a evaluar  
- Atributos y claves primarias  
- Dependencias funcionales  
- Forma Normal seleccionada por el usuario  



## 3. Salidas
El diagrama refleja las posibles salidas del sistema:

- Determinación: **CUMPLE** o **NO CUMPLE** la forma normal solicitada  
- Identificación de criterios incumplidos  
- Explicación textual posterior (producida por otros módulos)  



## 4. Herramientas utilizadas y entorno
- **Miro** para la creación del diagrama de flujo  
- Basado en criterios teóricos de normalización:  
  - 1FN  
  - 2FN  
  - 3FN  



## 5. Arquitectura o funcionamiento interno
El diagrama representa los pasos que sigue el sistema experto:

1. Inicio del proceso.  
2. Recepción del esquema.  
3. Selección de la Forma Normal a evaluar.  
4. Verificación de los criterios correspondientes:  
   - **1FN** → atomicidad  
   - **2FN** → PK compuesta + ausencia de dependencias parciales  
   - **3FN** → ausencia de dependencias transitivas  
5. Rama de decisión según se cumplan o no los criterios.  
6. Resultado final:  
   - “CUMPLE forma normal X”  
   - “NO CUMPLE forma normal X” con indicación del motivo  

> **📌 Captura del diagrama de procesos**

![Proyecto_Grupal- Diagrama de procesos](https://github.com/user-attachments/assets/e9b7b87b-30a8-40a7-b9f1-10491e885eef)



## 6. Código relevante
Este módulo **no tiene código**, ya que es puramente visual y conceptual, pero sirve como base de diseño para los módulos posteriores:

- Módulo 2 — Modelo Conceptual (Red Semántica)  
- Módulo 3 — Red de Frames Difusos  
- Módulo 4 — Base de Conocimiento en Neo4j  


## 7. Ejemplos de funcionamiento
Aunque este módulo no ejecuta acciones, permite visualizar cómo debería comportarse el sistema.

**Ejemplo:**  
- **Esquema:** Pedido  
- **FN solicitada:** 2FN
- El diagrama permite anticipar que si existen dependencias parciales, el flujo termina en **NO CUMPLE**.


## 8. Resultados obtenidos (pruebas)
El diagrama fue utilizado como guía para:

- Estructurar el modelo conceptual  
- Identificar los demonios y reglas activas en los Frames  
- Orientar la construcción del metamodelo y consultas en Neo4j  

El comportamiento obtenido en las pruebas coincide con la lógica representada gráficamente.



