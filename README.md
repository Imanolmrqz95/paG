<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Para Mi Novia - Nuestro Cuaderno de Recuerdos</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts: Quicksand & Fredoka -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;500;600&family=Quicksand:wght@400;500;600;700&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        pastelPink: '#FFD1DC',
                        pastelDarkPink: '#FFB7C5',
                        pastelMint: '#C1E1C1',
                        pastelLavender: '#E6E6FA',
                        pastelYellow: '#FFFACD',
                        pastelBlue: '#BCEEFA',
                        pastelTeal: '#A8E6CF',
                        pastelGold: '#FEE180',
                        pastelCream: '#FFFDF9',
                        cuteGray: '#4A4E69'
                    },
                    fontFamily: {
                        fredoka: ['Fredoka', 'sans-serif'],
                        quicksand: ['Quicksand', 'sans-serif']
                    }
                }
            }
        }
    </script>

    <style>
        body {
            font-family: 'Quicksand', sans-serif;
            background-color: #FFFDF9;
            color: #4A4E69;
            background-image: radial-gradient(#FFD1DC 0.75px, transparent 0.75px), radial-gradient(#FFD1DC 0.75px, #FFFDF9 0.75px);
            background-size: 30px 30px;
            background-position: 0 0, 15px 15px;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #FFFDF9;
        }
        ::-webkit-scrollbar-thumb {
            background: #FFD1DC;
            border-radius: 10px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #FFB7C5;
        }

        /* Paper note effect */
        .paper-card {
            background: #FFFFFF;
            box-shadow: 0 8px 20px -6px rgba(255, 183, 197, 0.4), 0 4px 10px -4px rgba(74, 78, 105, 0.05);
            border: 2px solid #FFF0F3;
            transition: all 0.3s ease;
        }
        .paper-card:hover {
            transform: translateY(-4px);
            box-shadow: 0 12px 25px -6px rgba(255, 183, 197, 0.6);
        }

        /* Tape Effect */
        .washi-tape {
            position: absolute;
            top: -12px;
            left: 50%;
            transform: translateX(-50%) rotate(-1deg);
            width: 100px;
            height: 24px;
            background-color: rgba(255, 209, 220, 0.75);
            backdrop-filter: blur(2px);
            border-left: 2px dashed rgba(255, 255, 255, 0.6);
            border-right: 2px dashed rgba(255, 255, 255, 0.6);
            z-index: 10;
        }

        .washi-tape-mint {
            background-color: rgba(193, 225, 193, 0.75);
        }
        .washi-tape-lavender {
            background-color: rgba(230, 230, 250, 0.75);
        }

        /* Genshin / Miku Accent Badge */
        .genshin-badge {
            background: linear-gradient(135deg, #BCEEFA 0%, #E6E6FA 50%, #FFD1DC 100%);
        }

        /* Tab navigation active style */
        .tab-btn.active {
            background-color: #FFD1DC;
            color: #4A4E69;
            font-weight: 700;
        }

        /* Custom Animations */
        @keyframes floatSlow {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-8px) rotate(2deg); }
        }

        .animate-float {
            animation: floatSlow 4s ease-in-out infinite;
        }

        /* Hide sections easily */
        .page-section {
            display: none;
        }
        .page-section.active-page {
            display: block;
            animation: fadeIn 0.4s ease-in-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(8px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between">

    <!-- TOP DECORATIVE BAR -->
    <div class="h-3 w-full bg-gradient-to-r from-pastelPink via-pastelLavender to-pastelBlue"></div>

    <!-- HEADER / NAVIGATION -->
    <header class="sticky top-0 z-40 bg-pastelCream/90 backdrop-blur-md border-b border-pastelPink/40 px-4 py-3">
        <div class="max-w-5xl mx-auto flex justify-between items-center">
            <!-- Brand / Title -->
            <div class="flex items-center space-x-3 cursor-pointer" onclick="showPage('inicio')">
                <span class="text-2xl animate-float">🦋</span>
                <div>
                    <h1 class="font-fredoka text-xl sm:text-2xl text-cuteGray font-semibold tracking-wide flex items-center gap-2">
                        Nuestro Cuaderno 
                        <span class="text-xs bg-pastelPink text-cuteGray px-2 py-0.5 rounded-full font-sans">♥ Especial</span>
                    </h1>
                    <p class="text-xs text-cuteGray/70 font-medium">Dedicado con todo mi amor</p>
                </div>
            </div>

            <!-- Menu Button -->
            <button id="menu-toggle-btn" class="flex items-center space-x-2 bg-pastelPink/60 hover:bg-pastelPink px-4 py-2 rounded-2xl transition text-cuteGray font-medium text-sm border border-pastelDarkPink/30">
                <i class="fa-solid fa-bars text-base"></i>
                <span class="hidden sm:inline">Menú de Recuerdos</span>
            </button>
        </div>
    </header>

    <!-- SIDEBAR NAVIGATION MENU (OFF-CANVAS) -->
    <div id="side-menu-backdrop" class="fixed inset-0 bg-cuteGray/20 backdrop-blur-sm z-50 hidden opacity-0 transition-opacity duration-300"></div>
    
    <aside id="side-menu" class="fixed top-0 right-0 h-full w-80 max-w-[85vw] bg-pastelCream shadow-2xl z-50 transform translate-x-full transition-transform duration-300 border-l-2 border-pastelPink/50 p-6 flex flex-col justify-between">
        <div>
            <!-- Close Button -->
            <div class="flex justify-between items-center mb-8 border-b border-pastelPink/40 pb-4">
                <div class="flex items-center space-x-2">
                    <span class="text-xl">🐱</span>
                    <h2 class="font-fredoka text-lg text-cuteGray">Secciones del Cuaderno</h2>
                </div>
                <button id="menu-close-btn" class="w-8 h-8 rounded-full bg-pastelPink/40 hover:bg-pastelPink flex items-center justify-center text-cuteGray transition">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <!-- Menu Links -->
            <nav class="space-y-2">
                <button onclick="showPage('inicio'); toggleMenu();" class="w-full text-left px-4 py-3 rounded-xl hover:bg-pastelPink/50 transition flex items-center space-x-3 text-cuteGray font-medium">
                    <span class="text-lg">🏠</span>
                    <span>Inicio & Galería</span>
                </button>
                <button onclick="showPage('conocimos'); toggleMenu();" class="w-full text-left px-4 py-3 rounded-xl hover:bg-pastelLavender transition flex items-center space-x-3 text-cuteGray font-medium">
                    <span class="text-lg">✨</span>
                    <span>Cómo nos conocimos</span>
                </button>
                <button onclick="showPage('favoritos'); toggleMenu();" class="w-full text-left px-4 py-3 rounded-xl hover:bg-pastelBlue transition flex items-center space-x-3 text-cuteGray font-medium">
                    <span class="text-lg">🎮</span>
                    <span>Sus Cosas Favoritas</span>
                </button>
                <button onclick="showPage('comida'); toggleMenu();" class="w-full text-left px-4 py-3 rounded-xl hover:bg-pastelMint transition flex items-center space-x-3 text-cuteGray font-medium">
                    <span class="text-lg">🍉</span>
                    <span>Comida y Delicias</span>
                </button>
                <button onclick="showPage('mascotas'); toggleMenu();" class="w-full text-left px-4 py-3 rounded-xl hover:bg-pastelYellow transition flex items-center space-x-3 text-cuteGray font-medium">
                    <span class="text-lg">🦋</span>
                    <span>Gatos y Polillas</span>
                </button>
            </nav>
        </div>

        <!-- Sidebar Footer Cute Note -->
        <div class="bg-white/80 p-4 rounded-2xl border border-pastelPink/40 text-center">
            <p class="text-xs text-cuteGray/80 italic">"Cada pequeño detalle tuyo hace que mi mundo sea más bonito."</p>
            <div class="mt-2 text-sm text-pastelDarkPink">💖 🎀 🐾</div>
        </div>
    </aside>

    <!-- MAIN CONTENT CONTAINER -->
    <main class="max-w-4xl mx-auto px-4 py-8 flex-grow w-full">

        <!-- PAGE 1: INICIO & GALERÍA -->
        <section id="page-inicio" class="page-section active-page space-y-8">
            
            <!-- HERO WELCOME BANNER -->
            <div class="relative paper-card rounded-3xl p-6 sm:p-8 text-center overflow-hidden">
                <div class="washi-tape"></div>
                
                <!-- Cute subtle floating decorations -->
                <span class="absolute top-4 left-4 text-xl opacity-60 animate-float">🌸</span>
                <span class="absolute bottom-4 right-4 text-xl opacity-60 animate-float" style="animation-delay: 1s;">🍉</span>
                <span class="absolute top-6 right-8 text-xl opacity-60 animate-float" style="animation-delay: 2s;">🐾</span>
                
                <div class="inline-block px-3 py-1 bg-pastelLavender rounded-full text-xs font-semibold text-cuteGray mb-3">
                    ✨ Un espacio hecho para ti ✨
                </div>
                
                <h2 class="font-fredoka text-2xl sm:text-4xl text-cuteGray font-medium mb-3">
                    Para la persona más especial de mi vida
                </h2>
                
                <p class="text-sm sm:text-base text-cuteGray/80 max-w-xl mx-auto leading-relaxed">
                    Este es nuestro rinconcito digital. Un pequeño cuaderno donde guardo todo lo que me fascina de ti, tus gustos, tus detalles y nuestros momentos juntos.
                </p>

                <!-- Quick tags / cute badges -->
                <div class="flex flex-wrap justify-center gap-2 mt-5">
                    <span class="text-xs bg-pastelPink/70 px-3 py-1 rounded-full font-medium">🎀 Hello Kitty Vibes</span>
                    <span class="text-xs bg-pastelBlue/70 px-3 py-1 rounded-full font-medium">🩵 Genshin & Cosplay</span>
                    <span class="text-xs bg-pastelTeal/70 px-3 py-1 rounded-full font-medium">🍉 Lover de la Sandía</span>
                    <span class="text-xs bg-pastelYellow/70 px-3 py-1 rounded-full font-medium">🦋 Polillas Bonitas</span>
                </div>
            </div>

            <!-- PHOTO CAROUSEL / ROTATING FRAME SECTION -->
            <div class="paper-card rounded-3xl p-6 relative">
                <div class="washi-tape washi-tape-mint"></div>

                <div class="flex justify-between items-center mb-4">
                    <h3 class="font-fredoka text-lg text-cuteGray flex items-center gap-2">
                        <span>📸</span> Nuestros Momentos Favoritos
                    </h3>
                    <span class="text-xs text-cuteGray/60">Haz clic en las flechas para ver más</span>
                </div>

                <!-- Slider Container -->
                <div class="relative w-full aspect-[16/9] sm:aspect-[21/9] rounded-2xl overflow-hidden bg-pastelPink/20 border-2 border-pastelPink/30 flex items-center justify-center">
                    
                    <!-- Slide Item 1 -->
                    <div class="carousel-slide absolute inset-0 transition-opacity duration-500 opacity-100 flex flex-col items-center justify-center p-4 text-center bg-gradient-to-br from-pastelPink/30 to-pastelLavender/30">
                        <!-- Placeholder Image Box (Ready for user to replace) -->
                        <div class="w-full h-full rounded-xl flex flex-col items-center justify-center border-2 border-dashed border-pastelDarkPink/40 bg-white/60 p-4">
                            <i class="fa-regular fa-image text-4xl text-pastelDarkPink/60 mb-2"></i>
                            <p class="font-bold text-cuteGray text-sm sm:text-base">[ Espacio para foto nuestra #1 ]</p>
                            <p class="text-xs text-cuteGray/70 mt-1">Puedes reemplazar esta caja con un tag &lt;img src="tu-foto.jpg"&gt;</p>
                        </div>
                    </div>

                    <!-- Slide Item 2 -->
                    <div class="carousel-slide absolute inset-0 transition-opacity duration-500 opacity-0 flex flex-col items-center justify-center p-4 text-center bg-gradient-to-br from-pastelBlue/30 to-pastelTeal/30">
                        <div class="w-full h-full rounded-xl flex flex-col items-center justify-center border-2 border-dashed border-blue-300/60 bg-white/60 p-4">
                            <i class="fa-regular fa-image text-4xl text-blue-300/80 mb-2"></i>
                            <p class="font-bold text-cuteGray text-sm sm:text-base">[ Espacio para foto nuestra #2 ]</p>
                            <p class="text-xs text-cuteGray/70 mt-1">Un día especial juntos</p>
                        </div>
                    </div>

                    <!-- Slide Item 3 -->
                    <div class="carousel-slide absolute inset-0 transition-opacity duration-500 opacity-0 flex flex-col items-center justify-center p-4 text-center bg-gradient-to-br from-pastelYellow/30 to-pastelPink/30">
                        <div class="w-full h-full rounded-xl flex flex-col items-center justify-center border-2 border-dashed border-amber-300/60 bg-white/60 p-4">
                            <i class="fa-regular fa-image text-4xl text-amber-300/80 mb-2"></i>
                            <p class="font-bold text-cuteGray text-sm sm:text-base">[ Espacio para foto nuestra #3 ]</p>
                            <p class="text-xs text-cuteGray/70 mt-1">Nuestra cita preferida</p>
                        </div>
                    </div>

                    <!-- Carousel Controls -->
                    <button id="prev-slide" class="absolute left-3 w-9 h-9 rounded-full bg-white/80 hover:bg-white text-cuteGray flex items-center justify-center shadow-md transition">
                        <i class="fa-solid fa-chevron-left"></i>
                    </button>
                    <button id="next-slide" class="absolute right-3 w-9 h-9 rounded-full bg-white/80 hover:bg-white text-cuteGray flex items-center justify-center shadow-md transition">
                        <i class="fa-solid fa-chevron-right"></i>
                    </button>

                    <!-- Indicators -->
                    <div class="absolute bottom-3 flex space-x-1.5">
                        <span class="slide-indicator w-2.5 h-2.5 rounded-full bg-pastelDarkPink cursor-pointer"></span>
                        <span class="slide-indicator w-2.5 h-2.5 rounded-full bg-white/80 cursor-pointer"></span>
                        <span class="slide-indicator w-2.5 h-2.5 rounded-full bg-white/80 cursor-pointer"></span>
                    </div>
                </div>
            </div>

            <!-- DETALLES SOBRE ELLA (GRID SUMMARY) -->
            <div class="space-y-4">
                <h3 class="font-fredoka text-xl text-cuteGray flex items-center gap-2">
                    <span>⭐</span> Pequeños Detalles Que Te Hacen Única
                </h3>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <!-- Card: Gustos Personales -->
                    <div class="paper-card rounded-2xl p-5 border-l-4 border-l-pastelPink">
                        <div class="flex items-center space-x-3 mb-2">
                            <span class="p-2 bg-pastelPink/50 rounded-xl text-lg">🎀</span>
                            <h4 class="font-fredoka text-base text-cuteGray">Estética & Colores</h4>
                        </div>
                        <p class="text-xs sm:text-sm text-cuteGray/80 leading-relaxed">
                            Te encantan los tonos pastelosos, los detalles suaves, todo lo relacionado con Hello Kitty y esa ternura tan natural que transmites en todo lo que haces.
                        </p>
                    </div>

                    <!-- Card: Cosplay & Anime -->
                    <div class="paper-card rounded-2xl p-5 border-l-4 border-l-pastelBlue">
                        <div class="flex items-center space-x-3 mb-2">
                            <span class="p-2 bg-pastelBlue/50 rounded-xl text-lg">🎧</span>
                            <h4 class="font-fredoka text-base text-cuteGray">Cosplay & Vocaloid</h4>
                        </div>
                        <p class="text-xs sm:text-sm text-cuteGray/80 leading-relaxed">
                            Hacer cosplay es una de tus pasiones favoritas. Tienes una vibra genial inspirada en Miku y Kasane Teto, transformando cada proyecto en algo mágico.
                        </p>
                    </div>

                    <!-- Card: Genshin Impact -->
                    <div class="paper-card rounded-2xl p-5 border-l-4 border-l-pastelLavender">
                        <div class="flex items-center space-x-3 mb-2">
                            <span class="p-2 bg-pastelLavender rounded-xl text-lg">⚔️</span>
                            <h4 class="font-fredoka text-base text-cuteGray">Genshin Impact</h4>
                        </div>
                        <p class="text-xs sm:text-sm text-cuteGray/80 leading-relaxed">
                            Te encanta jugar Genshin Impact y la estética del juego. Tus personajes favoritos son <strong>Kaeya</strong> y <strong>Kaveh</strong>.
                        </p>
                    </div>

                    <!-- Card: Comidas Favoritas -->
                    <div class="paper-card rounded-2xl p-5 border-l-4 border-l-pastelTeal">
                        <div class="flex items-center space-x-3 mb-2">
                            <span class="p-2 bg-pastelTeal/50 rounded-xl text-lg">🍉</span>
                            <h4 class="font-fredoka text-base text-cuteGray">Comidas Favoritas</h4>
                        </div>
                        <p class="text-xs sm:text-sm text-cuteGray/80 leading-relaxed">
                            Adoras las sandías por sobre todas las cosas, además del sushi delicioso y cualquier plato de pasta.
                        </p>
                    </div>
                </div>
            </div>

            <!-- CUADERNO DE NOTAS INTERACTIVO -->
            <div class="paper-card rounded-3xl p-6">
                <h3 class="font-fredoka text-lg text-cuteGray mb-4 flex items-center gap-2">
                    <span>📝</span> Notitas Afectivas para Ti
                </h3>

                <div class="space-y-3">
                    <details class="group bg-pastelCream p-4 rounded-2xl border border-pastelPink/40 transition">
                        <summary class="font-medium text-sm text-cuteGray cursor-pointer flex justify-between items-center list-none">
                            <span class="flex items-center gap-2"><span>🧸</span> Tu ternura infinita</span>
                            <span class="text-xs text-pastelDarkPink group-open:rotate-180 transition-transform">▼</span>
                        </summary>
                        <p class="text-xs sm:text-sm text-cuteGray/80 mt-3 pt-2 border-t border-pastelPink/30 leading-relaxed">
                            Me encanta lo dulce que eres en todo momento. Tus manos pequeñas, la forma en que me abrazas y tu manera tan suave de tocarme hacen que me sienta en paz y completamente feliz.
                        </p>
                    </details>

                    <details class="group bg-pastelCream p-4 rounded-2xl border border-pastelLavender/60 transition">
                        <summary class="font-medium text-sm text-cuteGray cursor-pointer flex justify-between items-center list-none">
                            <span class="flex items-center gap-2"><span>✨</span> Lo bonita que eres</span>
                            <span class="text-xs text-pastelDarkPink group-open:rotate-180 transition-transform">▼</span>
                        </summary>
                        <p class="text-xs sm:text-sm text-cuteGray/80 mt-3 pt-2 border-t border-pastelLavender/50 leading-relaxed">
                            Amo cada rasgo tuyo, tu figura natural, tu dulzura y lo auténtica que te muestras conmigo. Todo en ti me resulta perfecto y hermoso.
                        </p>
                    </details>

                    <details class="group bg-pastelCream p-4 rounded-2xl border border-pastelMint/60 transition">
                        <summary class="font-medium text-sm text-cuteGray cursor-pointer flex justify-between items-center list-none">
                            <span class="flex items-center gap-2"><span>🌱</span> Mi lugar seguro</span>
                            <span class="text-xs text-pastelDarkPink group-open:rotate-180 transition-transform">▼</span>
                        </summary>
                        <p class="text-xs sm:text-sm text-cuteGray/80 mt-3 pt-2 border-t border-pastelMint/50 leading-relaxed">
                            Solo acostarme a tu lado, abrazarte y sentir tu calidez es de mis momentos favoritos del día. No hace falta nada más para estar feliz.
                        </p>
                    </details>
                </div>
            </div>

        </section>

        <!-- PAGE 2: CÓMO NOS CONOCIMOS -->
        <section id="page-conocimos" class="page-section space-y-6">
            <div class="paper-card rounded-3xl p-6 sm:p-8 relative">
                <div class="washi-tape washi-tape-lavender"></div>

                <div class="text-center mb-8">
                    <span class="text-3xl">💌</span>
                    <h2 class="font-fredoka text-2xl sm:text-3xl text-cuteGray mt-2">Nuestra Historia de Amor</h2>
                    <p class="text-xs sm:text-sm text-cuteGray/70 mt-1">El comienzo de algo maravilloso que cuidamos todos los días.</p>
                </div>

                <!-- TIMELINE -->
                <div class="relative border-l-2 border-pastelPink/60 ml-4 sm:ml-8 space-y-8 my-6">
                    
                    <!-- Event 1 -->
                    <div class="relative pl-6 sm:pl-8">
                        <span class="absolute -left-[13px] top-1 w-6 h-6 rounded-full bg-pastelPink border-2 border-white flex items-center justify-center text-xs">✨</span>
                        <div class="bg-pastelCream p-4 rounded-2xl border border-pastelPink/40">
                            <span class="text-xs font-semibold text-pastelDarkPink bg-white px-2 py-0.5 rounded-full border border-pastelPink/30">Fecha especial</span>
                            <h3 class="font-fredoka text-base text-cuteGray mt-2">El Día que Nos Conocimos</h3>
                            <p class="text-xs sm:text-sm text-cuteGray/80 mt-2 leading-relaxed">
                                [ Escribe aquí la historia de cómo se conocieron por primera vez. Puedes mencionar dónde fue, qué sintieron o el primer detalle que te llamó la atención de ella. ]
                            </p>
                        </div>
                    </div>

                    <!-- Event 2 -->
                    <div class="relative pl-6 sm:pl-8">
                        <span class="absolute -left-[13px] top-1 w-6 h-6 rounded-full bg-pastelLavender border-2 border-white flex items-center justify-center text-xs">💬</span>
                        <div class="bg-pastelCream p-4 rounded-2xl border border-pastelLavender/60">
                            <span class="text-xs font-semibold text-purple-400 bg-white px-2 py-0.5 rounded-full border border-pastelLavender">Nuestra primera conversación</span>
                            <h3 class="font-fredoka text-base text-cuteGray mt-2">Horas Hablando Sin Parar</h3>
                            <p class="text-xs sm:text-sm text-cuteGray/80 mt-2 leading-relaxed">
                                [ Agrega detalles sobre sus primeras pláticas, risas compartidas o temas en común que los unieron. ]
                            </p>
                        </div>
                    </div>

                    <!-- Event 3 -->
                    <div class="relative pl-6 sm:pl-8">
                        <span class="absolute -left-[13px] top-1 w-6 h-6 rounded-full bg-pastelBlue border-2 border-white flex items-center justify-center text-xs">❤️</span>
                        <div class="bg-pastelCream p-4 rounded-2xl border border-pastelBlue">
                            <span class="text-xs font-semibold text-blue-400 bg-white px-2 py-0.5 rounded-full border border-pastelBlue">Paso a paso</span>
                            <h3 class="font-fredoka text-base text-cuteGray mt-2">Nuestra Primera Cita</h3>
                            <p class="text-xs sm:text-sm text-cuteGray/80 mt-2 leading-relaxed">
                                [ Agrega recuerdos de la primera vez que salieron como novios o ese momento mágico que nunca vas a olvidar. ]
                            </p>
                        </div>
                    </div>

                </div>

                <div class="text-center pt-4 border-t border-pastelPink/30">
                    <p class="text-xs text-cuteGray/70 italic">"De todos los momentos de la vida, haberte conocido es mi favorito."</p>
                </div>
            </div>
        </section>

        <!-- PAGE 3: SUS COSAS FAVORITAS (Genshin, Cosplay, Vocaloid) -->
        <section id="page-favoritos" class="page-section space-y-6">
            <div class="paper-card rounded-3xl p-6 sm:p-8">
                <div class="text-center mb-6">
                    <span class="text-3xl">🎮</span>
                    <h2 class="font-fredoka text-2xl text-cuteGray mt-2">Sus Grandes Pasiones</h2>
                    <p class="text-xs sm:text-sm text-cuteGray/70">Todo lo que le encanta crear y jugar</p>
                </div>

                <!-- Genshin Section -->
                <div class="bg-gradient-to-r from-pastelBlue/30 via-pastelLavender/30 to-pastelPink/30 p-5 rounded-2xl border border-pastelBlue/40 mb-6">
                    <div class="flex items-center space-x-3 mb-3">
                        <span class="text-2xl">⚔️</span>
                        <div>
                            <h3 class="font-fredoka text-lg text-cuteGray">Genshin Impact World</h3>
                            <p class="text-xs text-cuteGray/70">Mundo mágico & estética favorita</p>
                        </div>
                    </div>
                    <p class="text-xs sm:text-sm text-cuteGray/80 leading-relaxed mb-4">
                        Le encanta el universo de Genshin Impact, su música y sus diseños. De este juego proviene gran parte de su inspiración estética y de cosplay.
                    </p>

                    <!-- Characters -->
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                        <div class="bg-white/80 p-3 rounded-xl border border-pastelBlue/60 flex items-center space-x-3">
                            <span class="text-2xl">❄️</span>
                            <div>
                                <h4 class="font-fredoka text-sm text-cuteGray">Kaeya</h4>
                                <p class="text-xs text-cuteGray/70">Personaje Favorito</p>
                            </div>
                        </div>

                        <div class="bg-white/80 p-3 rounded-xl border border-pastelGold/60 flex items-center space-x-3">
                            <span class="text-2xl">🏛️</span>
                            <div>
                                <h4 class="font-fredoka text-sm text-cuteGray">Kaveh</h4>
                                <p class="text-xs text-cuteGray/70">Personaje Favorito</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Cosplay & Vocaloid Grid -->
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <div class="bg-pastelTeal/20 p-5 rounded-2xl border border-pastelTeal/40">
                        <div class="flex items-center space-x-2 mb-2">
                            <span class="text-xl">👗</span>
                            <h3 class="font-fredoka text-base text-cuteGray">El Arte del Cosplay</h3>
                        </div>
                        <p class="text-xs sm:text-sm text-cuteGray/80 leading-relaxed">
                            Hacer cosplay es una de sus actividades favoritas. Adoro ver su creatividad, dedicación y lo increíblemente bonita que se ve en cada traje.
                        </p>
                    </div>

                    <div class="bg-pastelPink/20 p-5 rounded-2xl border border-pastelPink/40">
                        <div class="flex items-center space-x-2 mb-2">
                            <span class="text-xl">🎶</span>
                            <h3 class="font-fredoka text-base text-cuteGray">Miku & Kasane Teto</h3>
                        </div>
                        <p class="text-xs sm:text-sm text-cuteGray/80 leading-relaxed">
                            Le encanta el universo Vocaloid / SynthV, especialmente Hatsune Miku y Kasane Teto, llenas de color y buena música.
                        </p>
                    </div>
                </div>
            </div>
        </section>

        <!-- PAGE 4: COMIDA Y DELICIAS -->
        <section id="page-comida" class="page-section space-y-6">
            <div class="paper-card rounded-3xl p-6 sm:p-8">
                <div class="text-center mb-6">
                    <span class="text-3xl">🍉</span>
                    <h2 class="font-fredoka text-2xl text-cuteGray mt-2">Sus Antojos & Comidas Favoritas</h2>
                    <p class="text-xs sm:text-sm text-cuteGray/70">Los platillos que siempre le sacan una sonrisa</p>
                </div>

                <div class="space-y-4">
                    <!-- Sandía Highlight -->
                    <div class="bg-pastelPink/30 p-5 rounded-2xl border-2 border-pastelPink flex flex-col sm:flex-row items-center gap-4">
                        <div class="text-5xl animate-float">🍉</div>
                        <div class="text-center sm:text-left">
                            <div class="inline-block px-2 py-0.5 bg-pastelDarkPink text-white text-[10px] font-bold rounded-full mb-1">
                                ¡SU FAVORITA NÚMERO 1!
                            </div>
                            <h3 class="font-fredoka text-lg text-cuteGray">La Sandía</h3>
                            <p class="text-xs sm:text-sm text-cuteGray/80 mt-1 leading-relaxed">
                                Le fascinan las sandías. Se come cualquiera y es sin duda una de sus frutas y alimentos preferidos en todo el mundo.
                            </p>
                        </div>
                    </div>

                    <!-- Sushi & Pasta Grid -->
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <div class="bg-pastelCream p-5 rounded-2xl border border-pastelTeal/60 flex items-start space-x-3">
                            <span class="text-3xl">🍣</span>
                            <div>
                                <h3 class="font-fredoka text-base text-cuteGray">Sushi</h3>
                                <p class="text-xs text-cuteGray/80 mt-1">
                                    Le encanta comer sushi en cualquier momento. ¡Nuestras citas para comer sushi siempre son geniales!
                                </p>
                            </div>
                        </div>

                        <div class="bg-pastelCream p-5 rounded-2xl border border-pastelYellow/80 flex items-start space-x-3">
                            <span class="text-3xl">🍝</span>
                            <div>
                                <h3 class="font-fredoka text-base text-cuteGray">Pastas</h3>
                                <p class="text-xs text-cuteGray/80 mt-1">
                                    Cualquier tipo de pasta le encanta. Es de sus platillos reconfortantes preferidos.
                                </p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- PAGE 5: GATOS Y POLILLAS -->
        <section id="page-mascotas" class="page-section space-y-6">
            <div class="paper-card rounded-3xl p-6 sm:p-8">
                <div class="text-center mb-6">
                    <span class="text-3xl">🦋</span>
                    <h2 class="font-fredoka text-2xl text-cuteGray mt-2">Naturaleza & Animalitos</h2>
                    <p class="text-xs sm:text-sm text-cuteGray/70">Los detalles tiernos que le llaman la atención</p>
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                    <!-- Polillas -->
                    <div class="bg-pastelLavender/30 p-5 rounded-2xl border border-pastelLavender/80 relative overflow-hidden">
                        <span class="absolute top-2 right-2 text-2xl opacity-40">✨</span>
                        <div class="flex items-center space-x-3 mb-3">
                            <span class="text-3xl">🦋</span>
                            <h3 class="font-fredoka text-lg text-cuteGray">Polillas Bonitas</h3>
                        </div>
                        <p class="text-xs sm:text-sm text-cuteGray/80 leading-relaxed">
                            A diferencia de mucha gente, a ella le encantan las polillas. Le parecen criaturas muy bonitas, suaves y con alas hermosas.
                        </p>
                    </div>

                    <!-- Gatos -->
                    <div class="bg-pastelYellow/30 p-5 rounded-2xl border border-pastelYellow/80 relative overflow-hidden">
                        <span class="absolute top-2 right-2 text-2xl opacity-40">🐾</span>
                        <div class="flex items-center space-x-3 mb-3">
                            <span class="text-3xl">🐱</span>
                            <h3 class="font-fredoka text-lg text-cuteGray">Sus Gatos</h3>
                        </div>
                        <p class="text-xs sm:text-sm text-cuteGray/80 leading-relaxed">
                            Tiene varios gatitos que le alegran sus días. Su amor por los animales y la forma en que los cuida demuestra el corazón tan lindo que tiene.
                        </p>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- FOOTER -->
    <footer class="bg-pastelCream border-t border-pastelPink/30 py-6 text-center text-xs text-cuteGray/70">
        <div class="max-w-4xl mx-auto px-4 space-y-2">
            <p class="font-fredoka text-sm text-cuteGray">Hecho con todo mi amor para ti ❤️</p>
            <p>Un pequeño recordatorio de lo mucho que te amo y me gustas tal como eres.</p>
        </div>
    </footer>

    <!-- JAVASCRIPT LOGIC -->
    <script>
        // MENU SLIDE TOGGLE
        const sideMenu = document.getElementById('side-menu');
        const backdrop = document.getElementById('side-menu-backdrop');
        const menuToggleBtn = document.getElementById('menu-toggle-btn');
        const menuCloseBtn = document.getElementById('menu-close-btn');

        function toggleMenu() {
            const isHidden = sideMenu.classList.contains('translate-x-full');
            if (isHidden) {
                sideMenu.classList.remove('translate-x-full');
                backdrop.classList.remove('hidden');
                setTimeout(() => backdrop.classList.remove('opacity-0'), 10);
            } else {
                sideMenu.classList.add('translate-x-full');
                backdrop.classList.add('opacity-0');
                setTimeout(() => backdrop.classList.add('hidden'), 300);
            }
        }

        menuToggleBtn.addEventListener('click', toggleMenu);
        menuCloseBtn.addEventListener('click', toggleMenu);
        backdrop.addEventListener('click', toggleMenu);

        // PAGE NAVIGATION LOGIC
        function showPage(pageId) {
            // Hide all pages
            const pages = document.querySelectorAll('.page-section');
            pages.forEach(page => page.classList.remove('active-page'));

            // Show selected page
            const targetPage = document.getElementById(`page-${pageId}`);
            if (targetPage) {
                targetPage.classList.add('active-page');
            }

            // Scroll smoothly to top
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // CAROUSEL SLIDER LOGIC
        const slides = document.querySelectorAll('.carousel-slide');
        const indicators = document.querySelectorAll('.slide-indicator');
        const prevBtn = document.getElementById('prev-slide');
        const nextBtn = document.getElementById('next-slide');
        let currentSlide = 0;

        function updateSlide(index) {
            slides.forEach((slide, i) => {
                if (i === index) {
                    slide.classList.remove('opacity-0');
                    slide.classList.add('opacity-100');
                } else {
                    slide.classList.remove('opacity-100');
                    slide.classList.add('opacity-0');
                }
            });

            indicators.forEach((ind, i) => {
                if (i === index) {
                    ind.classList.remove('bg-white/80');
                    ind.classList.add('bg-pastelDarkPink');
                } else {
                    ind.classList.remove('bg-pastelDarkPink');
                    ind.classList.add('bg-white/80');
                }
            });

            currentSlide = index;
        }

        if (nextBtn && prevBtn) {
            nextBtn.addEventListener('click', () => {
                let next = (currentSlide + 1) % slides.length;
                updateSlide(next);
            });

            prevBtn.addEventListener('click', () => {
                let prev = (currentSlide - 1 + slides.length) % slides.length;
                updateSlide(prev);
            });

            indicators.forEach((ind, index) => {
                ind.addEventListener('click', () => updateSlide(index));
            });

            // Auto-rotate every 5 seconds
            setInterval(() => {
                let next = (currentSlide + 1) % slides.length;
                updateSlide(next);
            }, 5000);
        }
    </script>
</body>
</html>
