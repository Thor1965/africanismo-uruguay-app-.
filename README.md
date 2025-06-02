# africanismo-uruguay-app-.
<!DOCTYPE html>
<html lang="es" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Huellas de África: Africanismo y Sincretismo en Uruguay</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Merriweather:wght@400;700&family=Roboto:wght@400;500&display=swap" rel="stylesheet">
    <!-- Visualization & Content Choices:
        - Raíces: Un cronograma interactivo (HTML/CSS) para mostrar el contexto histórico de forma clara. Interacción: Hover para detalles. Justificación: Facilita la comprensión de la secuencia de eventos.
        - Candombe: Diagrama interactivo de tambores (HTML/CSS/JS) y un gráfico de dona (Chart.js) para explicar sus componentes. Interacción: Clic en tambores. Justificación: Fomenta la exploración activa de los elementos culturales clave.
        - Fe y Fusión: Comparación lado a lado (HTML/CSS Grid) de Orishas y Santos. Interacción: Clic para ver descripciones. Justificación: Es la forma más directa y visual de explicar el sincretismo.
        - Huellas: Lista interactiva de palabras (HTML/CSS/JS). Interacción: Hover para ver significados. Justificación: Presenta la influencia lingüística de forma atractiva.
        - Legado Hoy: Un gráfico de barras conceptual (Chart.js) para visualizar las áreas de enfoque de la comunidad. Justificación: Ofrece un resumen visual y moderno de la situación actual.
        - Pregunta al Experto: Un campo de texto y botón para que el usuario formule preguntas relacionadas con el contenido del libro. Interacción: Envío de pregunta para recibir una respuesta generada por LLM. Justificación: Permite una exploración personalizada y profundiza el entendimiento del usuario sobre el tema, utilizando el modelo `gemini-2.0-flash`.
    -->
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            background-color: #FDFBF8;
            color: #4A4A4A;
        }
        h1, h2, h3, .nav-link {
            font-family: 'Merriweather', serif;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 450px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 350px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
                max-height: 400px;
            }
        }
        .nav-link.active {
            color: #D97706;
            font-weight: bold;
        }
        .timeline-item::before {
            content: '';
            position: absolute;
            left: -20px;
            top: 50%;
            transform: translateY(-50%);
            width: 10px;
            height: 10px;
            background-color: #D97706;
            border-radius: 50%;
            border: 2px solid #FDFBF8;
        }
    </style>
</head>
<body class="antialiased">

    <header class="bg-[#FDFBF8]/80 backdrop-blur-sm sticky top-0 z-50 shadow-sm">
        <nav class="container mx-auto px-6 py-3">
            <div class="flex justify-between items-center">
                <h3 class="text-xl font-bold text-amber-700">Huellas de África</h3>
                <div class="hidden md:flex space-x-8">
                    <a href="#raices" class="nav-link text-gray-700 hover:text-amber-600 transition">Raíces</a>
                    <a href="#candombe" class="nav-link text-gray-700 hover:text-amber-600 transition">Candombe</a>
                    <a href="#fe" class="nav-link text-gray-700 hover:text-amber-600 transition">Fe y Fusión</a>
                    <a href="#huellas" class="nav-link text-gray-700 hover:text-amber-600 transition">Huellas</a>
                    <a href="#legado" class="nav-link text-gray-700 hover:text-amber-600 transition">Legado</a>
                    <a href="#pregunta-experto" class="nav-link text-gray-700 hover:text-amber-600 transition">Pregunta al Experto ✨</a>
                </div>
                <div class="md:hidden">
                    <button id="menu-btn" class="text-gray-700 focus:outline-none">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path></svg>
                    </button>
                </div>
            </div>
            <div id="mobile-menu" class="hidden md:hidden mt-3">
                <a href="#raices" class="block py-2 px-4 text-sm nav-link text-gray-700 hover:bg-amber-50 rounded">Raíces</a>
                <a href="#candombe" class="block py-2 px-4 text-sm nav-link text-gray-700 hover:bg-amber-50 rounded">Candombe</a>
                <a href="#fe" class="block py-2 px-4 text-sm nav-link text-gray-700 hover:bg-amber-50 rounded">Fe y Fusión</a>
                <a href="#huellas" class="block py-2 px-4 text-sm nav-link text-gray-700 hover:bg-amber-50 rounded">Huellas</a>
                <a href="#legado" class="block py-2 px-4 text-sm nav-link text-gray-700 hover:bg-amber-50 rounded">Legado</a>
                <a href="#pregunta-experto" class="block py-2 px-4 text-sm nav-link text-gray-700 hover:bg-amber-50 rounded">Pregunta al Experto ✨</a>
            </div>
        </nav>
    </header>

    <main>
        <section id="hero" class="py-20 md:py-32 bg-amber-50">
            <div class="container mx-auto px-6 text-center">
                <h1 class="text-4xl md:text-6xl font-bold text-amber-900 mb-4">Africanismo y Sincretismos en Uruguay</h1>
                <p class="text-lg md:text-xl max-w-3xl mx-auto text-gray-700">
                    Uruguay es un crisol de culturas. A menudo hablamos de nuestras raíces europeas, pero hay una parte fundamental de nuestra identidad que a veces pasa desapercibida: la profunda huella africana. Este viaje interactivo te invita a descubrir cómo las tradiciones, la música y las creencias traídas desde África se fusionaron para crear algo nuevo y único en el corazón de nuestra identidad.
                </p>
            </div>
        </section>

        <section id="raices" class="py-16 md:py-24">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-3xl md:text-4xl font-bold text-amber-900">1. Las Raíces de la Llegada</h2>
                    <p class="mt-4 max-w-2xl mx-auto text-gray-600">Para entender el presente, debemos mirar al pasado. Esta sección explora el contexto histórico de la llegada de africanos a la región del Río de la Plata, un proceso marcado por la violencia de la trata transatlántica pero también por la inquebrantable resiliencia y la formación de nuevas comunidades.</p>
                </div>
                <div class="max-w-xl mx-auto border-l-2 border-amber-200 pl-8 relative">
                    <div class="timeline-item mb-12 relative">
                        <h3 class="text-xl font-bold text-amber-800">Siglos XVII-XIX</h3>
                        <p class="text-gray-600">La trata transatlántica trae a millones de africanos esclavizados a las Américas. Montevideo se convierte en un puerto clave para la introducción de esclavos en el Virreinato del Río de la Plata.</p>
                    </div>
                    <div class="timeline-item mb-12 relative">
                        <h3 class="text-xl font-bold text-amber-800">1825</h3>
                        <p class="text-gray-600">Durante las luchas por la independencia, se decreta la "Libertad de Vientres", declarando libres a los hijos de esclavas nacidos a partir de esa fecha, aunque la abolición total tardaría en llegar.</p>
                    </div>
                    <div class="timeline-item mb-12 relative">
                        <h3 class="text-xl font-bold text-amber-800">1842</h3>
                        <p class="text-gray-600">Uruguay finalmente abole la esclavitud. Comienza un largo y difícil proceso para la población afrodescendiente de integración social, económica y lucha por sus derechos civiles en una sociedad que aún mantenía profundos prejuicios.</p>
                    </div>
                     <div class="timeline-item relative">
                        <h3 class="text-xl font-bold text-amber-800">Finales del Siglo XIX</h3>
                        <p class="text-gray-600">Se consolidan las "sociedades de negros", espacios de ayuda mutua y preservación cultural. En sus locales, conocidos como "salas de naciones", se gesta y mantiene vivo el candombe.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="candombe" class="py-16 md:py-24 bg-amber-50">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-3xl md:text-4xl font-bold text-amber-900">2. El Ritmo del Candombe</h2>
                    <p class="mt-4 max-w-2xl mx-auto text-gray-600">El candombe es mucho más que música; es el alma de la cultura afrouruguaya. En esta sección exploraremos sus componentes, desde la llamada de los tambores hasta su significado como Patrimonio de la Humanidad. Haz clic en cada tambor para descubrir su voz única.</p>
                </div>
                <div class="grid md:grid-cols-2 gap-12 items-center">
                    <div>
                        <h3 class="text-2xl font-bold text-amber-800 mb-6 text-center">Los Tres Tambores</h3>
                        <div class="flex justify-around items-end text-center">
                            <div class="tambor cursor-pointer group" data-info="Chico: El más pequeño y agudo. Su patrón rítmico es constante y marca el pulso de la cuerda, como un reloj que sostiene el tiempo para los demás.">
                                <div class="w-16 h-24 md:w-20 md:h-32 bg-yellow-700 rounded-t-lg mx-auto group-hover:scale-105 transition"></div>
                                <p class="mt-2 font-bold">Chico</p>
                            </div>
                            <div class="tambor cursor-pointer group" data-info="Repique: De tamaño y registro intermedio. Es el tambor improvisador, el que dialoga con los otros dos y con los bailarines. Su toque es enérgico y sincopado.">
                                <div class="w-20 h-32 md:w-24 md:h-40 bg-orange-800 rounded-t-lg mx-auto group-hover:scale-105 transition"></div>
                                <p class="mt-2 font-bold">Repique</p>
                            </div>
                            <div class="tambor cursor-pointer group" data-info="Piano: El más grande y grave. Es la base, el corazón de la cuerda. Su sonido profundo y su ritmo lento y poderoso marcan los cimientos sobre los que se construye la música.">
                                <div class="w-24 h-40 md:w-28 md:h-48 bg-amber-900 rounded-t-lg mx-auto group-hover:scale-105 transition"></div>
                                <p class="mt-2 font-bold">Piano</p>
                            </div>
                        </div>
                        <div id="tambor-info" class="mt-6 p-4 bg-white rounded-lg shadow-inner text-center min-h-[80px] flex items-center justify-center">
                            <p class="text-gray-600">Haz clic en un tambor para leer su descripción.</p>
                        </div>
                    </div>
                    <div>
                         <h3 class="text-2xl font-bold text-amber-800 mb-4 text-center">Expresión Cultural Completa</h3>
                        <div class="chart-container">
                            <canvas id="candombeChart"></canvas>
                        </div>
                         <p class="text-center text-gray-600 mt-4">El candombe integra música, danza comunitaria y ritual social, siendo una expresión cultural indivisible.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="fe" class="py-16 md:py-24">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-3xl md:text-4xl font-bold text-amber-900">3. Fe y Fusión: Los Sincretismos</h2>
                     <p class="mt-4 max-w-2xl mx-auto text-gray-600">Frente a la imposición del catolicismo, las creencias africanas no desaparecieron; se transformaron. En esta sección exploramos el sincretismo, la fascinante fusión donde los Orishas yorubas encontraron un reflejo en los santos católicos, creando religiones únicas como la Umbanda.</p>
                </div>
                <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                    <div class="bg-white p-6 rounded-lg shadow-md hover:shadow-xl transition">
                        <h3 class="text-xl font-bold text-amber-800">Iemanjá ↔️ Virgen María</h3>
                        <p class="mt-2 text-gray-600">Considerada la madre de todos los Orishas y reina del mar, su figura protectora y maternal se sincretizó con la Virgen María, especialmente en su advocación de Stella Maris (Estrella del Mar), patrona de los navegantes.</p>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-md hover:shadow-xl transition">
                        <h3 class="text-xl font-bold text-amber-800">Oxalá ↔️ Jesucristo</h3>
                        <p class="mt-2 text-gray-600">El Orisha mayor, creador de la tierra y del hombre, se asocia con la paciencia y la paz. Su figura se corresponde con la de Jesucristo, por ser la principal deidad y símbolo de sacrificio y fe en el catolicismo.</p>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-md hover:shadow-xl transition">
                        <h3 class="text-xl font-bold text-amber-800">Xangô ↔️ San Juan Bautista / San Jerónimo</h3>
                        <p class="mt-2 text-gray-600">Orisha de la justicia, los truenos y el fuego. Su carácter fuerte y justiciero se asocia con San Jerónimo, conocido por su temperamento, y con San Juan Bautista, que clama por la justicia en el desierto.</p>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-md hover:shadow-xl transition">
                        <h3 class="text-xl font-bold text-amber-800">Ogum ↔️ San Jorge</h3>
                        <p class="mt-2 text-gray-600">El Orisha guerrero, señor del hierro, la guerra y la tecnología. Se le asocia con San Jorge, el santo soldado que venció al dragón, por su iconografía militar y su rol como protector en las batallas de la vida.</p>
                    </div>
                     <div class="bg-white p-6 rounded-lg shadow-md hover:shadow-xl transition">
                        <h3 class="text-xl font-bold text-amber-800">Oxóssi ↔️ San Sebastián</h3>
                        <p class="mt-2 text-gray-600">Es el Orisha de la caza, los bosques y la abundancia. Su relación con el arco y la flecha lo conecta directamente con San Sebastián, mártir que fue asaeteado y es patrono de los cazadores y soldados.</p>
                    </div>
                     <div class="bg-white p-6 rounded-lg shadow-md hover:shadow-xl transition">
                        <h3 class="text-xl font-bold text-amber-800">Exú y Pomba Gira</h3>
                        <p class="mt-2 text-gray-600">Guardianes de los caminos, mensajeros entre los mundos. A menudo malinterpretados, no tienen un sincretismo directo y representan la energía vital, la comunicación y la transformación en Umbanda y Kimbanda.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="huellas" class="py-16 md:py-24 bg-amber-50">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-3xl md:text-4xl font-bold text-amber-900">4. Huellas en el Lenguaje y las Costumbres</h2>
                    <p class="mt-4 max-w-2xl mx-auto text-gray-600">La influencia africana va más allá de la música y la fe, impregnando nuestro lenguaje y costumbres cotidianas. En esta sección, descubre algunas palabras y conceptos que usamos a diario y que tienen una profunda raíz afro. Pasa el cursor sobre cada término.</p>
                </div>
                <div class="p-8 bg-white rounded-lg shadow-lg flex flex-wrap justify-center items-center gap-4 md:gap-6">
                    <span class="palabra text-xl md:text-2xl font-bold text-orange-700 cursor-default" data-info="Originaria del quimbundo, se refiere a un niño o niña pequeña.">Mandinga</span>
                    <span class="palabra text-lg md:text-xl text-gray-600 cursor-default" data-info="Del quimbundo 'kilombo', que significaba asentamiento. Hoy se usa coloquialmente para referirse a un desorden o alboroto.">Quilombo</span>
                    <span class="palabra text-2xl md:text-3xl font-bold text-amber-800 cursor-default" data-info="Término bantú que puede referirse a un hechizo o brujería, aunque su significado original es más complejo.">Gualicho</span>
                    <span class="palabra text-lg md:text-xl text-gray-600 cursor-default" data-info="Proviene del yoruba y se refiere a una comida o festín, especialmente en un contexto ritual.">Batuque</span>
                    <span class="palabra text-xl md:text-2xl font-bold text-orange-700 cursor-default" data-info="De origen bantú, se refiere a una persona de poca inteligencia o tonta.">Bobo</span>
                     <span class="palabra text-2xl md:text-3xl font-bold text-amber-800 cursor-default" data-info="Del quimbundo 'kizumba', fiesta. Se usa para referirse a una celebración alegre y ruidosa.">Candombe</span>
                    <span class="palabra text-lg md:text-xl text-gray-600 cursor-default" data-info="Del quimbundo 'muchacha', sirvienta joven. Hoy se usa de forma más general.">Mucama</span>
                </div>
                 <div id="palabra-info" class="mt-6 p-4 bg-amber-100/50 rounded-lg text-center min-h-[60px] flex items-center justify-center">
                    <p class="text-amber-900">Pasa el cursor sobre una palabra para conocer su origen.</p>
                </div>
            </div>
        </section>

        <section id="legado" class="py-16 md:py-24">
            <div class="container mx-auto px-6">
                 <div class="text-center mb-12">
                    <h2 class="text-3xl md:text-4xl font-bold text-amber-900">5. El Legado Vivo: Africanismo Hoy</h2>
                    <p class="mt-4 max-w-2xl mx-auto text-gray-600">La herencia africana no es una pieza de museo, es una fuerza viva y activa en el Uruguay contemporáneo. Esta sección aborda la realidad actual de la comunidad afrodescendiente, sus contribuciones constantes a la identidad nacional y los desafíos que aún enfrenta.</p>
                </div>
                <div class="grid md:grid-cols-2 gap-12 items-center">
                    <div>
                         <h3 class="text-2xl font-bold text-amber-800 mb-4">Áreas de Enfoque Comunitario</h3>
                        <p class="text-gray-600 mb-4">La comunidad afrouruguaya continúa trabajando activamente en varias áreas clave para asegurar la equidad y el reconocimiento pleno. El gráfico representa de forma conceptual la importancia relativa de estas áreas de lucha y reivindicación en la actualidad.</p>
                        <ul class="list-disc list-inside space-y-2 text-gray-700">
                            <li><span class="font-bold">Visibilidad Cultural:</span> Promoción de eventos como las Llamadas y educación sobre el aporte afro.</li>
                            <li><span class="font-bold">Lucha Antirraci
