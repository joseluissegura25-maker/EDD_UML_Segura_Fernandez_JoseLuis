# Modelado de Comportamiento en Sistemas de E-commerce
# Autor: Jose Luis Segura Fernandez
1. ## Explicación técnica del proceso modelado.

Este proyecto consiste en el diseño de un diagrama con UML  que representa el proceso de "Confirmación de Pedido" de una tienda online. El sistema tiene las siguientes etapas:

* **Entrada y Validación:** El proceso se dispara cuando el usuario pulsa "Finalizar compra". Inmediatamente, el sistema realiza una verificación concurrente del stock y la validez de la sesión.  
* **Gestión de Pago:** Tras validar los datos, se procede a la conexión con la pasarela de pago segura.  
* **Fase de Post-Pago (Concurrencia Crítica):** Si el pago resulta exitoso, el sistema inicia tres tareas paralelas: se registra el pedido en la base de datos, se genera la factura en PDF y se notifica por correo electrónico.  
* **Cierre:** El flujo termina mostrando un mensaje de confirmación al cliente una vez todas las tareas paralelas hayan acabado.

**2\. Inserción de la imagen del diagrama** El diagrama que representa este flujo de trabajo complejo se encuentra en el repositorio, específicamente en /img. Aun así, adjunto la imagen del diagrama. (Referencia al archivo: [diagrama.png](img/diagrama.png)

**3\. Justificación del uso de los nodos de sincronización**

* **Uso de Fork (Bifurcación):** Se usa una barra de *fork* en la fase de validación inicial y en la fase de post-pago. Esto es necesario porque tareas como el envío de correos y la generación de facturas no deben ocurrir de forma secuencial, ya que esto restaría eficiencia a la aplicación web.  
* **Uso de Join (Sincronización):** Se implementa un nodo de *join* antes del cierre para garantizar que el mensaje de confirmación al cliente no se emita hasta que el registro en la base de datos y la facturación estén completamente terminados, evitando estados inconsistentes en el sistema.

**4\. Bibliografía (Estilo IEEE)** \[1\]	Object Management Group (OMG), "Unified Modeling Language (UML) Specification, Version 2.5.1," \[En línea\]. Disponible en: [https://www.omg.org/spec/UML/](https://www.omg.org/spec/UML/). \[2\]	IBM Documentation, "UML activity diagrams," 2021\. \[En línea\]. Disponible en: [https://www.ibm.com/docs/en/rhapsody/9.0.1?topic=diagrams-uml-activity](https://www.google.com/search?q=https://www.ibm.com/docs/en/rhapsody/9.0.1%3Ftopic%3Ddiagrams-uml-activity). \[3\]	Visual Paradigm, "UML Activity Diagram Tutorial." \[En línea\]. Disponible en: https://www.visual-paradigm.com/guide/uml/what-is-activity-diagram/.