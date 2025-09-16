# Comparativo: Tableau vs Power BI (TechStore – Lab 1)

Este documento resume cómo se abordó el mismo caso de negocio en **Tableau** y **Power BI**, los elementos construidos en cada herramienta, y las lecciones aprendidas.  

## 1) Carpeta del repositorio

- `tableau/` → Tablero, campos calculados y README del Lab 1 en Tableau  
- `powerbi/` → Reporte `.pbix`, capturas y README del Lab 1 en Power BI  

---

## 2) Métricas y KPIs comunes

| Métrica | Descripción |
|---------|------------|
| Ventas Netas | Total de ventas considerando descuentos |
| Costo Total | Suma de costos por venta |
| Margen $ y % | Diferencia entre ventas y costos |
| Meta Ventas Año / Mes | Comparativo con objetivo anual y mensual |
| Cumplimiento % | Ventas Netas / Meta Ventas |
| Estado/Bandas | Indicador de desempeño por color según Cumplimiento y Margen |

---

## 3) Visualizaciones equivalentes

- **KPI de Ventas**  
- **KPI de Cumplimiento %**  
- **Top 10 productos** (barras horizontales por ventas)  
- **Ventas por categoría** (gráfico circular / Pie)  
- **Tabla de Vendedores** (Cantidad, Margen $, Margen %, Ventas Netas)  

### Diferencias observadas

- **Power BI**: agregué KPI adicional de Clientes Activos y un gráfico dual “Ventas Netas vs Meta Ventas Mes” con tema JSON de Manuelita.  
- **Tableau**: se empleó **Measure Names/Values** para la tabla de vendedores y parámetros/filtros para seleccionar el año o mes.  

---

## 4) Resultados y consistencia

- **Tableau (KPI Ventas)**: ~$46.467.000  
- **Power BI (KPI Ventas)**: ~$43,34 M  
- Diferencia explicada por filtros de fecha: Power BI usaba rango 15/01/2024–18/02/2024; Tableau mostraba todo el año 2024.  
- Alineando el período, los valores coinciden dentro de redondeo.

---

## 5) Modelado y cálculos

| Aspecto | Tableau | Power BI |
|---------|--------|----------|
| Modelo | Relación entre ventas_techstore, productos, clientes, metas | Modelo estrella: ventas_techstore (hechos), productos, clientes, metas, calendario |
| Cálculos | Calculated Fields (Ventas Netas, Margen %, Cumplimiento %) | DAX Measures (Ventas, Margen, Cumplimiento, Estado, Color) |
| Fechas | Parámetro de año/mes y filtros | Tabla Calendario + slicers de fechas; join de metas por InicioMes |
| Tabla de Vendedores | Measure Names/Values | Matriz DAX con subtotales automáticos |

---

## 6) Experiencia de desarrollo

**Tableau:** rápido para prototipos, arrastrar y soltar campos, acciones y tooltips fáciles de personalizar.  
**Power BI:** modelado robusto, DAX potente, slicers integrados y temas JSON para estandarizar marca.

---

## 7) Despliegue y gobernanza

| Tema | Tableau | Power BI |
|------|--------|----------|
| Rendimiento | Extracts Hyper y caché | Import/DirectQuery, Composite |
| Publicación | Tableau Server/Cloud | Power BI Service (Pro/PPU/Fabric) |
| Gobernanza | Permisos por proyecto/vista | Roles RLS, datasets reutilizables |
| Licenciamiento | Por rol (Creator/Explorer/Viewer) | Pro/PPU; escalamiento con Fabric |

---

## 8) Versionado y archivos

| Elemento | Tableau | Power BI |
|----------|--------|----------|
| Formato | `.twbx` / `.twb` | `.pbix` |
| Git | `.twb` XML fácil de diff; `.twbx` binario | `.pbix` binario; se recomienda README y capturas para versionar |
| Evidencia | Captura `Dashboard_tableau.png` | Captura `Dashboard_power.png` |

---

## 9) Principales aprendizajes

- Alinear ventanas de tiempo es clave para consistencia de cifras.  
- DAX exige atención a contexto de filtro y agregaciones (SUMX, DIVIDE, SWITCH).  
- Temas JSON en Power BI facilitan estandarizar marca.  
- Ambos motores cumplen el objetivo del lab; la elección depende de stack, gobierno y complejidad del modelo.
