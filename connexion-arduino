<!DOCTYPE html>

<html lang="fr">
<head>
<meta charset="utf-8"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Interface Arduino - Gestion des Relais</title>
<style>
        /* Les styles restent inchangés */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #43484d;
            min-height: 100vh;
            padding: 20px;
        }
        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }
        .header {
            background: linear-gradient(135deg, #f7931e 0%, #f57200 100%);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
            overflow: hidden;
        }
        .header::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1) 20%, transparent 20%);
            background-size: 50px 50px;
            animation: float 20s linear infinite;
        }
        @keyframes float {
            0% { transform: translate(-50%, -50%) rotate(0deg); }
            100% { transform: translate(-50%, -50%) rotate(360deg); }
        }
        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
        }
        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }
        .main-content {
            padding: 30px;
        }
        .connection-panel {
            background: #f8f9fa;
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 30px;
            border: 2px solid #e9ecef;
        }
        .connection-status {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 20px;
        }
        .status-indicator {
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background: #dc3545;
            animation: pulse 2s infinite;
        }
        .status-indicator.connected {
            background: #28a745;
        }
        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }
        .connection-buttons {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }
        .btn {
            background: #43484d;
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0, 123, 255, 0.3);
        }
        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0, 123, 255, 0.4);
        }
        .btn.success {
            background: linear-gradient(135deg, #f7931e 0%, #f57200 100%);
            box-shadow: 0 4px 15px rgba(247, 147, 30, 0.3);
        }
        .btn.success:hover {
            box-shadow: 0 6px 20px rgba(40, 167, 69, 0.4);
        }
        .btn.danger {
            background: linear-gradient(135deg, #dc3545 0%, #c82333 100%);
            box-shadow: 0 4px 15px rgba(220, 53, 69, 0.3);
        }
        .btn.danger:hover {
            box-shadow: 0 6px 20px rgba(220, 53, 69, 0.4);
        }
        .dashboard {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin-bottom: 30px;
        }
        .card {
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            border: 1px solid #e9ecef;
            transition: transform 0.3s ease;
        }
        .card:hover {
            transform: translateY(-5px);
        }
        .card h3 {
            color: #333;
            margin-bottom: 20px;
            font-size: 1.4em;
            border-bottom: 3px solid #f57200;
            padding-bottom: 10px;
        }
        .data-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
            gap: 15px;
        }
        .data-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
}
        .data-value {
            font-size: 1.4em;
            font-weight: bold;
            color: #f7931e;
            margin-bottom: 3px;
            line-height: 1.2;
            white-space: normal;
}
        .data-label {
            font-size: 0.9em;
            color: #f7931e;
        }
        .relays-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(80px, 1fr));
            gap: 10px;
        }
        .relay-item {
            text-align: center;
            padding: 15px 10px;
            border-radius: 10px;
            border: 2px solid #e9ecef;
            transition: all 0.3s ease;
        }
        .relay-item.active {
            background: linear-gradient(135deg, #f7931e 0%, #f57200 100%);
            color: white;
            border-color: #f7931e;
            transform: scale(1.05);
        }
        .relay-item.inactive {
            background: #f8f9fa;
            color: #666;
            border-color: #e9ecef;
        }
        .relay-number {
            font-size: 1.2em;
            font-weight: bold;
            margin-bottom: 5px;
        }
        .relay-status {
            font-size: 0.8em;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        .schedule-container {
            background: white;
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
        }
        .schedule-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
        }
        .schedule-table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 20px;
        }
        .schedule-table th,
        .schedule-table td {
            padding: 12px;
            text-align: center;
            border: 1px solid #e9ecef;
        }
        .schedule-table th {
            background: #f8f9fa;
            font-weight: 600;
            color: #333;
        }
        .schedule-table tr:nth-child(even) {
            background: #f8f9fa;
        }
        .schedule-table tr:hover {
            background: #e3f2fd;
        }
        .time-input {
            border: 1px solid #ddd;
            border-radius: 5px;
            padding: 5px;
            width: 80px;
            text-align: center;
        }
        .code-output {
            background: #2d3748;
            color: #e2e8f0;
            padding: 20px;
            border-radius: 10px;
            font-family: 'Courier New', monospace;
            font-size: 14px;
            max-height: 400px;
            overflow-y: auto;
            white-space: pre;
            margin-top: 20px;
            border: 1px solid #4a5568;
        }
        .input-group {
            margin-bottom: 15px;
        }
        .input-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
            color: #333;
        }
        .input-group input,
        .input-group select {
            width: 100%;
            padding: 10px;
            border: 2px solid #e9ecef;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s ease;
        }
        .input-group input:focus,
        .input-group select:focus {
            outline: none;
            border-color: #007bff;
        }
        .tabs {
            display: flex;
            background: #f8f9fa;
            border-radius: 10px;
            padding: 5px;
            margin-bottom: 20px;
        }
        .tab {
            flex: 1;
            padding: 12px;
            text-align: center;
            background: transparent;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
        }
        .tab.active {
            background: white;
            color: #007bff;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        .tab-content {
            display: none;
        }
        .tab-content.active {
            display: block;
        }
        .alert {
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            border: 1px solid transparent;
        }
        .alert.success {
            background: #d4edda;
            color: #155724;
            border-color: #c3e6cb;
        }
        .alert.error {
            background: #f8d7da;
            color: #721c24;
            border-color: #f5c6cb;
        }
        .alert.warning {
            background: #fff3cd;
            color: #856404;
            border-color: #ffeeba;
        }
        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid #f3f3f3;
            border-top: 3px solid #007bff;
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        @media (max-width: 768px) {
            .main-content {
                padding: 15px;
            }
            .dashboard {
                grid-template-columns: 1fr;
            }
            .connection-buttons {
                flex-direction: column;
            }
            .btn {
                width: 100%;
            }
        }
    </style>
</head>
<body>
<div id="loginModal" style="position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; background: rgba(0,0,0,0.8); z-index: 9999; display: flex; justify-content: center; align-items: center;">
  <div style="background: white; padding: 40px; border-radius: 15px; box-shadow: 0 10px 30px rgba(0,0,0,0.2); width: 300px; text-align: center;">
    <h2>Connexion</h2>
    <div style="margin-bottom: 15px;">
      <input type="text" id="username" placeholder="Utilisateur" style="width: 100%; padding: 10px; border-radius: 8px; border: 1px solid #ccc;">
    </div>
    <div style="margin-bottom: 15px;">
      <input type="password" id="password" placeholder="Mot de passe" style="width: 100%; padding: 10px; border-radius: 8px; border: 1px solid #ccc;">
    </div>
    <button onclick="checkLogin()" style="background: #f57200; color: white; padding: 10px 20px; border: none; border-radius: 8px; cursor: pointer;">Se connecter</button>
    <div id="loginError" style="color: red; margin-top: 10px; display: none;">Identifiants incorrects</div>
  </div>
</div>

<div class="container">
<div class="header" style="display: flex; align-items: center; justify-content: space-between;">
<div style="text-align: left;">
  <h1>🔌 Interface Arduino</h1>
  <p>Système de contrôle via USB ou Réseau</p>
  <p id="connectedUser" style="margin-top: 10px; font-weight: bold;"></p>
</div>

<img alt="IRT M2P" src="logo-irtm2p-large.png" style="height: 200px; max-width: 750px; margin-right: 20px;"/>
</div>
<div class="main-content">
<!-- Panneau de Connexion -->
<div class="connection-panel">
<div class="connection-status">
<div class="status-indicator" id="statusIndicator"></div>
<span id="connectionStatus">Déconnecté</span>
</div>
<div class="tabs">
<button class="tab active" onclick="switchTab(event, 'usb')">Connexion USB</button>
<button class="tab" onclick="switchTab(event, 'network')">Connexion Réseau</button>
</div>
<div class="tab-content active" id="usb-tab">
<div class="input-group">
<label for="usbPort">Port USB:</label>
<select id="usbPort">
<option value="">Sélectionner un port</option>
</select>
</div>
<div class="connection-buttons">
<button class="btn" onclick="connectUSB()">Se connecter via USB</button>
<button class="btn" onclick="requestAndScanUSBPorts()">🔄 Rechercher manuellement</button>
</div>
</div>
<div class="tab-content" id="network-tab">
<div class="input-group">
<label for="ipAddress">Adresse IP:</label>
<input id="ipAddress" placeholder="192.168.1.100" type="text"/>
</div>
<div class="input-group">
<label for="networkPort">Port:</label>
<input id="networkPort" placeholder="80" type="number"/>
</div>
<div class="connection-buttons">
<button class="btn" onclick="connectNetwork()">Se connecter au réseau</button>
</div>
</div>
<div class="connection-buttons">
<button class="btn danger" onclick="disconnect()">Déconnecter</button>
</div>
</div>
<!-- Tableau de Bord -->
<div class="dashboard">
<div class="card">
<h3>📊 Données Système</h3>
<div class="data-grid">
<div class="data-item">
<div class="data-value" id="currentDate">--/--/----</div>
<div class="data-value" id="currentTime">--:--:--</div>
<div class="data-label">Date &amp; Heure</div>
</div>
<div class="data-item">
<div class="data-value" id="voltage">--.-- V</div>
<div class="data-label">Tension</div>
</div>
<div class="data-item">
<div class="data-value" id="powerSource">---</div>
<div class="data-label">Source</div>
</div>
</div>
</div>
<div class="card">
<h3>🌡️ Températures</h3>
<div class="data-grid">
<div class="data-item">
<div class="data-value" id="tempExt">--.-- °C</div>
<div class="data-label">Extérieure</div>
</div>
<div class="data-item">
<div class="data-value" id="tempInt">--.-- °C</div>
<div class="data-label">Intérieure</div>
</div>
<div class="data-item">
<div class="data-value" id="tempDiff">--.-- °C</div>
<div class="data-label">Différence</div>
</div>
</div>
</div>
<div class="card">
<h3>🔌 Relais Ethernet (2-9)</h3>
<div class="relays-grid">
<div class="relay-item inactive" id="relay2">
<div class="relay-number">2</div>
<div class="relay-status">OFF</div>
</div>
<div class="relay-item inactive" id="relay3">
<div class="relay-number">3</div>
<div class="relay-status">OFF</div>
</div>
<div class="relay-item inactive" id="relay4">
<div class="relay-number">4</div>
<div class="relay-status">OFF</div>
</div>
<div class="relay-item inactive" id="relay5">
<div class="relay-number">5</div>
<div class="relay-status">OFF</div>
</div>
<div class="relay-item inactive" id="relay6">
<div class="relay-number">6</div>
<div class="relay-status">OFF</div>
</div>
<div class="relay-item inactive" id="relay7">
<div class="relay-number">7</div>
<div class="relay-status">OFF</div>
</div>
<div class="relay-item inactive" id="relay8">
<div class="relay-number">8</div>
<div class="relay-status">OFF</div>
</div>
<div class="relay-item inactive" id="relay9">
<div class="relay-number">9</div>
<div class="relay-status">OFF</div>
</div>
</div>
</div>
<div class="card">
<h3>💾 Relais Disque (31-45)</h3>
<div class="relays-grid">
<div class="relay-item inactive" id="relay31">
<div class="relay-number">31</div>
<div class="relay-status">OFF</div>
</div>
<div class="relay-item inactive" id="relay33">
<div class="relay-number">33</div>
<div class="relay-status">OFF</div>
</div>
<div class="relay-item inactive" id="relay35">
<div class="relay-number">35</div>
<div class="relay-status">OFF</div>
</div>
<div class="relay-item inactive" id="relay37">
<div class="relay-number">37</div>
<div class="relay-status">OFF</div>
</div>
<div class="relay-item inactive" id="relay39">
<div class="relay-number">39</div>
<div class="relay-status">OFF</div>
</div>
<div class="relay-item inactive" id="relay41">
<div class="relay-number">41</div>
<div class="relay-status">OFF</div>
</div>
<div class="relay-item inactive" id="relay43">
<div class="relay-number">43</div>
<div class="relay-status">OFF</div>
</div>
<div class="relay-item inactive" id="relay45">
<div class="relay-number">45</div>
<div class="relay-status">OFF</div>
</div>
</div>
</div>
</div>
<!-- Programmation des Horaires -->
<div class="schedule-container">
<div class="schedule-header" style="display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap;">
<h3 style="margin-right: auto;">📅 Programmation des Horaires</h3>
<div style="display: flex; gap: 10px; align-items: center; flex-wrap: wrap;">
<button onclick="generateFullArduinoCode()">🛠 Générer le code Arduino complet</button>
<button id="downloadBtn" onclick="downloadArduinoFile()" style="display:none;">📥 Télécharger le fichier Arduino (.ino)</button>
</div>
<textarea class="code-output" id="codeOutput" rows="100" style="width:100%; font-family:monospace; margin-top:10px;"></textarea>
</div>
<div class="tabs">
<button class="tab active" onclick="switchScheduleTab(event, 'ethernet')">Relais Ethernet</button>
<button class="tab" onclick="switchScheduleTab(event, 'disk')">Relais Disque</button>
</div>
<div class="tab-content active" id="ethernet-schedule">
<h4>Horaires Relais Ethernet (2-9)</h4>
<table class="schedule-table">
<thead>
<tr>
<th>Jour</th>
<th>Activé</th>
<th>Heure Début</th>
<th>Minute Début</th>
<th>Heure Fin</th>
<th>Minute Fin</th>
</tr>
</thead>
<tbody>
<tr>
<td>Lundi</td>
<td><input checked="" id="eth_lundi" type="checkbox"/></td>
<td><input class="time-input" id="eth_lundi_h_start" max="23" min="0" type="number" value="11"/></td>
<td><input class="time-input" id="eth_lundi_m_start" max="59" min="0" type="number" value="57"/></td>
<td><input class="time-input" id="eth_lundi_h_end" max="23" min="0" type="number" value="19"/></td>
<td><input class="time-input" id="eth_lundi_m_end" max="59" min="0" type="number" value="0"/></td>
</tr>
<tr>
<td>Mardi</td>
<td><input checked="" id="eth_mardi" type="checkbox"/></td>
<td><input class="time-input" id="eth_mardi_h_start" max="23" min="0" type="number" value="11"/></td>
<td><input class="time-input" id="eth_mardi_m_start" max="59" min="0" type="number" value="57"/></td>
<td><input class="time-input" id="eth_mardi_h_end" max="23" min="0" type="number" value="19"/></td>
<td><input class="time-input" id="eth_mardi_m_end" max="59" min="0" type="number" value="0"/></td>
</tr>
<tr>
<td>Mercredi</td>
<td><input checked="" id="eth_mercredi" type="checkbox"/></td>
<td><input class="time-input" id="eth_mercredi_h_start" max="23" min="0" type="number" value="11"/></td>
<td><input class="time-input" id="eth_mercredi_m_start" max="59" min="0" type="number" value="57"/></td>
<td><input class="time-input" id="eth_mercredi_h_end" max="23" min="0" type="number" value="19"/></td>
<td><input class="time-input" id="eth_mercredi_m_end" max="59" min="0" type="number" value="0"/></td>
</tr>
<tr>
<td>Jeudi</td>
<td><input checked="" id="eth_jeudi" type="checkbox"/></td>
<td><input class="time-input" id="eth_jeudi_h_start" max="23" min="0" type="number" value="11"/></td>
<td><input class="time-input" id="eth_jeudi_m_start" max="59" min="0" type="number" value="57"/></td>
<td><input class="time-input" id="eth_jeudi_h_end" max="23" min="0" type="number" value="19"/></td>
<td><input class="time-input" id="eth_jeudi_m_end" max="59" min="0" type="number" value="0"/></td>
</tr>
<tr>
<td>Vendredi</td>
<td><input checked="" id="eth_vendredi" type="checkbox"/></td>
<td><input class="time-input" id="eth_vendredi_h_start" max="23" min="0" type="number" value="19"/></td>
<td><input class="time-input" id="eth_vendredi_m_start" max="59" min="0" type="number" value="45"/></td>
<td><input class="time-input" id="eth_vendredi_h_end" max="23" min="0" type="number" value="23"/></td>
<td><input class="time-input" id="eth_vendredi_m_end" max="59" min="0" type="number" value="59"/></td>
</tr>
<tr>
<td>Samedi</td>
<td><input checked="" id="eth_samedi" type="checkbox"/></td>
<td><input class="time-input" id="eth_samedi_h_start" max="23" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="eth_samedi_m_start" max="59" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="eth_samedi_h_end" max="23" min="0" type="number" value="23"/></td>
<td><input class="time-input" id="eth_samedi_m_end" max="59" min="0" type="number" value="0"/></td>
</tr>
<tr>
<td>Dimanche</td>
<td><input checked="" id="eth_dimanche" type="checkbox"/></td>
<td><input class="time-input" id="eth_dimanche_h_start" max="23" min="0" type="number" value="11"/></td>
<td><input class="time-input" id="eth_dimanche_m_start" max="59" min="0" type="number" value="57"/></td>
<td><input class="time-input" id="eth_dimanche_h_end" max="23" min="0" type="number" value="19"/></td>
<td><input class="time-input" id="eth_dimanche_m_end" max="59" min="0" type="number" value="0"/></td>
</tr>
</tbody>
</table>
</div>
<div class="tab-content" id="disk-schedule">
<h4>Programmation Système 2 (Disques)</h4>
<table class="schedule-table">
<thead>
<tr>
<th>Jour</th>
<th>Heure Début</th>
<th>Minute Début</th>
<th>Heure Fin</th>
<th>Minute Fin</th>
<th>Actif Paire</th>
<th>Actif Impaire</th>
</tr>
</thead>
<tbody>
<!-- Lignes jours dynamiques -->
<tr>
<td>Lundi</td>
<td><input class="time-input" id="disk_lundi_h_start" max="23" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_lundi_m_start" max="59" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_lundi_h_end" max="23" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_lundi_m_end" max="59" min="0" type="number" value="0"/></td>
<td><input checked="" id="disk_lundi_even" type="checkbox"/></td>
<td><input checked="" id="disk_lundi_odd" type="checkbox"/></td>
</tr>
<tr>
<td>Mardi</td>
<td><input class="time-input" id="disk_mardi_h_start" max="23" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_mardi_m_start" max="59" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_mardi_h_end" max="23" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_mardi_m_end" max="59" min="0" type="number" value="0"/></td>
<td><input checked="" id="disk_mardi_even" type="checkbox"/></td>
<td><input checked="" id="disk_mardi_odd" type="checkbox"/></td>
</tr>
<tr>
<td>Mercredi</td>
<td><input class="time-input" id="disk_mercredi_h_start" max="23" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_mercredi_m_start" max="59" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_mercredi_h_end" max="23" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_mercredi_m_end" max="59" min="0" type="number" value="0"/></td>
<td><input checked="" id="disk_mercredi_even" type="checkbox"/></td>
<td><input checked="" id="disk_mercredi_odd" type="checkbox"/></td>
</tr>
<tr>
<td>Jeudi</td>
<td><input class="time-input" id="disk_jeudi_h_start" max="23" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_jeudi_m_start" max="59" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_jeudi_h_end" max="23" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_jeudi_m_end" max="59" min="0" type="number" value="0"/></td>
<td><input checked="" id="disk_jeudi_even" type="checkbox"/></td>
<td><input checked="" id="disk_jeudi_odd" type="checkbox"/></td>
</tr>
<tr>
<td>Vendredi</td>
<td><input class="time-input" id="disk_vendredi_h_start" max="23" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_vendredi_m_start" max="59" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_vendredi_h_end" max="23" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_vendredi_m_end" max="59" min="0" type="number" value="0"/></td>
<td><input checked="" id="disk_vendredi_even" type="checkbox"/></td>
<td><input checked="" id="disk_vendredi_odd" type="checkbox"/></td>
</tr>
<tr>
<td>Samedi</td>
<td><input class="time-input" id="disk_samedi_h_start" max="23" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_samedi_m_start" max="59" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_samedi_h_end" max="23" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_samedi_m_end" max="59" min="0" type="number" value="0"/></td>
<td><input checked="" id="disk_samedi_even" type="checkbox"/></td>
<td><input checked="" id="disk_samedi_odd" type="checkbox"/></td>
</tr>
<tr>
<td>Dimanche</td>
<td><input class="time-input" id="disk_dimanche_h_start" max="23" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_dimanche_m_start" max="59" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_dimanche_h_end" max="23" min="0" type="number" value="0"/></td>
<td><input class="time-input" id="disk_dimanche_m_end" max="59" min="0" type="number" value="0"/></td>
<td><input checked="" id="disk_dimanche_even" type="checkbox"/></td>
<td><input checked="" id="disk_dimanche_odd" type="checkbox"/></td>
</tr>
</tbody>
</table>
<h4>État des relais</h4>
<strong>Semaine Paire :</strong>
<div class="relays-grid">
<label><input id="relais_even_0" type="checkbox"/> 31</label>
<label><input id="relais_even_1" type="checkbox"/> 33</label>
<label><input id="relais_even_2" type="checkbox"/> 35</label>
<label><input id="relais_even_3" type="checkbox"/> 37</label>
<label><input id="relais_even_4" type="checkbox"/> 39</label>
<label><input id="relais_even_5" type="checkbox"/> 41</label>
<label><input id="relais_even_6" type="checkbox"/> 43</label>
<label><input id="relais_even_7" type="checkbox"/> 45</label>
</div>
<strong style="margin-top:20px;display:block;">Semaine Impaire :</strong>
<div class="relays-grid">
<label><input id="relais_odd_0" type="checkbox"/> 31</label>
<label><input id="relais_odd_1" type="checkbox"/> 33</label>
<label><input id="relais_odd_2" type="checkbox"/> 35</label>
<label><input id="relais_odd_3" type="checkbox"/> 37</label>
<label><input id="relais_odd_4" type="checkbox"/> 39</label>
<label><input id="relais_odd_5" type="checkbox"/> 41</label>
<label><input id="relais_odd_6" type="checkbox"/> 43</label>
<label><input id="relais_odd_7" type="checkbox"/> 45</label>
</div>
</div>
</div>
</div>
</div>
<script>
        
        // Variables globales
let isConnected = false;
let connectionType = 'usb';
let currentPort = null;
let updateInterval = null;
let serialPort = null;
let reader = null;
let serialBuffer=""; 

        // Initialisation
        document.addEventListener('DOMContentLoaded', function() {
            updateConnectionStatus();
            showAlert('Aucun Arduino connecté. Veuillez vous connecter.', 'error');
        });
        navigator.serial.addEventListener("connect", scanUSBPorts);
        navigator.serial.addEventListener("disconnect", () => {
    showAlert("Arduino déconnecté.", "error");
    disconnect();
});

        // Fonction pour changer d'onglet
        function switchTab(event, tabType) {
            const tabs = document.querySelectorAll('.connection-panel .tab');
            const contents = document.querySelectorAll('.connection-panel .tab-content');
            tabs.forEach(tab => tab.classList.remove('active'));
            contents.forEach(content => content.classList.remove('active'));
            // Activer l'onglet sélectionné
            document.getElementById(`${tabType}-tab`).classList.add('active');
            event.currentTarget.classList.add('active');
        }

        // Fonction pour changer d'onglet de programmation
        function switchScheduleTab(event, tabType) {
            const tabs = document.querySelectorAll('.schedule-container .tab');
            const contents = document.querySelectorAll('.schedule-container .tab-content');
            tabs.forEach(tab => tab.classList.remove('active'));
            contents.forEach(content => content.classList.remove('active'));
            // Activer l'onglet sélectionné
            document.getElementById(`${tabType}-schedule`).classList.add('active');
            event.currentTarget.classList.add('active');
        }

  // Fonction pour se connecter via USB
      // Fonction pour se connecter via USB
      let availablePorts = [];

      async function scanUSBPorts() {
    const usbPortSelect = document.getElementById('usbPort');
    usbPortSelect.innerHTML = '<option value="">Sélectionner un port</option>';
    availablePorts = [];

    try {
        const ports = await navigator.serial.getPorts();
        ports.forEach((port, index) => {
            availablePorts.push(port);
            const option = document.createElement('option');
            option.value = index;
            option.textContent = `Port ${index + 1}`;
            usbPortSelect.appendChild(option);
        });

        if (availablePorts.length === 0) {
            showAlert('Aucun port USB détecté.', 'warning');
        } else {
            showAlert('Ports USB détectés.', 'success');
        }
    } catch (error) {
        showAlert('Erreur lors du scan des ports USB: ' + error, 'error');
    }
}

async function connectUSB() {
    const selectedIndex = document.getElementById('usbPort').value;
    if (selectedIndex === "") {
        showAlert("Veuillez sélectionner un port.", "error");
        return;
    }

    const port = availablePorts[parseInt(selectedIndex)];

    try {
        await port.open({ baudRate: 9600 });
        serialPort = port;

        isConnected = true;
        connectionType = 'usb';
        currentPort = "USB";
        updateConnectionStatus();
        showAlert("Connecté à l'Arduino via USB.", "success");

        startReadingSerialData(); 
        startPeriodicUpdate();
    } catch (error) {
        showAlert("Erreur de connexion : " + error.message, "error");
    }
}

async function startReadingSerialData() {
    if (!serialPort || !serialPort.readable) {
        showAlert("Le port série n'est pas lisible.", "error");
        return;
    }

    const decoder = new TextDecoderStream();
    const readableStreamClosed = serialPort.readable.pipeTo(decoder.writable);
    const inputStream = decoder.readable;
    reader = inputStream.getReader();

    try {
        while (true) {
            const { value, done } = await reader.read();
            if (done) break;
            if (value) {
    serialBuffer += value;
    let lines = serialBuffer.split('\n');

    // On garde la dernière ligne partielle en buffer
    serialBuffer = lines.pop();

    lines.forEach(line => {
        if (line.trim() !== '') {
            processSerialData(line.trim());
        }
    });
}
        }
    } catch (error) {
        console.error("Erreur de lecture série :", error);
        showAlert("Erreur lecture série : " + error.message, "error");
    }
}



// Fonction pour traiter les données série
function processSerialData(data) {
    console.log("💬 Données reçues brutes:", JSON.stringify(data));
    const parts = data.split('|');
    parts.forEach(part => {
        const [key, value] = part.split(':');
        if (key && value) {
            switch (key.trim()) {
                case 'Tension':
                    document.getElementById('voltage').textContent = `${value.trim()} V`;
                    break;
                case 'Source':
                    document.getElementById('powerSource').textContent = value.trim();
                    break;
                case 'TempExt':
                    document.getElementById('tempExt').textContent = `${value.trim()} °C`;
                    break;
                case 'TempInt':
                    document.getElementById('tempInt').textContent = `${value.trim()} °C`;
                    break;
                case 'Relais':
                    updateRelayStatus(value.trim());
                    break;
                case 'Relais2':
                    updateRelayDisqueStatus(value.trim());
                    break;
            }
        }
    });
}

// Fonction pour mettre à jour l'état des relais
function updateRelayStatus(relayData) {
    const relays = relayData.split('');
    for (let i = 0; i < relays.length; i++) {
        const relayElement = document.getElementById(`relay${i + 2}`);
        if (relayElement) {
            if (relays[i] === '1') {
                relayElement.classList.remove('inactive');
                relayElement.classList.add('active');
                relayElement.querySelector('.relay-status').textContent = 'ON';
            } else {
                relayElement.classList.remove('active');
                relayElement.classList.add('inactive');
                relayElement.querySelector('.relay-status').textContent = 'OFF';
            }
        }
    }
}
function updateRelayDisqueStatus(relayData) {
    const relays = relayData.split('');
    for (let i = 0; i < relays.length; i++) {
        const pin = 31 + i * 2; // → 31, 33, ..., 45
        const relayElement = document.getElementById(`relay${pin}`);
        if (relayElement) {
            const isOn = relays[i] === '1';
            relayElement.classList.toggle('active', isOn);
            relayElement.classList.toggle('inactive', !isOn);
            relayElement.querySelector('.relay-status').textContent = isOn ? 'ON' : 'OFF';
        }
    }
}


        // Fonction pour se connecter au réseau
async function connectNetwork() {
startPeriodicUpdate();
updateInterval = setInterval(() => {
    fetchDataFromArduino(ipAddress, networkPort);
}, 1000);
    const ipAddress = document.getElementById('ipAddress').value;
    const networkPort = document.getElementById('networkPort').value;

    if (!isValidIPAddress(ipAddress)) {
        showAlert('Veuillez entrer une adresse IP valide.', 'error');
        return;
    }

    showAlert('Tentative de connexion en cours...', 'warning');

 try {
        // Tentative de connexion à l'Arduino via une requête HTTP GET
        const response = await fetch(`http://${ipAddress}:${networkPort}/api/data`);
        if (response.ok) {
            // Si la connexion est réussie, mettre à jour l'interface utilisateur
            isConnected = true;
            connectionType = 'network';
            currentPort = `${ipAddress}:${networkPort}`;
            updateConnectionStatus();
            showAlert(`Connecté au réseau à l'adresse ${currentPort}`, 'success');
            // Commencez à récupérer et mettre à jour les données
            startPeriodicUpdate();
            fetchDataFromArduino(ipAddress, networkPort);
        } else {
            // Gérer les erreurs de connexion
            showAlert('Échec de la connexion. Vérifiez l\'adresse IP et le port.', 'error');
        }
    } catch (error) {
        // Capturer les erreurs réseau
        showAlert('Erreur réseau: ' + error.message, 'error');
    }
}

async function fetchDataFromArduino(ipAddress, port) {
    try {
        const response = await fetch(`http://${ipAddress}:${port}/api/data`);
        if (response.ok) {
            const data = await response.json();  // ✅ le serveur renvoie du JSON
            console.log("Données JSON réseau :", data);
            console.log("✅ Données reçues du réseau :", data);

            updateUIWithData(data);              // ✅ mettre à jour l’interface
        } else {
            console.error('Erreur de réponse du serveur');
            showAlert('Erreur de réponse du serveur', 'error');
        }
    } catch (error) {
        console.error('Erreur réseau:', error);
        showAlert('Erreur réseau: ' + error.message, 'error');
    }
}

function updateUIWithData(data) {
    document.getElementById('voltage').textContent = `${data.Tension ?? data.Voltage ?? '--'} V`;
    document.getElementById('powerSource').textContent = data.Source ?? '---';
    document.getElementById('tempExt').textContent = `${data.TempExt ?? '--'} °C`;
    document.getElementById('tempInt').textContent = `${data.TempInt ?? '--'} °C`;

    const diff = Math.abs((parseFloat(data.TempExt ?? 0) - parseFloat(data.TempInt ?? 0))).toFixed(2);
    document.getElementById('tempDiff').textContent = `${diff} °C`;

   const relais = typeof data.Relais === 'string' ? data.Relais :
                  typeof data.relais === 'string' ? data.relais :
                  null;

    if (!relais) {
        console.warn("⚠️ Aucune donnée 'Relais' dans la réponse JSON : ", data);
        return; // ❌ On quitte sans essayer relais.length
    }

  for (let i = 0; i < relais.length; i++) {
        const relayElement = document.getElementById(`relay${i + 2}`);
        if (relayElement) {
            const isOn = relais[i] === '1';
            relayElement.classList.toggle('active', isOn);
            relayElement.classList.toggle('inactive', !isOn);
            relayElement.querySelector('.relay-status').textContent = isOn ? 'ON' : 'OFF';
        }
    }

    const relais2 = typeof data.Relais2 === 'string' ? data.Relais2 :
                    typeof data.relais2 === 'string' ? data.relais2 :
                    null;

    if (relais2) {
        for (let i = 0; i < relais2.length; i++) {
            const relayElement = document.getElementById(`relay${31 + i * 2}`);
            if (relayElement) {
                const isOn = relais2[i] === '1';
                relayElement.classList.toggle('active', isOn);
                relayElement.classList.toggle('inactive', !isOn);
                relayElement.querySelector('.relay-status').textContent = isOn ? 'ON' : 'OFF';
            }
        }
    }

}
const relais2 = typeof data.Relais2 === 'string' ? data.Relais2 :
                typeof data.relais2 === 'string' ? data.relais2 :
                null;

if (relais2) {
    for (let i = 0; i < relais2.length; i++) {
        const relayElement = document.getElementById(`relay${31 + i * 2}`);
        if (relayElement) {
            const isOn = relais2[i] === '1';
            relayElement.classList.toggle('active', isOn);
            relayElement.classList.toggle('inactive', !isOn);
            relayElement.querySelector('.relay-status').textContent = isOn ? 'ON' : 'OFF';
        }
    }
}


        // Fonction pour vérifier la validité de l'adresse IP
        function isValidIPAddress(ipAddress) {
            const ipPattern = /^(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/;
            return ipPattern.test(ipAddress);
        }


        // Fonction pour se déconnecter
async function disconnect() {
    try {
        if (reader) {
            await reader.cancel();
            await reader.releaseLock();
            reader = null;
        }

        if (serialPort) {
            if (serialPort.readable) {
                await serialPort.close();
            }
            serialPort = null;
        }

        isConnected = false;
        currentPort = null;
        updateConnectionStatus();
        resetDataDisplay();
        clearInterval(updateInterval);
        showAlert("Déconnecté avec succès", "warning");
    } catch (error) {
        console.error("Erreur lors de la déconnexion :", error);
        showAlert("Erreur de déconnexion : " + error.message, "error");
    }
}

        //Fonction pour connecter de force
async function requestAndScanUSBPorts() {
    try {
        await navigator.serial.requestPort(); // ➕ affiche la popup
        await scanUSBPorts();                // 🔁 relance le scan
    } catch (error) {
        showAlert("Aucun port sélectionné", "error");
    }
}


        // Fonction pour générer le code
        function generateCode() {
            if (isConnected) {
                const codeOutput = document.getElementById('codeOutput');
                codeOutput.textContent = '// Code généré pour la programmation des relais\n\nvoid setup() {\n  // Initialisation des relais\n}\n\nvoid loop() {\n  // Logique de contrôle des relais\n}';
                showAlert('Code généré avec succès', 'success');
            } else {
                showAlert('Veuillez vous connecter à l\'Arduino pour générer le code.', 'error');
            }
        }

        // Fonction pour mettre à jour la programmation des relais des disques
        function updateDiskRelaySchedule() {
            const weekType = document.getElementById('diskWeekType').value;
            showAlert(`Configuration mise à jour pour les semaines ${weekType === 'even' ? 'paires' : 'impaires'}`, 'success');
        }



        // Fonction pour réinitialiser l'affichage des données
        function resetDataDisplay() {
            document.getElementById('currentTime').textContent = '--:--:--';
            document.getElementById('currentDate').textContent = '--/--/----';
            document.getElementById('voltage').textContent = '--.-- V';
            document.getElementById('powerSource').textContent = '---';
            document.getElementById('tempExt').textContent = '--.-- °C';
            document.getElementById('tempInt').textContent = '--.-- °C';
            document.getElementById('tempDiff').textContent = '--.-- °C';
        }

        // Fonction pour mettre à jour l'affichage
        function updateDisplay() {
            if (!isConnected) return;
            const now = new Date();
            document.getElementById('currentTime').textContent = now.toLocaleTimeString();
            document.getElementById('currentDate').textContent = now.toLocaleDateString();
        }

        // Fonction pour mettre à jour le statut de connexion
        function updateConnectionStatus() {
            const statusIndicator = document.getElementById('statusIndicator');
            const connectionStatus = document.getElementById('connectionStatus');
            if (isConnected) {
                statusIndicator.classList.add('connected');
                connectionStatus.textContent = 'Connecté';
            } else {
                statusIndicator.classList.remove('connected');
                connectionStatus.textContent = 'Déconnecté';
            }
        }

        // Fonction pour afficher une alerte
        function showAlert(message, type) {
            const alertDiv = document.createElement('div');
            alertDiv.className = `alert ${type}`;
            alertDiv.textContent = message;
            const mainContent = document.querySelector('.main-content');
            mainContent.insertBefore(alertDiv, mainContent.firstChild);
            setTimeout(() => {
                alertDiv.remove();
            }, 3000);
        }

        // Fonction pour démarrer la mise à jour périodique
        function startPeriodicUpdate() {
            updateInterval = setInterval(updateDisplay, 1000);
        }

        // Fonction pour emmettre le code

function generateFullArduinoCode() {
  const jours = ['lundi', 'mardi', 'mercredi', 'jeudi', 'vendredi', 'samedi', 'dimanche'];
  const jourIndex = { lundi: 1, mardi: 2, mercredi: 3, jeudi: 4, vendredi: 5, samedi: 6, dimanche: 7 };

  function buildSystem1Block() {
    let bloc = `// ------ CONFIGURATION DES RELAIS SYSTÈME 1 ------\n`;
    bloc += `struct RelaisSystem1Config {\n  int dayOfWeek;\n  int startHour;\n  int startMinute;\n  int endHour;\n  int endMinute;\n  bool active;\n};\n\n`;
    bloc += `RelaisSystem1Config relaisSystem1Schedule[] = {\n`;

    jours.forEach(jour => {
      const enabled = document.getElementById(`eth_${jour}`).checked;
      const hs = document.getElementById(`eth_${jour}_h_start`).value;
      const ms = document.getElementById(`eth_${jour}_m_start`).value;
      const he = document.getElementById(`eth_${jour}_h_end`).value;
      const me = document.getElementById(`eth_${jour}_m_end`).value;
      bloc += `  {${jourIndex[jour]}, ${hs}, ${ms}, ${he}, ${me}, ${enabled}},   // ${capitalize(jour)}\n`;
    });

    bloc += `};\n\n`;
    return bloc;
  }

  function buildSystem2Block() {
    let bloc = `// ------ CONFIGURATION DES RELAIS SYSTÈME 2 ------\n`;
    bloc += `struct RelaisSystem2Config {\n  int dayOfWeek;\n  int startHour;\n  int startMinute;\n  int endHour;\n  int endMinute;\n  bool semainePaire[8];\n  bool semaineImpaire[8];\n  bool active;\n};\n\n`;
    bloc += `RelaisSystem2Config relaisSystem2Schedule[] = {\n`;

    jours.forEach(jour => {
      const enabled = document.getElementById(`disk_${jour}`).checked;
      const hs = document.getElementById(`disk_${jour}_h_start`).value;
      const ms = document.getElementById(`disk_${jour}_m_start`).value;
      const he = document.getElementById(`disk_${jour}_h_end`).value;
      const me = document.getElementById(`disk_${jour}_m_end`).value;

      // Par défaut, hardcoded exemple : activer les deux premiers relais en paire ou impaire
      // (tu peux ensuite les modifier à la main dans le fichier généré si besoin)
      const semainePaire = `{true, true, false, false, false, false, false, false}`;
      const semaineImpaire = `{false, false, true, true, false, false, false, false}`;

      bloc += `  {${jourIndex[jour]}, ${hs}, ${ms}, ${he}, ${me}, ${semainePaire}, ${semaineImpaire}, ${enabled}},  // ${capitalize(jour)}\n`;
    });

    bloc += `};\n\n`;
    return bloc;
  }

  function capitalize(str) {
    return str.charAt(0).toUpperCase() + str.slice(1);
  }

  const system1Code = buildSystem1Block();
  const system2Code = buildSystem2Block();

  const fullCode = `// === CODE GÉNÉRÉ PAR L'INTERFACE ===\n\n${system1Code}${system2Code}`;
  document.getElementById("codeOutput").value = fullCode;
  document.getElementById("downloadBtn").style.display = "inline-block";
}



            //Fonction de téléchargement du fichier 
function downloadArduinoFile() {
  const code = document.getElementById("codeOutput").value;
  const blob = new Blob([code], { type: "text/plain" });
  const url = URL.createObjectURL(blob);

  const a = document.createElement("a");
  a.href = url;
  a.download = "relais_smart_schedule.ino"; // nom du fichier
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  URL.revokeObjectURL(url);
}




    
function generateFullArduinoCode() {
  const jours = ['lundi','mardi','mercredi','jeudi','vendredi','samedi','dimanche'];
  const jourIndex = { lundi:1, mardi:2, mercredi:3, jeudi:4, vendredi:5, samedi:6, dimanche:7 };

  function capitalize(str) {
    return str.charAt(0).toUpperCase() + str.slice(1);
  }

  // Système 1
  let sys1 = `// ------ CONFIGURATION DES RELAIS SYSTÈME 1 ------\n`;
  sys1 += `struct RelaisSystem1Config {\n  int dayOfWeek;\n  int startHour;\n  int startMinute;\n  int endHour;\n  int endMinute;\n  bool active;\n};\n\n`;
  sys1 += `RelaisSystem1Config relaisSystem1Schedule[] = {\n`;

  jours.forEach(jour => {
    const hs = document.getElementById(`eth_${jour}_h_start`).value;
    const ms = document.getElementById(`eth_${jour}_m_start`).value;
    const he = document.getElementById(`eth_${jour}_h_end`).value;
    const me = document.getElementById(`eth_${jour}_m_end`).value;
    const enabled = document.getElementById(`eth_${jour}`).checked ? "true" : "false";
    sys1 += `  {${jourIndex[jour]}, ${hs}, ${ms}, ${he}, ${me}, ${enabled}},  // ${capitalize(jour)}\n`;
  });

  sys1 += `};\n\n`;

  // Système 2 - horaires
  let horaires = `// ------ CONFIGURATION DES HORAIRES ------\n`;
  horaires += `struct HoraireConfig {\n  int dayOfWeek;\n  int startHour;\n  int startMinute;\n  int endHour;\n  int endMinute;\n  bool activeEvenWeek;\n  bool activeOddWeek;\n};\n\n`;
  horaires += `HoraireConfig relaisSystem2Horaires[] = {\n`;

  jours.forEach(jour => {
    const hs = document.getElementById(`disk_${jour}_h_start`).value;
    const ms = document.getElementById(`disk_${jour}_m_start`).value;
    const he = document.getElementById(`disk_${jour}_h_end`).value;
    const me = document.getElementById(`disk_${jour}_m_end`).value;
    const even = document.getElementById(`disk_${jour}_even`).checked ? "true" : "false";
    const odd = document.getElementById(`disk_${jour}_odd`).checked ? "true" : "false";
    horaires += `  {${jourIndex[jour]}, ${hs}, ${ms}, ${he}, ${me}, ${even}, ${odd}},  // ${capitalize(jour)}\n`;
  });

  horaires += `};\n\n`;

  // Système 2 - états relais
  let relais = `// ------ CONFIGURATION DES ÉTATS DES RELAIS ------\n`;
  relais += `struct RelaisStateConfig {\n  bool evenWeekRelais[8];\n  bool oddWeekRelais[8];\n};\n\n`;
  relais += `RelaisStateConfig relaisSystem2States = {\n  {`;

  const pair = [], impair = [];
  for (let i = 0; i < 8; i++) {
    pair.push(document.getElementById(`relais_even_${i}`).checked ? "true" : "false");
    impair.push(document.getElementById(`relais_odd_${i}`).checked ? "true" : "false");
  }
  relais += pair.join(', ') + '},\n  {' + impair.join(', ') + '}\n};\n';

  const full = `// === CODE GÉNÉRÉ PAR L'INTERFACE ===\n\n` + sys1 + horaires + relais;
  document.getElementById("codeOutput").value = full;
  document.getElementById("downloadBtn").style.display = "inline-block";
}
function checkLogin() {
    const users = {
        "huber.benjamin": "57jg;Gu!retkP",
        "fiolle.frederic": "password123",
    };

    const inputUser = document.getElementById("username").value;
    const inputPass = document.getElementById("password").value;

    if (users[inputUser] && users[inputUser] === inputPass) {
        document.getElementById("loginModal").style.display = "none";
        document.body.style.overflow = 'auto';
       const userDisplay = document.getElementById("connectedUser");
        if (userDisplay) {
            userDisplay.textContent = `👤 Connecté : ${inputUser}`;
        }
    } else {
        document.getElementById("loginError").style.display = "block";
    }
}

// Optionnel : empêcher interaction avec touches tant que non connecté
window.addEventListener('DOMContentLoaded', () => {
  document.body.style.overflow = 'hidden';
});

</script>
</body>
</html>
