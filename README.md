# 📡 DIALPA FIBRA - Sistema de Gestión de Instalaciones

Una aplicación web progresiva para que técnicos de instalación registren órdenes de trabajo, calculen comisiones y generen reportes automáticos.

![Versión](https://img.shields.io/badge/versión-1.0-blue)
![Licencia](https://img.shields.io/badge/licencia-MIT-green)
![Estado](https://img.shields.io/badge/estado-activo-brightgreen)

---

## 🎯 Características

✅ **Registro de Instalaciones**
- Soporte para 61 tipos diferentes de instalaciones (Single/Duo, Trio 1/2, Trio 3/4, Trio 5/6 STB)
- Código MDM automático con validación contra duplicados
- Búsqueda y filtrado de actividades en tiempo real

✅ **Cálculo Automático de Comisiones**
- Precios dinámicos según cantidad de órdenes en la quincena
- Descuento por garantía del 5% automático
- Soporte para dos períodos de pago (1ra y 2da quincena)

✅ **Integración con Google Sheets**
- Envío automático de órdenes individuales
- Envío de resumen de quincena
- Sincronización en tiempo real

✅ **Reportes Profesionales**
- Formato texto para WhatsApp
- Resumen de ganancia neta y acumulado
- Desglose por tipo de instalación

✅ **Funcionalidad Offline**
- Almacenamiento local con localStorage
- Sincronización cuando hay conexión
- Historial completo de órdenes

✅ **Multi-usuario**
- 4 técnicos registrados en el sistema
- Autenticación por cédula
- Datos independientes por usuario

---

## 🚀 Cómo Usar

### 1. **Acceso al Sistema**
- Abrir `index.html` en cualquier navegador
- Ingresar número de cédula de técnico:
  - `80493258` - Yoban
  - `80842485` - Román Suta Castro
  - `1006094077` - Alexander Caballero
  - `1001276680` - Andrés Sebastián Vélez

### 2. **Registrar una Instalación**
1. Seleccionar tipo de orden (SINGLE/DUO, TRIO 1/2, TRIO 3/4, TRIO 5/6)
2. Ingresar código MDM Fibra
3. Buscar y seleccionar la actividad específica
4. El precio se calcula automáticamente según:
   - 1ra o 2da orden → Precio columna 1
   - 3ra orden → Precio columna 2
   - 4+ órdenes → Precio columna 3

### 3. **Ver Mi Quincena**
- Ir a pestaña "💵 Mi Quincena"
- Seleccionar período (1ra o 2da quincena)
- Ver resumen de:
  - Total bruto
  - Retención (5%)
  - Neto a cobrar
  - Acumulado histórico

### 4. **Enviar Reporte a Sheets**
- Disponible el día 1 y día 16 de cada mes
- Click en "📤 Enviar Reporte de Quincena a Sheets"
- Las órdenes se archivan automáticamente
- Acumulado se actualiza

### 5. **Generar Reporte para WhatsApp**
- Click en "📋 Generar y Copiar Reporte"
- Se copia automáticamente al portapapeles
- Pegar en WhatsApp o correo

---

## 💾 Estructura de Datos

### Orden Registrada
```javascript
{
  mdm: "350001049885",           // Código MDM único
  actId: "1",                    // ID de actividad
  code: "350001049885",          // Código de producto
  actNombre: "HC SINGLE o DUO con ONT",
  cat: "single-duo",             // Categoría
  tablerCat: "DUOS PELADOS",     // Categoría Tabler
  precio: 37000,                 // Precio en COP
  tramo: "1ra o 2da orden",      // Tramo de precio
  quincena: "1",                 // Período (1 o 2)
  fecha: "07/06/2026",           // Fecha DD/MM/YYYY
  hora: "14:30",                 // Hora HH:MM
  tecnico: "Yoban",              // Nombre técnico
  cc: "80493258"                 // Cédula técnico
}
```

### Almacenamiento Local
```
localStorage.getItem("ord_80493258")        → Array de órdenes
localStorage.getItem("acum_80493258")       → Acumulado total
localStorage.getItem("appsScriptUrl")       → URL Google Apps Script
localStorage.getItem("env_80493258_q1_...")→ Flag de envío
```

---

## 🔌 Integración Google Sheets

### URL de Apps Script Configurada
```
https://script.google.com/macros/s/AKfycbx75-sopTLz-8IHc4eim_O0E5ox3PjpRYCeBhSDUS2DfgwOCWYoTtVaMF2xO1CHkphonA/exec
```

### Parámetros Enviados

**Registro Individual:**
```
accion=registrar&fecha=07/06/2026&hora=14:30&cedula=80493258
&tecnico=Yoban&mdm=350001049885&code=350001049885
&actNombre=HC SINGLE o DUO con ONT&tablerCat=DUOS PELADOS
&valor=37000&tramo=1ra o 2da orden&quincena=1ra Quincena
```

**Resumen Quincena:**
```
accion=quincena&tecnico=Yoban&cedula=80493258
&quincena=1ra Quincena&bruto=370000&retencion=18500&neto=351500
&single_duo=2&trio_1_2=1&trio_3_4=0&trio_5_6=0
```

---

## 📦 Tipos de Instalación (61 Actividades)

### Single/Duo (Códigos 350001049885-350001049899 + 350001056826)
- Desde HC SINGLE/DUO con ONT básico ($37,000)
- Hasta HC SINGLE/DUO con ONT + 4 AP + 2 PUNTOS DE RED ($66,000)
- Incluye opción Social Internet ($35,000)

### Trio 1/2 STB (Códigos 350001049900-350001049914)
- Desde HC TRIO (1/2 STB) básico ($48,000)
- Hasta HC TRIO (1/2 STB) + 4 AP + 2 PUNTOS DE RED ($82,000)

### Trio 3/4 STB (Códigos 350001049915-350001049929)
- Desde HC TRIO (3/4 STB) básico ($68,000)
- Hasta HC TRIO (3/4 STB) + 4 AP + 2 PUNTOS DE RED ($90,000)

### Trio 5/6 STB (Códigos 350001049930-350001049944)
- Desde HC TRIO (5/6 STB) básico ($100,000)
- Hasta HC TRIO (5/6 STB) + 4 AP + 2 PUNTOS DE RED ($124,000)

---

## 🛠️ Funcionalidades Avanzadas

### Calendario Interactivo
- Seleccionar fechas pasadas para registrar órdenes retroactivas
- Marcas de días con trabajo registrado
- Validación: no permite fechas futuras

### Modal de Día Anterior
- Pregunta automáticamente si trabajó ayer
- Opción de registrar órdenes del día anterior

### Validaciones
- ✅ Cédula debe estar registrada en el sistema
- ✅ MDM no puede repetirse
- ✅ Actividad debe ser seleccionada
- ✅ Código MDM es requerido

### Límites de Envío a Sheets
- Solo disponible días 1 y 16 de cada mes
- Máximo un envío por técnico y quincena
- Se pueden hacer múltiples registros individuales

---

## 🔐 Seguridad (Recomendaciones)

> ⚠️ **Nota:** Este es un prototipo. Para producción se recomienda:

1. **Backend de autenticación** - No hardcodear cédulas en cliente
2. **Base de datos** - Mover localStorage a servidor
3. **API segura** - Proteger URL de Google Apps Script
4. **Validación servidor** - Duplicar validaciones en backend
5. **HTTPS** - Usar conexión encriptada
6. **Rate limiting** - Limitar intentos de login
7. **Audit logs** - Registrar cambios en servidor

---

## 📱 Compatibilidad

| Navegador | Soporte |
|-----------|---------|
| Chrome | ✅ Completo |
| Firefox | ✅ Completo |
| Safari | ✅ Completo |
| Edge | ✅ Completo |
| Mobile (iOS/Android) | ✅ Optimizado |

**Requisitos:**
- JavaScript habilitado
- localStorage disponible
- Conexión a Internet (para envío a Sheets)

---

## 📊 Tabla de Precios Rápida

| Tipo | 1ra/2da | 3ra | 4+ |
|------|---------|-----|-----|
| Single/Duo Básico | $37,000 | $43,000 | $47,000 |
| Single/Duo + 1 AP | $45,000 | $50,000 | $55,000 |
| Trio 1/2 Básico | $48,000 | $55,000 | $63,000 |
| Trio 3/4 Básico | $68,000 | $76,000 | $86,000 |
| Trio 5/6 Básico | $100,000 | $110,000 | $120,000 |

*Ver archivo index.html para tabla completa de 61 actividades*

---

## 🐛 Reporte de Problemas

Si encuentras un bug:
1. Abre una Issue con descripción clara
2. Incluye: navegador, versión, pasos para reproducir
3. Adjunta screenshot o video si es posible

---

## 📝 Licencia

MIT License - Ver archivo LICENSE para detalles

---

## 👨‍💻 Autores

Desarrollado para DIALPA FIBRA
- Técnicos: Yoban, Román Suta Castro, Alexander Caballero, Andrés Sebastián Vélez

---

## 🔄 Versión Actual

**v1.0** - Lanzamiento inicial
- ✅ Sistema de registro de órdenes
- ✅ Cálculo de comisiones
- ✅ Integración Google Sheets
- ✅ Generador de reportes
- ✅ Sistema de quincenas

---

## 📧 Contacto & Soporte

Para preguntas sobre el sistema, contactar al administrador.

**Última actualización:** Junio 2026
