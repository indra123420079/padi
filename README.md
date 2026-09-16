<!DOCTYPE html>
<html lang="id" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AgroGogo - Panduan & Pengenalan Padi Gogo Interaktif</title>

    <!-- Google Fonts: Plus Jakarta Sans -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">

    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#f0fdf4',
                            100: '#dcfce7',
                            500: '#22c55e',
                            600: '#16a34a',
                            700: '#15803d',
                            800: '#166534',
                            900: '#14532d',
                        },
                        amberGold: {
                            400: '#fbbf24',
                            500: '#f59e0b',
                            600: '#d97706',
                        }
                    },
                    fontFamily: {
                        sans: ['Plus Jakarta Sans', 'sans-serif'],
                    }
                }
            }
        }
    </script>

    <!-- Chart.js CDN -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <style>
        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #10b981;
            border-radius: 4px;
        }
        .glass-nav {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(12px);
        }
        .hero-pattern {
            background-color: #f0fdf4;
            background-image: radial-gradient(#16a34a 0.75px, transparent 0.75px), radial-gradient(#16a34a 0.75px, #f0fdf4 0.75px);
            background-size: 30px 30px;
            background-position: 0 0,15px 15px;
            background-opacity: 0.1;
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 font-sans antialiased selection:bg-brand-500 selection:text-white">

    <!-- Toast Container -->
    <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 max-w-sm w-full pointer-events-none"></div>

    <!-- Navigation Bar -->
    <header class="fixed top-0 left-0 right-0 z-40 glass-nav border-b border-emerald-100/80 transition-all duration-300">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-20">
                <!-- Logo -->
                <a href="#" class="flex items-center gap-3 group">
                    <div class="w-11 h-11 rounded-2xl bg-gradient-to-tr from-brand-700 to-amberGold-500 flex items-center justify-center text-white shadow-lg shadow-brand-600/20 group-hover:scale-105 transition-transform">
                        <i class="fa-solid font-bold fa-wheat-awn text-xl"></i>
                    </div>
                    <div>
                        <span class="text-xl font-extrabold tracking-tight bg-gradient-to-r from-brand-800 to-amberGold-600 bg-clip-text text-transparent">AgroGogo</span>
                        <span class="block text-[10px] font-semibold uppercase tracking-widest text-emerald-600 -mt-1">Inovasi Padi Lahan Kering</span>
                    </div>
                </a>

                <!-- Desktop Menu -->
                <nav class="hidden md:flex items-center space-x-1 lg:space-x-2 font-medium text-sm text-slate-600">
                    <a href="#pengenalan" class="px-3 py-2 rounded-xl hover:text-brand-600 hover:bg-brand-50 transition-colors">Pengenalan</a>
                    <a href="#komparasi" class="px-3 py-2 rounded-xl hover:text-brand-600 hover:bg-brand-50 transition-colors">Komparasi</a>
                    <a href="#varietas" class="px-3 py-2 rounded-xl hover:text-brand-600 hover:bg-brand-50 transition-colors">Varietas Unggul</a>
                    <a href="#budidaya" class="px-3 py-2 rounded-xl hover:text-brand-600 hover:bg-brand-50 transition-colors">Panduan Budidaya</a>
                    <a href="#kalkulator" class="px-3 py-2 rounded-xl hover:text-brand-600 hover:bg-brand-50 transition-colors">Kalkulator Tani</a>
                    <a href="#kuis" class="px-3 py-2 rounded-xl hover:text-brand-600 hover:bg-brand-50 transition-colors">Kuis Edukasi</a>
                </nav>

                <!-- Header Actions -->
                <div class="hidden sm:flex items-center gap-3">
                    <a href="#kalkulator" class="px-4 py-2.5 rounded-xl bg-brand-600 text-white font-semibold text-sm hover:bg-brand-700 shadow-md shadow-brand-600/20 transition-all flex items-center gap-2">
                        <i class="fa-solid fa-calculator"></i>
                        <span>Hitung Kebutuhan</span>
                    </a>
                </div>

                <!-- Mobile Menu Button -->
                <div class="md:hidden">
                    <button id="mobile-menu-btn" type="button" class="p-2.5 rounded-xl text-slate-600 hover:bg-slate-100 focus:outline-none" aria-label="Menu Toggle">
                        <i class="fa-solid fa-bars text-xl"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- Mobile Drawer Menu -->
        <div id="mobile-menu" class="hidden md:hidden border-b border-slate-200 bg-white/95 backdrop-blur-md px-4 pt-2 pb-6 space-y-2">
            <a href="#pengenalan" class="mobile-nav-link block px-4 py-2.5 rounded-xl text-slate-700 hover:bg-brand-50 hover:text-brand-600 font-medium">Pengenalan</a>
            <a href="#komparasi" class="mobile-nav-link block px-4 py-2.5 rounded-xl text-slate-700 hover:bg-brand-50 hover:text-brand-600 font-medium">Komparasi</a>
            <a href="#varietas" class="mobile-nav-link block px-4 py-2.5 rounded-xl text-slate-700 hover:bg-brand-50 hover:text-brand-600 font-medium">Varietas Unggul</a>
            <a href="#budidaya" class="mobile-nav-link block px-4 py-2.5 rounded-xl text-slate-700 hover:bg-brand-50 hover:text-brand-600 font-medium">Panduan Budidaya</a>
            <a href="#kalkulator" class="mobile-nav-link block px-4 py-2.5 rounded-xl text-slate-700 hover:bg-brand-50 hover:text-brand-600 font-medium">Kalkulator Tani</a>
            <a href="#kuis" class="mobile-nav-link block px-4 py-2.5 rounded-xl text-slate-700 hover:bg-brand-50 hover:text-brand-600 font-medium">Kuis Edukasi</a>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="relative pt-32 pb-20 md:pt-40 md:pb-28 overflow-hidden hero-pattern">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-center">
                
                <!-- Hero Text -->
                <div class="lg:col-span-7 space-y-6 text-center lg:text-left">
                    <div class="inline-flex items-center gap-2 px-3.5 py-1.5 rounded-full bg-brand-100 border border-brand-200 text-brand-800 text-xs font-semibold shadow-sm">
                        <span class="flex h-2 w-2 rounded-full bg-brand-500 animate-pulse"></span>
                        Solusi Ketahanan Pangan & Perubahan Iklim
                    </div>

                    <h1 class="text-4xl sm:text-5xl lg:text-6xl font-extrabold text-slate-900 leading-tight tracking-tight">
                        Mengenal <span class="bg-gradient-to-r from-brand-600 to-amberGold-500 bg-clip-text text-transparent">Padi Gogo</span>: Beras Berkualitas dari Lahan Kering
                    </h1>

                    <p class="text-base sm:text-lg text-slate-600 leading-relaxed max-w-2xl mx-auto lg:mx-0">
                        Padi Gogo adalah sistem budidaya padi tanpa perlu penggenangan air kontinu. Tumbuh optimal di lahan ladang, lereng, dan wilayah curah hujan terbatas untuk mewujudkan kedaulatan pangan nasional.
                    </p>

                    <div class="flex flex-col sm:flex-row items-center justify-center lg:justify-start gap-4 pt-2">
                        <a href="#pengenalan" class="w-full sm:w-auto px-6 py-3.5 rounded-xl bg-brand-600 hover:bg-brand-700 text-white font-bold text-base shadow-lg shadow-brand-600/30 transition-all flex items-center justify-center gap-2">
                            <span>Mulai Eksplorasi</span>
                            <i class="fa-solid fa-arrow-right"></i>
                        </a>
                        <a href="#kalkulator" class="w-full sm:w-auto px-6 py-3.5 rounded-xl bg-white hover:bg-slate-100 text-slate-700 font-semibold border border-slate-200 text-base shadow-sm transition-all flex items-center justify-center gap-2">
                            <i class="fa-solid fa-calculator text-brand-600"></i>
                            <span>Simulasi Kebutuhan Tanam</span>
                        </a>
                    </div>

                    <!-- Highlight Badges -->
                    <div class="pt-6 grid grid-cols-3 gap-4 border-t border-slate-200/80">
                        <div class="text-center lg:text-left">
                            <p class="text-2xl sm:text-3xl font-extrabold text-brand-700">60-70%</p>
                            <p class="text-xs sm:text-sm text-slate-500 font-medium">Hemat Penggunaan Air</p>
                        </div>
                        <div class="text-center lg:text-left">
                            <p class="text-2xl sm:text-3xl font-extrabold text-amberGold-600">4-7 Ton</p>
                            <p class="text-xs sm:text-sm text-slate-500 font-medium">Potensi Panen / Ha</p>
                        </div>
                        <div class="text-center lg:text-left">
                            <p class="text-2xl sm:text-3xl font-extrabold text-brand-700">100%</p>
                            <p class="text-xs sm:text-sm text-slate-500 font-medium">Adaptif Lahan Kering</p>
                        </div>
                    </div>
                </div>

                <!-- Hero Interactive Visual Card -->
                <div class="lg:col-span-5">
                    <div class="relative mx-auto max-w-md lg:max-w-none">
                        <!-- Background Glow -->
                        <div class="absolute -inset-1.5 bg-gradient-to-r from-brand-500 to-amberGold-500 rounded-3xl blur-xl opacity-30 animate-pulse"></div>
                        
                        <div class="relative rounded-3xl bg-white p-6 sm:p-8 shadow-xl border border-emerald-100/80 space-y-6">
                            <div class="flex items-center justify-between border-b border-slate-100 pb-4">
                                <div class="flex items-center gap-3">
                                    <div class="w-10 h-10 rounded-xl bg-amber-100 text-amber-700 flex items-center justify-center">
                                        <i class="fa-solid fa-sun text-lg"></i>
                                    </div>
                                    <div>
                                        <h3 class="font-bold text-slate-800 text-sm">Status Ketahanan Iklim</h3>
                                        <p class="text-xs text-slate-500">Kondisi Lahan Kering & Rainfed</p>
                                    </div>
                                </div>
                                <span class="px-2.5 py-1 rounded-full text-xs font-semibold bg-emerald-100 text-emerald-800">Sangat Tangguh</span>
                            </div>

                            <!-- Feature list in card -->
                            <div class="space-y-4">
                                <div class="p-3.5 rounded-2xl bg-slate-50 border border-slate-100 flex items-start gap-3">
                                    <i class="fa-solid fa-droplet-slash text-brand-600 text-lg mt-0.5"></i>
                                    <div>
                                        <h4 class="text-sm font-bold text-slate-800">Efisiensi Pasokan Air</h4>
                                        <p class="text-xs text-slate-600">Tidak memerlukan air tergenang, hanya mengandalkan curah hujan atau penyiraman terbatas.</p>
                                    </div>
                                </div>

                                <div class="p-3.5 rounded-2xl bg-slate-50 border border-slate-100 flex items-start gap-3">
                                    <i class="fa-solid fa-plant-wilt text-amberGold-600 text-lg mt-0.5"></i>
                                    <div>
                                        <h4 class="text-sm font-bold text-slate-800">Toleran Penyakit Blast</h4>
                                        <p class="text-xs text-slate-600">Varietas Inpago dirancang memiliki ketahanan tinggi terhadap jamur *Pyricularia oryzae*.</p>
                                    </div>
                                </div>

                                <div class="p-3.5 rounded-2xl bg-slate-50 border border-slate-100 flex items-start gap-3">
                                    <i class="fa-solid fa-layer-group text-brand-600 text-lg mt-0.5"></i>
                                    <div>
                                        <h4 class="text-sm font-bold text-slate-800">Fleksibilitas Tumpangsari</h4>
                                        <p class="text-xs text-slate-600">Dapat ditanam bersama tanaman jagung, kedelai, atau di antara tanaman perkebunan muda.</p>
                                    </div>
                                </div>
                            </div>

                            <div class="pt-2">
                                <a href="#varietas" class="w-full py-3 rounded-xl bg-emerald-50 text-brand-700 hover:bg-emerald-100 font-bold text-sm transition-colors flex items-center justify-center gap-2">
                                    <i class="fa-solid fa-seedling"></i>
                                    <span>Lihat Katalog Varietas Inpago</span>
                                </a>
                            </div>
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </section>

    <!-- Pengenalan Section -->
    <section id="pengenalan" class="py-20 bg-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center max-w-3xl mx-auto mb-16 space-y-3">
                <span class="text-xs font-extrabold uppercase tracking-widest text-brand-600">Pemahaman Dasar</span>
                <h2 class="text-3xl sm:text-4xl font-extrabold text-slate-900">Apa itu Padi Gogo?</h2>
                <p class="text-slate-600 text-base sm:text-lg">
                    Padi Gogo (Upland Rice) merupakan jenis tanaman padi yang dibudidayakan pada lahan kering (tegalan atau ladang) tanpa penggenangan air permanen seperti padi sawah irigasi.
                </p>
            </div>

            <!-- Key Features Grid -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <!-- Card 1 -->
                <div class="p-8 rounded-3xl bg-slate-50 border border-slate-100 hover:border-brand-200 hover:shadow-xl transition-all group">
                    <div class="w-14 h-14 rounded-2xl bg-brand-100 text-brand-700 flex items-center justify-center text-2xl mb-6 group-hover:scale-110 transition-transform">
                        <i class="fa-solid fa-cloud-sun-rain"></i>
                    </div>
                    <h3 class="text-xl font-bold text-slate-900 mb-3">Toleransi Kekeringan</h3>
                    <p class="text-slate-600 text-sm leading-relaxed">
                        Sistem perakaran padi gogo cenderung lebih dalam dibandingkan padi sawah biasa, memungkinkannya menyerap kelembapan alami tanah saat musim kemarau atau curah hujan rendah.
                    </p>
                </div>

                <!-- Card 2 -->
                <div class="p-8 rounded-3xl bg-slate-50 border border-slate-100 hover:border-brand-200 hover:shadow-xl transition-all group">
                    <div class="w-14 h-14 rounded-2xl bg-amber-100 text-amberGold-600 flex items-center justify-center text-2xl mb-6 group-hover:scale-110 transition-transform">
                        <i class="fa-solid fa-mountain"></i>
                    </div>
                    <h3 class="text-xl font-bold text-slate-900 mb-3">Pemanfaatan Lahan Marginal</h3>
                    <p class="text-slate-600 text-sm leading-relaxed">
                        Sangat cocok ditanam di perbukitan, tanah masam (podsolik merah kuning), kawasan tumpang sari hutan, maupun lahan perkebunan rejuvenasi.
                    </p>
                </div>

                <!-- Card 3 -->
                <div class="p-8 rounded-3xl bg-slate-50 border border-slate-100 hover:border-brand-200 hover:shadow-xl transition-all group">
                    <div class="w-14 h-14 rounded-2xl bg-emerald-100 text-emerald-700 flex items-center justify-center text-2xl mb-6 group-hover:scale-110 transition-transform">
                        <i class="fa-solid fa-coins"></i>
                    </div>
                    <h3 class="text-xl font-bold text-slate-900 mb-3">Efisiensi Biaya Irigasi</h3>
                    <p class="text-slate-600 text-sm leading-relaxed">
                        Mengurangi pengeluaran operasional pembuatan galengan, pompa air berdaya tinggi, dan pengelolaan saluran irigasi yang rumit.
                    </p>
                </div>
            </div>
        </div>
    </section>

    <!-- Komparasi Section (Padi Gogo vs Padi Sawah) -->
    <section id="komparasi" class="py-20 bg-slate-50 border-y border-slate-200/60">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-center">
                
                <!-- Left Info -->
                <div class="lg:col-span-5 space-y-6">
                    <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-amber-100 text-amberGold-600 text-xs font-extrabold uppercase tracking-wider">
                        Komparasi Teknis
                    </div>
                    <h2 class="text-3xl sm:text-4xl font-extrabold text-slate-900 leading-tight">
                        Padi Gogo vs Padi Sawah Irigasi
                    </h2>
                    <p class="text-slate-600 text-base leading-relaxed">
                        Meskipun padi sawah memiliki potensi hasil yang sangat tinggi di lahan tergenang, Padi Gogo menjadi pilihan paling rasional dan efisien untuk lahan tegalan dan antisipasi fenomena El Niño.
                    </p>

                    <!-- Feature Check Matrix -->
                    <div class="space-y-3 pt-2">
                        <div class="p-3.5 rounded-xl bg-white border border-slate-200 flex items-center justify-between text-sm">
                            <span class="font-semibold text-slate-700"><i class="fa-solid fa-faucet-drip text-emerald-600 mr-2"></i>Kebutuhan Air (L/kg beras)</span>
                            <span class="font-bold text-slate-900">~1.500 L (Gogo) vs ~4.000 L (Sawah)</span>
                        </div>
                        <div class="p-3.5 rounded-xl bg-white border border-slate-200 flex items-center justify-between text-sm">
                            <span class="font-semibold text-slate-700"><i class="fa-solid fa-disease text-amber-500 mr-2"></i>Toleransi Jamur Blast</span>
                            <span class="font-bold text-emerald-700">Tinggi (Varietas Inpago)</span>
                        </div>
                        <div class="p-3.5 rounded-xl bg-white border border-slate-200 flex items-center justify-between text-sm">
                            <span class="font-semibold text-slate-700"><i class="fa-solid fa-seedling text-brand-600 mr-2"></i>Metode Penanaman</span>
                            <span class="font-bold text-slate-900">Tugal / Alur (Direct Seeding)</span>
                        </div>
                    </div>
                </div>

                <!-- Right Chart Container -->
                <div class="lg:col-span-7 bg-white p-6 sm:p-8 rounded-3xl shadow-lg border border-slate-200/80">
                    <div class="flex items-center justify-between mb-6">
                        <div>
                            <h3 class="text-lg font-bold text-slate-900">Grafik Perbandingan Efisiensi Sumber Daya</h3>
                            <p class="text-xs text-slate-500">Estimasi penggunaan air & input operasional per Hektar</p>
                        </div>
                        <span class="text-xs bg-slate-100 text-slate-600 font-semibold px-2.5 py-1 rounded-lg">Chart Visual</span>
                    </div>

                    <div class="relative h-72 sm:h-80 w-full">
                        <canvas id="comparisonChart"></canvas>
                    </div>
                </div>

            </div>
        </div>
    </section>

    <!-- Katalog Varietas Unggul Section -->
    <section id="varietas" class="py-20 bg-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center max-w-3xl mx-auto mb-12 space-y-3">
                <span class="text-xs font-extrabold uppercase tracking-widest text-brand-600">Database Varietas</span>
                <h2 class="text-3xl sm:text-4xl font-extrabold text-slate-900">Katalog Varietas Padi Gogo Unggul</h2>
                <p class="text-slate-600 text-base">
                    Pilihlah varietas padi gogo (seri Inpago, Situ Bagendit, dll.) yang sesuai dengan kondisi tekstur tanah, ketinggian tempat, dan preferensi rasa nasi di daerah Anda.
                </p>
            </div>

            <!-- Controls: Search & Category Filter -->
            <div class="flex flex-col md:flex-row items-center justify-between gap-4 mb-10 bg-slate-50 p-4 rounded-2xl border border-slate-200/80">
                <!-- Search Input -->
                <div class="relative w-full md:w-80">
                    <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-400"></i>
                    <input type="text" id="variety-search" placeholder="Cari varietas (mis. Inpago, Situ...)" class="w-full pl-10 pr-4 py-2.5 rounded-xl border border-slate-300 focus:outline-none focus:border-brand-500 focus:ring-2 focus:ring-brand-500/20 text-sm">
                </div>

                <!-- Category Buttons -->
                <div class="flex items-center gap-2 overflow-x-auto w-full md:w-auto pb-2 md:pb-0 scrollbar-none">
                    <button class="variety-filter-btn px-4 py-2 rounded-xl text-xs font-bold transition-all bg-brand-600 text-white shadow-sm" data-filter="all">Semua</button>
                    <button class="variety-filter-btn px-4 py-2 rounded-xl text-xs font-bold transition-all bg-white text-slate-600 hover:bg-slate-200 border border-slate-200" data-filter="pulen">Rasa Pulen</button>
                    <button class="variety-filter-btn px-4 py-2 rounded-xl text-xs font-bold transition-all bg-white text-slate-600 hover:bg-slate-200 border border-slate-200" data-filter="blast">Tahan Blast</button>
                    <button class="variety-filter-btn px-4 py-2 rounded-xl text-xs font-bold transition-all bg-white text-slate-600 hover:bg-slate-200 border border-slate-200" data-filter="masam">Toleran Tanah Masam</button>
                </div>
            </div>

            <!-- Variety Grid -->
            <div id="variety-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Dynamic cards injected via JS -->
            </div>
        </div>
    </section>

    <!-- Modal for Variety Details -->
    <div id="variety-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/60 backdrop-blur-sm hidden">
        <div class="bg-white rounded-3xl max-w-2xl w-full p-6 sm:p-8 shadow-2xl relative max-h-[90vh] overflow-y-auto border border-slate-100">
            <button id="close-variety-modal" class="absolute top-5 right-5 w-9 h-9 rounded-full bg-slate-100 text-slate-500 hover:bg-slate-200 flex items-center justify-center transition-colors">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>
            <div id="modal-content">
                <!-- Injected via JS -->
            </div>
        </div>
    </div>

    <!-- Panduan Budidaya Langkah Demi Langkah Section -->
    <section id="budidaya" class="py-20 bg-slate-50 border-t border-slate-200/80">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center max-w-3xl mx-auto mb-14 space-y-3">
                <span class="text-xs font-extrabold uppercase tracking-widest text-brand-600">Standard Operating Procedure</span>
                <h2 class="text-3xl sm:text-4xl font-extrabold text-slate-900">Panduan Budidaya Padi Gogo</h2>
                <p class="text-slate-600 text-base">
                    Ikuti tahapan resmi budidaya padi gogo untuk mencapai produktivitas panen yang optimal.
                </p>
            </div>

            <!-- Interactive Tabbed Stepper -->
            <div class="bg-white rounded-3xl shadow-xl border border-slate-200/80 overflow-hidden">
                <!-- Tab Headers -->
                <div class="flex overflow-x-auto border-b border-slate-200 bg-slate-50/50 scrollbar-none">
                    <button class="step-tab-btn flex-1 min-w-[140px] py-4 px-4 text-center font-bold text-sm border-b-2 border-brand-600 text-brand-700 bg-white transition-all" data-step="1">
                        <span class="block text-xs font-normal text-slate-400">Langkah 1</span>
                        Persiapan Lahan
                    </button>
                    <button class="step-tab-btn flex-1 min-w-[140px] py-4 px-4 text-center font-bold text-sm border-b-2 border-transparent text-slate-500 hover:text-slate-800 transition-all" data-step="2">
                        <span class="block text-xs font-normal text-slate-400">Langkah 2</span>
                        Penanaman (Tugal)
                    </button>
                    <button class="step-tab-btn flex-1 min-w-[140px] py-4 px-4 text-center font-bold text-sm border-b-2 border-transparent text-slate-500 hover:text-slate-800 transition-all" data-step="3">
                        <span class="block text-xs font-normal text-slate-400">Langkah 3</span>
                        Pemupukan
                    </button>
                    <button class="step-tab-btn flex-1 min-w-[140px] py-4 px-4 text-center font-bold text-sm border-b-2 border-transparent text-slate-500 hover:text-slate-800 transition-all" data-step="4">
                        <span class="block text-xs font-normal text-slate-400">Langkah 4</span>
                        Pengendalian OPT
                    </button>
                    <button class="step-tab-btn flex-1 min-w-[140px] py-4 px-4 text-center font-bold text-sm border-b-2 border-transparent text-slate-500 hover:text-slate-800 transition-all" data-step="5">
                        <span class="block text-xs font-normal text-slate-400">Langkah 5</span>
                        Panen & Pasca
                    </button>
                </div>

                <!-- Step Contents -->
                <div class="p-6 sm:p-10">
                    <!-- Step 1 Content -->
                    <div id="step-content-1" class="step-content space-y-6">
                        <div class="flex items-start gap-4">
                            <div class="w-12 h-12 rounded-2xl bg-brand-100 text-brand-700 flex items-center justify-center font-bold text-xl shrink-0">1</div>
                            <div>
                                <h3 class="text-2xl font-bold text-slate-900">Pengolahan & Pengapuran Tanah</h3>
                                <p class="text-slate-600 text-sm mt-1">Langkah krusial untuk memperbaiki porositas tanah dan menetralkan keasaman (pH) tanah kering.</p>
                            </div>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6 pt-2">
                            <div class="p-5 rounded-2xl bg-slate-50 border border-slate-100 space-y-2">
                                <h4 class="font-bold text-slate-800 text-sm flex items-center gap-2">
                                    <i class="fa-solid fa-shovels text-brand-600"></i> Pembajakan & Penggemburan
                                </h4>
                                <p class="text-xs text-slate-600 leading-relaxed">
                                    Bajak tanah sedalam 20-30 cm sebanyak 2 kali, lalu ratakan. Hal ini bertujuan untuk merusak perakaran gulma dan meningkatkan aerasi udara tanah.
                                </p>
                            </div>
                            <div class="p-5 rounded-2xl bg-slate-50 border border-slate-100 space-y-2">
                                <h4 class="font-bold text-slate-800 text-sm flex items-center gap-2">
                                    <i class="fa-solid fa-flask text-amberGold-600"></i> Pengapuran (Kapur Dolomit)
                                </h4>
                                <p class="text-xs text-slate-600 leading-relaxed">
                                    Jika pH tanah di bawah 5,5 (tanah masam), aplikasikan Kapur Dolomit 1-2 Ton/Ha sekitar 2 minggu sebelum tanam untuk mencegah keracunan Alumunium (Al).
                                </p>
                            </div>
                        </div>

                        <div class="p-4 rounded-xl bg-amber-50 border border-amber-200 text-amber-900 text-xs flex items-center gap-3">
                            <i class="fa-solid fa-lightbulb text-amber-600 text-lg"></i>
                            <span><strong>Tips Praktis:</strong> Tebarkan pupuk kandang/kompos matang sebanyak 2-3 ton per hektar bersamaan dengan pengolahan tanah terakhir.</span>
                        </div>
                    </div>

                    <!-- Step 2 Content -->
                    <div id="step-content-2" class="step-content hidden space-y-6">
                        <div class="flex items-start gap-4">
                            <div class="w-12 h-12 rounded-2xl bg-brand-100 text-brand-700 flex items-center justify-center font-bold text-xl shrink-0">2</div>
                            <div>
                                <h3 class="text-2xl font-bold text-slate-900">Teknik Penanaman Sistem Tugal</h3>
                                <p class="text-slate-600 text-sm mt-1">Sistem penanaman langsung benih (Direct Seeding) menggunakan kayu tugal.</p>
                            </div>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-3 gap-6 pt-2">
                            <div class="p-5 rounded-2xl bg-slate-50 border border-slate-100 space-y-2">
                                <h4 class="font-bold text-slate-800 text-sm">1. Jarak Tanam Ideal</h4>
                                <p class="text-xs text-slate-600">Gunakan jarak 20 cm x 20 cm atau sistem Legowo 2:1 (20 x 10 x 40 cm) untuk menambah populasi rumpun.</p>
                            </div>
                            <div class="p-5 rounded-2xl bg-slate-50 border border-slate-100 space-y-2">
                                <h4 class="font-bold text-slate-800 text-sm">2. Lubang Tugal</h4>
                                <p class="text-xs text-slate-600">Buat lubang tugal kedalaman 3-5 cm. Masukkan 3-5 butir benih berkualitas per lubang.</p>
                            </div>
                            <div class="p-5 rounded-2xl bg-slate-50 border border-slate-100 space-y-2">
                                <h4 class="font-bold text-slate-800 text-sm">3. Penutupan Lubang</h4>
                                <p class="text-xs text-slate-600">Tutup lubang secara tipis dengan tanah gembur atau kompos halus agar benih tidak dimakan burung.</p>
                            </div>
                        </div>
                    </div>

                    <!-- Step 3 Content -->
                    <div id="step-content-3" class="step-content hidden space-y-6">
                        <div class="flex items-start gap-4">
                            <div class="w-12 h-12 rounded-2xl bg-brand-100 text-brand-700 flex items-center justify-center font-bold text-xl shrink-0">3</div>
                            <div>
                                <h3 class="text-2xl font-bold text-slate-900">Jadwal Pemupukan Berimbang</h3>
                                <p class="text-slate-600 text-sm mt-1">Aplikasi pupuk secara bertahap sesuai fase vegetatif dan generatif.</p>
                            </div>
                        </div>

                        <div class="overflow-x-auto">
                            <table class="w-full text-left text-xs text-slate-700 border-collapse">
                                <thead>
                                    <tr class="bg-slate-100 text-slate-900 border-b border-slate-200">
                                        <th class="p-3 font-bold">Waktu Aplikasi</th>
                                        <th class="p-3 font-bold">Jenis Pupuk</th>
                                        <th class="p-3 font-bold">Dosis / Ha (Rekomendasi)</th>
                                        <th class="p-3 font-bold">Keterangan</th>
                                    </tr>
                                </thead>
                                <tbody class="divide-y divide-slate-100">
                                    <tr>
                                        <td class="p-3 font-semibold">Tanam (0 HST)</td>
                                        <td class="p-3">SP-36 / NPK Dasaran</td>
                                        <td class="p-3">100 kg SP-36</td>
                                        <td class="p-3 text-slate-500">Dimasukkan dekat lubang tugal</td>
                                    </tr>
                                    <tr>
                                        <td class="p-3 font-semibold">15 - 20 HST</td>
                                        <td class="p-3">Urea + KCl (Susulan I)</td>
                                        <td class="p-3">100 kg Urea + 50 kg KCl</td>
                                        <td class="p-3 text-slate-500">Mendorong anakan vegetatif</td>
                                    </tr>
                                    <tr>
                                        <td class="p-3 font-semibold">35 - 40 HST</td>
                                        <td class="p-3">Urea + KCl (Susulan II)</td>
                                        <td class="p-3">100 kg Urea + 50 kg KCl</td>
                                        <td class="p-3 text-slate-500">Fase primordial / pembentukan malai</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>

                    <!-- Step 4 Content -->
                    <div id="step-content-4" class="step-content hidden space-y-6">
                        <div class="flex items-start gap-4">
                            <div class="w-12 h-12 rounded-2xl bg-brand-100 text-brand-700 flex items-center justify-center font-bold text-xl shrink-0">4</div>
                            <div>
                                <h3 class="text-2xl font-bold text-slate-900">Pengendalian Hama & Penyakit (OPT)</h3>
                                <p class="text-slate-600 text-sm mt-1">Proteksi tanaman dari Hama Blast, Penggerek Batang, dan Walangsangit.</p>
                            </div>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div class="p-5 rounded-2xl bg-red-50/50 border border-red-100 space-y-2">
                                <h4 class="font-bold text-red-900 text-sm flex items-center gap-2">
                                    <i class="fa-solid fa-bug text-red-600"></i> Hama Utama (Penggerek Batang & Walangsangit)
                                </h4>
                                <p class="text-xs text-slate-600 leading-relaxed">
                                    Lakukan pengamatan rutin. Gunakan perangkap kuning atau agen hayati (*Beauveria bassiana*). Semprot insektisida nabati jika populasi melebihi ambang ekonomi.
                                </p>
                            </div>
                            <div class="p-5 rounded-2xl bg-amber-50/50 border border-amber-100 space-y-2">
                                <h4 class="font-bold text-amber-900 text-sm flex items-center gap-2">
                                    <i class="fa-solid fa-virus text-amber-600"></i> Penyakit Blast (*Pyricularia oryzae*)
                                </h4>
                                <p class="text-xs text-slate-600 leading-relaxed">
                                    Penyakit paling krusial di lahan kering. Cegah dengan varietas tahan (Inpago), hindari dosis Urea berlebihan, dan semprot fungisida hayati bila tampak bercak belah ketupat di daun.
                                </p>
                            </div>
                        </div>
                    </div>

                    <!-- Step 5 Content -->
                    <div id="step-content-5" class="step-content hidden space-y-6">
                        <div class="flex items-start gap-4">
                            <div class="w-12 h-12 rounded-2xl bg-brand-100 text-brand-700 flex items-center justify-center font-bold text-xl shrink-0">5</div>
                            <div>
                                <h3 class="text-2xl font-bold text-slate-900">Panen & Pascapanen</h3>
                                <p class="text-slate-600 text-sm mt-1">Menjaga rendemen beras pecah kulit dan menekan kehilangan hasil (*losses*).</p>
                            </div>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div class="p-5 rounded-2xl bg-slate-50 border border-slate-100 space-y-2">
                                <h4 class="font-bold text-slate-800 text-sm">Ciri Padi Siap Panen</h4>
                                <ul class="text-xs text-slate-600 space-y-1.5 list-disc list-inside">
                                    <li>90-95% bulir pada malai telah menguning sempurna.</li>
                                    <li>Kadar air gabah berkisar 21 - 24%.</li>
                                    <li>Batang bagian bawah mulai mengering secara alami.</li>
                                </ul>
                            </div>
                            <div class="p-5 rounded-2xl bg-slate-50 border border-slate-100 space-y-2">
                                <h4 class="font-bold text-slate-800 text-sm">Penanganan Pascapanen</h4>
                                <ul class="text-xs text-slate-600 space-y-1.5 list-disc list-inside">
                                    <li>Rontokkan gabah segera setelah sabit dipotong (maksimal 1x24 jam).</li>
                                    <li>Jemur gabah di atas lantai jemur hingga kadar air turun mencapai 13 - 14%.</li>
                                    <li>Simpan di karung bersih dalam gudang yang aerasi udaranya lancar.</li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Kalkulator Kebutuhan Tani Section -->
    <section id="kalkulator" class="py-20 bg-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-start">
                
                <!-- Calculator Inputs Panel -->
                <div class="lg:col-span-6 bg-slate-50 p-6 sm:p-8 rounded-3xl border border-slate-200/80 shadow-md space-y-6">
                    <div>
                        <span class="text-xs font-extrabold uppercase tracking-widest text-brand-600">Simulasi Interaktif</span>
                        <h2 class="text-2xl sm:text-3xl font-extrabold text-slate-900">Kalkulator Kebutuhan Tanam</h2>
                        <p class="text-xs sm:text-sm text-slate-600 mt-1">Masukkan luas lahan Anda untuk menghitung perkiraan benih, pupuk, dan potensi hasil panen.</p>
                    </div>

                    <form id="calc-form" class="space-y-4">
                        <!-- Land Area Input -->
                        <div class="grid grid-cols-3 gap-3">
                            <div class="col-span-2">
                                <label class="block text-xs font-bold text-slate-700 mb-1">Luas Lahan</label>
                                <input type="number" id="land-size" value="1000" min="1" step="any" class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 focus:ring-2 focus:ring-brand-500/20 focus:border-brand-500 text-sm font-semibold">
                            </div>
                            <div>
                                <label class="block text-xs font-bold text-slate-700 mb-1">Satuan</label>
                                <select id="land-unit" class="w-full px-3 py-2.5 rounded-xl border border-slate-300 focus:ring-2 focus:ring-brand-500/20 focus:border-brand-500 text-sm bg-white font-semibold">
                                    <option value="m2">m² (Meter persegi)</option>
                                    <option value="ha">Hektar (Ha)</option>
                                    <option value="uubin">Ubin (14 m²)</option>
                                </select>
                            </div>
                        </div>

                        <!-- Spacing Choice -->
                        <div>
                            <label class="block text-xs font-bold text-slate-700 mb-1">Pola & Jarak Tanam</label>
                            <select id="spacing-type" class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 focus:ring-2 focus:ring-brand-500/20 focus:border-brand-500 text-sm bg-white font-medium">
                                <option value="20x20">Tugal Reguler (20 x 20 cm) - Standard</option>
                                <option value="25x25">Tugal Longgar (25 x 25 cm)</option>
                                <option value="legowo">Legowo 2:1 (20 x 10 x 40 cm) - Populasi Tinggi</option>
                            </select>
                        </div>

                        <!-- Target Yield Variety Potential -->
                        <div>
                            <label class="block text-xs font-bold text-slate-700 mb-1">Pilih Varietas Benih</label>
                            <select id="calc-variety" class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 focus:ring-2 focus:ring-brand-500/20 focus:border-brand-500 text-sm bg-white font-medium">
                                <option value="5.5">Inpago 8 (Potensi ~5.5 Ton/Ha)</option>
                                <option value="6.5">Inpago 12 Agritan (Potensi ~6.5 Ton/Ha)</option>
                                <option value="5.0">Situ Bagendit (Potensi ~5.0 Ton/Ha)</option>
                                <option value="7.0">Inpago Unram 1 (Potensi ~7.0 Ton/Ha)</option>
                            </select>
                        </div>

                        <button type="button" id="btn-calculate" class="w-full py-3.5 rounded-xl bg-brand-600 hover:bg-brand-700 text-white font-bold text-sm shadow-md transition-all flex items-center justify-center gap-2">
                            <i class="fa-solid fa-calculator"></i>
                            <span>Hitung Sekarang</span>
                        </button>
                    </form>
                </div>

                <!-- Calculation Output Results Card -->
                <div class="lg:col-span-6 bg-gradient-to-br from-brand-900 to-slate-900 text-white p-6 sm:p-8 rounded-3xl shadow-xl space-y-6 relative overflow-hidden">
                    <!-- Subtle Leaf Watermark -->
                    <i class="fa-solid fa-wheat-awn absolute -right-10 -bottom-10 text-white/5 text-9xl pointer-events-none"></i>

                    <div class="border-b border-white/10 pb-4">
                        <span class="text-xs font-semibold uppercase tracking-wider text-amberGold-400">Hasil Estimasi Kebutuhan</span>
                        <h3 class="text-2xl font-bold text-white mt-1">Rincian Sarana Production (Saprotan)</h3>
                        <p class="text-xs text-slate-300">Disesuaikan berdasarkan standar luas lahan yang dimasukkan.</p>
                    </div>

                    <!-- Output Grid -->
                    <div class="grid grid-cols-2 gap-4">
                        <!-- Seeds Needed -->
                        <div class="p-4 rounded-2xl bg-white/10 backdrop-blur-md border border-white/10">
                            <p class="text-xs text-slate-300 font-medium">Kebutuhan Benih</p>
                            <p id="out-seed" class="text-2xl font-extrabold text-amberGold-400 mt-1">3.0 <span class="text-sm font-normal text-white">kg</span></p>
                            <p class="text-[10px] text-slate-400 mt-0.5">Metode Tugal 3-4 biji/lubang</p>
                        </div>

                        <!-- Expected Harvest Yield -->
                        <div class="p-4 rounded-2xl bg-white/10 backdrop-blur-md border border-white/10">
                            <p class="text-xs text-slate-300 font-medium">Potensi Panen (GKP)</p>
                            <p id="out-yield" class="text-2xl font-extrabold text-emerald-400 mt-1">0.55 <span class="text-sm font-normal text-white">Ton</span></p>
                            <p class="text-[10px] text-slate-400 mt-0.5">Gabah Kering Panen</p>
                        </div>
                    </div>

                    <!-- Fertilizers Detailed Breakdown -->
                    <div class="space-y-3 pt-2">
                        <h4 class="text-xs font-bold uppercase tracking-wider text-slate-300">Estimasi Pupuk Kimia & Organik:</h4>

                        <div class="space-y-2 text-xs">
                            <div class="flex items-center justify-between p-2.5 rounded-xl bg-white/5 border border-white/5">
                                <span class="text-slate-300"><i class="fa-solid fa-cubes text-emerald-400 mr-2"></i>Pupuk Urea (Nitrogen)</span>
                                <span id="out-urea" class="font-bold text-white">20.0 kg</span>
                            </div>
                            <div class="flex items-center justify-between p-2.5 rounded-xl bg-white/5 border border-white/5">
                                <span class="text-slate-300"><i class="fa-solid fa-cubes text-amberGold-400 mr-2"></i>Pupuk SP-36 (Fosfat)</span>
                                <span id="out-sp36" class="font-bold text-white">10.0 kg</span>
                            </div>
                            <div class="flex items-center justify-between p-2.5 rounded-xl bg-white/5 border border-white/5">
                                <span class="text-slate-300"><i class="fa-solid fa-cubes text-blue-400 mr-2"></i>Pupuk KCl (Kalium)</span>
                                <span id="out-kcl" class="font-bold text-white">10.0 kg</span>
                            </div>
                            <div class="flex items-center justify-between p-2.5 rounded-xl bg-white/5 border border-white/5">
                                <span class="text-slate-300"><i class="fa-solid fa-leaf text-brand-400 mr-2"></i>Pupuk Organik / Kompos</span>
                                <span id="out-compost" class="font-bold text-white">250.0 kg</span>
                            </div>
                        </div>
                    </div>

                    <!-- Action Button -->
                    <div class="pt-2">
                        <button id="btn-copy-calc" type="button" class="w-full py-2.5 rounded-xl bg-white/10 hover:bg-white/20 border border-white/20 text-white font-semibold text-xs transition-colors flex items-center justify-center gap-2">
                            <i class="fa-solid fa-copy"></i>
                            <span>Salin Ringkasan Kebutuhan</span>
                        </button>
                    </div>
                </div>

            </div>
        </div>
    </section>

    <!-- Interactive Quiz Section -->
    <section id="kuis" class="py-20 bg-slate-50 border-t border-slate-200/80">
        <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center max-w-2xl mx-auto mb-10 space-y-3">
                <span class="text-xs font-extrabold uppercase tracking-widest text-brand-600">Uji Pemahaman</span>
                <h2 class="text-3xl font-extrabold text-slate-900">Kuis Edukasi Padi Gogo</h2>
                <p class="text-slate-600 text-sm">
                    Uji pengetahuan Anda seputar karakteristik, varietas, dan teknik budidaya padi gogo!
                </p>
            </div>

            <!-- Quiz Card Widget -->
            <div class="bg-white rounded-3xl p-6 sm:p-10 shadow-xl border border-slate-200/80 relative overflow-hidden">
                <div id="quiz-screen">
                    <!-- Progress Header -->
                    <div class="flex items-center justify-between border-b border-slate-100 pb-4 mb-6">
                        <span id="quiz-step-indicator" class="text-xs font-bold text-brand-700 bg-brand-50 px-3 py-1 rounded-full">Soal 1 dari 5</span>
                        <span id="quiz-score-badge" class="text-xs font-semibold text-slate-500">Skor: 0</span>
                    </div>

                    <!-- Question Text -->
                    <h3 id="quiz-question-text" class="text-lg sm:text-xl font-bold text-slate-900 mb-6">
                        Loading pertanyaan...
                    </h3>

                    <!-- Options Grid -->
                    <div id="quiz-options" class="space-y-3">
                        <!-- Options dynamically injected -->
                    </div>

                    <!-- Feedback Container -->
                    <div id="quiz-feedback" class="hidden mt-6 p-4 rounded-2xl text-xs font-semibold"></div>

                    <!-- Next Button -->
                    <div class="mt-8 flex justify-end">
                        <button id="quiz-next-btn" class="hidden px-6 py-2.5 rounded-xl bg-brand-600 hover:bg-brand-700 text-white font-bold text-sm shadow-md transition-all">
                            Pertanyaan Selanjutnya <i class="fa-solid fa-arrow-right ml-1"></i>
                        </button>
                    </div>
                </div>

                <!-- Quiz Results Screen (Hidden initially) -->
                <div id="quiz-result-screen" class="hidden text-center space-y-6 py-6">
                    <div class="w-20 h-20 rounded-full bg-emerald-100 text-brand-700 mx-auto flex items-center justify-center text-3xl shadow-inner">
                        <i class="fa-solid fa-trophy"></i>
                    </div>

                    <div class="space-y-2">
                        <h3 class="text-2xl font-extrabold text-slate-900">Kuis Selesai!</h3>
                        <p class="text-slate-600 text-sm">Terima kasih telah menguji wawasan pertanian lahan kering Anda.</p>
                    </div>

                    <div class="p-6 bg-slate-50 rounded-2xl border border-slate-200/80 max-w-sm mx-auto">
                        <p class="text-xs uppercase font-extrabold tracking-widest text-slate-400">Skor Akhir Anda</p>
                        <p id="final-score" class="text-4xl font-black text-brand-700 mt-1">100 / 100</p>
                        <p id="score-comment" class="text-xs font-semibold text-emerald-800 mt-2">Sangat Luar Biasa! Anda Mahir Padi Gogo!</p>
                    </div>

                    <button id="quiz-restart-btn" class="px-6 py-3 rounded-xl bg-brand-600 hover:bg-brand-700 text-white font-bold text-sm shadow-md transition-all inline-flex items-center gap-2">
                        <i class="fa-solid fa-rotate-right"></i>
                        <span>Ulangi Kuis</span>
                    </button>
                </div>
            </div>
        </div>
    </section>

    <!-- FAQ Section -->
    <section class="py-16 bg-white">
        <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-12">
                <h2 class="text-2xl sm:text-3xl font-extrabold text-slate-900">Pertanyaan Sering Diajukan (FAQ)</h2>
                <p class="text-slate-500 text-xs sm:text-sm mt-1">Jawaban cepat seputar kendala di lapangan.</p>
            </div>

            <div class="space-y-4">
                <details class="group bg-slate-50 p-5 rounded-2xl border border-slate-200/80 [&_summary::-webkit-details-marker]:hidden">
                    <summary class="flex items-center justify-between cursor-pointer font-bold text-slate-800 text-sm">
                        <span>Apakah Padi Gogo bisa ditanam pada musim hujan penuh?</span>
                        <span class="transition group-open:rotate-180"><i class="fa-solid fa-chevron-down text-slate-400"></i></span>
                    </summary>
                    <p class="mt-3 text-xs text-slate-600 leading-relaxed">
                        Bisa. Namun pastikan sanitasi dan drainase lahan cukup baik agar air hujan tidak menggenang terlalu lama (menghindari pembusukan akar) serta tingkatkan kewaspadaan terhadap serangan jamur Blast.
                    </p>
                </details>

                <details class="group bg-slate-50 p-5 rounded-2xl border border-slate-200/80 [&_summary::-webkit-details-marker]:hidden">
                    <summary class="flex items-center justify-between cursor-pointer font-bold text-slate-800 text-sm">
                        <span>Mengapa benih tidak disemai terlebih dahulu seperti padi sawah?</span>
                        <span class="transition group-open:rotate-180"><i class="fa-solid fa-chevron-down text-slate-400"></i></span>
                    </summary>
                    <p class="mt-3 text-xs text-slate-600 leading-relaxed">
                        Sistem lahan kering menggunakan penanaman langsung (tugal) untuk meminimalkan risiko 'stres pindahtanam' (*transplanting shock*) pada bibit akibat minimnya kelembapan air tergenang.
                    </p>
                </details>

                <details class="group bg-slate-50 p-5 rounded-2xl border border-slate-200/80 [&_summary::-webkit-details-marker]:hidden">
                    <summary class="flex items-center justify-between cursor-pointer font-bold text-slate-800 text-sm">
                        <span>Bagaimana rasa nasi dari varietas Padi Gogo modern (Inpago)?</span>
                        <span class="transition group-open:rotate-180"><i class="fa-solid fa-chevron-down text-slate-400"></i></span>
                    </summary>
                    <p class="mt-3 text-xs text-slate-600 leading-relaxed">
                        Varietas unggul baru seperti Inpago 8 dan Inpago 12 Agritan dipromosikan dengan tingkat amilosa sedang sehingga menghasilkan nasi dengan tekstur pulen, tidak kalah lezat dibandingkan beras sawah irigasi.
                    </p>
                </details>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-slate-900 text-slate-400 py-12 border-t border-slate-800">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8 mb-8">
                <div class="md:col-span-2 space-y-3">
                    <div class="flex items-center gap-3">
                        <div class="w-9 h-9 rounded-xl bg-brand-600 text-white flex items-center justify-center font-bold">
                            <i class="fa-solid fa-wheat-awn"></i>
                        </div>
                        <span class="text-xl font-bold text-white">AgroGogo</span>
                    </div>
                    <p class="text-xs text-slate-400 leading-relaxed max-w-sm">
                        Platform media interaktif edukasi budidaya dan pengembangan padi lahan kering (padi gogo) demi memperkuat kedaulatan pangan nasional Indonesia.
                    </p>
                </div>

                <div>
                    <h4 class="text-white text-xs font-bold uppercase tracking-wider mb-3">Navigasi Utama</h4>
                    <ul class="space-y-2 text-xs">
                        <li><a href="#pengenalan" class="hover:text-white transition-colors">Pengenalan Dasar</a></li>
                        <li><a href="#komparasi" class="hover:text-white transition-colors">Komparasi Sawah vs Gogo</a></li>
                        <li><a href="#varietas" class="hover:text-white transition-colors">Katalog Varietas</a></li>
                        <li><a href="#budidaya" class="hover:text-white transition-colors">SOP Budidaya Tugal</a></li>
                    </ul>
                </div>

                <div>
                    <h4 class="text-white text-xs font-bold uppercase tracking-wider mb-3">Alat & Fitur</h4>
                    <ul class="space-y-2 text-xs">
                        <li><a href="#kalkulator" class="hover:text-white transition-colors">Kalkulator Benih & Pupuk</a></li>
                        <li><a href="#kuis" class="hover:text-white transition-colors">Kuis Interaktif</a></li>
                        <li><a href="#" onclick="showToast('Panduan PDF akan diunduh!', 'info'); return false;" class="hover:text-white transition-colors"><i class="fa-solid fa-file-pdf text-red-400 mr-1"></i>Unduh Module PDF</a></li>
                    </ul>
                </div>
            </div>

            <div class="pt-8 border-t border-slate-800 text-center md:text-left flex flex-col md:flex-row items-center justify-between text-xs text-slate-500">
                <p>&copy; 2026 AgroGogo - Platform Edukasi Pertanian Lahan Kering. All rights reserved.</p>
                <p class="mt-2 md:mt-0">Didesain dengan perhatian UI/UX & Responstivitas Tinggi.</p>
            </div>
        </div>
    </footer>

    <!-- JavaScript Application Logic -->
    <script>
        // Database Varietas Padi Gogo
        const varietyData = [
            {
                id: 'inpago-8',
                name: 'Inpago 8',
                category: ['pulen', 'blast'],
                yieldPotential: '5.5 - 6.5 Ton/Ha',
                maturation: '115 Hari',
                texture: 'Pulen (Amilosa ~21%)',
                resistance: 'Tahan Penyakit Blast Ras 073 & 133',
                description: 'Varietas gogo unggulan nasional yang memiliki adaptasi luas di lahan kering iklim basah maupun kering. Nasi pulen dan anakan produktif banyak.',
                suitableArea: 'Lahan Kering Dataran Rendah (< 600 mdpl)'
            },
            {
                id: 'inpago-12',
                name: 'Inpago 12 Agritan',
                category: ['pulen', 'blast', 'masam'],
                yieldPotential: '6.7 - 8.4 Ton/Ha',
                maturation: '111 Hari',
                texture: 'Pulen',
                resistance: 'Sangat Tahan Blast & Toleran Keracunan Alumunium',
                description: 'Didesain khusus untuk lahan kering masam dengan kejenuhan Aluminium tinggi. Memiliki potensi hasil sangat tinggi mendekati padi sawah.',
                suitableArea: 'Lahan Kering Masam Podsolik Merah Kuning'
            },
            {
                id: 'situ-bagendit',
                name: 'Situ Bagendit',
                category: ['pulen'],
                yieldPotential: '4.5 - 5.5 Ton/Ha',
                maturation: '110 - 120 Hari',
                texture: 'Pulen',
                resistance: 'Agak Tahan Hama Penggerek Batang',
                description: 'Varietas amfibi yang sangat populer. Dapat ditanam dengan baik di lahan kering (gogo) maupun di lahan sawah irigasi.',
                suitableArea: 'Lahan Kering & Sawah Tadah Hujan'
            },
            {
                id: 'inpago-unram-1',
                name: 'Inpago Unram 1',
                category: ['blast'],
                yieldPotential: '6.0 - 7.2 Ton/Ha',
                maturation: '108 Hari',
                texture: 'Sedang / Puan',
                resistance: 'Toleran Kekeringan Ekstrem & Blast',
                description: 'Hasil pemuliaan Universitas Mataram yang sangat tangguh di wilayah Nusa Tenggara dengan curah hujan amat minim.',
                suitableArea: 'Kawasan Iklim Kering / Rainfed Sub-optimal'
            },
            {
                id: 'inpago-9',
                name: 'Inpago 9',
                category: ['masam', 'blast'],
                yieldPotential: '5.2 - 6.0 Ton/Ha',
                maturation: '109 Hari',
                texture: 'Pulen',
                resistance: 'Toleran Keracunan Na & Al',
                description: 'Varietas unggul dengan daya adaptasi luar biasa pada jenis tanah Ultisol ber-pH rendah.',
                suitableArea: 'Lahan Reklamasi Tambang & Sub-optimal'
            },
            {
                id: 'limboto',
                name: 'Limboto',
                category: ['pulen'],
                yieldPotential: '4.0 - 5.0 Ton/Ha',
                maturation: '115 Hari',
                texture: 'Pulen',
                resistance: 'Toleran Naungan Ringan',
                description: 'Sangat fleksibel untuk ditanam sebagai tanaman sela di bawah tegakan pohon kayu atau perkebunan kelapa sawit muda.',
                suitableArea: 'Lahan Tumpangsari & Tegakan Perkebunan'
            }
        ];

        function renderVarieties(filterCategory = 'all', searchQuery = '') {
            const grid = document.getElementById('variety-grid');
            grid.innerHTML = '';

            const filtered = varietyData.filter(v => {
                const matchesCategory = filterCategory === 'all' || v.category.includes(filterCategory);
                const matchesSearch = v.name.toLowerCase().includes(searchQuery.toLowerCase()) || 
                                      v.description.toLowerCase().includes(searchQuery.toLowerCase());
                return matchesCategory && matchesSearch;
            });

            if (filtered.length === 0) {
                grid.innerHTML = `
                    <div class="col-span-full text-center py-12 text-slate-400">
                        <i class="fa-solid fa-magnifying-glass text-4xl mb-3"></i>
                        <p class="text-sm font-semibold">Tidak ada varietas yang sesuai pencarian.</p>
                    </div>
                `;
                return;
            }

            filtered.forEach(v => {
                const card = document.createElement('div');
                card.className = "bg-slate-50 rounded-3xl p-6 border border-slate-200/80 hover:border-brand-300 hover:shadow-xl transition-all flex flex-col justify-between group";
                card.innerHTML = `
                    <div class="space-y-4">
                        <div class="flex items-center justify-between">
                            <span class="px-2.5 py-1 rounded-full text-[10px] font-extrabold uppercase bg-brand-100 text-brand-800">
                                ${v.maturation}
                            </span>
                            <i class="fa-solid fa-seedling text-slate-300 group-hover:text-brand-600 transition-colors"></i>
                        </div>

                        <div>
                            <h3 class="text-xl font-extrabold text-slate-900 group-hover:text-brand-700 transition-colors">${v.name}</h3>
                            <p class="text-xs text-slate-500 mt-0.5">Potensi: <span class="font-bold text-slate-800">${v.yieldPotential}</span></p>
                        </div>

                        <p class="text-xs text-slate-600 line-clamp-2 leading-relaxed">${v.description}</p>

                        <div class="pt-2 flex flex-wrap gap-1.5">
                            <span class="text-[10px] px-2 py-0.5 rounded-md bg-white border border-slate-200 font-semibold text-slate-600">${v.texture}</span>
                            <span class="text-[10px] px-2 py-0.5 rounded-md bg-white border border-slate-200 font-semibold text-slate-600">Blast Resistan</span>
                        </div>
                    </div>

                    <button onclick="openVarietyModal('${v.id}')" class="mt-6 w-full py-2.5 rounded-xl bg-white hover:bg-brand-600 hover:text-white border border-slate-200 text-slate-700 font-bold text-xs transition-all shadow-sm">
                        Detail Spesifikasi & Tips <i class="fa-solid fa-arrow-right ml-1"></i>
                    </button>
                `;
                grid.appendChild(card);
            });
        }

        function openVarietyModal(id) {
            const v = varietyData.find(item => item.id === id);
            if (!v) return;

            const modalContent = document.getElementById('modal-content');
            modalContent.innerHTML = `
                <div class="space-y-5">
                    <div class="flex items-center gap-3 border-b border-slate-100 pb-4">
                        <div class="w-12 h-12 rounded-2xl bg-gradient-to-tr from-brand-600 to-amberGold-500 text-white flex items-center justify-center text-xl font-bold">
                            <i class="fa-solid fa-wheat-awn"></i>
                        </div>
                        <div>
                            <h3 class="text-2xl font-extrabold text-slate-900">${v.name}</h3>
                            <p class="text-xs text-brand-600 font-bold uppercase tracking-wider">${v.suitableArea}</p>
                        </div>
                    </div>

                    <p class="text-xs sm:text-sm text-slate-600 leading-relaxed">${v.description}</p>

                    <div class="grid grid-cols-2 gap-3 text-xs">
                        <div class="p-3 bg-slate-50 rounded-xl border border-slate-100">
                            <span class="text-slate-400 block font-medium">Potensi Hasil</span>
                            <span class="font-bold text-slate-900 text-sm">${v.yieldPotential}</span>
                        </div>
                        <div class="p-3 bg-slate-50 rounded-xl border border-slate-100">
                            <span class="text-slate-400 block font-medium">Umur Tanaman</span>
                            <span class="font-bold text-slate-900 text-sm">${v.maturation}</span>
                        </div>
                        <div class="p-3 bg-slate-50 rounded-xl border border-slate-100">
                            <span class="text-slate-400 block font-medium">Tekstur Nasi</span>
                            <span class="font-bold text-slate-900 text-sm">${v.texture}</span>
                        </div>
                        <div class="p-3 bg-slate-50 rounded-xl border border-slate-100">
                            <span class="text-slate-400 block font-medium">Ketahanan Hama/Penyakit</span>
                            <span class="font-bold text-slate-900 text-sm">${v.resistance}</span>
                        </div>
                    </div>

                    <div class="p-4 rounded-2xl bg-brand-50 border border-brand-100 text-xs text-brand-900 space-y-1">
                        <span class="font-bold block text-brand-800"><i class="fa-solid fa-circle-info mr-1"></i> Rekomendasi Budidaya:</span>
                        <p>Sangat responsif terhadap penambahan pupuk organik/kompos matang 2 ton/ha dan penyiangan gulma berkala pada umur 20 & 40 HST.</p>
                    </div>

                    <button onclick="closeModal()" class="w-full py-3 rounded-xl bg-slate-900 text-white font-bold text-xs hover:bg-slate-800 transition-colors">
                        Tutup Modal
                    </button>
                </div>
            `;

            document.getElementById('variety-modal').classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('variety-modal').classList.add('hidden');
        }

        function initComparisonChart() {
            const ctx = document.getElementById('comparisonChart').getContext('2d');
            new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['Air (Liter/Kg Beras)', 'Kebutuhan Pupuk K (Kg/Ha)', 'Ketahanan Kekeringan (%)', 'Potensi Hasil (Ton/Ha)'],
                    datasets: [
                        {
                            label: 'Padi Gogo',
                            data: [1500, 80, 95, 6.5],
                            backgroundColor: '#16a34a',
                            borderRadius: 8,
                        },
                        {
                            label: 'Padi Sawah Irigasi',
                            data: [4000, 120, 35, 7.5],
                            backgroundColor: '#cbd5e1',
                            borderRadius: 8,
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                font: { family: 'Plus Jakarta Sans', size: 12 }
                            }
                        },
                        tooltip: {
                            padding: 10,
                            titleFont: { family: 'Plus Jakarta Sans', size: 12, weight: 'bold' }
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            grid: { color: '#f1f5f9' },
                            ticks: { font: { family: 'Plus Jakarta Sans', size: 11 } }
                        },
                        x: {
                            grid: { display: false },
                            ticks: { font: { family: 'Plus Jakarta Sans', size: 11 } }
                        }
                    }
                }
            });
        }

        function calculateFarmNeeds() {
            const rawSize = parseFloat(document.getElementById('land-size').value) || 0;
            const unit = document.getElementById('land-unit').value;
            const spacing = document.getElementById('spacing-type').value;
            const potentialTonHa = parseFloat(document.getElementById('calc-variety').value) || 5.5;

            // Convert to Hectares
            let sizeHa = rawSize;
            if (unit === 'm2') sizeHa = rawSize / 10000;
            if (unit === 'uubin') sizeHa = (rawSize * 14) / 10000;

            if (sizeHa <= 0) {
                showToast('Mohon masukkan luas lahan yang valid.', 'warning');
                return;
            }

            // Seed rates based on spacing
            let seedRatePerHa = 30; // kg/ha default
            if (spacing === '25x25') seedRatePerHa = 25;
            if (spacing === 'legowo') seedRatePerHa = 35;

            const totalSeeds = (sizeHa * seedRatePerHa).toFixed(1);
            const totalUrea = (sizeHa * 200).toFixed(1);
            const totalSP36 = (sizeHa * 100).toFixed(1);
            const totalKCl = (sizeHa * 100).toFixed(1);
            const totalCompost = (sizeHa * 2500).toFixed(1);
            const estimatedYield = (sizeHa * potentialTonHa).toFixed(2);

            // Update DOM
            document.getElementById('out-seed').innerText = `${totalSeeds} kg`;
            document.getElementById('out-yield').innerText = `${estimatedYield} Ton`;
            document.getElementById('out-urea').innerText = `${totalUrea} kg`;
            document.getElementById('out-sp36').innerText = `${totalSP36} kg`;
            document.getElementById('out-kcl').innerText = `${totalKCl} kg`;
            document.getElementById('out-compost').innerText = `${totalCompost} kg`;

            showToast('Kalkulasi berhasil diperbarui!', 'success');
        }

        const quizQuestions = [
            {
                q: "Apa ciri utama sistem budidaya Padi Gogo dibandingkan Padi Sawah?",
                options: [
                    "Wajib digenangi air setinggi 10 cm sepanjang waktu",
                    "Ditanam di lahan kering (ladang/tegalan) tanpa air tergenang",
                    "Hanya bisa ditanam di dalam rumah kaca",
                    "Menggunakan bibit dari irigasi pasang surut"
                ],
                answer: 1,
                explanation: "Padi Gogo dibudidayakan di lahan kering tanpa butuh penggenangan air kontinu."
            },
            {
                q: "Metode penanaman benih langsung padi gogo di lapangan disebut dengan istilah...",
                options: [
                    "Sistem Transplanter Sawah",
                    "Sistem Tugal (Direct Seeding)",
                    "Sistem Aeroponik Rawa",
                    "Sistem Hidroponik NFT"
                ],
                answer: 1,
                explanation: "Sistem Tugal adalah pelubangan tanah kering menggunakan kayu runcing untuk memasukkan benih langsung."
            },
            {
                q: "Penyakit cendawan paling krusial yang paling sering menyerang Padi Gogo adalah...",
                options: [
                    "Penyakit Blast (Pyricularia oryzae)",
                    "Busuk Akar Terendam",
                    "Hawar Daun Bakteri Sawah",
                    "Kerdil Rumput Rawa"
                ],
                answer: 0,
                explanation: "Penyakit Blast sangat menyukai kelembapan udara relatif di lahan kering dan merupakan tantangan utama padi gogo."
            },
            {
                q: "Seri varietas unggul padi gogo rilis resmi Badan Standardisasi Instrumen Pertanian (BSIP) dinamakan...",
                options: [
                    "Inpari (Inbrida Padi Irigasi)",
                    "Inpago (Inbrida Padi Gogo)",
                    "Inpara (Inbrida Padi Rawa)",
                    "Ciherang Sawah"
                ],
                answer: 1,
                explanation: "Inpago singkatan dari Inbrida Padi Gogo."
            },
            {
                q: "Berapa kadar air ideal gabah saat penjemuran agar siap disimpan lama?",
                options: [
                    "20 - 25%",
                    "13 - 14%",
                    "5 - 8%",
                    "30 - 35%"
                ],
                answer: 1,
                explanation: "Kadar air 13-14% adalah standar ideal gabah kering simpan agar bebas jamur dan hama gudang."
            }
        ];

        let currentQuestion = 0;
        let userScore = 0;

        function loadQuizQuestion() {
            const qData = quizQuestions[currentQuestion];
            document.getElementById('quiz-step-indicator').innerText = `Soal ${currentQuestion + 1} dari ${quizQuestions.length}`;
            document.getElementById('quiz-score-badge').innerText = `Skor: ${userScore}`;
            document.getElementById('quiz-question-text').innerText = qData.q;

            const optionsContainer = document.getElementById('quiz-options');
            optionsContainer.innerHTML = '';

            const feedback = document.getElementById('quiz-feedback');
            feedback.className = "hidden mt-6 p-4 rounded-2xl text-xs font-semibold";
            document.getElementById('quiz-next-btn').classList.add('hidden');

            qData.options.forEach((opt, idx) => {
                const btn = document.createElement('button');
                btn.className = "quiz-opt-btn w-full text-left p-4 rounded-2xl border border-slate-200 hover:border-brand-500 hover:bg-brand-50/50 font-semibold text-xs sm:text-sm transition-all flex items-center justify-between";
                btn.innerHTML = `<span>${opt}</span> <i class="fa-regular fa-circle text-slate-300"></i>`;
                btn.onclick = () => selectQuizOption(idx, btn);
                optionsContainer.appendChild(btn);
            });
        }

        function selectQuizOption(idx, btnEl) {
            const qData = quizQuestions[currentQuestion];
            const allBtns = document.querySelectorAll('.quiz-opt-btn');
            allBtns.forEach(b => b.disabled = true);

            const feedback = document.getElementById('quiz-feedback');
            feedback.classList.remove('hidden');

            if (idx === qData.answer) {
                userScore += 20;
                btnEl.classList.add('border-emerald-500', 'bg-emerald-50', 'text-emerald-900');
                btnEl.querySelector('i').className = "fa-solid fa-circle-check text-emerald-600";
                feedback.classList.add('bg-emerald-50', 'text-emerald-900', 'border', 'border-emerald-200');
                feedback.innerHTML = `<i class="fa-solid fa-check-circle mr-1"></i> <strong>Benar!</strong> ${qData.explanation}`;
            } else {
                btnEl.classList.add('border-red-500', 'bg-red-50', 'text-red-900');
                btnEl.querySelector('i').className = "fa-solid fa-circle-xmark text-red-600";
                
                // Highlight correct
                allBtns[qData.answer].classList.add('border-emerald-500', 'bg-emerald-50');

                feedback.classList.add('bg-red-50', 'text-red-900', 'border', 'border-red-200');
                feedback.innerHTML = `<i class="fa-solid fa-triangle-exclamation mr-1"></i> <strong>Jawaban Kurang Tepat.</strong> ${qData.explanation}`;
            }

            document.getElementById('quiz-score-badge').innerText = `Skor: ${userScore}`;
            document.getElementById('quiz-next-btn').classList.remove('hidden');
        }

        function showToast(message, type = 'info') {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            
            let bg = 'bg-slate-900 text-white';
            let icon = 'fa-info-circle';
            if (type === 'success') { bg = 'bg-emerald-700 text-white'; icon = 'fa-check-circle'; }
            if (type === 'warning') { bg = 'bg-amber-600 text-white'; icon = 'fa-exclamation-triangle'; }

            toast.className = `p-4 rounded-2xl shadow-xl border border-white/10 ${bg} flex items-center justify-between pointer-events-auto transition-all duration-300 transform translate-y-2 opacity-0`;
            toast.innerHTML = `
                <div class="flex items-center gap-2.5 text-xs font-semibold">
                    <i class="fa-solid ${icon} text-base"></i>
                    <span>${message}</span>
                </div>
                <button onclick="this.parentElement.remove()" class="ml-3 opacity-70 hover:opacity-100">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            `;

            container.appendChild(toast);
            setTimeout(() => {
                toast.classList.remove('translate-y-2', 'opacity-0');
            }, 10);

            setTimeout(() => {
                toast.classList.add('opacity-0', 'translate-y-2');
                setTimeout(() => toast.remove(), 300);
            }, 3500);
        }

        window.addEventListener('DOMContentLoaded', () => {
            // Render Initial Catalog
            renderVarieties();

            // Init Chart
            initComparisonChart();

            // Init Calculator
            calculateFarmNeeds();

            // Init Quiz
            loadQuizQuestion();

            // Search and Filter Events
            document.getElementById('variety-search').addEventListener('input', (e) => {
                const activeFilter = document.querySelector('.variety-filter-btn.bg-brand-600')?.dataset.filter || 'all';
                renderVarieties(activeFilter, e.target.value);
            });

            document.querySelectorAll('.variety-filter-btn').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    document.querySelectorAll('.variety-filter-btn').forEach(b => {
                        b.className = "variety-filter-btn px-4 py-2 rounded-xl text-xs font-bold transition-all bg-white text-slate-600 hover:bg-slate-200 border border-slate-200";
                    });
                    e.target.className = "variety-filter-btn px-4 py-2 rounded-xl text-xs font-bold transition-all bg-brand-600 text-white shadow-sm";
                    
                    const searchQuery = document.getElementById('variety-search').value;
                    renderVarieties(e.target.dataset.filter, searchQuery);
                });
            });

            // Modal Close Events
            document.getElementById('close-variety-modal').addEventListener('click', closeModal);
            document.getElementById('variety-modal').addEventListener('click', (e) => {
                if (e.target.id === 'variety-modal') closeModal();
            });

            // Stepper Tab Switching
            document.querySelectorAll('.step-tab-btn').forEach(btn => {
                btn.addEventListener('click', () => {
                    const step = btn.dataset.step;
                    
                    // Style active tab
                    document.querySelectorAll('.step-tab-btn').forEach(b => {
                        b.className = "step-tab-btn flex-1 min-w-[140px] py-4 px-4 text-center font-bold text-sm border-b-2 border-transparent text-slate-500 hover:text-slate-800 transition-all";
                    });
                    btn.className = "step-tab-btn flex-1 min-w-[140px] py-4 px-4 text-center font-bold text-sm border-b-2 border-brand-600 text-brand-700 bg-white transition-all";

                    // Show content
                    document.querySelectorAll('.step-content').forEach(c => c.classList.add('hidden'));
                    document.getElementById(`step-content-${step}`).classList.remove('hidden');
                });
            });

            // Calculator triggers
            document.getElementById('btn-calculate').addEventListener('click', calculateFarmNeeds);
            document.getElementById('land-size').addEventListener('input', calculateFarmNeeds);
            document.getElementById('land-unit').addEventListener('change', calculateFarmNeeds);
            document.getElementById('spacing-type').addEventListener('change', calculateFarmNeeds);
            document.getElementById('calc-variety').addEventListener('change', calculateFarmNeeds);

            // Copy calculation summary
            document.getElementById('btn-copy-calc').addEventListener('click', () => {
                const seed = document.getElementById('out-seed').innerText;
                const yieldEst = document.getElementById('out-yield').innerText;
                const urea = document.getElementById('out-urea').innerText;
                const sp36 = document.getElementById('out-sp36').innerText;
                const kcl = document.getElementById('out-kcl').innerText;
                const compost = document.getElementById('out-compost').innerText;

                const text = `--- RINGKASAN KEBUTUHAN PADI GOGO (AGROGOGO) ---\nKebutuhan Benih: ${seed}\nEstimasi Hasil Panen: ${yieldEst}\nPupuk Urea: ${urea}\nPupuk SP-36: ${sp36}\nPupuk KCl: ${kcl}\nPupuk Organik: ${compost}`;

                const dummy = document.createElement("textarea");
                document.body.appendChild(dummy);
                dummy.value = text;
                dummy.select();
                document.execCommand("copy");
                document.body.removeChild(dummy);

                showToast('Ringkasan berhasil disalin ke Clipboard!', 'success');
            });

            // Quiz Next
            document.getElementById('quiz-next-btn').addEventListener('click', () => {
                currentQuestion++;
                if (currentQuestion < quizQuestions.length) {
                    loadQuizQuestion();
                } else {
                    // Show final score screen
                    document.getElementById('quiz-screen').classList.add('hidden');
                    document.getElementById('quiz-result-screen').classList.remove('hidden');
                    document.getElementById('final-score').innerText = `${userScore} / 100`;

                    let comment = "Bagus! Terus tingkatkan pemahaman Anda.";
                    if (userScore >= 80) comment = "Sangat Luar Biasa! Anda Mahir Padi Gogo!";
                    else if (userScore <= 40) comment = "Pelajari kembali modul budidaya di atas ya!";

                    document.getElementById('score-comment').innerText = comment;
                }
            });

            // Quiz Restart
            document.getElementById('quiz-restart-btn').addEventListener('click', () => {
                currentQuestion = 0;
                userScore = 0;
                document.getElementById('quiz-result-screen').classList.add('hidden');
                document.getElementById('quiz-screen').classList.remove('hidden');
                loadQuizQuestion();
            });

            // Mobile Menu Drawer
            const mobileBtn = document.getElementById('mobile-menu-btn');
            const mobileMenu = document.getElementById('mobile-menu');
            mobileBtn.addEventListener('click', () => {
                mobileMenu.classList.toggle('hidden');
            });

            document.querySelectorAll('.mobile-nav-link').forEach(link => {
                link.addEventListener('click', () => mobileMenu.classList.add('hidden'));
            });
        });
    </script>
</body>
</html>
