<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Metrik Tarzı Kod Akışı</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background: black;
            color: #00ff00;
            font-family: 'Courier New', monospace;
        }
        canvas {
            position: absolute;
            top: 0;
            left: 0;
        }
    </style>
</head>
<body>
    <canvas id="metricCanvas"></canvas>

    <script>
        const canvas = document.getElementById("metricCanvas");
        const ctx = canvas.getContext("2d");

        // Canvas boyutları
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        // Akacak metinler
        const words = [
            "Elektrik", "Elektronik", "Yazılım", "Python", "SCADA", 
            "İşletme", "IoT", "PLC", "Endüstri 4.0", "Verimlilik",
            "Sensör", "Kontrol", "Otomasyon", "Veri Analizi", "AI",
            "Machine Learning", "Endüstriyel Yazılım", "HMI"
        ];

        const fontSize = 18; // Yazı büyüklüğü
        const columns = canvas.width / fontSize; // Sütun sayısı
        const drops = Array(columns).fill(1); // Her sütun için başlangıç noktası

        function drawMetric() {
            ctx.fillStyle = "rgba(0, 0, 0, 0.05)"; // Ekranı hafif karartarak iz bırakma
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            ctx.fillStyle = "#00ff00"; // Yazı rengi
            ctx.font = fontSize + "px Courier New";

            drops.forEach((drop, i) => {
                const text = words[Math.floor(Math.random() * words.length)]; // Rastgele kelime
                ctx.fillText(text, i * fontSize, drop * fontSize);

                if (drop * fontSize > canvas.height && Math.random() > 0.975) {
                    drops[i] = 0; // Sütunu sıfırla
                }

                drops[i]++;
            });
        }

        setInterval(drawMetric, 50); // 50ms'de bir çalıştır

        // Pencere boyutu değiştiğinde tuvali yeniden ayarla
        window.addEventListener("resize", () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });
    </script>
</body>
</html>
