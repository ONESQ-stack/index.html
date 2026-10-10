# index.html
app/web aegis
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AEGIS - Dashboard Keamanan Kapal</title>
    
    <!-- Memanggil alat bantu untuk desain (Bootstrap/CSS standar) agar pasti bisa diakses -->
    <style>
        body { font-family: sans-serif; background-color: #f3f4f6; padding: 20px; }
        .container { max-width: 900px; margin: auto; }
        .card { background: white; border-radius: 15px; padding: 25px; margin-bottom: 20px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
        .header { display: flex; align-items: center; justify-content: space-between; }
        .logo-container { display: flex; align-items: center; gap: 15px; }
        .title { color: #0284c7; font-size: 28px; font-weight: bold; margin: 0; }
        .subtitle { color: #6b7280; font-size: 12px; margin: 0; letter-spacing: 1px; }
        .status-badge { background-color: #d1fae5; color: #065f46; padding: 5px 15px; border-radius: 20px; font-size: 14px; font-weight: bold; }
        
        .grid { display: grid; grid-template-columns: 1fr; gap: 20px; }
        @media (min-width: 768px) { .grid { grid-template-columns: 1fr 1fr; } }
        
        h2 { color: #4b5563; font-size: 18px; margin-top: 0; }
        
        .meter-container { text-align: center; margin-top: 20px; }
        .value { font-size: 48px; font-weight: bold; color: #10b981; }
        .status-text { font-size: 24px; font-weight: bold; color: #10b981; margin-top: 15px; }
        
        #map { height: 300px; width: 100%; border-radius: 10px; background-color: #e5e7eb; border: 1px solid #d1d5db; display: flex; align-items: center; justify-content: center; color: #6b7280; }
        .coords { background: #f9fafb; padding: 10px; border-radius: 8px; border: 1px solid #e5e7eb; margin-top: 15px; font-size: 14px; color: #4b5563; }
    </style>
</head>
<body>

    <div class="container">
        
        <!-- BAGIAN ATAS: LOGO DAN JUDUL -->
        <div class="card header">
            <div class="logo-container">
                <!-- Gambar Logo Perisai (AEGIS) -->
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" width="60" height="60">
                    <defs>
                        <linearGradient id="grad1" x1="0%" y1="0%" x2="100%" y2="100%">
                            <stop offset="0%" style="stop-color:#0284c7;stop-opacity:1" />
                            <stop offset="100%" style="stop-color:#06b6d4;stop-opacity:1" />
                        </linearGradient>
                    </defs>
                    <path d="M50 5 L10 20 L10 50 C10 75 30 90 50 95 C70 90 90 75 90 50 L90 20 Z" fill="url(#grad1)" />
                    <path d="M25 60 Q 37.5 45, 50 60 T 75 60 L75 80 C60 88 40 88 25 80 Z" fill="#ffffff" opacity="0.4" />
                    <circle cx="50" cy="40" r="10" fill="#ffffff" />
                </svg>
                <div>
                    <h1 class="title">AEGIS</h1>
                    <p class="subtitle">SISTEM PANTAU LAMBUNG KAPAL</p>
                </div>
            </div>
            <div>
                <span class="status-badge">Terhubung</span>
            </div>
        </div>

        <!-- BAGIAN TENGAH: KOTAK INFORMASI -->
        <div class="grid">
            
            <!-- KOTAK 1: METERAN AIR -->
            <div class="card">
                <h2>Level Genangan Air</h2>
                
                <div class="meter-container">
                    <!-- Simulasi angka meteran -->
                    <div id="waterValue" class="value">0</div>
                    <div style="color: #9ca3af;">dari 4095</div>
                    
                    <div id="statusText" class="status-text">SAFE - Kering</div>
                </div>
            </div>

            <!-- KOTAK 2: PETA LOKASI -->
            <div class="card">
                <h2>Lokasi Koordinat</h2>
                
                <div id="map">Peta akan dimuat di sini (Butuh Leaflet.js)</div>
                
                <div class="coords">
                    Lat: -7.309892 | Long: 112.760017
                </div>
            </div>

        </div>
    </div>

    <script>
        // Simulasi perubahan data sederhana agar kamu bisa melihat efeknya
        function updateDashboard(value) {
            const waterValueText = document.getElementById('waterValue');
            const statusText = document.getElementById('statusText');

            waterValueText.innerText = value;

            if (value < 1000) {
                waterValueText.style.color = '#10b981'; // Hijau
                statusText.innerText = 'SAFE - Kering';
                statusText.style.color = '#10b981';
            } else if (value < 2000) {
                waterValueText.style.color = '#f59e0b'; // Oranye
                statusText.innerText = 'ALERT - Rembesan Air';
                statusText.style.color = '#f59e0b';
            } else {
                waterValueText.style.color = '#ef4444'; // Merah
                statusText.innerText = 'EMERGENCY - KEBOCORAN!';
                statusText.style.color = '#ef4444';
            }
        }

        setInterval(() => {
            const randomLevels = [250, 1691, 3200];
            const randomValue = randomLevels[Math.floor(Math.random() * randomLevels.length)];
            updateDashboard(randomValue);
        }, 4000); // Ganti tiap 4 detik
    </script>
</body>
</html>
