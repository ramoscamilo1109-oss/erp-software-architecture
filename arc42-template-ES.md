---
date: 10 Febrero 2026
title: Documentación de Arquitectura ERP - Módulo de Compras
---

# Introducción y Metas {#section-introduction-and-goals}

## Vista de Requerimientos {#_vista_de_requerimientos}
Este sistema es un ERP diseñado para centralizar la operación empresarial. El *Módulo de Compras* tiene como prioridad:
* Gestionar el catálogo de productos y sus especificaciones.
* Administrar una base de datos de proveedores confiables.
* Automatizar la generación de Órdenes de Compra digitales.
* Mantener trazabilidad de precios históricos para negociación.

## Metas de Calidad {#_metas_de_calidad}
* *Mantenibilidad:* Código estructurado bajo arquitectura de contenedores.
* *Integridad:* Garantizar que no existan duplicidad de productos (SKU único).
* *Disponibilidad:* Interfaz responsiva accesible para el personal de compras.

## Partes interesadas (Stakeholders) {#_partes_interesadas_stakeholders}

| Rol/Nombre        | Contacto          | Expectativas                                      |
|-------------------|-------------------|---------------------------------------------------|
| Gestor Inventario | Interno           | Catálogo actualizado y sin errores de registro.   |
| Jefe de Compras   | Interno           | Generación rápida de órdenes y control de costos. |
| Proveedores       | Externo           | Recibir órdenes de compra claras y formales.      |

# Restricciones de la Arquitectura {#section-architecture-constraints}
* Documentación basada en la plantilla *arc42*.
* Diagramación estándar utilizando *C4 Model* y *UML*.
* Control de versiones alojado en *GitHub*.
* Uso de *PlantUML* para la generación de diagramas mediante código.

# Alcance y Contexto del Sistema {#section-context-and-scope}

## Contexto de Negocio {#_contexto_de_negocio}
El ERP interactúa con usuarios internos (compras) y sistemas externos para el reporte contable.

![Diagrama de Contexto](./docs/images/Diagrama de Contexto (Nivel 1 - C1).png)

## Contexto Técnico {#_contexto_técnico}
El sistema se comunica mediante protocolos HTTPS y utiliza formatos JSON para el intercambio de datos entre la interfaz y el servidor.

# Estrategia de solución {#section-solution-strategy}
Se implementa una arquitectura de contenedores para separar la lógica de negocio de la interfaz de usuario, facilitando el despliegue independiente y la escalabilidad del módulo de compras.

# Vista de Bloques {#section-building-block-view}

## Sistema General (Caja Blanca) {#_sistema_general_de_caja_blanca}
El sistema ERP se divide en tres componentes principales:

![Diagrama de Contenedores](./docs/images/Diagrama de Contenedores (Nivel 2 - C2).png)

### Bloques de construcción contenidos
1.  *Single-Page Application (SPA):* Interfaz desarrollada en React/JavaScript que permite la interacción con el usuario.
2.  *API Monolítica:* Backend en Java/Spring Boot que procesa las reglas de negocio de compras y validaciones.
3.  *Base de Datos:* PostgreSQL para el almacenamiento persistente de productos, proveedores y órdenes.

# Vista de Ejecución {#section-runtime-view}

## Registro de un Nuevo Producto {#_escenario_de_ejecución_1}
Este flujo describe el proceso desde que el usuario envía los datos hasta que se confirman en el sistema.

![Diagrama de Secuencia](./docs/images/Diagrama de Secuencia (Registrar Producto).png)

* El usuario envía el formulario desde la *SPA*.
* La *API* valida los datos (nombre no vacío, SKU no duplicado).
* La *DB* registra el producto y devuelve el ID único.

# Vista de Despliegue {#section-deployment-view}
El sistema está diseñado para ser desplegado en entornos cloud, utilizando servidores de aplicaciones para el backend y servicios de bases de datos gestionadas.

# Conceptos Transversales {#section-concepts}
* *Persistencia:* Uso de JPA/Hibernate para el mapeo de objetos a la base de datos.
* *Validación:* Reglas aplicadas en el nivel de API para asegurar la calidad de los datos de entrada.

# Decisiones de Diseño {#section-design-decisions}
Se decidió utilizar *Markdown* para la documentación técnica con el fin de integrarla directamente con el repositorio de código en GitHub, facilitando la colaboración.

# Glosario {#section-glossary}

| Término          | Definición                                                    |
|------------------|---------------------------------------------------------------|
| *SKU* | Stock Keeping Unit, identificador único para cada producto.   |
| *ERP* | Enterprise Resource Planning, sistema de gestión empresarial. |
| *NIT* | Número de Identificación Tributaria del proveedor.            |
| *MoSCoW* | Técnica de priorización (Must, Should, Could, Won't).         |
