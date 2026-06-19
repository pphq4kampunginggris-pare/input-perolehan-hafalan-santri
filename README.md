<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Perolehan Hafalan Santri - PPHQ PUTRI 4</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.29/jspdf.plugin.autotable.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Plus Jakarta Sans', 'sans-serif'],
                    }
                }
            }
        }
    </script>
</head>
<body class="bg-slate-50 font-sans min-h-screen text-slate-800 flex flex-col antialiased">

    <div class="container mx-auto px-4 py-6 max-w-7xl flex-grow">
        <!-- HEADER -->
        <header class="text-center mb-8 bg-gradient-to-r from-emerald-800 to-teal-700 text-white p-8 rounded-3xl shadow-lg relative overflow-hidden">
            <div class="absolute inset-0 bg-[radial-gradient(circle_at_30%_20%,rgba(255,255,255,0.1),transparent_50%)]"></div>
            <div class="relative z-10">
                <span class="inline-block px-4 py-1.5 bg-emerald-900/40 text-emerald-100 rounded-full text-xs font-bold tracking-wider uppercase mb-2">Sistem Informasi Tahfidz</span>
                <h1 class="text-3xl md:text-4xl font-extrabold tracking-wide">PEROLEHAN HAFALAN SANTRI</h1>
                <p class="text-teal-100 text-base md:text-lg mt-2 font-medium">PPHQ PUTRI 4 (Pondok Pesantren Hamalatul Quran Putri 4)</p>
            </div>
        </header>

        <!-- STATS DASHBOARD -->
        <div class="grid grid-cols-2 lg:grid-cols-4 gap-4 mb-8">
            <div class="bg-white p-5 rounded-2xl shadow-sm border border-slate-100 flex items-center gap-4">
                <div class="w-12 h-12 rounded-xl bg-emerald-50 text-emerald-500 flex items-center justify-center text-xl font-bold">🕌</div>
                <div>
                    <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Total Santri</p>
                    <h3 id="statTotalSantri" class="text-xl font-extrabold text-slate-800">0</h3>
                </div>
            </div>
            <div class="bg-white p-5 rounded-2xl shadow-sm border border-slate-100 flex items-center gap-4">
                <div class="w-12 h-12 rounded-xl bg-blue-50 text-blue-600 flex items-center justify-center text-xl font-bold">📚</div>
                <div>
                    <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Status Ziyadah</p>
                    <h3 id="statZiyadah" class="text-xl font-extrabold text-slate-800">0</h3>
                </div>
            </div>
            <div class="bg-white p-5 rounded-2xl shadow-sm border border-slate-100 flex items-center gap-4">
                <div class="w-12 h-12 rounded-xl bg-amber-50 text-amber-600 flex items-center justify-center text-xl font-bold">🔁</div>
                <div>
                    <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Murojaah Active</p>
                    <h3 id="statMurojaah" class="text-xl font-extrabold text-slate-800">0</h3>
                </div>
            </div>
            <div class="bg-white p-5 rounded-2xl shadow-sm border border-slate-100 flex items-center gap-4">
                <div class="w-12 h-12 rounded-xl bg-purple-50 text-purple-600 flex items-center justify-center text-xl font-bold">✨</div>
                <div>
                    <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Dauroh Tasmik</p>
                    <h3 id="statTasmik" class="text-xl font-extrabold text-slate-800">0</h3>
                </div>
            </div>
        </div>

        <!-- MAIN LAYOUT: Form vs Table -->
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            
            <!-- COLUMN LEFT: Form Input -->
            <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-100 h-fit">
                <h2 id="formTitle" class="text-xl font-bold mb-4 text-emerald-800 border-b border-slate-100 pb-3 flex items-center gap-2">
                    <span>✍️</span> Input Data Hafalan Santri
                </h2>
                <form id="hafalanForm" class="space-y-4">
                    <input type="hidden" id="editIndex" value="">

                    <!-- Row 1: Nama & Kategori Santri -->
                    <div class="grid grid-cols-3 gap-3">
                        <div class="col-span-2">
                            <label class="block text-xs font-bold text-slate-500 uppercase mb-1">Nama Santri</label>
                            <input type="text" id="nama" required class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-emerald-500 text-sm transition" placeholder="Nama santri">
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-slate-500 uppercase mb-1">Kategori Santri</label>
                            <select id="kategori" required class="w-full px-3 py-2 border border-slate-200 rounded-xl bg-white focus:outline-none focus:ring-2 focus:ring-emerald-500 text-sm transition">
                                <option value="Reguler">Reguler</option>
                                <option value="Dauroh Tasmik">Dauroh Tasmik</option>
                            </select>
                        </div>
                    </div>

                    <!-- Row 2: Setoran Awal & Setoran Akhir -->
                    <div class="grid grid-cols-2 gap-3">
                        <div>
                            <label class="block text-xs font-bold text-slate-500 uppercase mb-1">Setoran Awal</label>
                            <input type="text" id="awalSetoran" required class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-emerald-500 text-sm transition" placeholder="juz 2 hlm 5">
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-slate-500 uppercase mb-1">Setoran Akhir</label>
                            <input type="text" id="akhirSetoran" required class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-emerald-500 text-sm transition" placeholder="juz 2 hlm 10">
                        </div>
                    </div>

                    <!-- Row 3: Minggu Ini & Total Perolehan -->
                    <div class="grid grid-cols-2 gap-3">
                        <div>
                            <label class="block text-xs font-bold text-slate-500 uppercase mb-1">Minggu Ini</label>
                            <input type="text" id="mingguIni" required class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-emerald-500 text-sm transition" placeholder="Contoh: 15 hlm/1 Juz">
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-slate-500 uppercase mb-1">Total Perolehan</label>
                            <input type="text" id="totalPerolehan" required class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-emerald-500 text-sm transition" placeholder="1 Juz 10 hlm">
                        </div>
                    </div>

                    <!-- Row 4: Target Mingguan & Pencapaian Target -->
                    <div class="grid grid-cols-2 gap-3">
                        <div>
                            <label class="block text-xs font-bold text-slate-500 uppercase mb-1">Target Mingguan</label>
                            <select id="targetMingguan" required class="w-full px-3 py-2 border border-slate-200 rounded-xl bg-white focus:outline-none focus:ring-2 focus:ring-emerald-500 text-sm transition">
                                <option value="3/4 Juz">3/4 Juz</option>
                                <option value="1 Juz">1 Juz</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-slate-500 uppercase mb-1">Pencapaian Target</label>
                            <select id="pencapaianTarget" required class="w-full px-3 py-2 border border-slate-200 rounded-xl bg-white focus:outline-none focus:ring-2 focus:ring-emerald-500 text-sm transition">
                                <option value="Tercapai">Tercapai</option>
                                <option value="Belum Tercapai" selected>Belum Tercapai</option>
                            </select>
                        </div>
                    </div>

                    <!-- Row 5: Terakhir Tasmik & Status -->
                    <div class="grid grid-cols-2 gap-3">
                        <div>
                            <label class="block text-xs font-bold text-slate-500 uppercase mb-1">Terakhir Tasmik</label>
                            <input type="text" id="terakhirTasmik" class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-emerald-500 text-sm transition" placeholder="10 Juz">
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-slate-500 uppercase mb-1">Status Hafalan</label>
                            <select id="statusHafalan" required class="w-full px-3 py-2 border border-slate-200 rounded-xl bg-white focus:outline-none focus:ring-2 focus:ring-emerald-500 text-sm transition">
                                <option value="" disabled selected hidden>Pilih status...</option>
                                <option value="Iqro">Iqro</option>
                                <option value="Binnadzor">Binnadzor</option>
                                <option value="Ziyadah">Ziyadah</option>
                                <option value="Murojaah 1">Murojaah 1</option>
                                <option value="Murojaah 2">Murojaah 2</option>
                                <option value="Murojaah 3">Murojaah 3</option>
                                <option value="Dauroh Tasmik">Dauroh Tasmik</option>
                            </select>
                        </div>
                    </div>

                    <!-- Row 6: Guru Pengampu (Ustazah) -->
                    <div>
                        <label class="block text-xs font-bold text-slate-500 uppercase mb-1">Ustazah Pengampu / Penyimak</label>
                        <select id="guru" required class="w-full px-3 py-2 border border-slate-200 rounded-xl bg-white focus:outline-none focus:ring-2 focus:ring-emerald-500 text-sm transition">
                            <option value="" disabled selected hidden>Pilih nama ustazah di sini...</option>
                            <option value="Ustazah Ayu Umairoh">Ustazah Ayu Umairoh</option>
                            <option value="Ustazah Ayuniz Zakia">Ustazah Ayuniz Zakia</option>
                            <option value="Ustazah Rima Niswa">Ustazah Rima Niswa</option>
                            <option value="Ustazah Durotun Nafisah">Ustazah Durotun Nafisah</option>
                        </select>
                    </div>

                    <!-- Row 7: Submit & Reset Buttons (No Emojis) -->
                    <div class="grid grid-cols-2 gap-3 pt-2">
                        <button type="button" id="resetFormBtn" class="bg-slate-100 hover:bg-slate-200 text-slate-700 font-semibold py-2.5 rounded-xl transition text-sm cursor-pointer flex items-center justify-center gap-1.5 border border-slate-200">
                            Batal / Reset
                        </button>
                        <button type="submit" id="submitBtn" class="bg-emerald-600 hover:bg-emerald-700 text-white font-semibold py-2.5 rounded-xl transition text-sm shadow-sm cursor-pointer flex items-center justify-center">
                            Simpan Data
                        </button>
                    </div>
                </form>
            </div>

            <!-- COLUMN RIGHT: Table and Controls -->
            <div class="lg:col-span-2 bg-white p-6 rounded-2xl shadow-sm border border-slate-100 flex flex-col justify-between">
                <div>
                    <!-- Filter and Search Header -->
                    <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 mb-6 border-b border-slate-100 pb-4">
                        <h2 class="text-xl font-bold text-emerald-800 flex items-center gap-2">
                            <span>📊</span> Rekapitulasi Hafalan Santri
                        </h2>
                        <button id="downloadPdfBtn" class="bg-rose-600 hover:bg-rose-700 text-white font-medium px-4 py-2 rounded-xl text-xs transition flex items-center gap-1.5 shadow-sm cursor-pointer ml-auto sm:ml-0">
                            <span>📄</span> Unduh PDF Laporan
                        </button>
                    </div>

                    <!-- Search and Filtering Toolbar -->
                    <div class="grid grid-cols-1 sm:grid-cols-5 gap-2 mb-4">
                        <div class="relative">
                            <span class="absolute inset-y-0 left-0 pl-3 flex items-center text-slate-400 pointer-events-none text-xs">🔍</span>
                            <input type="text" id="searchName" placeholder="Cari nama..." class="w-full pl-8 pr-3 py-2 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-emerald-500">
                        </div>
                        <div>
                            <select id="filterKategori" class="w-full px-3 py-2 border border-slate-200 rounded-xl text-xs bg-white focus:outline-none focus:ring-2 focus:ring-emerald-500">
                                <option value="">Semua Kategori Santri</option>
                                <option value="Reguler">Reguler</option>
                                <option value="Dauroh Tasmik">Dauroh Tasmik</option>
                            </select>
                        </div>
                        <div>
                            <select id="filterStatus" class="w-full px-3 py-2 border border-slate-200 rounded-xl text-xs bg-white focus:outline-none focus:ring-2 focus:ring-emerald-500">
                                <option value="">Semua Status</option>
                                <option value="Iqro">Iqro</option>
                                <option value="Binnadzor">Binnadzor</option>
                                <option value="Ziyadah">Ziyadah</option>
                                <option value="Murojaah">Murojaah (Semua)</option>
                                <option value="Dauroh Tasmik">Dauroh Tasmik</option>
                            </select>
                        </div>
                        <div>
                            <select id="filterPencapaian" class="w-full px-3 py-2 border border-slate-200 rounded-xl text-xs bg-white focus:outline-none focus:ring-2 focus:ring-emerald-500">
                                <option value="">Semua Pencapaian</option>
                                <option value="Tercapai">Tercapai</option>
                                <option value="Belum Tercapai">Belum Tercapai</option>
                            </select>
                        </div>
                        <div>
                            <select id="filterGuru" class="w-full px-3 py-2 border border-slate-200 rounded-xl text-xs bg-white focus:outline-none focus:ring-2 focus:ring-emerald-500">
                                <option value="">Semua Ustazah</option>
                                <option value="Ustazah Ayu Umairoh">Ustazah Ayu Umairoh</option>
                                <option value="Ustazah Ayuniz Zakia">Ustazah Ayuniz Zakia</option>
                                <option value="Ustazah Rima Niswa">Ustazah Rima Niswa</option>
                                <option value="Ustazah Durotun Nafisah">Ustazah Durotun Nafisah</option>
                            </select>
                        </div>
                    </div>

                    <!-- Table Container -->
                    <div class="overflow-x-auto rounded-xl border border-slate-100">
                        <table class="w-full text-left border-collapse text-sm">
                            <thead>
                                <tr class="bg-slate-50 text-slate-500 uppercase text-[10px] tracking-wider border-b border-slate-100">
                                    <th class="py-3 px-2 font-bold text-center">No</th>
                                    <th class="py-3 px-2 font-bold text-left">Nama Santri</th>
                                    <th class="py-3 px-2 font-bold text-left">Kategori Santri</th>
                                    <th class="py-3 px-2 font-bold">Setoran Awal</th>
                                    <th class="py-3 px-2 font-bold">Setoran Akhir</th>
                                    <th class="py-3 px-2 text-center font-bold">Target mingguan</th>
                                    <th class="py-3 px-2 text-center font-bold">keterangan</th>
                                    <th class="py-3 px-2 text-center font-bold">Total</th>
                                    <th class="py-3 px-2 text-center font-bold">Terakhir Tasmik</th>
                                    <th class="py-3 px-2 text-center font-bold">Status</th>
                                    <th class="py-3 px-2 font-bold">Penyimak</th>
                                    <th class="py-3 px-2 font-bold text-center">Aksi</th>
                                </tr>
                            </thead>
                            <tbody id="tabelBody" class="divide-y divide-slate-100">
                            </tbody>
                        </table>
                        <div id="emptyState" class="text-center py-12 text-slate-400 text-sm bg-slate-50/50 rounded-b-xl">
                            Belum ada data setoran hafalan santri yang disimpan.
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- FOOTER -->
    <footer class="bg-white border-t border-slate-100 mt-12 py-6">
        <div class="container mx-auto px-4 max-w-7xl text-center text-xs text-slate-400">
            &copy; 2026 PPHQ PUTRI 4 - Pondok Pesantren Hamalatul Quran. All rights reserved.
        </div>
    </footer>

    <!-- CUSTOM TOAST CONTAINER (Replaces Native Alert) -->
    <div id="toastContainer" class="fixed top-5 right-5 z-50 flex flex-col gap-2 max-w-md w-full pointer-events-none"></div>

    <!-- CUSTOM CONFIRM MODAL (Replaces Native Confirm) -->
    <div id="confirmModal" class="fixed inset-0 z-50 bg-slate-900/40 backdrop-blur-sm hidden items-center justify-center p-4">
        <div class="bg-white rounded-2xl max-w-sm w-full p-6 shadow-xl border border-slate-100 animate-in fade-in zoom-in-95 duration-150">
            <h3 class="text-lg font-bold text-slate-800">Konfirmasi Hapus</h3>
            <p id="confirmModalText" class="text-sm text-slate-500 mt-2">Apakah Anda yakin ingin menghapus data hafalan ini secara permanen?</p>
            <div class="mt-6 flex justify-end gap-3">
                <button id="confirmCancelBtn" class="px-4 py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 font-semibold rounded-xl text-xs transition cursor-pointer">
                    Batal
                </button>
                <button id="confirmOkBtn" class="px-4 py-2 bg-rose-600 hover:bg-rose-700 text-white font-semibold rounded-xl text-xs transition cursor-pointer">
                    Hapus Data
                </button>
            </div>
        </div>
    </div>

    <script>
        const STORAGE_KEY = 'data_hafalan_pphq_putri_4_v2';

        let dataHafalan = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];

        // Elements
        const form = document.getElementById('hafalanForm');
        const editIndexInput = document.getElementById('editIndex');
        const formTitle = document.getElementById('formTitle');
        const submitBtn = document.getElementById('submitBtn');
        const tabelBody = document.getElementById('tabelBody');
        const emptyState = document.getElementById('emptyState');
        const downloadPdfBtn = document.getElementById('downloadPdfBtn');
        const resetFormBtn = document.getElementById('resetFormBtn');
        
        // Form field elements
        const namaInput = document.getElementById('nama');
        const kategoriInput = document.getElementById('kategori');
        const awalSetoranInput = document.getElementById('awalSetoran');
        const akhirSetoranInput = document.getElementById('akhirSetoran');
        const mingguIniInput = document.getElementById('mingguIni');
        const totalPerolehanInput = document.getElementById('totalPerolehan');
        const targetMingguanSelect = document.getElementById('targetMingguan');
        const pencapaianTargetSelect = document.getElementById('pencapaianTarget');
        const terakhirTasmikInput = document.getElementById('terakhirTasmik');
        const statusHafalanSelect = document.getElementById('statusHafalan');
        const guruSelect = document.getElementById('guru');

        // Filters
        const searchNameInput = document.getElementById('searchName');
        const filterKategoriInput = document.getElementById('filterKategori');
        const filterStatusInput = document.getElementById('filterStatus');
        const filterPencapaianInput = document.getElementById('filterPencapaian');
        const filterGuruInput = document.getElementById('filterGuru');

        // Confirm Modal variables
        let confirmActionCallback = null;

        // Smart Guess / Asisten Deteksi Pencapaian Otomatis
        function asistenPencapaianOtomatis() {
            const textProgress = mingguIniInput.value.toLowerCase().trim();
            const targetVal = targetMingguanSelect.value;
            
            if (!textProgress) return;

            // Ekstrak angka dari teks minggu ini
            const matchAngka = textProgress.match(/\d+/);
            const jumlahHalaman = matchAngka ? parseInt(matchAngka[0]) : 0;

            if (targetVal === "3/4 Juz") {
                if (
                    jumlahHalaman >= 15 || 
                    textProgress.includes("3/4 juz") || 
                    textProgress.includes("0.75 juz") || 
                    textProgress.includes("1 juz") || 
                    textProgress.includes("tercapai") || 
                    textProgress.includes("tuntas") || 
                    textProgress.includes("lulus")
                ) {
                    pencapaianTargetSelect.value = "Tercapai";
                } else {
                    pencapaianTargetSelect.value = "Belum Tercapai";
                }
            } else if (targetVal === "1 Juz") {
                if (
                    jumlahHalaman >= 20 || 
                    (textProgress.includes("1 juz") && !textProgress.includes("setengah")) || 
                    textProgress.includes("tercapai") || 
                    textProgress.includes("tuntas") || 
                    textProgress.includes("lulus")
                ) {
                    pencapaianTargetSelect.value = "Tercapai";
                } else {
                    pencapaianTargetSelect.value = "Belum Tercapai";
                }
            }
        }

        // Hubungkan asisten deteksi ke input & select target
        mingguIniInput.addEventListener('input', asistenPencapaianOtomatis);
        targetMingguanSelect.addEventListener('change', asistenPencapaianOtomatis);

        // Custom notification system (Toast)
        function showToast(message, type = 'success') {
            const container = document.getElementById('toastContainer');
            const toast = document.createElement('div');
            toast.className = `p-4 rounded-xl shadow-md text-xs font-semibold text-white pointer-events-auto flex items-center justify-between gap-3 transform translate-y-2 opacity-0 transition-all duration-300 ${
                type === 'success' ? 'bg-emerald-600' : type === 'danger' ? 'bg-rose-600' : 'bg-amber-500'
            }`;
            
            let icon = '✨';
            if (type === 'danger') icon = '⚠️';
            if (type === 'warning') icon = '🔔';

            toast.innerHTML = `
                <div class="flex items-center gap-2">
                    <span>${icon}</span>
                    <span>${message}</span>
                </div>
                <button class="text-white/80 hover:text-white transition" onclick="this.parentElement.remove()">✕</button>
            `;

            container.appendChild(toast);
            
            // Trigger animation
            setTimeout(() => {
                toast.classList.remove('translate-y-2', 'opacity-0');
            }, 10);

            // Auto dismiss
            setTimeout(() => {
                toast.classList.add('translate-y-2', 'opacity-0');
                setTimeout(() => toast.remove(), 300);
            }, 4000);
        }

        // Custom Confirm Modal Handler
        function showConfirmModal(text, onConfirm) {
            const modal = document.getElementById('confirmModal');
            document.getElementById('confirmModalText').innerText = text;
            modal.classList.remove('hidden');
            modal.classList.add('flex');
            confirmActionCallback = onConfirm;
        }

        function closeConfirmModal() {
            const modal = document.getElementById('confirmModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
            confirmActionCallback = null;
        }

        document.getElementById('confirmCancelBtn').addEventListener('click', closeConfirmModal);
        document.getElementById('confirmOkBtn').addEventListener('click', () => {
            if (confirmActionCallback) confirmActionCallback();
            closeConfirmModal();
        });

        function updateStats() {
            // Unique Santri Count
            const uniqueSantri = new Set(dataHafalan.map(item => item.nama.trim().toLowerCase()));
            document.getElementById('statTotalSantri').innerText = uniqueSantri.size;

            // Ziyadah Count
            const ziyadahCount = dataHafalan.filter(item => item.status === 'Ziyadah').length;
            document.getElementById('statZiyadah').innerText = ziyadahCount;

            // Murojaah Active (Murojaah 1, 2, or 3)
            const murojaahCount = dataHafalan.filter(item => item.status && item.status.includes('Murojaah')).length;
            document.getElementById('statMurojaah').innerText = murojaahCount;

            // Dauroh Tasmik Count
            const tasmikCount = dataHafalan.filter(item => item.status === 'Dauroh Tasmik').length;
            document.getElementById('statTasmik').innerText = tasmikCount;
        }

        function saveData() {
            localStorage.setItem(STORAGE_KEY, JSON.stringify(dataHafalan));
            updateStats();
        }

        // Get currently filtered data
        function getFilteredData() {
            const query = searchNameInput.value.toLowerCase().trim();
            const kategoriFilter = filterKategoriInput.value;
            const statusFilter = filterStatusInput.value;
            const pencapaianFilter = filterPencapaianInput.value;
            const guruFilter = filterGuruInput.value;

            return dataHafalan.filter(item => {
                const matchesSearch = item.nama.toLowerCase().includes(query);
                
                const itemKategori = item.kategori || "Reguler";
                const matchesKategori = kategoriFilter ? itemKategori === kategoriFilter : true;
                
                let matchesStatus = true;
                if (statusFilter) {
                    if (statusFilter === 'Murojaah') {
                        matchesStatus = item.status && item.status.includes('Murojaah');
                    } else {
                        matchesStatus = item.status === statusFilter;
                    }
                }

                const itemPencapaian = item.pencapaianTarget || "Belum Tercapai";
                const matchesPencapaian = pencapaianFilter ? itemPencapaian === pencapaianFilter : true;

                const matchesGuru = guruFilter ? item.guru === guruFilter : true;

                return matchesSearch && matchesKategori && matchesStatus && matchesPencapaian && matchesGuru;
            });
        }

        function updateTable() {
            tabelBody.innerHTML = '';
            const filteredData = getFilteredData();

            if (filteredData.length === 0) {
                emptyState.classList.remove('hidden');
            } else {
                emptyState.classList.add('hidden');
                
                filteredData.forEach((item, index) => {
                    const actualIndex = dataHafalan.indexOf(item);

                    let statusColor = 'bg-slate-100 text-slate-700';
                    if(item.status === 'Ziyadah') statusColor = 'bg-blue-50 text-blue-700 border border-blue-100';
                    else if(item.status && item.status.includes('Murojaah')) statusColor = 'bg-amber-50 text-amber-700 border border-amber-100';
                    else if(item.status === 'Dauroh Tasmik') statusColor = 'bg-purple-50 text-purple-700 border border-purple-100';
                    else if(item.status === 'Iqro') statusColor = 'bg-rose-50 text-rose-700 border border-rose-100';
                    else if(item.status === 'Binnadzor') statusColor = 'bg-emerald-50 text-emerald-700 border border-emerald-100';

                    const displayKategori = item.kategori || "Reguler";
                    const displayTarget = item.targetMingguan || "3/4 Juz";
                    const displayPencapaian = item.pencapaianTarget || "Belum Tercapai";

                    let pencapaianBadge = '';
                    if (displayPencapaian === "Tercapai") {
                        pencapaianBadge = '<span class="px-2 py-0.5 rounded-full text-[10px] font-bold bg-emerald-100 text-emerald-800 border border-emerald-200">🏆 Tercapai</span>';
                    } else {
                        pencapaianBadge = '<span class="px-2 py-0.5 rounded-full text-[10px] font-bold bg-rose-50 text-rose-700 border border-rose-100">⏳ Belum</span>';
                    }

                    // Rata kiri diatur pada kolom Nama Santri (text-left) dan Kategori Santri (text-left)
                    const row = `
                        <tr class="hover:bg-slate-50/50 transition duration-150">
                            <td class="py-3 px-2 text-center font-medium text-slate-400 text-xs">${index + 1}</td>
                            <td class="py-3 px-2 font-bold text-slate-900 text-xs text-left">${item.nama}</td>
                            <td class="py-3 px-2 text-slate-700 font-semibold text-xs text-left">${displayKategori}</td>
                            <td class="py-3 px-2 text-slate-600 text-xs">${item.awal}</td>
                            <td class="py-3 px-2 text-slate-600 text-xs">${item.akhir}</td>
                            <td class="py-3 px-2 text-center text-xs">
                                <div class="font-bold text-slate-800">${item.mingguIni}</div>
                                <div class="text-[9px] text-slate-400">Target: ${displayTarget}</div>
                            </td>
                            <td class="py-3 px-2 text-center text-xs">
                                ${pencapaianBadge}
                            </td>
                            <td class="py-3 px-2 text-center font-extrabold text-slate-800 text-xs">${item.total}</td>
                            <td class="py-3 px-2 text-center font-medium text-purple-600 text-xs">${item.terakhirTasmik || '-'}</td>
                            <td class="py-3 px-2 text-center">
                                <span class="px-2 py-0.5 rounded-full text-[10px] font-bold ${statusColor}">${item.status || 'Pilih'}</span>
                            </td>
                            <td class="py-3 px-2 text-slate-700 font-medium text-xs truncate max-w-[110px]" title="${item.guru}">${item.guru}</td>
                            <td class="py-3 px-2 text-center">
                                <div class="flex items-center justify-center gap-1.5">
                                    <button onclick="editData(${actualIndex})" class="text-amber-600 hover:text-amber-800 font-bold text-[11px] transition cursor-pointer flex items-center gap-0.5">✏️</button>
                                    <span class="text-gray-200">|</span>
                                    <button onclick="hapusData(${actualIndex})" class="text-rose-500 hover:text-rose-700 font-bold text-[11px] transition cursor-pointer flex items-center gap-0.5">❌</button>
                                </div>
                            </td>
                        </tr>
                    `;
                    tabelBody.insertAdjacentHTML('beforeend', row);
                });
            }
        }

        // Live Search & Filter triggers
        searchNameInput.addEventListener('input', updateTable);
        filterKategoriInput.addEventListener('change', updateTable);
        filterStatusInput.addEventListener('change', updateTable);
        filterPencapaianInput.addEventListener('change', updateTable);
        filterGuruInput.addEventListener('change', updateTable);

        form.addEventListener('submit', function(e) {
            e.preventDefault();

            const nama = namaInput.value;
            const kategori = kategoriInput.value;
            const awal = awalSetoranInput.value;
            const akhir = akhirSetoranInput.value;
            const mingguIni = mingguIniInput.value;
            const total = totalPerolehanInput.value;
            const targetMingguan = targetMingguanSelect.value;
            const pencapaianTarget = pencapaianTargetSelect.value;
            const terakhirTasmik = terakhirTasmikInput.value;
            const status = statusHafalanSelect.value;
            const guru = guruSelect.value;
            const editIndex = editIndexInput.value;

            if (status === "Pilih disini" || !status) {
                showToast("Silakan pilih status hafalan terlebih dahulu!", "warning");
                return;
            }

            if (editIndex !== "") {
                dataHafalan[editIndex] = { nama, kategori, awal, akhir, mingguIni, total, targetMingguan, pencapaianTarget, terakhirTasmik, status, guru };
                showToast("Data setoran hafalan santri berhasil diperbarui!");
                clearEditMode();
            } else {
                dataHafalan.push({ nama, kategori, awal, akhir, mingguIni, total, targetMingguan, pencapaianTarget, terakhirTasmik, status, guru });
                showToast("Data setoran hafalan santri berhasil disimpan!");
            }

            saveData();    
            updateTable(); 
            form.reset();  
            namaInput.focus();
        });

        function editData(index) {
            const item = dataHafalan[index];
            
            namaInput.value = item.nama;
            kategoriInput.value = item.kategori || "Reguler";
            awalSetoranInput.value = item.awal;
            akhirSetoranInput.value = item.akhir;
            mingguIniInput.value = item.mingguIni;
            totalPerolehanInput.value = item.total;
            targetMingguanSelect.value = item.targetMingguan || "3/4 Juz";
            pencapaianTargetSelect.value = item.pencapaianTarget || "Belum Tercapai";
            terakhirTasmikInput.value = item.terakhirTasmik || '';
            statusHafalanSelect.value = item.status;
            guruSelect.value = item.guru;
            
            editIndexInput.value = index;
            formTitle.innerHTML = "<span>✏️</span> Edit Data Hafalan Santri";
            submitBtn.innerText = "Perbarui Data";
            submitBtn.className = "bg-amber-600 hover:bg-amber-700 text-white font-semibold py-2.5 rounded-xl transition text-sm shadow-sm cursor-pointer flex items-center justify-center";
            
            namaInput.focus();
        }

        function clearEditMode() {
            editIndexInput.value = "";
            formTitle.innerHTML = "<span>📝</span> Input Data Hafalan Santri";
            submitBtn.innerText = "Simpan Data";
            submitBtn.className = "bg-emerald-600 hover:bg-emerald-700 text-white font-semibold py-2.5 rounded-xl transition text-sm shadow-sm cursor-pointer flex items-center justify-center";
        }

        resetFormBtn.addEventListener('click', function() {
            form.reset();
            clearEditMode();
            showToast("Form berhasil di-reset", "warning");
        });

        function hapusData(index) {
            showConfirmModal("Apakah Anda yakin ingin menghapus data hafalan santri ini secara permanen?", () => {
                dataHafalan.splice(index, 1);
                saveData();
                updateTable();
                showToast("Data setoran hafalan berhasil dihapus", "danger");
                if(editIndexInput.value == index) {
                    form.reset();
                    clearEditMode();
                }
            });
        }

        downloadPdfBtn.addEventListener('click', function() {
            const filteredData = getFilteredData();

            if(filteredData.length === 0) {
                showToast("Tidak ada data hafalan untuk dicetak!", "warning");
                return;
            }

            const { jsPDF } = window.jspdf;
            const doc = new jsPDF('l', 'mm', 'a4');

            // Header Background Accent (Solid Dark Green Emerald)
            doc.setFillColor(16, 74, 53); 
            doc.rect(0, 0, 297, 34, 'F');

            doc.setTextColor(255, 255, 255);
            doc.setFont("Helvetica", "bold");
            doc.setFontSize(16);
            doc.text("LAPORAN PEROLEHAN HAFALAN SANTRI", 148, 12, { align: "center" });
            
            doc.setFontSize(11);
            doc.setFont("Helvetica", "normal");
            doc.text("PONDOK PESANTREN HAMALATUL QURAN (PPHQ PUTRI 4)", 148, 19, { align: "center" });
            
            doc.setFontSize(9);
            doc.text("Jl. Ringinagung, Magetan, Jawa Timur", 148, 25, { align: "center" });
            
            // Sub Header Metadata (Date & Active Teacher)
            const opsiTanggal = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            const tanggalSekarang = new Date().toLocaleDateString('id-ID', opsiTanggal);
            
            doc.setTextColor(71, 85, 105); // Slate-600
            doc.setFontSize(9);
            doc.setFont("Helvetica", "italic");
            doc.text("Dicetak pada: " + tanggalSekarang, 15, 41);

            // Deteksi Guru Pengampu berdasarkan filter/isi data
            const activeGuruFilter = filterGuruInput.value;
            let labelUstazah = "Semua Ustazah";
            
            if (activeGuruFilter) {
                labelUstazah = activeGuruFilter;
            } else {
                const uniqueGurus = [...new Set(filteredData.map(item => item.guru))];
                if (uniqueGurus.length === 1) {
                    labelUstazah = uniqueGurus[0];
                } else if (uniqueGurus.length > 1) {
                    labelUstazah = "Campuran (" + uniqueGurus.length + " Ustazah)";
                }
            }

            doc.setFont("Helvetica", "bold");
            doc.text("Ustazah Pengampu: " + labelUstazah, 15, 46);

            // Map data for PDF Table
            const bodyData = filteredData.map((item, idx) => [
                idx + 1,
                item.nama,
                item.kategori || "Reguler",
                item.awal,
                item.akhir,
                item.mingguIni,
                item.targetMingguan || "3/4 Juz",
                item.pencapaianTarget || "Belum",
                item.total,
                item.terakhirTasmik || '-',
                item.status,
                item.guru
            ]);

            doc.autoTable({
                startY: 50,
                head: [['No', 'Nama Santri', 'Kategori Santri', 'Setoran Awal', 'Setoran Akhir', 'Perolehan', 'Target', 'Pencapaian', 'Total', 'Terakhir Tasmik', 'Status', 'Ustazah']],
                body: bodyData,
                theme: 'striped',
                headStyles: { 
                    fillColor: [15, 118, 110], 
                    halign: 'center', 
                    fontSize: 8.5, 
                    fontStyle: 'bold',
                    textColor: [255, 255, 255]
                }, 
                columnStyles: {
                    0: { halign: 'center', cellWidth: 8 },
                    1: { halign: 'left', fontStyle: 'bold', cellWidth: 32 }, // Left align Nama Santri
                    2: { halign: 'left', cellWidth: 26 }, // Left align Kategori Santri
                    3: { halign: 'left', cellWidth: 16 },
                    4: { halign: 'left', cellWidth: 16 },
                    5: { halign: 'center', cellWidth: 20 },
                    6: { halign: 'center', cellWidth: 16 },
                    7: { halign: 'center', fontStyle: 'bold', cellWidth: 22 },
                    8: { halign: 'center', fontStyle: 'bold', cellWidth: 20 },
                    9: { halign: 'center', cellWidth: 24 },
                    10: { halign: 'center', cellWidth: 22 },
                    11: { halign: 'left', fontStyle: 'normal' }
                },
                styles: { 
                    fontSize: 8, 
                    cellPadding: 2.2, 
                    font: 'Helvetica', 
                    textColor: [15, 23, 42], 
                    lineColor: [226, 232, 240], 
                    lineWidth: 0.1,
                    overflow: 'linebreak' // Auto wrapping text
                },
                didParseCell: function(data) {
                    if (data.section === 'body') {
                        const cellValue = data.cell.text.join(' ').trim();
                        if (cellValue === 'Dauroh Tasmik') {
                            data.cell.styles.fillColor = [126, 34, 206]; // Purple-700
                            data.cell.styles.textColor = [255, 255, 255]; // Pure White text
                            data.cell.styles.fontStyle = 'bold';
                        }
                    }
                }
            });

            const fileOutputName = `Rekap_Hafalan_${labelUstazah.replace(/\s+/g, '_')}.pdf`;
            doc.save(fileOutputName);
            showToast(`Berhasil mengunduh dokumen laporan: ${fileOutputName}`);
        });

        // Initialize state on first run
        updateStats();
        updateTable();
    </script>
</body>
</html>
