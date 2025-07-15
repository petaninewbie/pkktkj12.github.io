# pkktkj12.github.io
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dasbor Interaktif: Konsep Produksi Massal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Warm Neutrals with Teal Accent -->
    <!-- Application Structure Plan: Aplikasi ini dirancang sebagai dasbor interaktif dengan navigasi berbasis tab, bukan sebagai presentasi linier. Struktur ini (Pengantar, Perencanaan, Peramalan, Proses & Keberhasilan) memungkinkan pengguna untuk secara bebas menjelajahi topik yang diminati, meningkatkan keterlibatan dan pemahaman. Tata letak tematik ini lebih intuitif untuk eksplorasi mandiri dibandingkan urutan slide yang kaku, sehingga pengguna dapat langsung menuju informasi yang paling relevan bagi mereka. -->
    <!-- Visualization & Content Choices: 
        - Pengantar: Menggunakan kartu untuk definisi (Inform) dan layout dua kolom untuk perbandingan pro/kontra (Compare). Interaksi hover sederhana untuk fokus.
        - Perencanaan: Diagram alir horisontal interaktif (Organize/Inform) dibuat dengan HTML/CSS untuk menyajikan langkah-langkah perencanaan. Ini lebih menarik daripada daftar statis.
        - Peramalan: Bagan garis dinamis (Change/Inform) dengan Chart.js digunakan untuk memvisualisasikan komponen deret waktu, memungkinkan pengguna untuk melihat dampak setiap elemen secara terpisah.
        - Proses & Keberhasilan: Bagan batang (Compare) dengan Chart.js digunakan untuk metrik OEE, dan diagram alir vertikal (Organize) dengan HTML/CSS untuk proses perakitan. Visualisasi ini menyederhanakan konsep yang kompleks.
        - Semua pilihan ini menghindari SVG/Mermaid dan mengutamakan interaktivitas untuk mengubah presentasi pasif menjadi pengalaman belajar aktif. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body { font-family: 'Inter', sans-serif; }
        .tab-btn.active { 
            border-color: #0d9488; 
            background-color: #ccfbf1;
            color: #134e4a;
            font-weight: 600;
        }
        .tab-content { display: none; }
        .tab-content.active { display: block; }
        .flowchart-step { transition: all 0.3s ease; }
        .flowchart-step:hover { transform: translateY(-5px); box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05); }
        .chart-container { position: relative; width: 100%; max-width: 600px; margin-left: auto; margin-right: auto; height: 320px; max-height: 400px; }
        @media (min-width: 640px) {
            .chart-container { height: 350px; }
        }
    </style>
</head>
<body class="bg-gray-50 text-gray-800">

    <div class="container mx-auto p-4 sm:p-6 lg:p-8">
        
        <header class="text-center mb-8">
            <h1 class="text-3xl sm:text-4xl font-bold text-teal-800">Menjelajahi Produksi Massal</h1>
            <p class="mt-2 text-lg text-gray-600">Sebuah Tinjauan Interaktif Konsep, Perencanaan, dan Proses</p>
        </header>

        <nav class="flex flex-wrap justify-center gap-2 sm:gap-4 mb-8">
            <button class="tab-btn active text-sm sm:text-base font-medium py-2 px-4 rounded-lg border-2 border-transparent transition-colors duration-300" onclick="switchTab('pengantar')">1. Pengantar</button>
            <button class="tab-btn text-sm sm:text-base font-medium py-2 px-4 rounded-lg border-2 border-transparent transition-colors duration-300" onclick="switchTab('perencanaan')">2. Perencanaan</button>
            <button class="tab-btn text-sm sm:text-base font-medium py-2 px-4 rounded-lg border-2 border-transparent transition-colors duration-300" onclick="switchTab('peramalan')">3. Peramalan</button>
            <button class="tab-btn text-sm sm:text-base font-medium py-2 px-4 rounded-lg border-2 border-transparent transition-colors duration-300" onclick="switchTab('proses')">4. Proses & Keberhasilan</button>
        </nav>

        <main>
            <!-- Section 1: Pengantar -->
            <div id="pengantar" class="tab-content active">
                <div class="bg-white p-6 rounded-xl shadow-md">
                    <h2 class="text-2xl font-bold text-teal-700 mb-4">Memahami Dasar-Dasar Produksi Massal</h2>
                    <p class="mb-6 text-gray-600">Bagian ini memperkenalkan konsep fundamental produksi massal. Anda akan mempelajari definisi inti, karakteristik utama yang membedakannya dari jenis produksi lain, serta menimbang kelebihan dan kekurangannya. Ini adalah fondasi untuk memahami mengapa dan bagaimana produksi massal diterapkan di berbagai industri.</p>
                    
                    <div class="grid md:grid-cols-2 gap-6 mb-6">
                        <div class="bg-teal-50 p-4 rounded-lg">
                            <h3 class="font-bold text-lg text-teal-800 mb-2">Definisi Produksi</h3>
                            <p>Kegiatan menambah nilai guna suatu benda atau menciptakan benda baru untuk memenuhi kebutuhan.</p>
                        </div>
                        <div class="bg-teal-50 p-4 rounded-lg">
                            <h3 class="font-bold text-lg text-teal-800 mb-2">Definisi Produksi Massal</h3>
                            <p>Kegiatan memproduksi barang dengan spesifikasi standar dalam jumlah besar, menggunakan serangkaian operasi yang sama dan berulang.</p>
                        </div>
                    </div>

                    <div class="grid md:grid-cols-2 gap-6">
                        <div class="bg-gray-100 p-6 rounded-lg">
                            <h3 class="text-xl font-semibold mb-3 text-gray-700">Ciri Khas</h3>
                            <ul class="space-y-2 list-disc list-inside text-gray-600">
                                <li>Produk dalam jumlah besar</li>
                                <li>Biaya per unit rendah</li>
                                <li>Bertujuan menguasai pasar</li>
                                <li>Dijual di pasar bebas</li>
                                <li>Hampir tidak ada variasi produk</li>
                                <li>Memerlukan stok untuk masa tunggu</li>
                            </ul>
                        </div>

                        <div class="grid grid-rows-2 gap-6">
                            <div class="bg-green-100 p-4 rounded-lg">
                                <h3 class="text-lg font-semibold text-green-800 mb-2">Kelebihan 👍</h3>
                                <ul class="space-y-1 list-disc list-inside text-green-700">
                                    <li>Hemat biaya produksi</li>
                                    <li>Efisiensi waktu tinggi</li>
                                    <li>Tingkat keakuratan produk konsisten</li>
                                    <li>Tingkat produksi sangat cepat</li>
                                </ul>
                            </div>
                            <div class="bg-red-100 p-4 rounded-lg">
                                <h3 class="text-lg font-semibold text-red-800 mb-2">Kekurangan 👎</h3>
                                <ul class="space-y-1 list-disc list-inside text-red-700">
                                    <li>Proses produksi sangat kaku</li>
                                    <li>Variasi produk sangat terbatas</li>
                                    <li>Biaya awal untuk mesin mahal</li>
                                    <li>Risiko produk tidak laku di pasar</li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Section 2: Perencanaan -->
            <div id="perencanaan" class="tab-content">
                <div class="bg-white p-6 rounded-xl shadow-md">
                     <h2 class="text-2xl font-bold text-teal-700 mb-4">Jantung Operasi: Perencanaan Produksi</h2>
                    <p class="mb-6 text-gray-600">Perencanaan adalah cetak biru dari seluruh kegiatan produksi massal. Di bagian ini, kita akan membedah proses perencanaan, mulai dari definisi dan ruang lingkupnya, hingga faktor-faktor internal dan eksternal yang memengaruhinya. Puncaknya adalah visualisasi langkah-langkah kunci dalam merencanakan sebuah produksi, dari ide hingga skala produksi.</p>

                    <div class="grid md:grid-cols-2 gap-6 mb-6">
                        <div class="bg-gray-100 p-4 rounded-lg">
                             <h3 class="text-lg font-semibold text-gray-700 mb-2">Tujuan Perencanaan</h3>
                             <ul class="space-y-1 list-disc list-inside text-sm">
                                <li>Meminimalkan biaya, memaksimalkan laba</li>
                                <li>Memaksimalkan kepuasan pelanggan</li>
                                <li>Menjaga kestabilan nilai produksi & tenaga kerja</li>
                                <li>Memaksimalkan utilisasi pabrik</li>
                             </ul>
                        </div>
                        <div class="bg-gray-100 p-4 rounded-lg">
                             <h3 class="text-lg font-semibold text-gray-700 mb-2">Faktor Pengaruh</h3>
                             <p class="font-semibold text-gray-600">Internal:</p>
                             <p class="text-sm mb-2">Kapasitas mesin, produktivitas pekerja, kemampuan pengadaan.</p>
                             <p class="font-semibold text-gray-600">Eksternal:</p>
                             <p class="text-sm">Kebijakan pemerintah, inflasi, bencana alam.</p>
                        </div>
                    </div>

                    <h3 class="text-xl font-semibold text-center mb-2 text-gray-700">Langkah-Langkah Perencanaan Produksi</h3>
                    <p class="text-center text-gray-500 mb-6">Jelajahi setiap tahap dalam proses perencanaan produksi massal.</p>
                    <div class="flex flex-col md:flex-row justify-between items-center gap-4 text-center">
                        <div class="flowchart-step bg-teal-100 p-4 rounded-lg w-full md:w-1/3">
                            <div class="text-2xl mb-2">🔬</div>
                            <h4 class="font-bold">1. Penelitian & Pengembangan</h4>
                            <p class="text-sm text-teal-800">Menganalisis proses dan produk yang akan dibuat.</p>
                        </div>
                        <div class="text-2xl text-teal-500 hidden md:block">&rarr;</div>
                        <div class="flowchart-step bg-teal-100 p-4 rounded-lg w-full md:w-1/3">
                            <div class="text-2xl mb-2">💡</div>
                            <h4 class="font-bold">2. Mencari Gagasan & Seleksi</h4>
                            <p class="text-sm text-teal-800">Dari ide, seleksi, desain awal, pengujian, hingga desain akhir.</p>
                        </div>
                        <div class="text-2xl text-teal-500 hidden md:block">&rarr;</div>
                        <div class="flowchart-step bg-teal-100 p-4 rounded-lg w-full md:w-1/3">
                            <div class="text-2xl mb-2">📈</div>
                            <h4 class="font-bold">3. Menetapkan Skala Produksi</h4>
                            <p class="text-sm text-teal-800">Menentukan waktu, kualitas, biaya, tenaga kerja, dan bahan baku.</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Section 3: Peramalan -->
            <div id="peramalan" class="tab-content">
                <div class="bg-white p-6 rounded-xl shadow-md">
                    <h2 class="text-2xl font-bold text-teal-700 mb-4">Memprediksi Masa Depan: Peramalan Permintaan</h2>
                     <p class="mb-6 text-gray-600">Peramalan adalah upaya memperkirakan kebutuhan pasar di masa depan. Bagian ini menjelaskan pentingnya peramalan dan metode yang digunakan. Anda dapat berinteraksi dengan visualisasi komponen-komponen utama dalam analisis deret waktu untuk memahami bagaimana tren, siklus, musim, dan variasi acak memengaruhi permintaan pasar.</p>
                    
                     <h3 class="text-xl font-semibold text-center mb-2 text-gray-700">Analisis Deret Waktu</h3>
                     <p class="text-center text-gray-500 mb-6">Visualisasi komponen yang memengaruhi peramalan permintaan dari waktu ke waktu.</p>
                    <div class="chart-container">
                        <canvas id="forecastingChart"></canvas>
                    </div>
                    <div class="text-center mt-4">
                        <p class="text-sm text-gray-500">Gunakan legenda di atas bagan untuk menampilkan/menyembunyikan setiap komponen.</p>
                    </div>
                </div>
            </div>

            <!-- Section 4: Proses & Keberhasilan -->
            <div id="proses" class="tab-content">
                <div class="bg-white p-6 rounded-xl shadow-md">
                    <h2 class="text-2xl font-bold text-teal-700 mb-4">Dari Konsep ke Produk: Proses & Indikator Keberhasilan</h2>
                    <p class="mb-6 text-gray-600">Bagian terakhir ini membawa kita ke lantai produksi. Kita akan melihat bagaimana sebuah produk dirakit melalui tahapan proses yang terstruktur, dengan mengambil contoh perakitan sepeda motor. Selain itu, kita akan mempelajari bagaimana keberhasilan produksi diukur melalui indikator kinerja utama seperti OEE (*Overall Equipment Effectiveness*).</p>

                    <div class="grid md:grid-cols-2 gap-8">
                        <div>
                            <h3 class="text-xl font-semibold text-center mb-2 text-gray-700">Indikator Kinerja Mesin (OEE)</h3>
                            <p class="text-center text-gray-500 mb-4">Mengukur efektivitas peralatan produksi secara keseluruhan.</p>
                             <div class="chart-container" style="height:280px; max-height:300px;">
                                <canvas id="oeeChart"></canvas>
                            </div>
                        </div>

                        <div>
                            <h3 class="text-xl font-semibold text-center mb-2 text-gray-700">Tahapan Proses Produksi</h3>
                            <p class="text-center text-gray-500 mb-4">(Contoh: Perakitan Sepeda Motor)</p>
                            <div class="space-y-2 text-sm">
                                <div class="flowchart-step bg-gray-100 p-2 rounded-md flex items-center gap-3">
                                    <span class="bg-teal-600 text-white rounded-full flex items-center justify-center w-6 h-6 font-bold">1</span><span>Penyediaan Komponen</span>
                                </div>
                                <div class="flowchart-step bg-gray-100 p-2 rounded-md flex items-center gap-3">
                                    <span class="bg-teal-600 text-white rounded-full flex items-center justify-center w-6 h-6 font-bold">2</span><span>Injeksi Plastik & Pengelasan</span>
                                </div>
                                <div class="flowchart-step bg-gray-100 p-2 rounded-md flex items-center gap-3">
                                    <span class="bg-teal-600 text-white rounded-full flex items-center justify-center w-6 h-6 font-bold">3</span><span>Pengecatan & Pelapisan</span>
                                </div>
                                <div class="flowchart-step bg-gray-100 p-2 rounded-md flex items-center gap-3">
                                    <span class="bg-teal-600 text-white rounded-full flex items-center justify-center w-6 h-6 font-bold">4</span><span>Sub-Assembling & Assembling</span>
                                </div>
                                <div class="flowchart-step bg-gray-100 p-2 rounded-md flex items-center gap-3">
                                    <span class="bg-teal-600 text-white rounded-full flex items-center justify-center w-6 h-6 font-bold">5</span><span>Final Inspection & Shipping</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

        </main>
        
        <footer class="text-center mt-12">
            <p class="text-sm text-gray-500">Aplikasi Interaktif dibuat berdasarkan "Modul Produk Kreatif dan Kewirausahaan untuk SMK".</p>
        </footer>

    </div>

    <script>
        const tabs = document.querySelectorAll('.tab-btn');
        const contents = document.querySelectorAll('.tab-content');
        let forecastingChartInstance, oeeChartInstance;

        function switchTab(tabId) {
            contents.forEach(content => {
                content.classList.remove('active');
                if (content.id === tabId) {
                    content.classList.add('active');
                }
            });

            tabs.forEach(tab => {
                tab.classList.remove('active');
                if (tab.getAttribute('onclick').includes(tabId)) {
                    tab.classList.add('active');
                }
            });
            
            // Render charts only when their tab is active to save resources
            if (tabId === 'peramalan' && !forecastingChartInstance) {
                renderForecastingChart();
            }
            if (tabId === 'proses' && !oeeChartInstance) {
                renderOeeChart();
            }
        }

        function generateChartData() {
            const labels = Array.from({ length: 12 }, (_, i) => `Bulan ${i + 1}`);
            const trend = labels.map((_, i) => 50 + i * 4);
            const seasonality = labels.map((_, i) => 20 * Math.sin(i * (Math.PI / 6)));
            const cycle = labels.map((_, i) => 10 * Math.cos(i * (Math.PI / 12)));
            const random = labels.map(() => Math.random() * 10 - 5);
            const total = labels.map((_, i) => trend[i] + seasonality[i] + cycle[i] + random[i]);
            return { labels, trend, seasonality, cycle, random, total };
        }

        function renderForecastingChart() {
            const ctx = document.getElementById('forecastingChart').getContext('2d');
            const data = generateChartData();
            
            forecastingChartInstance = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: data.labels,
                    datasets: [
                        {
                            label: 'Permintaan Aktual',
                            data: data.total,
                            borderColor: '#0d9488',
                            backgroundColor: 'rgba(13, 148, 136, 0.1)',
                            borderWidth: 3,
                            tension: 0.3,
                            fill: true,
                        },
                        {
                            label: 'Tren (T)',
                            data: data.trend,
                            borderColor: '#f97316',
                            borderWidth: 2,
                            borderDash: [5, 5],
                            hidden: true,
                        },
                        {
                            label: 'Pola Musiman (S)',
                            data: data.seasonality,
                            borderColor: '#3b82f6',
                            borderWidth: 2,
                            hidden: true,
                        },
                         {
                            label: 'Siklus (C)',
                            data: data.cycle,
                            borderColor: '#8b5cf6',
                            borderWidth: 2,
                            borderDash: [2, 2],
                            hidden: true,
                        },
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { position: 'top' },
                        tooltip: {
                            mode: 'index',
                            intersect: false,
                        },
                        title: {
                            display: false,
                            text: 'Analisis Komponen Deret Waktu'
                        }
                    },
                    scales: {
                        y: { beginAtZero: true, title: { display: true, text: 'Unit Permintaan' } },
                        x: { title: { display: true, text: 'Waktu' } }
                    }
                }
            });
        }
        
        function renderOeeChart(){
            const ctx = document.getElementById('oeeChart').getContext('2d');
            oeeChartInstance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['Availability', 'Performance', 'Quality'],
                    datasets: [{
                        label: 'Persentase Kinerja (%)',
                        data: [90, 95, 99],
                        backgroundColor: [
                            'rgba(54, 162, 235, 0.6)',
                            'rgba(75, 192, 192, 0.6)',
                            'rgba(255, 206, 86, 0.6)'
                        ],
                        borderColor: [
                            'rgba(54, 162, 235, 1)',
                            'rgba(75, 192, 192, 1)',
                            'rgba(255, 206, 86, 1)'
                        ],
                        borderWidth: 1
                    }]
                },
                options: {
                    indexAxis: 'y',
                    responsive: true,
                    maintainAspectRatio: false,
                     plugins: {
                        legend: { display: false },
                        title: { display: false }
                    },
                    scales: {
                        x: {
                            beginAtZero: true,
                            max: 100,
                            title: { display: true, text: 'Efektivitas (%)' }
                        }
                    }
                }
            });
        }
        
        // Initial call for the first tab
        switchTab('pengantar');
    </script>

</body>
</html>
