# Documentación del Sistema de Gestión Financiera (MVC)

## 1. Introducción

Este sistema implementa un gestor financiero personal utilizando el patrón Modelo-Vista-Controlador (MVC) con las siguientes características:
- Gestión de tareas con prioridades y fechas límite
- Registro de gastos por categorías
- Interfaz gráfica basada en Tkinter
- Persistencia de datos en formato JSON

## 2. Estructura del Proyecto

### Arquitectura MVC

| Componente | Archivos | Descripción |
|------------|----------|-------------|
| **Modelo** | database.py, gasto.py, tarea.py | Maneja los datos y la lógica de negocio |
| **Vista** | consola.py | Interfaz de usuario (Tkinter) |
| **Controlador** | core.py | Mediador entre Modelo y Vista |

## 3. Documentación de Clases

### 3.1. Vista (`consola.py`)

**Clase `FinanzasUI`**:
- Interfaz gráfica principal del sistema
- Implementa dos módulos principales: gestión de tareas y gestión de gastos

**Métodos principales**:
- `__init__(self, controlador)`: Inicializa la ventana principal
- `_crear_pantalla_inicio()`: Muestra la pantalla de bienvenida
- `_mostrar_tareas()`: Muestra la interfaz de gestión de tareas
- `_mostrar_gastos()`: Muestra la interfaz de gestión de gastos
- `_agregar_tarea()`: Valida y envía datos para crear nueva tarea
- `_eliminar_tarea_seleccionada()`: Elimina tarea seleccionada
- `_actualizar_lista_tareas()`: Actualiza el TreeView de tareas
- `_agregar_gasto()`: Valida y envía datos para registrar gasto
- `_eliminar_gasto_seleccionado()`: Elimina gasto seleccionado
- `_actualizar_lista_gastos()`: Actualiza el TreeView de gastos

### 3.2. Controlador (`core.py`)

**Clase `Controlador`**:
- Gestiona la comunicación entre la vista y el modelo
- Proporciona métodos para todas las operaciones del sistema

**Métodos principales**:
- `crear_tarea(nombre, descripcion, fecha_limite, prioridad)`: Crea nueva tarea
- `eliminar_tarea(nombre_tarea)`: Elimina tarea existente
- `crear_gasto(monto, categoria, descripcion)`: Registra nuevo gasto
- `eliminar_gasto(monto, categoria, descripcion, fecha)`: Elimina gasto existente
- `obtener_tareas()`: Devuelve lista de todas las tareas
- `obtener_gastos()`: Devuelve lista de todos los gastos

### 3.3. Modelo (`database.py`, `gasto.py`, `tarea.py`)

**Clase `Database`**:
- Maneja la persistencia de datos en archivo JSON
- Proporciona métodos CRUD para tareas y gastos

**Métodos principales**:
- `_cargar_datos()`: Carga datos desde archivo JSON
- `guardar_datos()`: Guarda datos en archivo JSON
- `agregar_tarea(tarea)`: Añade nueva tarea
- `agregar_gasto(gasto)`: Añade nuevo gasto

**Clase `Gasto`**:
- Modelo para representar gastos financieros

**Atributos**:
- `monto`: Valor del gasto (float)
- `categoria`: Categoría del gasto
- `ubicacion`: Lugar donde se realizó el gasto
- `factura`: Información de factura (opcional)
- `foto`: Ruta a imagen (opcional)
- `fecha`: Fecha de registro

**Clase `Tarea`**:
- Modelo básico para representar tareas

**Atributos**:
- `descripcion`: Texto descriptivo de la tarea
- `completada`: Estado de completitud (booleano)

## 4. Flujo de Datos

1. **Interacción del usuario**:
   - El usuario realiza acciones en la interfaz (Vista)
   - La Vista envía solicitudes al Controlador

2. **Procesamiento**:
   - El Controlador valida los datos
   - El Controlador solicita operaciones al Modelo

3. **Persistencia**:
   - El Modelo actualiza los datos en memoria
   - El Modelo guarda los cambios en el archivo JSON

4. **Retroalimentación**:
   - El Modelo devuelve resultados al Controlador
   - El Controlador actualiza la Vista

## 5. Estructura de Datos

### Tareas
```json
{
  "nombre": "string",
  "descripcion": "string",
  "fecha_limite": "string (DD/MM/YYYY)",
  "prioridad": "string (Alta/Media/Baja)",
  "completada": "boolean",
  "fecha_creacion": "string (YYYY-MM-DD HH:MM:SS)"
}
```

### Gastos
```json
{
  "monto": "float",
  "categoria": "string",
  "descripcion": "string",
  "fecha": "string (DD/MM/YYYY HH:MM:SS)"
}
```

## 6. Requisitos del Sistema

- Python 3.6+
- Módulos requeridos:
  - `tkinter` (incluido en Python estándar)
  - `json` (incluido en Python estándar)
  - `os` (incluido en Python estándar)
  - `datetime` (incluido en Python estándar)

## 7. Ejecución del Sistema

Para iniciar la aplicación:
```python
from controlador.core import Controlador
from vista.consola import FinanzasUI

if __name__ == "__main__":
    controlador = Controlador()
    app = FinanzasUI(controlador)
    app.iniciar()
```

## 8. Consideraciones

- Los datos se guardan automáticamente en `data.json`
- La interfaz utiliza colores para diferenciar secciones
- Validaciones incluidas:
  - Formato de fechas
  - Campos obligatorios
  - Valores numéricos para montos
  - Confirmación antes de eliminar registros

## 9. Mejoras Futuras

1. Implementar edición de tareas/gastos existentes
2. Añadir gráficos de análisis financiero
3. Implementar filtros y búsquedas avanzadas
4. Añadir sistema de categorías personalizadas
5. Implementar exportación de datos a CSV/Excel
