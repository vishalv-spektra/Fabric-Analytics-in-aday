# Microsoft Fabric - Fabric Analyst in a Day - Laboratorio 2

![](../media/Lab-1/ii2.png)

## Contenido

- Presentación
- Licencia de Fabric
  - Tarea 1: Habilitar una licencia de prueba de Microsoft Fabric
- Área de trabajo de Fabric
  - Tarea 2: Crear un área de trabajo de Fabric
  - Tarea 3: Crear un Lakehouse
- Información general de las experiencias de Fabric
  - Tarea 4: Experiencia de Data Factory
  - Tarea 5: Experiencia de Industry Solutions
  - Tarea 6: Experiencia de Real-Time Intelligence
  - Tarea 7: Experiencia de Data Engineering
  - Tarea 8: Experiencia de Data Science
  - Tarea 9: Experiencia de Data Warehouse
  - Tarea 10: Experiencia de bases de datos
- Referencias


# Presentación

Hoy tendrá ocasión de aprender diversas características clave de Microsoft Fabric. Este es un taller introductorio destinado a presentarle las diversas experiencias de productos y artículos disponibles en Fabric. Al final de este taller, habrá aprendido a utilizar almacenes de lago de datos, flujos de datos Gen2, canalización, DirectLake, etc.

Al final de este laboratorio, habrá aprendido:

- Cómo crear un área de trabajo de Fabric

- Cómo crear un lakehouse

# Licencia de Fabric

## Tarea 1: Habilitar una licencia de prueba de Microsoft Fabric

1. Seleccione **PowerBI Portal** en el escritorio de la máquina virtual. Se le solicitará que inicie sesión.

    ![](../media/Lab-2/image6.png)

    >**Nota:** Si está utilizando el entorno de laboratorio, es posible que inicie sesión automáticamente.

    >**Nota:** Si Fabric no se abre, vaya a http://app.fabric.microsoft.com/ en el explorador.

2. Copie el nombre de usuario y péguelo en el campo Correo electrónico del cuadro de diálogo y seleccione Enviar.

    - **Correo electrónico/nombre de usuario:** <inject key="AzureAdUserEmail"></inject>

        ![](../media/Lab-2/image7.png)

3. En la pestaña de **inicio de sesión de Microsoft Azure**, verá la pantalla de inicio de sesión. Introduzca el siguiente **EmailUsername** y luego haga clic en **Siguiente**.

    - **Correo electrónico/nombre de usuario**: <inject key="AzureAdUserEmail"></inject>

        ![](../media/Lab-2/image8.png)

4. Ahora introduzca el siguiente **Pase de acceso temporal** y haga clic en **Iniciar sesión**.

    - **Pase de acceso temporal:** <inject key="AzureAdUserPassword"></inject>

        ![](../media/Lab-2/image9.png)

5. Se le dirigirá a la **página principal del servicio Power BI** que ya conoce.

6. Asumimos que está familiarizado con el diseño del servicio Power BI. Si tiene alguna pregunta, no dude en consultar al instructor.

    Actualmente, se encuentra en **Mi área de trabajo**. Para trabajar con elementos de Fabric, necesitará una licencia de prueba y un área de trabajo que tenga una licencia de Fabric asignada. Configurémoslo.

7. En la esquina superior derecha de la pantalla, seleccione el **icono** del **usuario**.

8. Seleccione **Prueba gratuita**.

    ![](../media/Lab-2/image10.png)

9. Se abre un cuadro de diálogo para actualizar a una prueba de Microsoft Fabric gratuita. Seleccione **Activar**.

    >**Nota:** No cambie la región predeterminada. Manténgala tal y como está.

    ![](../media/Lab-2/image11.png)

10. Se abre el cuadro de diálogo Actualizado correctamente a Microsoft Fabric. Seleccione **Fabric Home Page.**

    ![](../media/Lab-2/image12.png)

11. Se le dirigirá a la **página Inicio de Microsoft Fabric**. Es posible que se abra un cuadro de diálogo "Le damos la bienvenida a la vista de Fabric". Si lo desea, puede seleccionar la opción **Iniciar recorrido** o **Cancelar**.

    ![](../media/Lab-2/image13.png)

# Área de trabajo de Fabric

## Tarea 2: Crear un área de trabajo de Fabric

1. Creemos ahora un área de trabajo con una licencia de Fabric. Seleccione **Áreas de trabajo** (1) en la barra de navegación de la izquierda. Se abre un cuadro de diálogo.

2. Haga clic en **+Nueva área de trabajo** (2) que se encuentra en la parte inferior del menú emergente.

    ![](../media/Lab-2/image14.png)

3. El cuadro de diálogo **Crear un área de trabajo** se abre en el lado derecho del explorador.

4. En el campo **Nombre**, introduzca FAIAD_<inject key="Deployment ID" enableCopy="false"/>

    >**Nota:** El nombre del área de trabajo debe ser único. Asegúrese de que aparezca una marca de verificación verde con “Este nombre está disponible” debajo del campo Nombre.

5. Si lo desea, puede escribir una Descripción para el área de trabajo. Este campo es opcional.

6. Haga clic en **Avanzado** para expandir la sección.

    ![](../media/Lab-2/image15.png)

7. En **Modo de licencia**, asegúrese de que **Prueba** esté seleccionado. (Debería estar seleccionado por defecto).

8. Seleccione **Aplicar** para crear un nuevo área de trabajo.

    ![](../media/Lab-2/image16.png)

    Se le dirigirá al área de trabajo que acaba de crear. Traeremos datos de los diferentes orígenes de datos a un almacén de lago de datos y utilizaremos los datos del almacén de lago de datos para crear nuestro modelo y generar informes en él. El primer paso es crear un almacén de lago de datos. Haremos esto a continuación.

## Tarea 3: Crear un Lakehouse

1. En el espacio de trabajo **FAIAD_<inject key="Deployment ID" enableCopy="false"/>** recién creado, localice el botón **+ Nuevo elemento (1)** en el panel de navegación de la izquierda. Aquí es donde puede comenzar a crear nuevos elementos en su área de trabajo.

2. En el cuadro de búsqueda, escriba **Lakehouse (2)** y, en los resultados de búsqueda, seleccione la opción **Lakehouse (3)**. Esto le permitirá crear un nuevo almacén de lago de datos para almacenar, consultar y administrar sus macrodatos.

    ![](../media/Lab-2/image17.png)

3. Aparecerá un cuadro de diálogo Nuevo lakehouse. Escriba **lh_FAIAD** en el cuadro de texto Nombre.

    >**Nota:** lh aquí se refiere al Lakehouse. Vamos a anteponer lh para que sea fácil de identificar y buscar.

    >**Nota:** Esta característica ya no se encuentra en versión preliminar, **pero aún no necesitamos habilitarla**.

4. Seleccione **Crear**.

    ![](../media/Lab-2/image18.png)

    En unos momentos, se crea un almacén de lago y se le dirigirá a la interfaz del explorador del mismo. En la parte superior izquierda, junto al nombre de Fabric del encabezado, tendrá el icono del almacén de lago de datos. El icono del espacio de trabajo en la navegación izquierda reflejará que ahora contiene un elemento.

    Dentro del explorador del almacén de lago de datos, verá una sección Tables y Files. Un almacén de lago de datos podría exponer archivos de Azure Data Lake Storage Gen2 en la sección de archivos o un flujo de datos podría cargar datos en las tablas del almacén de lago de datos. Existen varias opciones disponibles. Le mostraremos algunas de las opciones en las siguientes prácticas de laboratorio.

    ![](../media/Lab-2/image19.png)

# Información general de las experiencias de Fabric

## Tarea 4: Experiencia de Data Factory

1. Seleccione el icono de Cargas de trabajo en la parte izquierda de su pantalla. Se abrirá un cuadro de diálogo con la lista de experiencias de Fabric. La lista de experiencias incluye Power BI, Data Factory, Industry Solutions, Real-Time Intelligence, Data Engineering, Data Science y Data Warehouse. Exploremos.

    ![](../media/Lab-2/image20.png)

2. Seleccione **Data Factory**.

    ![](../media/Lab-2/image21.png)

3. Se le dirigirá a la página principal de Data Factory. A continuación, se muestra una explicación detallada de sus secciones, diseñada para guiar paso a paso en el uso efectivo de Data Factory. El flujo de datos de segunda generación es la nueva generación de flujos de datos.

    **¿Qué es Data Factory?**

    Data Factory es una herramienta que le ayuda a administrar y organizar datos de diferentes orígenes. Le permite recopilar, preparar y transformar los datos para que se puedan utilizar de forma eficaz. Tanto si es principiante como experto, Data Factory proporciona herramientas para que la transformación de datos sea más fácil y eficiente.

    **Tipos de elementos:**

    1) **Flujo de datos Gen2:** los flujos de datos son como recetas para transformar datos. Ofrecen más de 300 transformaciones diferentes que puede aplicar a sus datos. Esto significa que puede limpiar, combinar y cambiar los datos de muchas maneras para adaptarlos a sus necesidades.

    2) **Canalización:** las canalizaciones son flujos de trabajo que le ayudan a automatizar los procesos de datos. Le permiten crear flujos de trabajo de datos flexibles que se pueden adaptar a sus requisitos específicos. Esto facilita la gestión y el procesamiento de datos de forma estructurada.

    3) **Azure Data Factory**: Azure Data Factory es un servicio de integración de datos basado en la nube que le permite crear flujos de trabajo basados en datos para orquestar y automatizar el movimiento y la transformación de datos.

    4) **Trabajo de Apache Airflow**: Apache Airflow es una plataforma de código abierto que se utiliza para crear, programar y supervisar flujos de trabajo mediante programación. En Data Factory, le permite crear, programar y administrar flujos de trabajo de datos complejos.

    5) **Copiar trabajo**: Copiar trabajo es una característica que le permite copiar datos de un origen a otro. Proporciona una forma sencilla y eficaz de mover datos entre diferentes almacenes de datos.

    6) **Base de datos reflejada:** una característica para crear versiones duplicadas de bases de datos para copia de seguridad, prueba o acceso de solo lectura.

    7) **SAP reflejado:** integre a la perfección su patrimonio de SAP existente con el resto de sus datos en Fabric.

    8) **Oracle reflejado:** una creación de reflejo en Fabric replica sus bases de datos de Oracle en una plataforma unificada, lo que permite un análisis de baja latencia casi en tiempo real junto con otros orígenes de datos.

    9) **Google BigQuery reflejada (versión preliminar):** la creación de reflejo en Fabric le permite replicar continuamente los datos de Google BigQuery en OneLake, lo que elimina el ETL complejo y permite un uso fluido entre análisis, IA e intercambio de datos.

    10) **Lista de SharePoint Online reflejada (versión preliminar):** replica los datos de lista de SharePoint casi en tiempo real en de Microsoft Fabric OneLake como un origen de solo lectura y listo para análisis. Elimina ETL y expone los datos a través de un punto de conexión de análisis SQL creado automáticamente y otras cargas de trabajo de Power BI Fabric.

    11) **Biblioteca de variables:** contiene una lista de variables y sus valores predeterminados. También puede contener otros conjuntos de valores que contengan valores alternativos.

    12) **Trabajo de dbt (versión preliminar):** le permite tomar dbt y transformar datos con SQL en un entorno familiar.

    **Introducción:**

    Para empezar a usar Data Factory, puede seguir estos pasos:

    1) **Aprender a usar Data Factory**: en esta sección encontrará ayuda para empezar a utilizar Data Factory. Proporciona orientación sobre cómo comenzar a usar la herramienta de manera efectiva.

    2) **Crear su primer flujo de datos**: aquí puede aprender a crear su primer flujo de datos. Los flujos de datos son esenciales para transformar sus datos de acuerdo con sus necesidades.

    3) **Crear la primera canalización:** esta sección le guía sobre cómo crear su primera canalización. Las canalizaciones ayudan a automatizar y administrar sus procesos de datos de manera eficiente.

    4) **Aprenda a supervisar Data Factory**: la supervisión es fundamental para garantizar que sus procesos de datos funcionen sin problemas. En esta sección se aprende a supervisar las actividades de Data Factory.

    5) **Aprender a transformar datos con flujos de datos**: esta sección le ayuda a comprender cómo usar los flujos de datos para transformar sus datos de manera efectiva.

    6) **Crear su primera API para GraphQL**: si le interesa utilizar API con GraphQL, esta sección le guiará sobre cómo empezar.

    7) **Crear sus primeras funciones de datos de usuario**: esta sección le ayuda a crear funciones de datos de usuario, que son útiles para administrar y transformar los datos del usuario.

       ![](../media/Lab-2/image22.png)

4. Haga clic en **Volver a las cargas de trabajo** en la esquina superior izquierda de la pantalla. Esta acción le llevará a la página principal de cargas de trabajo, donde puede explorar otras herramientas o secciones.

    ![](../media/Lab-2/image23.png)

## Tarea 5: Experiencia de Industry Solutions

1. En la página **Cargas de trabajo**, haga clic en **Industry** **Solutions** para continuar.

    ![](../media/Lab-2/image24.png)

2. Se le dirigirá a la página principal de Industry Solutions. A continuación, se muestra una descripción detallada de sus secciones, diseñadas para ayudarle a utilizar Industry Solutions de manera efectiva y paso a paso.

    **¿Qué es Industry Solutions?**

    Industry Solutions son soluciones de datos listas para usar de Microsoft Fabric que proporcionan soluciones y recursos para diversos sectores. Industry Solutions le ayuda a comenzar con escenarios empresariales clave mediante el uso de modelos de datos, conectores, transformaciones, informes y otros activos relacionados con el sector.

    **Tipos de elementos**:

    1) **Soluciones de sostenibilidad**: admiten la ingesta, la estandarización y el análisis de datos ambientales, sociales y de gobernanza (ASG).

    2) **Soluciones de datos de atención sanitaria:** están diseñadas estratégicamente para acelerar el tiempo de creación de valor para los clientes al abordar la necesidad crítica de transformar de manera eficiente los datos sanitarios en un formato adecuado para el análisis.

    >**Nota:** Es posible que algunas soluciones no aparezcan para usted.

    **Introducción:**

    Para empezar a usar Industry Solutions, siga estos pasos:

    1) **Obtener información sobre las soluciones de datos de atención sanitaria**: haga clic en el botón “Más información” para leer sobre las soluciones de datos de atención sanitaria y comprender cómo se pueden utilizar en sus proyectos.

    2) **Empiece a usar soluciones de datos de asistencia sanitaria:** empiece a implementar soluciones de datos de atención sanitaria e impleméntelas en sus proyectos.

    3) **Obtener información sobre las soluciones de sostenibilidad**: haga clic en el botón “Más información” para leer sobre las soluciones de sostenibilidad y comprender cómo se pueden utilizar en sus proyectos.

    4) **Empiece a usar soluciones de datos de sostenibilidad:** comience a implementar soluciones de sostenibilidad e impleméntelas en sus proyectos.

    5) **Obtener información sobre la solución minorista**: haga clic en el botón “Más información” para leer sobre las soluciones de comercio minorista y comprender cómo se pueden utilizar en sus proyectos.

    6) **Empiece a usar soluciones de datos de comercio minorista:** comience a implementar soluciones de datos de comercio minorista e impleméntelas en sus proyectos.

       ![](../media/Lab-2/image25.png)

3. Haga clic en Volver a las cargas de trabajo en la esquina superior izquierda de la pantalla. Esta acción le llevará a la página principal de cargas de trabajo, donde puede explorar otras herramientas o secciones.

    ![](../media/Lab-2/image23.png)

## Tarea 6: Experiencia de Real-Time Intelligence

1. En la página **Cargas de trabajo**, haga clic en **Real-Time Intelligence** para continuar.

    ![](../media/Lab-2/image26.png)

2. Se le dirigirá a la página principal de Real-Time Intelligence. A continuación, se muestra una descripción detallada de sus secciones, diseñadas para ayudarle a utilizar Real-Time Intelligence de manera efectiva y paso a paso.

    **¿Qué es Real-Time Intelligence?**

    Real-Time Intelligence es una herramienta que le ayuda a administrar y analizar datos de gran volumen y alta granularidad de varios orígenes. Le permite ingerir, analizar y tomar medidas sobre sus datos en tiempo real, lo que mejora sus operaciones comerciales con una toma de decisiones y acciones oportunas.

    **Tipos de elementos**:

    1. **Casa de eventos**: se utiliza para crear un área de trabajo de una o varias bases de datos KQL, que se puede compartir entre proyectos.

    2. **Conjunto de consultas KQL**: se utiliza para ejecutar consultas sobre los datos para producir tablas y objetos visuales que se pueden compartir.

    3. **Panel en tiempo real**: se utiliza para visualizar paneles de información en tiempo real en cuestión de segundos desde la ingesta de datos.

    4. **Eventstream**: se utiliza para capturar, transformar y enrutar el flujo de eventos en tiempo real.

    5. **Activador**: se utiliza para supervisar conjuntos de datos, consultas y flujos de eventos en busca de patrones.

    6. **Conjunto de esquemas de eventos (versión preliminar):** le ayuda a organizar y estandarizar estructuras de datos (esquemas) para sus flujos de trabajo de análisis en tiempo real, lo que facilita el procesamiento y análisis de datos de streaming de manera coherente.

    7. **Conector de secuencias personalizadas (versión preliminar):** le permite enviar eventos en tiempo real a un eventstream desde sus propios puntos de conexión y aplicaciones personalizados.

    8. **Anomaly Detector (versión preliminar):** la detección de anomalías identifica automáticamente patrones inusuales y valores atípicos en las tablas de Event house.

    9. **Agente de operaciones (versión preliminar):** los agentes de operaciones automatizan el ciclo de observar > analizar, > decidir > actuar. Realizan un seguimiento continuo de métricas clave, extraen información y recomiendan acciones específicas.

    10. **Mapa:** incorpore información geoespacial en Real-Time Intelligence, para permitir a cualquier persona visualizar dónde ocurren los eventos, integrar datos espaciales con otras capacidades de Fabric y tomar decisiones más inteligentes que tengan en cuenta la ubicación.

    11. **Generador de gemelos digitales (versión preliminar):** el generador de gemelos digitales proporciona a los usuarios experiencias con poco o ningún código para crear y modelar sus conceptos empresariales, como activos y procesos, a través de una ontología.

    **Introducción:**

    Para empezar a utilizar Real-Time Intelligence, siga estos pasos:

    1. **Experiencias integrales en tiempo real:** haga clic en el botón "Comenzar" para explorar el análisis de datos con conjuntos de datos de ejemplo.

    2. **Explorar ejemplo de inteligencia de tiempo real**: haga clic en el botón “Abrir” para explorar el análisis de datos en tiempo real con un ejemplo.

    3. **Explore un ejemplo de Eventhouse:** haga clic en el botón "Seleccionar" para usar un ejemplo y obtener información sobre Real-Time Intelligence.

    4. **Introducción a la Inteligencia en tiempo real**: haga clic en el botón “Abrir” para obtener una descripción general de Real-Time Intelligence y comenzar a usar la herramienta de manera eficaz.

    5. **Obtenga información sobre KQL con datos de ejemplo**: haga clic en el botón “Abrir” para aprender KQL con datos de ejemplo.

    6. **¿Qué es un centro en tiempo real?**: haga clic en el botón “Abrir” para saber qué es un centro en tiempo real y cómo se puede utilizar.

    7. **Explorar un activador de ejemplo**: haga clic en el botón “Abrir” para usar un activador de muestra y comprender las características y capacidades de Real-Time Intelligence.

    8. **Comenzar con activador**: haga clic en el botón “Abrir” para comenzar con los conceptos de activador y comenzar a usar la herramienta de manera efectiva.

        ![](../media/Lab-2/image27.png)

3. Haga clic en Volver a las cargas de trabajo en la esquina superior izquierda de la pantalla. Esta acción le llevará a la página principal de cargas de trabajo, donde puede explorar otras herramientas o secciones.

    ![](../media/Lab-2/image23.png)

## Tarea 7: Experiencia de Data Engineering

1. En la página **Cargas de trabajo**, haga clic en Data Engineering para continuar.

    ![](../media/Lab-2/image28.png)

2. Se le dirigirá a la página principal de **Data Engineering**. A continuación, se muestra una descripción detallada de sus secciones, diseñadas para ayudarle a utilizar **Data Engineering** de manera efectiva y paso a paso.

    **¿Qué es Data Engineering?**

    Data Engineering es una herramienta que le ayuda a diseñar, construir y mantener infraestructuras y sistemas para recopilar, almacenar, procesar y analizar grandes volúmenes de datos. Le permite crear almacenes de lago y poner en funcionamiento su flujo de trabajo para crear, transformar y compartir su patrimonio de datos.

    **Tipos de elementos:**

    1. **Lakehouse**: se utiliza para almacenar macrodatos para limpiar, consultar, generar informes y compartir.

    2. **Bloc de notas**: se utiliza para la ingesta de datos, la preparación, el análisis y otras tareas relacionadas con los datos utilizando varios lenguajes como Python y Scala.

    3. **Entorno**: se utiliza para configurar bibliotecas compartidas, configuraciones y recursos informáticos de Spark para portátiles y definiciones de trabajos de Spark.

    4. **Definición de trabajo de Spark**: se utiliza para definir, programar y administrar trabajos de Apache.

    5. **Funciones de datos de usuario**: plataforma que le permite hospedar y ejecutar aplicaciones en Fabric.

    6. **API para GraphQL**: es una API para consultar varios orígenes de datos.

    7. **Base de datos de Snowflake**: permite a los usuarios duplicar la base de datos de Snowflake dentro de Fabric.

    **Introducción:**

    Para empezar a usar Data Engineering, siga estos pasos:

    1. **Explorar un ejemplo**: haga clic en el botón “Seleccionar” para usar una muestra y obtener información sobre Data Engineering.

    1. **¿Qué es un lakehouse?:** haga clic en el botón “Abrir” para obtener información sobre los almacenes de lago de datos y cómo se pueden usar.

    1. **Obtención de la experiencia de datos en un lakehouse**: haga clic en el botón “Abrir” para comenzar con ingeniería de datos y los almacenes de lago de datos.

    1. **Introducción a las definiciones de trabajo de Spark**: haga clic en el botón “Abrir” para aprender a utilizar las definiciones de trabajo de Spark para el procesamiento de datos.

    1. **Desarrollar y ejecutar cuadernos**: haga clic en el botón “Abrir” para aprender a desarrollar y ejecutar cuadernos para el análisis de datos.

    1. **Cómo usar NotebookUtils**: haga clic en el botón “Abrir” para aprender a usar NotebookUtils para un análisis de datos mejorado.

    1. **Aprovechar los Notebooks para su almacén de lago de datos**: haga clic en el botón “Abrir” para aprender a aprovechar los notebooks para su almacén de lago de datos.

    1. **Aprovechar los conjuntos de datos para su almacén de lago de datos**: haga clic en el botón “Abrir” para aprender a aprovechar los conjuntos de datos para su almacén de lago de datos.

    1. **Crear sus primeras funciones de datos de usuario**: haga clic en el botón “Abrir” para aprender a crear funciones de datos de usuario.

    1. **Crear su primera API para GraphQL**: haga clic en el botón “Abrir” para aprender a crear una API para GraphQL.

       ![](../media/Lab-2/image29.png)

3. Haga clic en **Volver a las cargas de trabajo** en la esquina superior izquierda de la pantalla. Esta acción le llevará a la página principal de cargas de trabajo, donde puede explorar otras herramientas o secciones.

    ![](../media/Lab-2/image23.png)

## Tarea 8: Experiencia de Data Science

1. En la página **Cargas de trabajo**, haga clic en **Data Science** para continuar.

    ![](../media/Lab-2/image30.png)

2. Se le dirigirá a la página principal de **Data Science**. A continuación, se muestra una descripción detallada de sus secciones, diseñadas para ayudarle a utilizar **Data Science** de manera efectiva.

    **¿Qué es Data Science?**

    Data Science es una herramienta que le ayuda a desbloquear información valiosa mediante IA y tecnología de aprendizaje automático. Proporciona herramientas de IA diseñadas para ayudarle a completar flujos de trabajo de ciencia de datos a gran escala y aprovecha la IA para el enriquecimiento de datos y la información empresarial.

    **Tipos de elementos:**

    1. **Modelos de ML**: se usa para crear modelos de Machine Learning.

    2. **Experimento**: se utiliza para crear, ejecutar y hacer un seguimiento del desarrollo de múltiples modelos.

    3. **Bloc de notas**: se utiliza para explorar datos y crear soluciones de aprendizaje automático.

    4. **Entorno**: se utiliza para configurar bibliotecas compartidas, configuraciones y recursos informáticos de Spark para portátiles y definiciones de trabajos de Spark.

    5. **Agente de datos:** se utiliza para crear experiencias de IA conversacional que respondan preguntas sobre datos almacenados en almacenes de lago de datos, almacenes, modelos semánticos de Power BI y bases de datos KQL.

    6. **Cuaderno de Python**: se utiliza para importar cuadernos de Python desde una máquina local.

    **Introducción:**

    Para empezar a usar Data Science, siga estos pasos

    1. **Explorar un ejemplo**: haga clic en el botón “Seleccionar” para usar una muestra y obtener información sobre Data Science.

    2. **Introducción a los modelos de ML**: haga clic en el botón “Abrir” para comenzar con los modelos de Machine Learning.

    3. **Introducción a los experimentos de ML**: haga clic en el botón “Abrir” para aprender a hacer experimentos de aprendizaje automático.

    4. **Introducción a Notebooks:** haga clic en el botón "Abrir" para comenzar con notebooks.

    5. **Desarrollar y ejecutar Notebooks:** haga clic en el botón "Abrir" para aprender a desarrollar y ejecutar cuadernos para el análisis de datos.

       ![](../media/Lab-2/image31.png)

3. Haga clic en **Volver a las cargas de trabajo** en la esquina superior izquierda de la pantalla. Esta acción le llevará a la página principal de cargas de trabajo, donde puede explorar otras herramientas o secciones.

    ![](../media/Lab-2/image23.png)

## Tarea 9: Experiencia de Data Warehouse

1. En la página **Cargas de trabajo**, haga clic en **Data Warehouse** para continuar.

    ![](../media/Lab-2/image32.png)

2. Se le dirigirá a la página principal de Data Warehouse. A continuación se muestra una descripción detallada de sus secciones, diseñadas para ayudarlo a usar Data Warehouse de manera efectiva y paso a paso.

    **¿Qué es Data Warehouse?**

    Data Warehouse es una herramienta que le ayuda a almacenar y analizar datos en un almacén SQL seguro. Le permite ampliar sus conocimientos al beneficiarse de un rendimiento de primer nivel a escala de petabytes en un formato de datos abiertos.

    **Tipos de elementos:**

    1. **Almacén**: se usa para crear un Data Warehouse.

    2. **Almacén de muestra**: se utiliza para explorar y probar las capacidades de almacenamiento de datos con conjuntos de datos y modelos preconfigurados.

    3. **Cuaderno**: se utiliza para crear y compartir tareas interactivas de análisis y visualización de datos.

    4. **Azure SQL Database reflejada**: se utiliza para reflejar Azure SQL Database.

    5. **Catálogo de Azure Databricks reflejado**: se utiliza para reflejar datos de Azure Databricks para mejorar la integración y el análisis.

    6. **Snowflake reflejado**: se utiliza para reflejar la base de datos de Snowflake.

    7. **Oracle reflejado:** se utiliza para reflejar Oracle.

    8. **Google BigQuery reflejada (versión preliminar):** se utiliza para reflejar Google BigQuery.

    9. **Lista de SharePoint Online reflejada (versión preliminar):** replica los datos de lista de SharePoint casi en tiempo real en Microsoft Fabric OneLake como un origen de solo lectura y listo para análisis. Elimina ETL y expone los datos a través de un punto de conexión de análisis SQL creado automáticamente y otras cargas de trabajo de Power BI Fabric.

    10. **Azure Cosmos DB reflejado:** se utiliza para reflejar Azure Cosmos DB.

    11. **SQL Server reflejado:** se utiliza para reflejar SQL Server.

    12. **Mirrored Azure Database for PostgreSQL:** se usa para reflejar la Azure Database for PostgreSQL existente.

    13. **Azure Database for MySQL reflejada (versión preliminar):** replica datos de MySQL en Microsoft Fabric OneLake como un origen de solo lectura y listo para análisis, lo que permite un análisis casi en tiempo real sin ETL.

    14. **Base de datos administrada de Azure SQL reflejada**: se utiliza para reflejar bases de datos administradas de Azure SQL para alta disponibilidad y recuperación ante desastres.

    15. **Base de datos reflejada:** se utiliza para replicar bases de datos para alta disponibilidad y recuperación ante desastres.

    16. **Catálogo de Dremio reflejado (versión preliminar):** refleja los metadatos del catálogo de Dremio en Microsoft Fabric (no se copian datos), lo que crea accesos directos que permiten que las cargas de trabajo de Fabric consulten los datos administrados por Dremio a través de un punto de conexión de análisis SQL de solo lectura.

    **Introducción:**

    Para empezar a utilizar Data Warehouse, siga los siguientes pasos:

    1. **Explorar un almacén de muestra**: inicie un nuevo almacén con datos de ejemplo ya cargados.

    1. **Introducción al almacén**: haga clic en el botón “Abrir” para aprender a utilizar un almacén para analizar datos.

        ![](../media/Lab-2/image33.png)

3. Haga clic en **Volver a las cargas de trabajo** en la esquina superior izquierda de la pantalla. Esta acción le llevará a la página principal de cargas de trabajo, donde puede explorar otras herramientas o secciones.

    ![](../media/Lab-2/image23.png)

## Tarea 10: Experiencia de bases de datos

1. En la página **Cargas de trabajo**, haga clic en **Databases** para continuar.

    ![](../media/Lab-2/image34.png)

2. Se le dirigirá a la página principal de Bases de datos. A continuación se muestra una descripción general detallada de sus secciones, diseñadas para ayudarle a utilizar las bases de datos con eficacia.

    **¿Qué es una Fabric Database?**

    Una SQL Database en Microsoft Fabric es una base de datos transaccional fácil de usar para desarrolladores, basada en Azure SQL Database, que le permite crear con facilidad su base de datos operativa en Fabric. Una SQL Database en Fabric utiliza el mismo motor de SQL Database que Azure SQL Database.

    **Tipos de elementos:**

    1. **Base de datos SQL:** la base de datos SQL en Fabric es parte de la carga de trabajo de Database y se puede acceder a los datos desde otros elementos de Fabric. Los datos de su base de datos de SQL también se mantienen actualizados en un formato que se pueden consultar en OneLake, para que pueda usar todos los diferentes servicios de Fabric, como la ejecución de análisis con Spark, la ejecución de cuadernos, la ingeniería de datos y la visualización a través Power BI de informes, entre otros.

    2. **Cosmos DB:** Cosmos DB en Microsoft Fabric es una base de datos NoSQL optimizada para IA con una experiencia de administración simplificada. Como desarrollador, puede utilizar Cosmos DB en Fabric para desarrollar aplicaciones de IA con menos fricción y sin tener que asumir tareas típicas de administración de bases de datos.

    **Introducción:**

    Para empezar a utilizar Databases, siga los siguientes pasos:

    1. **Explorar**: haga clic en “Abrir” para explorar una base de datos de ejemplo.

    1. **Database concepts**: explica los términos y conceptos comunes en torno a la base de datos transaccional para que pueda familiarizarse con cómo trabajar con SQL Database.

    1. **Database templates**: revise una biblioteca de plantillas creadas previamente con diseños comunes de bases de datos.

       ![](../media/Lab-2/image35.png)

3. Haga clic en Volver a las cargas de trabajo en la esquina superior izquierda de la pantalla. Esta acción le llevará a la página principal de cargas de trabajo, donde puede explorar otras herramientas o secciones.

    ![](../media/Lab-2/image23.png)

    En esta práctica de laboratorio, exploramos la interfaz de Fabric, creamos un área de trabajo de Fabric y un almacén de lago de datos. En el próximo laboratorio, aprenderemos a utilizar accesos directos en el almacén de lago de datos para conectarnos a los datos de ADLS Gen2 y a transformar estos datos mediante vistas.

# Referencias

Fabric Analyst in a Day (FAIAD) le presenta algunas funciones clave disponibles en Microsoft Fabric. En el menú del servicio, la sección Ayuda (?) tiene vínculos a algunos recursos excelentes.

![](../media/Lab-2/image36.png)

Estos son algunos recursos más que podrán ayudarle a seguir avanzando con Microsoft Fabric.

- Vea la publicación del blog para leer el texto completo.

- Explore Fabric a través de la [Visita guiada](https://aka.ms/Fabric-GuidedTour)

- Regístrese en la [prueba gratuita de Microsoft Fabric](https://aka.ms/try-fabric).

- Visite el [sitio web de Microsoft Fabric](https://aka.ms/microsoft-fabric).

- Adquiera nuevas capacidades mediante la exploración de los [módulos de aprendizaje de Fabric](https://aka.ms/learn-fabric)

- Explore la [documentación técnica de Fabric](https://aka.ms/fabric-docs).

- Lea el [libro electrónico gratuito sobre cómo empezar a usar Fabric](https://aka.ms/fabric-get-started-ebook).

- Únase a la [comunidad de Fabric](https://aka.ms/fabric-community) para publicar sus preguntas, compartir sus comentarios y aprender de otros.

Obtenga más información en los blogs de anuncios de la experiencia Fabric:

- [Experiencia de Data Factory en el blog de Fabric](https://aka.ms/Fabric-Data-Factory-Blog)

- [Experiencia de Synapse Data Engineering en el blog de Fabric](https://aka.ms/Fabric-DE-Blog)

- [Experiencia de Synapse Data Science en el blog de Fabric](https://aka.ms/Fabric-DS-Blog)

- [Experiencia de Synapse Data Warehousing en el blog de Fabric](https://aka.ms/Fabric-DW-Blog)

- [Experiencia de Synapse Real-Time Analytics en el blog de Fabric](https://aka.ms/Fabric-RTA-Blog)

- [Blog de anuncios de Power BI](https://aka.ms/Fabric-PBI-Blog)

- [Experiencia de Data Activator en el blog de Fabric](https://aka.ms/Fabric-DA-Blog)

- [Administración y gobernanza en el blog de Fabric](https://aka.ms/Fabric-Admin-Gov-Blog)

- [OneLake en el blog de Fabric](https://aka.ms/Fabric-OneLake-Blog)

- [Blog de integración de Dataverse y Microsoft Fabric](https://aka.ms/Dataverse-Fabric-Blog)

© 2026 Microsoft Corporation. Todos los derechos reservados.

Al participar en esta demostración o laboratorio práctico, acepta las siguientes condiciones:

Microsoft Corporation pone a su disposición la tecnología o funcionalidad descrita en esta demostración/laboratorio práctico con el fin de obtener comentarios por su parte y de facilitarle una experiencia de aprendizaje. Esta demostración/laboratorio práctico solo se puede usar para evaluar las características de tal tecnología o funcionalidad y para proporcionar comentarios a Microsoft. No se puede usar para ningún otro propósito. Ninguna parte de esta demostración/laboratorio práctico se puede modificar, copiar, distribuir, transmitir, mostrar, realizar, reproducir, publicar, licenciar, transferir ni vender, ni tampoco crear trabajos derivados de ella.

LA COPIA O REPRODUCCIÓN DE ESTA DEMOSTRACIÓN/LABORATORIO PRÁCTICO (O PARTE DE ELLA) EN CUALQUIER OTRO SERVIDOR O UBICACIÓN PARA SU REPRODUCCIÓN O DISTRIBUCIÓN POSTERIOR QUEDA EXPRESAMENTE PROHIBIDA.

ESTA DEMOSTRACIÓN/LABORATORIO PRÁCTICO PROPORCIONA CIERTAS FUNCIONES Y CARACTERÍSTICAS DE PRODUCTOS O TECNOLOGÍAS DE SOFTWARE (INCLUIDOS POSIBLES NUEVOS CONCEPTOS Y CARACTERÍSTICAS) EN UN ENTORNO SIMULADO SIN INSTALACIÓN O CONFIGURACIÓN COMPLEJA PARA EL PROPÓSITO ARRIBA DESCRITO. LA TECNOLOGÍA/CONCEPTOS DESCRITOS EN ESTA DEMOSTRACIÓN/LABORATORIO PRÁCTICO NO REPRESENTAN LA FUNCIONALIDAD COMPLETA DE LAS CARACTERÍSTICAS Y, EN ESTE SENTIDO, ES POSIBLE QUE NO FUNCIONEN DEL MODO EN QUE LO HARÁN EN UNA VERSIÓN FINAL. ASIMISMO, PUEDE QUE NO SE PUBLIQUE UNA VERSIÓN FINAL DE TALES CARACTERÍSTICAS O CONCEPTOS. DE IGUAL MODO, SU EXPERIENCIA CON EL USO DE ESTAS CARACTERÍSTICAS Y FUNCIONALIDADES EN UN ENTORNO FÍSICO PUEDE SER DIFERENTE.

**COMENTARIOS.** Si envía comentarios a Microsoft sobre las características, funcionalidades o conceptos de tecnología descritos en esta demostración/laboratorio práctico, acepta otorgar a Microsoft, sin cargo alguno, el derecho a usar, compartir y comercializar sus comentarios de cualquier modo y para cualquier fin. También concederá a terceros, sin cargo alguno, los derechos de patente necesarios para que sus productos, tecnologías y servicios usen o interactúen con cualquier parte específica de un software o servicio de Microsoft que incluya los comentarios. No enviará comentarios que estén sujetos a una licencia que obligue a Microsoft a conceder su software o documentación bajo licencia a terceras partes porque incluyamos sus comentarios en ellos. Estos derechos seguirán vigentes después del vencimiento de este acuerdo.

MICROSOFT CORPORATION RENUNCIA POR LA PRESENTE A TODAS LAS GARANTÍAS Y CONDICIONES RELATIVAS A LA DEMOSTRACIÓN/LABORATORIO PRÁCTICO, INCLUIDA CUALQUIER GARANTÍA Y CONDICIÓN DE COMERCIABILIDAD (YA SEA EXPRESA, IMPLÍCITA O ESTATUTARIA), DE IDONEIDAD PARA UN FIN DETERMINADO, DE TITULARIDAD Y DE AUSENCIA DE INFRACCIÓN. MICROSOFT NO DECLARA NI GARANTIZA LA EXACTITUD DE LOS RESULTADOS, EL RESULTADO DERIVADO DE LA REALIZACIÓN DE LA DEMOSTRACIÓN/LABORATORIO PRÁCTICO NI LA IDONEIDAD DE LA INFORMACIÓN CONTENIDA EN ELLA CON NINGÚN PROPÓSITO.

**DECLINACIÓN DE RESPONSABILIDADES**

Esta demostración/laboratorio práctico contiene solo una parte de las nuevas características y mejoras realizadas en Microsoft Power BI. Puede que algunas de las características cambien en versiones futuras del producto. En esta demostración/laboratorio práctico, conocerá algunas de estas nuevas características, pero no todas.
