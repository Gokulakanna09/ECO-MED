<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ECOMED - Advanced Wound Monitoring</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        .header {
            background: #27ae60;
            color: white;
            text-align: center;
            padding: 20px;
        }
        .container {
            width: 80%;
            margin: auto;
            padding: 20px;
        }
        .section {
            background: white;
            padding: 20px;
            margin: 20px 0;
            border-radius: 8px;
            box-shadow: 0px 0px 10px rgba(0,0,0,0.1);
        }
        .sensor-data {
            font-size: 18px;
            font-weight: bold;
            color: #27ae60;
        }
        .contact-form {
            display: flex;
            flex-direction: column;
        }
        .contact-form input, .contact-form textarea {
            margin-bottom: 10px;
            padding: 10px;
            font-size: 16px;
        }
        .contact-form button {
            background: #27ae60;
            color: white;
            padding: 10px;
            border: none;
            cursor: pointer;
        }
        .patient-info {
            display: flex;
            align-items: center;
            gap: 20px;
            margin-bottom: 20px;
        }
        .patient-info img {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            object-fit: cover;
        }
        .patient-details {
            font-size: 16px;
        }
        .chart-container {
            margin-top: 20px;
            position: relative;
            height: 300px;
        }
    </style>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
    <div class="header">
        <h1>ECOMED</h1>
        <p>Advanced Wound Monitoring and Healing Solutions</p>
    </div>
    <div class="container">
        <div class="section">
            <h2>Patient Information</h2>
            <div class="patient-info">
                <img src="https://media-hosting.imagekit.io//f8302d104f644665/WhatsApp%20Image%202025-03-03%20at%2015.06.25_64adef43.jpg?Expires=1835602753&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=TAk-31t9pZKO8eUzla7T5MVZVZkfdr4hJbWCbNVjzPD7BKoi7kol6~DwxympkAsONWUWwV6O8L3cF09sMpYqOZpIwrCCBPPJsLQZoEOoYM9ncSCOAYpHb68KoPy5EvhmxEhx8awBT7~sYEVZi~uGebMtXhdbqgpbnhPR~gfqBeP7gh8i5Sy1WdaoMvNCuaDHNv1Wix025F-R-GTxysSd43VY6-MTUq~j6Vegt93IejirNvd-sd34Q8V3ICC9jyg~sglQCloXZ7YxknkT6W8ks016kiT3EpnU8apSoAiuXwRXVHL7LnMII6TfG2eYYf2XLteVTu--0h7IJW6GLRzPhw__" alt="Patient Image">
                <div class="patient-details">
                    <p>Patient Name: Nivrithi S</p>
                    <p>Age: 18</p>
                    <p>Wound Degree: First Degree Wound</p>
                </div>
            </div>
        </div>
        <div class="section">
            <h2>Wound Monitoring Dashboard</h2>
            <p>Patch Lifetime: <span class="sensor-data" id="patch-lifetime">--</span> hours</p>
            <p>Temperature: <span class="sensor-data" id="temp">--</span>°C</p>
            <p>Moisture Level: <span class="sensor-data" id="moisture">--</span>%</p>
            <p>Infection Risk: <span class="sensor-data" id="infection">--</span></p>
            <p>Recovery Percentage: <span class="sensor-data" id="recovery-percent">--</span>%</p>
            <p>Estimated Recovery Time: <span class="sensor-data" id="recovery-time">--</span> days</p>
            
            <div class="chart-container">
                <canvas id="sensorChart"></canvas>
            </div>
        </div>
        <div class="section">
            <h2>Contact Medical Support</h2>
            <form class="contact-form">
                <input type="text" placeholder="Your Name" required>
                <input type="email" placeholder="Your Email" required>
                <textarea placeholder="Your Message" rows="5" required></textarea>
                <button type="submit">Send</button>
            </form>
        </div>
    </div>
    <script>
        // Initialize Chart.js
        const ctx = document.getElementById('sensorChart').getContext('2d');
        const chart = new Chart(ctx, {
            type: 'line',
            data: {
                labels: [],
                datasets: [
                    {
                        label: 'Temperature (°C)',
                        data: [],
                        borderColor: '#FF6384',
                        fill: false
                    },
                    {
                        label: 'Moisture Level (%)',
                        data: [],
                        borderColor: '#36A2EB',
                        fill: false
                    },
                    {
                        label: 'Recovery Percentage (%)',
                        data: [],
                        borderColor: '#4BC0C0',
                        fill: false
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                scales: {
                    y: {
                        beginAtZero: true
                    }
                }
            }
        });

        function updateSensorData() {
            const temp = (36 + Math.random() * 2).toFixed(1);
            const moisture = (50 + Math.random() * 10).toFixed(1);
            const recoveryPercent = (Math.random() * 100).toFixed(1);
            const recoveryTime = Math.floor(Math.random() * 30 + 1);
            const patchLifetime = (Math.random() * 48).toFixed(1);
            
            // Update text displays
            document.getElementById("temp").innerText = temp;
            document.getElementById("moisture").innerText = moisture;
            document.getElementById("infection").innerText = Math.random() > 0.8 ? "High" : "Low";
            document.getElementById("recovery-percent").innerText = recoveryPercent;
            document.getElementById("recovery-time").innerText = recoveryTime;
            document.getElementById("patch-lifetime").innerText = patchLifetime;

            // Update chart data
            const labels = chart.data.labels;
            const datasets = chart.data.datasets;
            
            // Add new timestamp
            const now = new Date();
            labels.push(now.toLocaleTimeString());
            
            // Add new data points
            datasets[0].data.push(temp);
            datasets[1].data.push(moisture);
            datasets[2].data.push(recoveryPercent);
            
            // Keep only last 10 data points
            if (labels.length > 10) {
                labels.shift();
                datasets.forEach(dataset => dataset.data.shift());
            }
            
            chart.update();
        }

        setInterval(updateSensorData, 2000);
    </script>
</body>
</html>
