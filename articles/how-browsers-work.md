---
title: How browsers work
subtitle: Behind the scenes of modern web browsers
date: 05-08-2011
authors: ['Tali Garsiel', 'Paul Irish']
source: https://web.dev/howbrowserswork/
---

# How browsers work

## The browser's main functionality

1. Barra de dirección para insertar una *URI* (Uniform Resource Identifier)
2. Botones de atrás y delante
3. Opciones de marcadores
4. Botones de refrescado y parado
5. Botón *Home*

## The browser's high level structure

1. **User interface:** Los elementos visuales por los que el usuario interactúa con las herramientas del navegador.
2. **Browser engine:** Traduce las interacciones del usuario para el motor de renderizado.
3. **Render engine:** Muestra en pantalla el contenido solicitado. En su mayoría, renderiza archivos HTML y CSS, pero gracias al uso de plug-ins puede renderizar archivos pdf, etc.
4. **Networking:** Realiza las llamadas de red solicitadas por el usuario, como peticiones HTTP.
5. **JavaScript interpreter:** Analiza y ejecuta código JavaScript.
6. **UI Backend:** Estilos genéricos que usa los recursos del sistema operativo.
7. **Data Persistence:** Cada de persistencia para almacenar datos del usuario.

![High-level Componenets of Browser](https://d6vdma9166ldh.cloudfront.net/media/images/d196578a-3922-4823-8d85-96ad0141277f.jpg)

## Rendering engines

| Navegador         | Motor de renderizado |
| ----------------- | -------------------- |
| Internet Explorer | Trident              |
| Firefox           | Gecko                |
| Safari            | Webkit               |
| Chrome            | Blink                |
| Opera             | Blink                |

## The main flow

1. El **motor de renderizado** obtiene el cuerpo de la petición desde la **capa de red** (normalmente en chunks de 8kB).
2. El motor analiza el documento HTML y convierte los elementos HTML en **nodos DOM** en un árbol, el **content tree**. También se analizan las hojas de estilos (tanto internas como externas)
3. Renderiza la construcción del árbol.
4. Diseño del árbol de renderizado.
5. Pinta el árbol de renderizado.
