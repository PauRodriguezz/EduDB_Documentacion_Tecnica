# 📘 Ficha Técnica — Módulo 2: Red Semántica (Modelo Conceptual)

## 1. Propósito del componente
La Red Semántica constituye el **modelo conceptual central** del sistema EduDB.  
Su función es representar formalmente el conocimiento del dominio de normalización de bases de datos mediante **nodos (conceptos)** y **relaciones**.

Este módulo responde a estas preguntas:
- ¿Qué conceptos existen en el dominio?  
- ¿Cómo se relacionan entre sí?  
- ¿Qué necesita el sistema para evaluar una Forma Normal?  
- ¿Cómo modelamos dependencias funcionales, atributos y esquemas?  

La red semántica sirve como **fuente de verdad conceptual** y como puente entre:
- el diagrama de procesos (Módulo 1),  
- el modelo lógico con frames (Módulo 3),  
- y la implementación final en Neo4j (Módulo 4).


## 2. Entradas
Este módulo no recibe entradas del usuario; define la estructura base del conocimiento.
Toda instancia futura (esquemas ingresados por usuarios, DF, atributos, evaluaciones) se modela **siguiendo este diseño conceptual**.

## 3. Salidas
- Un **modelo conceptual completo** del dominio de normalización.  
- Definición explícita de:
  - entidades principales  
  - relaciones entre conceptos  
  - elementos necesarios para evaluar 1FN, 2FN y 3FN  
- Una base conceptual que permite construir:
  - reglas en los Frames  
  - constraints y metamodelo en Neo4j  
  - consultas para el agente LLM

## 4. Herramientas utilizadas y entorno
- Diagrama de red semántica realizado mediante herramientas de diagramación (Miro).  
- Basado en teoría formal:
  - Dependencias funcionales
  - Claves primarias y compuestas
  - Conceptos de 1FN, 2FN y 3FN
- Definición estructural antes de la implementación en grafos.


## 5. Arquitectura o funcionamiento interno
La red semántica se construye con los siguientes **conceptos (nodos)**:

### 📌 **Nodos centrales**
- **Evaluar Forma Normal**  
- **Esquema**  
- **Atributo**  
- **Dependencia Funcional**  

### 📌 **Nodos teóricos**
- **Tipo de Forma Normal**: 1FN, 2FN, 3FN  
- **Criterios asociados**:
  - Sin atributos multivaluados  
  - Clave primaria compuesta  
  - Sin dependencias parciales  
  - Sin dependencias transitivas  

### 📌 **Relaciones principales**
- **Evaluar FN → Esquema**  
- **Esquema → Tiene Atributos**  
- **Esquema → Define Dependencias Funcionales**  
- **Dependencia Funcional → Determina Desde/Hasta un Atributo**  
- **Tipo FN → Requiere → Criterio**  
- **2FN → Depende de 1FN**  
- **3FN → Depende de 2FN**  

Estas relaciones permiten que el sistema comprenda *cómo* debe analizase un esquema y *qué* condiciones se deben verificar.

### Tabla de conceptos del modelo

| Nodo | Relaciones | Descripción |
|------|------------|-------------|
| **Evaluar Forma Normal** | Evalúa → Esquema, Determina → FN | Proceso que inicia la evaluación. |
| **Esquema** | Tiene → Atributo, Define → DF | Representa un conjunto de atributos y dependencias. |
| **Atributo** | Puede ser → PK o No-PK | Cada columna del esquema. |
| **Dependencia Funcional** | Desde → Atributo, Hasta → Atributo, Tipo → (Plena, Parcial, Transitiva) | Relación funcional usada para evaluar FN. |
| **Tipo FN (1FN, 2FN, 3FN)** | Requiere → Criterio, Depende de → FN anterior | Nivel teórico de normalización. |
| **Criterios** | Cumplen → (Condiciones específicas) | Reglas necesarias para alcanzar cada FN. |


> **📌 Captura del diagrama de MODELO CONCEPTUAL**  

![Proyecto_Grupal_Modelo conceptual](https://github.com/user-attachments/assets/1850f83c-42a6-4906-8e64-4715e45befbf)


## 7. Ejemplo de instancia dentro del modelo conceptual
### **Esquema modelado: Pedido**

**Atributos:**
- IDProducto (PK)  
- IDPedido (PK)  
- NroPedido  
- NombreProducto  
- Cantidad  

**Dependencias funcionales:**
- (IDProducto, IDPedido) → Cantidad  
- IDProducto → NombreProducto  
- IDPedido → NroPedido  

**Interpretación conceptual:**
- Existe una PK compuesta.  
- Hay dependencias parciales.  
- Esto indica violaciones de **2FN**.  

El modelo conceptual muestra cómo estas relaciones se conectan a los criterios:
- PK compuesta ✔  
- Sin dependencias parciales ❌  
→ **Resultado conceptual: NO CUMPLE 2FN**

> **📌 Captura del diagrama de modelo conceptual con instancia**

![Proyecto_grupal - Modelo conceptual con una instancia](https://github.com/user-attachments/assets/7acefe66-fa35-43c6-adfa-3fb1e3b68452)

### Relación con módulos posteriores

#### 🔗 Módulo 3 — Frames
Cada nodo de la red semántica se convierte en un Frame o Slot:
- Esquema → Frame ESQUEMA  
- DF → Frame DEPENDENCIA_FUNCIONAL  
- Criterios → Slots booleanos  
- FN → Frames 1FN, 2FN y 3FN  

####  🔗 Módulo 4 — Neo4j
La red semántica es la **plantilla** con la que se construyó:
- El metamodelo  
- Las constraints  
- Las relaciones del grafo  
- La instanciación real de esquemas  

#### 🔗 Módulo 5 — LLM + LangChain
El LLM interpreta preguntas y extrae elementos definidos aquí:
- nombres de esquemas  
- atributos  
- forma normal solicitada  


## 8. Resultados obtenidos (pruebas)
La red semántica: 
- Permitió definir reglas consistentes para 1FN, 2FN y 3FN.  
- Gui­ó correctamente la estructuración del grafo en Neo4j.  
- Mostró ser suficiente para representar todos los casos de uso requeridos.

## 9. Observaciones y sugerencias
- En una versión futura, podría integrarse información sobre *violaciones detectadas* como nodos adicionales.  
- El modelo puede extenderse si el sistema incorpora recomendación automática de correcciones.

