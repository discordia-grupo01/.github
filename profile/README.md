# Discordia — Grupo 01

Plataforma de comunidades en línea inspirada en Discord, desarrollada como trabajo práctico para **Ingeniería de Software 2** (Facultad de Ingeniería de la Universidad de Buenos Aires - FIUBA - Cátedra Rojas | 2C2026).

Permite registrarse, crear o unirse a servidores organizados en canales de texto y voz, gestionar roles y permisos, enviar mensajes directos, recibir notificaciones en tiempo real y push, moderar comunidades y suscribirse a un plan **Premium** integrado con Mercado Pago. Incluye además un panel de *backoffice* para que el personal de la plataforma administre cuentas, servidores y métricas.

- **[Probar la aplicación](https://discordia-g1.vercel.app)**
- **[Ver documentación técnica](https://discordia-grupo01.github.io/docs/index.html)**

---

## Arquitectura del sistema

El sistema está diseñado como una arquitectura distribuida de microservicios orientada a eventos, con un único punto de entrada y múltiples clientes:

* **API Gateway:** [Kong](https://konghq.com/) centraliza todo el tráfico de los clientes mediante **REST** y **WebSockets**.
* **Microservicios Backend (Go y Elixir):** Ocho servicios independientes, cada uno con su propia base de datos (**PostgreSQL** o **MongoDB**):
  * `identify-service` — Autenticación, usuarios y sesiones.
  * `servers` — Gestión de servidores, canales, roles y permisos.
  * `messaging` — Mensajería en canales y mensajes directos.
  * `notifications` — Alertas en tiempo real y notificaciones *push*.
  * `billing` — Suscripciones Premium y pagos con Mercado Pago.
  * `admin` — Moderación de plataforma, suspensiones de cuentas y servidores.
  * `metrics` — Recolección y consulta de métricas del sistema.
  * `voice-sfu` — Gestión de salas de voz (tráfico de audio enrutado directamente a través de **LiveKit**).
* **Comunicación asíncrona:** Los servicios publican y consumen eventos de dominio a través de **RabbitMQ**, implementando el patrón **Transactional Outbox** para garantizar la consistencia y evitar pérdida de mensajes.
* **Clientes:**
  * **Web:** Aplicación construida con **Next.js**.
  * **Mobile:** Aplicación móvil desarrollada en **React Native**.
  * **Backoffice:** Interfaz web interna para el equipo de administración y soporte.

---

## Integrantes

* Facundo Madotta
* Fabricio Batastini
* Manuel Peñalva
* Mora Lema
* Juana Galli
* Alexia Aroa
