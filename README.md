<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sandfjärdsgatan 42 Intranät</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
        }
        
        .message-item {
            animation: fadeIn 0.3s ease-in;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .hover-scale:hover {
            transform: scale(1.02);
        }
        
        .transition-all {
            transition: all 0.2s ease;
        }
    </style>
</head>
<body class="min-h-screen bg-gray-50 text-gray-900">
    <div class="container mx-auto px-6 py-8 max-w-6xl">
        
        <!-- Header -->
        <div class="bg-white rounded-3xl shadow-lg border border-gray-200 p-8 mb-8 text-center">
            <h1 class="text-4xl md:text-5xl font-bold text-blue-600 mb-4">
                🏢 Sandfjärdsgatan 42
            </h1>
            <p class="text-xl text-gray-600 mb-2">Lokalt intranät för krisberedskap</p>
            <p class="text-gray-500 mb-4">Årsta, Stockholm</p>
            <p class="text-sm text-gray-400" id="currentTime">
                Senast uppdaterad: <span id="timeDisplay"></span>
            </p>
        </div>

        <!-- Alert -->
        <div class="bg-red-50 border-2 border-red-200 rounded-2xl p-6 mb-8">
            <div class="flex items-center">
                <svg class="text-red-500 mr-4" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="m21.73 18-8-14a2 2 0 0 0-3.48 0l-8 14A2 2 0 0 0 4 21h16a2 2 0 0 0 1.73-3Z"/>
                    <path d="M12 9v4"/>
                    <path d="m12 17 .01 0"/>
                </svg>
                <div>
                    <h3 class="text-xl font-bold text-red-700">Krisberedskapsläge aktiverat</h3>
                    <p class="text-red-600">Extern internetuppkoppling otillgänglig</p>
                </div>
            </div>
        </div>

        <!-- Status Cards -->
        <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-8">
            <div class="bg-white rounded-2xl shadow-md border border-gray-200 p-6 text-center">
                <svg class="text-green-500 mx-auto mb-3" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="m2 3 20 20"/>
                    <path d="M6.3 6.3a4.67 4.67 0 0 0 0 6.6l3.7 3.7a4.67 4.67 0 0 0 6.6 0l3.7-3.7a4.67 4.67 0 0 0 0-6.6"/>
                </svg>
                <h3 class="font-bold text-gray-900 text-lg">Lokalt nätverk</h3>
                <p class="text-green-600 font-medium">● Online</p>
            </div>

            <div class="bg-white rounded-2xl shadow-md border border-gray-200 p-6 text-center">
                <svg class="text-red-500 mx-auto mb-3" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <line x1="2" x2="22" y1="2" y2="22"/>
                    <path d="M8.5 16.5a5 5 0 0 1 7 0"/>
                    <path d="M2 8.82a15 15 0 0 1 4.17-2.65"/>
                    <path d="M10.66 5c4.01-.36 8.14.9 11.34 3.76"/>
                    <path d="M16.85 11.25a10 10 0 0 1 2.22 1.68"/>
                    <path d="M5 13a10 10 0 0 1 5.24-2.76"/>
                    <line x1="12" x2="12.01" y1="20" y2="20"/>
                </svg>
                <h3 class="font-bold text-gray-900 text-lg">Internet</h3>
                <p class="text-red-600 font-medium">● Otillgängligt</p>
            </div>

            <div class="bg-white rounded-2xl shadow-md border border-gray-200 p-6 text-center">
                <svg class="text-blue-500 mx-auto mb-3" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M22 12h-4l-3 9L9 3l-3 9H2"/>
                </svg>
                <h3 class="font-bold text-gray-900 text-lg">Aktiva enheter</h3>
                <p class="text-blue-600 font-bold text-2xl" id="deviceCount">12</p>
            </div>

            <div class="bg-white rounded-2xl shadow-md border border-gray-200 p-6 text-center">
                <svg class="text-orange-500 mx-auto mb-3" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="m2 5 18 2"/>
                    <path d="m5 2 2 18"/>
                    <path d="m12 12 4-10"/>
                    <path d="m12 12-4 10"/>
                </svg>
                <h3 class="font-bold text-gray-900 text-lg">P4 Stockholm</h3>
                <p class="text-orange-600 font-mono font-bold">103.3 MHz</p>
            </div>
        </div>

        <!-- Main Communication -->
        <div class="grid lg:grid-cols-2 gap-8 mb-8">
          
            <!-- Messages -->
            <div class="bg-white rounded-3xl shadow-lg border border-gray-200 p-8">
                <div class="flex items-center mb-6">
                    <svg class="text-blue-500 mr-4" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
                    </svg>
                    <h2 class="text-2xl font-bold text-gray-900">Meddelanden</h2>
                </div>
                
                <div id="messageList" class="space-y-4 max-h-96 overflow-y-auto">
                    <!-- Messages will be populated here -->
                </div>
            </div>

            <!-- Send Message -->
            <div class="bg-white rounded-3xl shadow-lg border border-gray-200 p-8">
                <div class="flex items-center mb-6">
                    <svg class="text-green-500 mr-4" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="m22 2-7 20-4-9-9-4Z"/>
                        <path d="M22 2 11 13"/>
                    </svg>
                    <h2 class="text-2xl font-bold text-gray-900">Nytt meddelande</h2>
                </div>

                <form id="messageForm" class="space-y-6">
                    <div>
                        <label class="block text-sm font-bold text-gray-700 mb-2">Typ</label>
                        <select id="messageType" class="w-full p-4 border-2 border-gray-200 rounded-xl text-gray-900 focus:border-blue-500 focus:ring-0 text-lg">
                            <option value="info">Allmän information</option>
                            <option value="urgent">Brådskande meddelande</option>
                            <option value="resource">Resursförfrågan</option>
                            <option value="help">Behöver hjälp</option>
                        </select>
                    </div>

                    <div>
                        <label class="block text-sm font-bold text-gray-700 mb-2">Till</label>
                        <select id="targetFloor" class="w-full p-4 border-2 border-gray-200 rounded-xl text-gray-900 focus:border-blue-500 focus:ring-0 text-lg">
                            <option value="all">Alla våningar</option>
                            <option value="12">Våning 12</option>
                            <option value="11">Våning 11</option>
                            <option value="10">Våning 10</option>
                            <option value="9">Våning 9</option>
                            <option value="8">Våning 8</option>
                            <option value="7">Våning 7</option>
                            <option value="6">Våning 6</option>
                            <option value="5">Våning 5</option>
                            <option value="4">Våning 4</option>
                            <option value="3">Våning 3</option>
                            <option value="2">Våning 2</option>
                            <option value="1">Våning 1</option>
                        </select>
                    </div>

                    <div>
                        <label class="block text-sm font-bold text-gray-700 mb-2">Från</label>
                        <input type="text" id="senderName" value="Läg. 7B" placeholder="Ditt namn/lägenhetsnummer" class="w-full p-4 border-2 border-gray-200 rounded-xl text-gray-900 focus:border-blue-500 focus:ring-0 text-lg">
                    </div>

                    <div>
                        <label class="block text-sm font-bold text-gray-700 mb-2">Meddelande</label>
                        <textarea id="messageText" placeholder="Skriv ditt meddelande..." rows="4" class="w-full p-4 border-2 border-gray-200 rounded-xl text-gray-900 focus:border-blue-500 focus:ring-0 text-lg resize-none"></textarea>
                    </div>

                    <button type="submit" class="w-full bg-blue-500 hover:bg-blue-600 text-white font-bold py-4 px-6 rounded-xl text-lg transition-colors duration-200 flex items-center justify-center hover-scale transition-all">
                        <svg class="mr-3" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                            <path d="m22 2-7 20-4-9-9-4Z"/>
                            <path d="M22 2 11 13"/>
                        </svg>
                        Skicka meddelande
                    </button>
                </form>
            </div>
        </div>

        <!-- Emergency Info -->
        <div class="bg-white rounded-3xl shadow-lg border border-gray-200 p-8 mb-8">
            <div class="flex items-center mb-6">
                <svg class="text-red-500 mr-4" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="m21.73 18-8-14a2 2 0 0 0-3.48 0l-8 14A2 2 0 0 0 4 21h16a2 2 0 0 0 1.73-3Z"/>
                    <path d="M12 9v4"/>
                    <path d="m12 17 .01 0"/>
                </svg>
                <h2 class="text-2xl font-bold text-gray-900">Krisberedskap</h2>
            </div>

            <div class="bg-yellow-50 border-2 border-yellow-200 rounded-2xl p-6 mb-6">
                <h3 class="font-bold text-yellow-800 text-lg mb-4">🚨 Varningssignaler</h3>
                <div class="space-y-2 text-yellow-700">
                    <p><strong>VMA (7s + 14s paus):</strong> Gå in, stäng fönster, lyssna P4</p>
                    <p><strong>Beredskapslarm (30s + 15s paus):</strong> Krig/krigsfara</p>
                    <p><strong>Flyglarm (korta signaler 1 min):</strong> Till skyddsrum genast</p>
                </div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                <button onclick="showEmergencyInfo()" class="bg-green-500 hover:bg-green-600 text-white font-bold py-4 px-6 rounded-xl text-lg transition-colors duration-200 hover-scale transition-all">
                    📋 Beredskapslista
                </button>
                <button onclick="showEvacuationPlan()" class="bg-orange-500 hover:bg-orange-600 text-white font-bold py-4 px-6 rounded-xl text-lg transition-colors duration-200 hover-scale transition-all">
                    🚪 Utrymning
                </button>
                <button onclick="showShelterInfo()" class="bg-purple-500 hover:bg-purple-600 text-white font-bold py-4 px-6 rounded-xl text-lg transition-colors duration-200 hover-scale transition-all">
                    🛡️ Skyddsrum
                </button>
            </div>

            <div class="bg-gray-100 rounded-2xl p-6 text-center">
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 text-sm">
                    <div>
                        <p class="font-bold text-gray-700">📻 P4 Stockholm</p>
                        <p class="text-gray-600">103.3 MHz</p>
                    </div>
                    <div>
                        <p class="font-bold text-gray-700">📞 Viktiga nummer</p>
                        <p class="text-gray-600">112 • 113 13 • 1177</p>
                    </div>
                    <div>
                        <p class="font-bold text-gray-700">ℹ️ Information</p>
                        <p class="text-gray-600">krisinformation.se</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Building Overview -->
        <div class="grid lg:grid-cols-2 gap-8">
          
            <!-- Floors -->
            <div class="bg-white rounded-3xl shadow-lg border border-gray-200 p-8">
                <div class="flex items-center mb-6">
                    <svg class="text-blue-500 mr-4" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="M3 21h18"/>
                        <path d="M5 21V7l8-4v18"/>
                        <path d="M19 21V11l-6-4"/>
                    </svg>
                    <h2 class="text-2xl font-bold text-gray-900">Våningar</h2>
                </div>
                
                <div class="grid grid-cols-3 gap-3" id="floorGrid">
                    <!-- Floors will be populated here -->
                </div>
            </div>

            <!-- Transport -->
            <div class="bg-white rounded-3xl shadow-lg border border-gray-200 p-8">
                <div class="flex items-center mb-6">
                    <svg class="text-blue-500 mr-4" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="m5 9 7-7 7 7"/>
                        <path d="m12 16 7-7"/>
                        <path d="m12 16-7-7"/>
                    </svg>
                    <h2 class="text-2xl font-bold text-gray-900">Transport</h2>
                </div>

                <div class="space-y-4 mb-6">
                    <div class="flex items-center justify-between p-4 bg-green-50 border border-green-200 rounded-xl">
                        <div class="flex items-center">
                            <span class="text-2xl mr-3">🛗</span>
                            <div>
                                <p class="font-bold text-gray-900">Hiss A</p>
                                <p class="text-green-600">Fungerande</p>
                            </div>
                        </div>
                        <p class="text-sm text-gray-500">Våning 7</p>
                    </div>

                    <div class="flex items-center justify-between p-4 bg-red-50 border border-red-200 rounded-xl">
                        <div class="flex items-center">
                            <span class="text-2xl mr-3">🛗</span>
                            <div>
                                <p class="font-bold text-gray-900">Hiss B</p>
                                <p class="text-red-600">Fastnad</p>
                            </div>
                        </div>
                        <p class="text-sm text-gray-500">Våning 4</p>
                    </div>

                    <div class="flex items-center justify-between p-4 bg-blue-50 border border-blue-200 rounded-xl">
                        <div class="flex items-center">
                            <span class="text-2xl mr-3">🚶‍♂️</span>
                            <div>
                                <p class="font-bold text-gray-900">Trappuppgång</p>
                                <p class="text-blue-600">Fri passage</p>
                            </div>
                        </div>
                        <p class="text-sm text-gray-500">Alla våningar</p>
                    </div>
                </div>

                <div class="bg-gray-100 rounded-2xl p-6">
                    <h3 class="font-bold text-gray-800 mb-3">🚨 Utrymning</h3>
                    <ul class="space-y-2 text-gray-700">
                        <li>• Trappuppgång för alla</li>
                        <li>• Hiss A för rörelsehinder</li>
                        <li>• Samling: Årstafältet</li>
                    </ul>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Initial data
        let messages = [
            {
                id: 1,
                type: 'urgent',
                sender: 'MSB Information',
                target: 'all',
                text: '⚠️ VIKTIGT: Kontrollera att ni har minst 1 veckas beredskap hemma. Mat, vatten, värme och medicin.',
                time: new Date(Date.now() - 300000)
            },
            {
                id: 2,
                type: 'info',
                sender: 'Fastighetsskötsel',
                target: 'all',
                text: 'Skyddsrum inspekteras imorgon. Fastighetsägaren ansvarar för iordningställande vid höjd beredskap.',
                time: new Date(Date.now() - 240000)
            },
            {
                id: 3,
                type: 'resource',
                sender: 'Ahmed R. (Elektriker)',
                target: 'all',
                text: '⚡ Kan hjälpa med att kontrollera elsäkerhet och installera backup-batterier. Kontakta mig!',
                time: new Date(Date.now() - 180000)
            },
            {
                id: 4,
                type: 'help',
                sender: 'Läg. 10C',
                target: 'all',
                text: 'Behöver hjälp med att komma till skyddsrum - har rörelsehinder. Kan någon hjälpa till?',
                time: new Date(Date.now() - 120000)
            }
        ];

        const floors = [
            { id: 12, active: 4, contact: 'Anna K.', status: 'ok' },
            { id: 11, active: 3, contact: 'Erik M.', status: 'ok' },
            { id: 10, active: 2, contact: 'Behöver ansvarig', status: 'warning' },
            { id: 9, active: 4, contact: 'Maria S.', status: 'ok' },
            { id: 8, active: 3, contact: 'Johan P.', status: 'ok' },
            { id: 7, active: 4, contact: 'Lisa A.', status: 'ok' },
            { id: 6, active: 2, contact: 'Ahmed R.', status: 'ok' },
            { id: 5, active: 1, contact: 'Behöver ansvarig', status: 'warning' },
            { id: 4, active: 3, contact: 'Ingrid L.', status: 'ok' },
            { id: 3, active: 4, contact: 'Behöver ansvarig', status: 'ok' },
            { id: 2, active: 3, contact: 'Mikael T.', status: 'ok' },
            { id: 1, active: 2, contact: 'Dr. Sara J.', status: 'ok' }
        ];

        // Helper functions
        function getMessageIcon(type) {
            switch (type) {
                case 'urgent': return '🚨';
                case 'resource': return '📦';
                case 'help': return '🆘';
                default: return 'ℹ️';
            }
        }

        function getMessageLabel(type) {
            switch (type) {
                case 'urgent': return 'Brådskande';
                case 'resource': return 'Resurs';
                case 'help': return 'Hjälp';
                default: return 'Info';
            }
        }

        // Update time display
        function updateTime() {
            const now = new Date();
            document.getElementById('timeDisplay').textContent = now.toLocaleString('sv-SE');
        }

        // Display messages
        function displayMessages() {
            const messageList = document.getElementById('messageList');
            messageList.innerHTML = '';
            
            messages.sort((a, b) => b.time - a.time);
            
            messages.forEach(msg => {
                const div = document.createElement('div');
                div.className = `message-item p-5 rounded-2xl border-2 ${
                    msg.type === 'urgent' 
                        ? 'bg-red-50 border-red-200' 
                        : 'bg-gray-50 border-gray-200'
                }`;
                
                div.innerHTML = `
                    <div class="flex justify-between items-start mb-3">
                        <div class="flex items-center space-x-2">
                            <span class="text-lg">${getMessageIcon(msg.type)}</span>
                            <span class="font-bold text-gray-700 text-sm">${getMessageLabel(msg.type)}</span>
                            <span class="text-gray-500">•</span>
                            <span class="text-gray-600 text-sm font-medium">${msg.sender}</span>
                        </div>
                        <span class="text-xs text-gray-400">${msg.time.toLocaleTimeString('sv-SE')}</span>
                    </div>
                    <p class="text-gray-800 leading-relaxed">${msg.text}</p>
                `;
                
                messageList.appendChild(div);
            });
        }

        // Display floors
        function displayFloors() {
            const floorGrid = document.getElementById('floorGrid');
            
            floors.forEach(floor => {
                const div = document.createElement('div');
                div.className = `p-4 rounded-xl border-2 cursor-pointer hover:shadow-md transition-all text-center hover-scale transition-all ${
                    floor.status === 'warning'
                        ? 'bg-yellow-50 border-yellow-300 hover:bg-yellow-100'
                        : 'bg-green-50 border-green-300 hover:bg-green-100'
                }`;
                
                div.onclick = () => {
                    alert(`Våning ${floor.id}\nKontakt: ${floor.contact}\n${floor.active} aktiva enheter`);
                };
                
                div.innerHTML = `
                    <p class="font-bold text-gray-900 text-lg">V${floor.id}</p>
                    <p class="text-xs text-gray-600 mt-1">${floor.active} aktiva</p>
                    <p class="text-xs text-gray-500 mt-1">${floor.contact}</p>
                `;
                
                floorGrid.appendChild(div);
            });
        }

        // Send message
        function sendMessage(e) {
            e.preventDefault();
            
            const type = document.getElementById('messageType').value;
            const target = document.getElementById('targetFloor').value;
            const sender = document.getElementById('senderName').value;
            const text = document.getElementById('messageText').value;
            
            if (!sender || !text) {
                alert('Fyll i både namn och meddelande!');
                return;
            }
            
            const newMessage = {
                id: Date.now(),
                type: type,
                sender: sender,
                target: target,
                text: text,
                time: new Date()
            };
            
            messages.unshift(newMessage);
            displayMessages();
            
            document.getElementById('messageText').value = '';
        }

        // Emergency info functions
        function showEmergencyInfo() {
            alert(`📋 BEREDSKAPSCHECKLISTA (minst 1 vecka):

💧 VATTEN (3L/person/dag)
🍝 MAT: Torrvaror, konserver, protein
🔥 VÄRME: Varma kläder, filtar
📱 KOMMUNIKATION: Batteriradio P4 103.3 MHz
💊 MEDICIN: Första hjälpen + receptmedicin`);
        }

        function showEvacuationPlan() {
            alert(`🚪 UTRYMNINGSPLAN

📍 VÄGAR:
1. Trappuppgång (alla)
2. Hiss A (rörelsehinder)
3. Samlingspunkt: Årstafältet

📞 NUMMER:
112 (nöd) | 113 13 (kris)`);
        }

        function showShelterInfo() {
            alert(`🛡️ SKYDDSRUM

📍 Märkning: Orange fyrkant + blå triangel
🎒 Ta med: Mat 3 dagar, medicin, ficklampa
⏱️ Förberedelse: 48h vid höjd beredskap`);
        }

        // Simulate device count changes
        function updateDeviceCount() {
            const count = Math.floor(Math.random() * 5) + 10;
            document.getElementById('deviceCount').textContent = count;
        }

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            updateTime();
            displayMessages();
            displayFloors();
            
            // Event listeners
            document.getElementById('messageForm').addEventListener('submit', sendMessage);
            
            // Update timers
            setInterval(updateTime, 60000);
            setInterval(updateDeviceCount, 30000);
            
            // Enter key to send message
            document.getElementById('messageText').addEventListener('keypress', function(e) {
                if (e.key === 'Enter' && !e.shiftKey) {
                    e.preventDefault();
                    sendMessage(e);
                }
            });
        });
    </script>
</body>
</html>
