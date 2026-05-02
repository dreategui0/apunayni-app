# Apunayni — Contabilidad para Negocios Familiares

Aplicación web progresiva (PWA) de contabilidad diseñada para pequeños negocios que manejan múltiples fuentes de ingresos y cuentas bancarias. Desarrollada para uso real en un negocio familiar con tres unidades de negocio: servicio de alojamiento, tienda y servicios adicionales.

## Demo en vivo

🔗 [Ver demo en vivo] (https://youtu.be/YTG9_GSGqY0)

Instálala como app en tu celular: en Android abre Chrome → menú → *"Añadir a pantalla de inicio"*. En iPhone usa Safari → compartir → *"Añadir a pantalla de inicio"*.

---

## El problema que resuelve

Muchos negocios pequeños llevan la contabilidad en Excel o en papel, sin visibilidad en tiempo real del flujo de caja. El dueño no sabe cuánto hay en cada cuenta bancaria, ni si los costos fijos del mes ya fueron pagados, a menos que revise manualmente el archivo.

Esta app resuelve eso: cualquier persona del negocio puede registrar un movimiento desde su celular, y todos los saldos se actualizan en tiempo real gracias a Google Sheets como backend.

---

## Funcionalidades

- **Registro de transacciones** — ingresos y egresos categorizados por fuente y tipo
- **Saldos en tiempo real** — efectivo, Bancolombia, Nequi/Nu, actualizados al instante
- **Control de costos fijos** — estado de pagos mensuales (internet, arriendo, servicios, etc.)
- **Resumen mensual** — vista consolidada de ingresos vs. egresos por mes
- **Sincronización en la nube** — backend en Google Sheets, accesible desde cualquier dispositivo
- **Modo offline** — funciona sin conexión y sincroniza cuando vuelve el internet
- **Instalable como app nativa** — sin App Store ni Play Store

---

## Stack técnico

| Capa | Tecnología |
|---|---|
| Frontend | HTML5, CSS3, JavaScript (Vanilla) |
| Backend / Base de datos | Google Sheets API v4 |
| Hosting | GitHub Pages (gratuito) |
| Sincronización | Google Apps Script (webhook de escritura) |
| PWA | Web App Manifest + Service Worker |

---

## Arquitectura

```
Celular (PWA instalada)
    │
    ├── Lectura  → Google Sheets API (REST, JSON)
    └── Escritura → Google Apps Script (webhook HTTP POST)
                        │
                        └── Google Sheets (fuente de verdad)
```

La app usa Google Sheets como base de datos liviana: la API de solo lectura no requiere autenticación de usuario (el Sheet es público en modo lectura), y la escritura pasa por un Apps Script desplegado como web app, lo que evita exponer credenciales en el cliente.

---

## Estructura del proyecto

```
apunayni-app/
├── index.html          # App completa (SPA — Single Page Application)
├── manifest.json       # Configuración PWA (nombre, íconos, colores)
├── icon-192.png        # Ícono para pantalla de inicio (Android)
├── icon-512.png        # Ícono para pantalla de inicio (iOS/splash)
└── apple-touch-icon.png
```

---

## Configuración inicial

La primera vez que se abre la app solicita dos parámetros que quedan guardados localmente en el celular:

1. **Sheet ID** — el identificador del Google Sheet (en la URL entre `/d/` y `/edit`)
2. **API Key** — clave de la Google Sheets API (console.cloud.google.com)

Una vez configurados, la app funciona de forma autónoma sin volver a pedirlos.

---

## Lo que aprendí construyendo esto

- Integración con Google Sheets API v4 — autenticación, lectura de rangos, parseo de valores numéricos con distintos formatos
- Diseño de PWA instalable con Service Worker y Web App Manifest
- Manejo de estado en JavaScript vanilla sin frameworks
- Deploy continuo con GitHub Pages
- Lógica de contabilidad real: saldos acumulados, costos fijos periódicos, conciliación entre cuentas

---

## Contexto

Proyecto real desarrollado para un negocio familiar. La app está actualmente en producción y en uso diario. Fue construida iterativamente respondiendo a necesidades reales: primero la lógica de saldos, luego sincronización en la nube, luego la instalación como PWA, luego corrección de bugs de parseo numérico con Google Sheets.

---

## Próximas mejoras

- [ ] Notificaciones push cuando se registra un movimiento
- [ ] Exportación de resumen mensual a PDF
- [ ] Integración con WhatsApp Business API para captura automática de comprobantes
- [ ] Gráficas de evolución de saldos por mes

---

*Desarrollado con HTML/JS puro y la API gratuita de Google Sheets. Sin servidores propios, sin costos de infraestructura.*
