# StatusInsight

Aplicación web para el seguimiento de la productividad hora a hora en las estaciones de prueba y del avance contra el plan de metas de producción. Lee el reporte *Hour Status for Production*, guarda el resultado del día y lo compara con el plan de metas por día, modelo y turno.

![Avance por turno](capturas/meta-diaria.png)

## Características

- Avance por turno: para cada modelo muestra lo empacado en cada turno contra su meta, con el cumplimiento y el delta del día.
- Empacado por hora: detalle de las franjas de 2 horas del día por modelo.
- Meta semanal: rendimiento de un periodo (por omisión, de jueves a miércoles) con el concentrado del periodo, el cumplimiento por día, por modelo y por turno, y una tarjeta por modelo.
- Plan de metas: se carga desde el Excel de planning (DIA / MODELO / TURNO / QTY META) y es la referencia de todas las vistas.
- Catálogo de modelos en el servidor: la lista se guarda una vez y alimenta todas las consultas.
- Bitácora: registra quién consultó qué y cuándo, y cuántos modelos salieron con y sin información.
- Roles: planeador (consulta y captura) y piso (solo consulta).
- Edición con candado: un solo editor a la vez, con aviso de quién tiene el bloqueo y en qué vista.
- Exportación del periodo a Excel.
- Estado del proveedor de datos en el pie del menú, para distinguir un hueco de "no se consultó" de un "no traía datos".
- Interfaz con tema grafito y semáforo andón (verde, ámbar y rojo). Las gráficas son HTML, CSS y SVG, así que no dependen de librerías externas ni de internet.

![Meta semanal](capturas/meta-semanal.png)

## Requisitos

- Python 3.9 o superior.
- Flask, Waitress, Requests, BeautifulSoup, openpyxl y cryptography.
- Acceso de red a las carpetas del sistema de producción.
- Una base de cuentas SQLite para el control de accesos.

## Instalación y uso

1. Instala las dependencias.
2. Ejecuta la aplicación:

   ```
   python StatusInsight.py
   ```

3. Abre `http://<ip-de-la-maquina>:10004`.

El puerto por omisión es 10004.

## Roles

| Rol | Permisos |
| --- | --- |
| planeador | Consulta, carga el plan de metas y captura valores |
| piso | Consulta el tablero completo, sin escribir |

Una cuenta sin rol asignado hereda el permiso mínimo (piso).

## Estructura del proyecto

```text
StatusInsight/
├── StatusInsight.py      # servidor Flask y lógica del reporte
├── bases.py              # acceso a las bases SQLite
├── licencia.py           # verificación de la licencia de uso
├── templates/            # login y tablero
└── static/               # CSS, JS y fuentes
```

## Licencia

Software propietario de uso interno. El acceso requiere una licencia firmada: la aplicación verifica la firma y la máquina en cada arranque.

## Autor

Alejandro Espinoza
Foxconn México
