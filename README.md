# 🕒 Gestor de Turnos y Horas Extras - Web App

Una aplicación web de página única (SPA) diseñada para digitalizar, gestionar y automatizar el cálculo de turnos y horas extras de un equipo de trabajo. Construida con tecnologías web estándar y respaldada por **Supabase** (PostgreSQL) para la persistencia de datos y la seguridad en la nube.

## 🚀 Descripción del Proyecto

Este proyecto nació de la necesidad de sustituir el registro manual de horarios por una herramienta ágil, segura y automatizada. La aplicación permite registrar jornadas diarias, añadir comentarios y, mediante un motor matemático interno, calcula las horas extras exactas aplicando reglas de negocio complejas basadas en el perfil del trabajador y el día de la semana.

## ✨ Características Principales

* **Autenticación Segura (Login):** Acceso restringido mediante credenciales gestionadas por Supabase Auth. Los datos están protegidos con Row Level Security (RLS).
* **Motor de Cálculo Inteligente:** Algoritmo dinámico que lee la fecha y el nombre del trabajador para aplicar los descuentos de horas base según contrato (ej. 3h o 4h) solo en días específicos (Miércoles y Domingos). El resto de los días, el 100% de la jornada se contabiliza como horas extras automáticamente.
* **Diseño 100% Responsive:** Interfaz de usuario adaptativa mediante Media Queries. Optimizada para usarse a pie de tienda en dispositivos móviles (tablas con scroll horizontal) y en ordenadores de escritorio.
* **Filtros Avanzados:** Capacidad de consultar el historial de turnos acotando por rango de fechas (Desde/Hasta) y por empleado específico.
* **Generador de Reportes PDF:** Motor de impresión nativo optimizado con CSS (`@media print`). Permite generar 4 tipos de reportes limpios y sin elementos de interfaz innecesarios:
    * Grupal Detallado
    * Grupal Resumido (Solo totales)
    * Individual Detallado
    * Individual Resumido
* **Gestión Antifallos de Datos:** La app escanea la base de datos completa de turnos para autocompletar la lista de trabajadores disponibles, evitando duplicados o errores tipográficos en los nombres.

## 🛠️ Tecnologías Utilizadas

* **Frontend:** HTML5, CSS3 (Variables nativas, Flexbox, Grid, Media Queries) y Vanilla JavaScript (ES6+). No se utilizaron frameworks pesados para mantener la aplicación ultraligera y rápida.
* **Backend & Base de Datos:** [Supabase](https://supabase.com/) (PostgreSQL).
* **Seguridad:** Supabase Auth y Políticas de Nivel de Fila (RLS) configuradas en SQL.

## 📋 Lógica de Negocio (El Motor Matemático)

La aplicación maneja las complejidades de los contratos del equipo de forma invisible para el usuario:
1.  Calcula los minutos exactos trabajados a partir de las horas de entrada y salida, adaptándose a los turnos nocturnos que cruzan la medianoche.
2.  Determina el día de la semana a partir de la fecha seleccionada.
3.  Asigna una "Base de Contrato" (horas que no son extras) dependiendo de si el día es clave (Miércoles/Domingo) y del perfil del trabajador seleccionado.
4.  Realiza todas las sumatorias mensuales basándose en minutos enteros para evitar los errores clásicos de coma flotante en JavaScript al sumar horas en formato decimal.

## 💻 Instalación y Despliegue

Al ser una arquitectura "Serverless" impulsada por Supabase, el despliegue es inmediato:
1.  Clonar el repositorio.
2.  Configurar un proyecto en Supabase con dos tablas: `Horarios` y `zara_empleados`.
3.  Reemplazar las constantes `SUPABASE_URL` y `SUPABASE_KEY` en el archivo `index.html` con las del nuevo proyecto.
4.  Habilitar la autenticación por Email/Password en Supabase y crear al menos un usuario.
5.  Alojar el archivo `index.html` en cualquier servidor estático (GitHub Pages, Vercel, Netlify).
