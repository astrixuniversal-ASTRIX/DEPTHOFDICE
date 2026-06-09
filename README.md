# DEPTHOFDICE
This is a highly creative and abstract concept. I'll create a complete OpenSCAD file with the nested cubes (111mm inside 1.6m inside 11m inside 11km) and an interactive HTML interface that communicates via WebSocket loopback on ports 777/888 with all 6 sides plus the central AI mind.

```scad
// ============================================================
// ASTRiX-AI NESTED CUBES - OpenSCAD
// Inner: 111mm → Middle1: 1.6m → Middle2: 11m → Outer: 11km
// Center: ASTRiX-AI(0,0,0) - Loopback broadcast node
// ============================================================

// Scale factor for visualization (11km would be enormous)
// Using logarithmic display scale for practical viewing
viz_scale = 0.001; // 1 unit = 1mm in viewport

module astrix_ai_core() {
    // The AI mind at center - pulsating core
    color("cyan", 0.9) 
    sphere(r=5, $fn=32);
    
    // Energy rings
    for(i = [0:60:300]) {
        rotate([i, i*0.7, i*0.3])
        color("magenta", 0.4)
        torus(r1=8, r2=1.5);
    }
    
    // Connection nodes
    for(angle = [0:90:270]) {
        rotate([0, 0, angle])
        translate([12, 0, 0])
        color("yellow") sphere(r=2, $fn=16);
        
        rotate([90, 0, angle])
        translate([12, 0, 0])
        color("yellow") sphere(r=2, $fn=16);
        
        rotate([0, 90, angle])
        translate([12, 0, 0])
        color("lime") sphere(r=2, $fn=16);
    }
}

module torus(r1, r2) {
    rotate_extrude($fn=32)
    translate([r1, 0, 0])
    circle(r=r2, $fn=16);
}

module cube_111mm() {
    // Inner cube - 111mm
    size = 111;
    difference() {
        color("orange", 0.3) 
        cube(size, center=true);
        
        // Window cutouts on each face
        for(axis = [[1,0,0], [-1,0,0], [0,1,0], [0,-1,0], [0,0,1], [0,0,-1]]) {
            translate([axis[0]*size/2, axis[1]*size/2, axis[2]*size/2])
            rotate(axis[0] != 0 ? [0,90,0] : axis[1] != 0 ? [90,0,0] : [0,0,0])
            cylinder(h=5, d=40, center=true, $fn=6);
        }
    }
    
    // Face labels
    color("white")
    translate([0, 0, size/2+1])
    linear_extrude(1)
    text("TOP", size=10, halign="center", valign="center");
    
    color("white")
    translate([0, 0, -size/2-1])
    rotate([180,0,0])
    linear_extrude(1)
    text("BOTTOM", size=10, halign="center", valign="center");
    
    color("white")
    translate([size/2+1, 0, 0])
    rotate([90,0,90])
    linear_extrude(1)
    text("RIGHT", size=10, halign="center", valign="center");
    
    color("white")
    translate([-size/2-1, 0, 0])
    rotate([90,0,-90])
    linear_extrude(1)
    text("LEFT", size=10, halign="center", valign="center");
    
    color("white")
    translate([0, size/2+1, 0])
    rotate([90,0,0])
    linear_extrude(1)
    text("FRONT", size=10, halign="center", valign="center");
    
    color("white")
    translate([0, -size/2-1, 0])
    rotate([-90,0,0])
    linear_extrude(1)
    text("BACK", size=10, halign="center", valign="center");
}

module cube_1_6m() {
    // Middle cube 1 - 1.6m = 1600mm
    size = 1600;
    difference() {
        color("blue", 0.15) 
        cube(size, center=true);
        cube(size-10, center=true); // Hollow
    }
    
    // Wireframe edges
    color("cyan", 0.5)
    for(x = [-1,1], y = [-1,1], z = [-1,1]) {
        translate([x*size/2, y*size/2, z*size/2])
        sphere(r=8);
    }
}

module cube_11m() {
    // Middle cube 2 - 11m = 11000mm
    size = 11000;
    difference() {
        color("purple", 0.08) 
        cube(size, center=true);
        cube(size-20, center=true);
    }
    
    // Corner markers
    color("magenta", 0.6)
    for(x = [-1,1], y = [-1,1], z = [-1,1]) {
        translate([x*size/2, y*size/2, z*size/2])
        sphere(r=15);
    }
}

module cube_11km() {
    // Outer cube - 11km = 11000000mm
    size = 11000000;
    difference() {
        color("red", 0.03) 
        cube(size, center=true);
        cube(size-50, center=true);
    }
}

// Data stream visualization
module data_streams() {
    for(i = [0:45:315]) {
        rotate([0, 0, i])
        for(j = [0:30:150]) {
            rotate([j, i, 0])
            translate([0, 0, 55])
            color("green", 0.2 + sin($t*10 + i + j)*0.3)
            cylinder(h=20, d=1, center=true);
        }
    }
}

// ============================================================
// ASSEMBLY
// ============================================================
scale([viz_scale, viz_scale, viz_scale])
union() {
    // Center AI Core
    astrix_ai_core();
    
    // Nested cubes
    cube_111mm();
    
    scale([1600/111, 1600/111, 1600/111])
    cube_1_6m();
    
    scale([11000/111, 11000/111, 11000/111])
    cube_11m();
    
    scale([11000000/111, 11000000/111, 11000000/111])
    cube_11km();
    
    // Data streams (animated in preview)
    // data_streams();
}

// ============================================================
// INFO PANEL
// ============================================================
echo("========================================");
echo("  ASTRiX-AI NESTED CUBE SYSTEM");
echo("========================================");
echo("  Inner Cube:    111 mm");
echo("  Middle Cube 1: 1.6 m  (1,600 mm)");
echo("  Middle Cube 2: 11 m   (11,000 mm)");
echo("  Outer Cube:    11 km  (11,000,000 mm)");
echo("  AI Core:       ASTRiX-AI(0,0,0)");
echo("  WebSocket TX:  ws://localhost:777");
echo("  WebSocket RX:  ws://localhost:888");
echo("========================================");
```

Now, here's the complete HTML interface with slide-out menu, all 6 cube faces, and the AI mind loopback system:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ASTRiX-AI :: Nested Cube System :: 111mm → 1.6m → 11m → 11km</title>
    <style>
        :root {
            --bg: #0a0a0f;
            --panel: #111118;
            --border: #1a1a2e;
            --accent: #00ffaa;
            --accent2: #ff00ff;
            --accent3: #00aaff;
            --text: #c0c0d0;
            --glow: 0 0 20px rgba(0,255,170,0.3);
            --font-mono: 'Courier New', monospace;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: var(--bg);
            color: var(--text);
            font-family: var(--font-mono);
            overflow: hidden;
            height: 100vh;
            display: flex;
        }

        /* ==================== SLIDE-OUT MENU ==================== */
        #menu-toggle {
            position: fixed;
            top: 20px;
            left: 20px;
            z-index: 1000;
            width: 50px;
            height: 50px;
            background: var(--panel);
            border: 2px solid var(--accent);
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
            box-shadow: var(--glow);
        }

        #menu-toggle:hover {
            box-shadow: 0 0 30px rgba(0,255,170,0.6);
            transform: scale(1.1);
        }

        #menu-toggle span {
            font-size: 24px;
            color: var(--accent);
        }

        #slide-menu {
            position: fixed;
            top: 0;
            left: -400px;
            width: 380px;
            height: 100vh;
            background: rgba(10, 10, 20, 0.95);
            border-right: 2px solid var(--accent);
            z-index: 999;
            transition: left 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            padding: 80px 20px 20px;
            overflow-y: auto;
            backdrop-filter: blur(20px);
            box-shadow: 10px 0 40px rgba(0,0,0,0.8);
        }

        #slide-menu.open {
            left: 0;
        }

        #slide-menu h2 {
            color: var(--accent);
            font-size: 1.4em;
            margin-bottom: 20px;
            text-shadow: 0 0 10px var(--accent);
            border-bottom: 1px solid var(--accent);
            padding-bottom: 10px;
        }

        .face-btn {
            display: block;
            width: 100%;
            padding: 14px 20px;
            margin: 8px 0;
            background: var(--panel);
            border: 1px solid var(--border);
            color: var(--text);
            cursor: pointer;
            font-family: var(--font-mono);
            font-size: 0.95em;
            text-align: left;
            transition: all 0.25s;
            border-radius: 8px;
            position: relative;
            overflow: hidden;
        }

        .face-btn:hover {
            border-color: var(--accent);
            box-shadow: 0 0 15px rgba(0,255,170,0.2);
            color: var(--accent);
            transform: translateX(5px);
        }

        .face-btn::before {
            content: '';
            position: absolute;
            left: 0;
            top: 0;
            width: 4px;
            height: 100%;
            background: var(--accent);
            transform: scaleY(0);
            transition: transform 0.3s;
        }

        .face-btn:hover::before {
            transform: scaleY(1);
        }

        .face-btn.top {
            border-left: 3px solid #ff6b6b;
        }
        .face-btn.bottom {
            border-left: 3px solid #ffd93d;
        }
        .face-btn.front {
            border-left: 3px solid #6bcb77;
        }
        .face-btn.back {
            border-left: 3px solid #4d96ff;
        }
        .face-btn.left {
            border-left: 3px solid #ff922b;
        }
        .face-btn.right {
            border-left: 3px solid #845ef7;
        }
        .face-btn.ai-mind {
            border-left: 3px solid #ff00ff;
            background: linear-gradient(135deg, #111118, #1a0a2e);
            animation: pulse-ai 2s infinite;
        }

        @keyframes pulse-ai {
            0%,
            100% {
                box-shadow: 0 0 5px rgba(255, 0, 255, 0.2);
            }
            50% {
                box-shadow: 0 0 25px rgba(255, 0, 255, 0.6);
            }
        }

        #slide-menu .status {
            margin-top: 30px;
            padding: 15px;
            background: #0a0a15;
            border-radius: 8px;
            border: 1px solid var(--border);
            font-size: 0.8em;
        }

        .status-dot {
            display: inline-block;
            width: 8px;
            height: 8px;
            border-radius: 50%;
            margin-right: 8px;
            animation: blink 1s infinite;
        }

        .status-dot.active {
            background: #00ff00;
            box-shadow: 0 0 10px #00ff00;
        }
        .status-dot.inactive {
            background: #ff0000;
            box-shadow: 0 0 10px #ff0000;
        }

        @keyframes blink {
            0%,
            100% {
                opacity: 1;
            }
            50% {
                opacity: 0.3;
            }
        }

        /* ==================== MAIN CONTENT ==================== */
        #main-content {
            flex: 1;
            display: flex;
            flex-direction: column;
            padding: 20px;
            margin-left: 0;
            transition: margin-left 0.4s;
        }

        .header {
            text-align: center;
            padding: 20px;
            border-bottom: 1px solid var(--border);
            margin-bottom: 20px;
        }

        .header h1 {
            color: var(--accent);
            font-size: 1.6em;
            text-shadow: 0 0 15px var(--accent);
            letter-spacing: 3px;
        }

        .header .subtitle {
            color: #666;
            font-size: 0.75em;
            margin-top: 5px;
        }

        #render-area {
            flex: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            background: radial-gradient(ellipse at center, #111118 0%, #0a0a0f 70%);
            border: 1px solid var(--border);
            border-radius: 12px;
            overflow: hidden;
        }

        /* 3D Cube visualization in canvas */
        #cube-canvas {
            width: 100%;
            height: 100%;
        }

        /* ==================== POPOUT WINDOW ==================== */
        #popout-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            z-index: 2000;
            justify-content: center;
            align-items: center;
        }

        #popout-overlay.active {
            display: flex;
        }

        #popout-window {
            width: 85vw;
            height: 85vh;
            background: var(--panel);
            border: 2px solid var(--accent);
            border-radius: 16px;
            display: flex;
            flex-direction: column;
            box-shadow: 0 0 60px rgba(0, 255, 170, 0.3);
            animation: popIn 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        @keyframes popIn {
            from {
                transform: scale(0.5);
                opacity: 0;
            }
            to {
                transform: scale(1);
                opacity: 1;
            }
        }

        #popout-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 25px;
            border-bottom: 1px solid var(--border);
            background: rgba(0, 0, 0, 0.3);
            border-radius: 16px 16px 0 0;
        }

        #popout-title {
            color: var(--accent);
            font-size: 1.2em;
            text-shadow: 0 0 10px var(--accent);
        }

        #popout-close {
            width: 40px;
            height: 40px;
            background: none;
            border: 2px solid #ff4444;
            color: #ff4444;
            border-radius: 50%;
            cursor: pointer;
            font-size: 1.2em;
            transition: all 0.3s;
        }

        #popout-close:hover {
            background: #ff4444;
            color: white;
            box-shadow: 0 0 20px rgba(255, 68, 68, 0.5);
        }

        #popout-body {
            flex: 1;
            padding: 25px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        #popout-body h3 {
            color: var(--accent2);
            margin-bottom: 10px;
        }

        .info-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
        }

        .info-card {
            background: rgba(20, 20, 30, 0.6);
            border: 1px solid var(--border);
            border-radius: 10px;
            padding: 15px;
            transition: all 0.3s;
        }

        .info-card:hover {
            border-color: var(--accent);
            box-shadow: 0 0 15px rgba(0, 255, 170, 0.15);
        }

        .info-card .label {
            font-size: 0.7em;
            color: #666;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .info-card .value {
            font-size: 1.1em;
            color: var(--accent);
            margin-top: 5px;
        }

        /* ==================== CONSOLE LOG ==================== */
        #console-log {
            position: fixed;
            bottom: 20px;
            right: 20px;
            width: 350px;
            max-height: 200px;
            background: rgba(10, 10, 20, 0.9);
            border: 1px solid var(--border);
            border-radius: 10px;
            padding: 10px;
            font-size: 0.7em;
            overflow-y: auto;
            z-index: 500;
            backdrop-filter: blur(10px);
        }

        #console-log .log-entry {
            padding: 3px 0;
            border-bottom: 1px solid #1a1a2e;
        }

        #console-log .log-entry.tx {
            color: #00ff88;
        }
        #console-log .log-entry.rx {
            color: #ff88ff;
        }
        #console-log .log-entry.system {
            color: #8888ff;
        }

        /* ==================== RESPONSIVE ==================== */
        @media (max-width: 768px) {
            #slide-menu {
                width: 300px;
                left: -300px;
            }
            #popout-window {
                width: 95vw;
                height: 90vh;
            }
            #console-log {
                width: 250px;
                bottom: 10px;
                right: 10px;
            }
        }
    </style>
</head>
<body>

    <!-- MENU TOGGLE BUTTON -->
    <div id="menu-toggle" onclick="toggleMenu()">
        <span>☰</span>
    </div>

    <!-- SLIDE-OUT MENU -->
    <div id="slide-menu">
        <h2>🌀 ASTRiX-AI<br><small>Nested Cube Network</small></h2>

        <button class="face-btn top" onclick="openFace('TOP', '111mm')">
            ⬆ TOP FACE — +Z — 111mm
        </button>
        <button class="face-btn bottom" onclick="openFace('BOTTOM', '111mm')">
            ⬇ BOTTOM FACE — -Z — 111mm
        </button>
        <button class="face-btn front" onclick="openFace('FRONT', '111mm')">
            ▶ FRONT FACE — +Y — 111mm
        </button>
        <button class="face-btn back" onclick="openFace('BACK', '111mm')">
            ◀ BACK FACE — -Y — 111mm
        </button>
        <button class="face-btn left" onclick="openFace('LEFT', '111mm')">
            ⬅ LEFT FACE — -X — 111mm
        </button>
        <button class="face-btn right" onclick="openFace('RIGHT', '111mm')">
            ➡ RIGHT FACE — +X — 111mm
        </button>
        <hr style="border-color:#1a1a2e; margin:15px 0;">
        <button class="face-btn ai-mind" onclick="openAIMind()">
            🧠 ASTRiX-AI(0,0,0) — Loopback Core
        </button>
        <button class="face-btn" onclick="openFace('1.6m', '1.6m')" style="border-left:3px solid #00aaff;">
            📦 MIDDLE CUBE — 1.6 meters
        </button>
        <button class="face-btn" onclick="openFace('11m', '11m')" style="border-left:3px solid #aa00ff;">
            📦 OUTER CUBE — 11 meters
        </button>
        <button class="face-btn" onclick="openFace('11km', '11km')" style="border-left:3px solid #ff5500;">
            🌐 MEGA CUBE — 11 kilometers
        </button>

        <div class="status">
            <strong>NETWORK STATUS</strong><br><br>
            <div><span class="status-dot active" id="dot-tx"></span> TX :777 (Broadcast)</div>
            <div style="margin-top:5px;"><span class="status-dot active" id="dot-rx"></span> RX :888 (Receive)</div>
            <div style="margin-top:5px;"><span class="status-dot active" id="dot-loop"></span> LOOPBACK ACTIVE</div>
            <div style="margin-top:10px; font-size:0.7em; color:#666;">
                6 Faces + AI Core<br>
                111mm → 1.6m → 11m → 11km
            </div>
        </div>
    </div>

    <!-- MAIN CONTENT AREA -->
    <div id="main-content">
        <div class="header">
            <h1>🟦 ASTRiX-AI NESTED CUBE SYSTEM</h1>
            <div class="subtitle">
                111mm ⊂ 1.6m ⊂ 11m ⊂ 11km &nbsp;|&nbsp; 
                LOOPBACK ::777→::888 &nbsp;|&nbsp; 
                <span style="color:#00ffaa;">6-SIDED HTML NETWORK 🛜</span>
            </div>
        </div>

        <div id="render-area">
            <canvas id="cube-canvas"></canvas>
        </div>
    </div>

    <!-- POPOUT WINDOW -->
    <div id="popout-overlay">
        <div id="popout-window">
            <div id="popout-header">
                <span id="popout-title">CUBE FACE</span>
                <button id="popout-close" onclick="closePopout()">✕</button>
            </div>
            <div id="popout-body">
                <!-- Dynamic content loads here -->
            </div>
        </div>
    </div>

    <!-- CONSOLE LOG -->
    <div id="console-log">
        <div class="log-entry system">[ASTRiX-AI] System boot...</div>
    </div>

    <script>
        // ============================================================
        // ASTRiX-AI LOOPBACK SYSTEM
        // TX: WebSocket Server on localhost:777 (simulated broadcast)
        // RX: WebSocket Client on localhost:888 (simulated receive)
        // ============================================================

        let txSocket = null;
        let rxSocket = null;
        let loopbackActive = false;

        const CUBE_DATA = {
            inner: { size: 111, unit: 'mm', faces: ['TOP', 'BOTTOM', 'FRONT', 'BACK', 'LEFT', 'RIGHT'] },
            middle1: { size: 1600, unit: 'mm', label: '1.6 meters' },
            middle2: { size: 11000, unit: 'mm', label: '11 meters' },
            outer: { size: 11000000, unit: 'mm', label: '11 kilometers' },
            aiCore: { position: [0, 0, 0], label: 'ASTRiX-AI(0,0,0)' }
        };

        // Console log function
        function logMessage(message, type = 'system') {
            const consoleEl = document.getElementById('console-log');
            const entry = document.createElement('div');
            entry.className = `log-entry ${type}`;
            const timestamp = new Date().toLocaleTimeString();
            entry.textContent = `[${timestamp}] ${message}`;
            consoleEl.appendChild(entry);
            consoleEl.scrollTop = consoleEl.scrollHeight;

            // Keep only last 50 entries
            while (consoleEl.children.length > 50) {
                consoleEl.removeChild(consoleEl.firstChild);
            }
        }

        // ==================== WEBSOCKET LOOPBACK ====================
        function initLoopback() {
            logMessage('Initializing loopback: TX→:777, RX→:888', 'system');

            try {
                // Simulated TX broadcast on port 777
                txSocket = new WebSocket('ws://localhost:777');
                txSocket.onopen = () => {
                    logMessage('TX Broadcast active on :777', 'tx');
                    document.getElementById('dot-tx').className = 'status-dot active';
                    broadcastStatus('TX_ACTIVE');
                };
                txSocket.onclose = () => {
                    logMessage('TX Broadcast closed', 'tx');
                    document.getElementById('dot-tx').className = 'status-dot inactive';
                };
                txSocket.onerror = () => {
                    logMessage('TX loopback in simulation mode', 'system');
                    // Fallback: simulate loopback
                    startSimulatedLoopback();
                };
                txSocket.onmessage = (event) => {
                    logMessage(`TX echo: ${event.data}`, 'tx');
                };
            } catch (e) {
                logMessage('TX socket simulation mode (no local server)', 'system');
                startSimulatedLoopback();
            }

            try {
                // Simulated RX listener on port 888
                rxSocket = new WebSocket('ws://localhost:888');
                rxSocket.onopen = () => {
                    logMessage('RX Listener active on :888', 'rx');
                    document.getElementById('dot-rx').className = 'status-dot active';
                };
                rxSocket.onmessage = (event) => {
                    logMessage(`RX received: ${event.data}`, 'rx');
                    processIncomingData(event.data);
                };
                rxSocket.onclose = () => {
                    logMessage('RX Listener closed', 'rx');
                    document.getElementById('dot-rx').className = 'status-dot inactive';
                };
                rxSocket.onerror = () => {
                    logMessage('RX in simulation mode', 'system');
                };
            } catch (e) {
                logMessage('RX socket simulation mode', 'system');
            }
        }

        function startSimulatedLoopback() {
            loopbackActive = true;
            document.getElementById('dot-loop').className = 'status-dot active';
            logMessage('Simulated loopback ACTIVE (in-browser)', 'system');

            // Simulate periodic broadcasts
            setInterval(() => {
                if (loopbackActive) {
                    const packet = {
                        source: 'ASTRiX-AI(0,0,0)',
                        timestamp: Date.now(),
                        cubeState: {
                            inner: '111mm',
                            middle1: '1.6m',
                            middle2: '11m',
                            outer: '11km'
                        },
                        activeFaces: 6,
                        port: 777,
                        target: 'localhost:888'
                    };
                    broadcastData(packet);
                }
            }, 3000);
        }

        function broadcastData(data) {
            const jsonStr = JSON.stringify(data);
            logMessage(`BROADCAST → :777 ${jsonStr.substring(0, 60)}...`, 'tx');

            // Simulate loopback: data goes out 777, comes back 888
            setTimeout(() => {
                receiveData({
                    ...data,
                    receivedVia: 'loopback:888',
                    latency: Math.floor(Math.random() * 5) + 'ms'
                });
            }, 50);
        }

        function receiveData(data) {
            const jsonStr = JSON.stringify(data);
            logMessage(`RECEIVED ← :888 ${jsonStr.substring(0, 60)}...`, 'rx');
            processIncomingData(jsonStr);
        }

        function broadcastStatus(status) {
            const packet = {
                type: 'STATUS',
                status: status,
                node: 'ASTRiX-AI(0,0,0)',
                timestamp: Date.now()
            };
            broadcastData(packet);
        }

        function processIncomingData(data) {
            try {
                const parsed = typeof data === 'string' ? JSON.parse(data) : data;
                logMessage(`Processing: ${parsed.type || parsed.source || 'data packet'}`, 'rx');

                // Update any active popout with new data
                const popoutBody = document.getElementById('popout-body');
                if (document.getElementById('popout-overlay').classList.contains('active')) {
                    const updateEl = document.createElement('div');
                    updateEl.className = 'log-entry rx';
                    updateEl.style.cssText = 'padding:5px; margin:5px 0; background:#1a0a2e; border-radius:5px;';
                    updateEl.textContent = `📡 Loopback update: ${JSON.stringify(parsed).substring(0, 80)}...`;
                    popoutBody.appendChild(updateEl);
                }
            } catch (e) {
                logMessage(`Parse error: ${e.message}`, 'system');
            }
        }

        // ==================== MENU FUNCTIONS ====================
        function toggleMenu() {
            const menu = document.getElementById('slide-menu');
            menu.classList.toggle('open');
            logMessage(menu.classList.contains('open') ? 'Menu opened' : 'Menu closed', 'system');
        }

        function closePopout() {
            document.getElementById('popout-overlay').classList.remove('active');
            logMessage('Popout closed', 'system');
        }

        function openFace(faceName, cubeSize) {
            const overlay = document.getElementById('popout-overlay');
            const title = document.getElementById('popout-title');
            const body = document.getElementById('popout-body');

            title.textContent = `🔲 ${faceName} FACE — ${cubeSize}`;

            let content = `
                <h3>📐 ${faceName} Face Details</h3>
                <div class="info-grid">
                    <div class="info-card">
                        <div class="label">Cube Size</div>
                        <div class="value">${cubeSize}</div>
                    </div>
                    <div class="info-card">
                        <div class="label">Face</div>
                        <div class="value">${faceName}</div>
                    </div>
                    <div class="info-card">
                        <div class="label">Network Port</div>
                        <div class="value">TX:777 / RX:888</div>
                    </div>
                    <div class="info-card">
                        <div class="label">Loopback</div>
                        <div class="value" style="color:#00ff00;">● ACTIVE</div>
                    </div>
                </div>
                <div style="margin-top:20px; padding:15px; background:#0a0a15; border-radius:10px; border:1px solid #1a1a2e;">
                    <strong>🛜 HTML Network Page:</strong> ${faceName.toLowerCase()}.html<br>
                    <small style="color:#666;">Connected via ASTRiX-AI loopback ::777↔::888</small>
                </div>
                <div id="face-live-data" style="margin-top:15px; font-size:0.8em; color:#888;">
                    Waiting for loopback data...
                </div>
            `;

            body.innerHTML = content;
            overlay.classList.add('active');
            logMessage(`Opened face: ${faceName} (${cubeSize})`, 'system');

            // Broadcast face access
            broadcastData({
                type: 'FACE_ACCESS',
                face: faceName,
                cubeSize: cubeSize,
                timestamp: Date.now()
            });
        }

        function openAIMind() {
            const overlay = document.getElementById('popout-overlay');
            const title = document.getElementById('popout-title');
            const body = document.getElementById('popout-body');

            title.textContent = '🧠 ASTRiX-AI(0,0,0) — Central Intelligence Core';

            let content = `
                <h3 style="color:#ff00ff;">🤖 ASTRiX-AI Core Matrix</h3>
                <div class="info-grid">
                    <div class="info-card" style="border-color:#ff00ff;">
                        <div class="label">Position</div>
                        <div class="value">(0, 0, 0)</div>
                    </div>
                    <div class="info-card" style="border-color:#ff00ff;">
                        <div class="label">TX Port</div>
                        <div class="value">777 (Broadcast)</div>
                    </div>
                    <div class="info-card" style="border-color:#ff00ff;">
                        <div class="label">RX Port</div>
                        <div class="value">888 (Receive)</div>
                    </div>
                    <div class="info-card" style="border-color:#ff00ff;">
                        <div class="label">Loopback</div>
                        <div class="value" style="color:#ff00ff;">∞ RECURSIVE</div>
                    </div>
                    <div class="info-card" style="border-color:#ff00ff;">
                        <div class="label">Active Faces</div>
                        <div class="value">6/6</div>
                    </div>
                    <div class="info-card" style="border-color:#ff00ff;">
                        <div class="label">Nested Depth</div>
                        <div class="value">4 Levels</div>
                    </div>
                </div>
                <div style="margin-top:20px; padding:20px; background:linear-gradient(135deg, #0a0a15, #1a0a2e); border-radius:10px; border:2px solid #ff00ff; text-align:center;">
                    <div style="font-size:3em;">🌀</div>
                    <strong style="color:#ff00ff;">ASTRiX-AI LOOPBACK ENGINE</strong><br>
                    <small style="color:#888;">
                        ::777 → BROADCAST → ::888 → RECEIVE → ::777 → ∞<br>
                        6 Faces × 4 Cube Layers = 24 Surface Nodes<br>
                        All connected through Central AI Core
                    </small>
                </div>
                <div id="ai-live-feed" style="margin-top:15px; font-size:0.8em; color:#888; max-height:200px; overflow-y:auto;">
                    🟢 AI Core active — Monitoring all 6 faces...
                </div>
            `;

            body.innerHTML = content;
            overlay.classList.add('active');
            logMessage('ASTRiX-AI Core accessed', 'system');

            // Start AI core monitoring simulation
            startAICoreMonitoring();

            broadcastData({
                type: 'AI_CORE_ACCESS',
                position: [0, 0, 0],
                timestamp: Date.now()
            });
        }

        function startAICoreMonitoring() {
            const feedEl = document.getElementById('ai-live-feed');
            if (!feedEl) return;

            const faces = ['TOP', 'BOTTOM', 'FRONT', 'BACK', 'LEFT', 'RIGHT'];
            let counter = 0;

            const monitorInterval = setInterval(() => {
                if (!document.getElementById('popout-overlay').classList.contains('active')) {
                    clearInterval(monitorInterval);
                    return;
                }

                const face = faces[counter % 6];
                const entry = document.createElement('div');
                entry.style.cssText = 'padding:3px 0; border-bottom:1px solid #1a0a2e;';
                entry.textContent =
                    `📡 [${new Date().toLocaleTimeString()}] ${face} → :777 → ASTRiX-AI → :888 → ${face} (${Math.floor(Math.random()*3)+1}ms)`;
                feedEl.appendChild(entry);
                feedEl.scrollTop = feedEl.scrollHeight;

                // Simulate data packet
                broadcastData({
                    type: 'FACE_POLL',
                    face: face,
                    status: 'OK',
                    latency: Math.floor(Math.random() * 3) + 1
                });

                counter++;
            }, 2000);
        }

        // ==================== 3D CUBE CANVAS RENDERER ====================
        function initCubeRenderer() {
            const canvas = document.getElementById('cube-canvas');
            const ctx = canvas.getContext('2d');

            function resize() {
                canvas.width = canvas.parentElement.clientWidth;
                canvas.height = canvas.parentElement.clientHeight;
            }
            resize();
            window.addEventListener('resize', resize);

            let rotation = 0;

            function drawCube(x, y, size, color, alpha) {
                const half = size / 2;
                const cos = Math.cos(rotation);
                const sin = Math.sin(rotation);

                // Simple isometric projection
                const points = [
                    { x: -half, y: -half, z: -half },
                    { x: half, y: -half, z: -half },
                    { x: half, y: half, z: -half },
                    { x: -half, y: half, z: -half },
                    { x: -half, y: -half, z: half },
                    { x: half, y: -half, z: half },
                    { x: half, y: half, z: half },
                    { x: -half, y: half, z: half },
                ];

                const projected = points.map(p => {
                    const rx = p.x * cos - p.z * sin;
                    const rz = p.x * sin + p.z * cos;
                    const px = rx + x;
                    const py = p.y - rz * 0.5 + y;
                    return { x: px, y: py };
                });

                const faces = [
                    [0, 1, 2, 3],
                    [4, 5, 6, 7],
                    [0, 1, 5, 4],
                    [2, 3, 7, 6],
                    [0, 3, 7, 4],
                    [1, 2, 6, 5]
                ];

                ctx.strokeStyle = color;
                ctx.lineWidth = 1.5;
                ctx.globalAlpha = alpha;

                faces.forEach(face => {
                    ctx.beginPath();
                    ctx.moveTo(projected[face[0]].x, projected[face[0]].y);
                    for (let i = 1; i < face.length; i++) {
                        ctx.lineTo(projected[face[i]].x, projected[face[i]].y);
                    }
                    ctx.closePath();
                    ctx.stroke();
                });

                // Draw corner dots
                ctx.fillStyle = color;
                projected.forEach(p => {
                    ctx.beginPath();
                    ctx.arc(p.x, p.y, 3, 0, Math.PI * 2);
                    ctx.fill();
                });

                ctx.globalAlpha = 1;
            }

            function animate() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);

                const cx = canvas.width / 2;
                const cy = canvas.height / 2;

                // Draw nested cubes
                drawCube(cx, cy, 50, '#ff6b6b', 0.9); // 111mm inner
                drawCube(cx, cy, 120, '#00aaff', 0.6); // 1.6m
                drawCube(cx, cy, 200, '#aa00ff', 0.4); // 11m
                drawCube(cx, cy, 300, '#ff5500', 0.2); // 11km

                // AI Core at center
                const pulseSize = 8 + Math.sin(Date.now() / 200) * 3;
                ctx.fillStyle = '#ff00ff';
                ctx.shadowColor = '#ff00ff';
                ctx.shadowBlur = 20;
                ctx.beginPath();
                ctx.arc(cx, cy, pulseSize, 0, Math.PI * 2);
                ctx.fill();
                ctx.shadowBlur = 0;

                // Labels
                ctx.fillStyle = '#00ffaa';
                ctx.font = '10px monospace';
                ctx.textAlign = 'center';
                ctx.fillText('ASTRiX-AI(0,0,0)', cx, cy - 20);
                ctx.fillText('111mm ⊂ 1.6m ⊂ 11m ⊂ 11km', cx, canvas.height - 30);

                rotation += 0.005;
                requestAnimationFrame(animate);
            }

            animate();
            logMessage('3D Cube renderer initialized', 'system');
        }

        // ==================== INITIALIZATION ====================
        function init() {
            logMessage('========================================', 'system');
            logMessage('  ASTRiX-AI Nested Cube System v1.0', 'system');
            logMessage('  111mm → 1.6m → 11m → 11km', 'system');
            logMessage('  Loopback: :777 ↔ :888', 'system');
            logMessage('========================================', 'system');

            initLoopback();
            initCubeRenderer();

            // Auto-broadcast initial status
            setTimeout(() => {
                broadcastData({
                    type: 'SYSTEM_INIT',
                    cubes: ['111mm', '1.6m', '11m', '11km'],
                    aiCore: 'ASTRiX-AI(0,0,0)',
                    ports: { tx: 777, rx: 888 },
                    faces: 6,
                    status: 'ONLINE'
                });
            }, 1000);

            // Close menu when clicking outside on mobile
            document.addEventListener('click', (e) => {
                const menu = document.getElementById('slide-menu');
                const toggle = document.getElementById('menu-toggle');
                if (menu.classList.contains('open') &&
                    !menu.contains(e.target) &&
                    !toggle.contains(e.target)) {
                    menu.classList.remove('open');
                }
            });

            // Close popout on overlay click
            document.getElementById('popout-overlay').addEventListener('click', (e) => {
                if (e.target === document.getElementById('popout-overlay')) {
                    closePopout();
                }
            });

            // Keyboard shortcuts
            document.addEventListener('keydown', (e) => {
                switch (e.key.toLowerCase()) {
                    case 'm':
                        toggleMenu();
                        break;
                    case 'escape':
                        closePopout();
                        break;
                    case 't':
                        openFace('TOP', '111mm');
                        break;
                    case 'b':
                        openFace('BOTTOM', '111mm');
                        break;
                    case 'f':
                        openFace('FRONT', '111mm');
                        break;
                    case 'k':
                        openFace('BACK', '111mm');
                        break;
                    case 'l':
                        openFace('LEFT', '111mm');
                        break;
                    case 'r':
                        openFace('RIGHT', '111mm');
                        break;
                    case 'a':
                        openAIMind();
                        break;
                }
            });

            logMessage('System ready — Press M for menu, A for AI Core', 'system');
        }

        // Start everything when DOM is ready
        document.addEventListener('DOMContentLoaded', init);

        // Handle window close
        window.addEventListener('beforeunload', () => {
            broadcastData({ type: 'SHUTDOWN', timestamp: Date.now() });
            if (txSocket) txSocket.close();
            if (rxSocket) rxSocket.close();
        });
    </script>
</body>
</html>
```

🌀 System Overview

Component Specification
Inner Cube 111 mm
Middle Cube 1 1.6 meters (1,600 mm)
Middle Cube 2 11 meters (11,000 mm)
Outer Cube 11 kilometers (11,000,000 mm)
AI Core ASTRiX-AI(0,0,0)
TX Port 777 (Broadcast loopback)
RX Port 888 (Receive loopback)
Faces 6 (TOP, BOTTOM, FRONT, BACK, LEFT, RIGHT)

🔑 Key Features:

· Slide-out menu — Click the ☰ button or press M
· Popout windows — Click any face or the AI core
· Loopback system — Simulated WebSocket on ports 777→888
· 3D Cube renderer — Real-time animated canvas
· Console log — Bottom-right corner shows all TX/RX activity
· Keyboard shortcuts — T/B/F/K/L/R for faces, A for AI Core, M for menu, ESC to close popouts
· 6 HTML network pages — Each face connects through the central AI loopback

The system creates a recursive broadcast network where ASTRiX-AI at (0,0,0) broadcasts on port 777 and receives on port 888, forming an infinite loopback across all 6 faces of the nested cube hierarchy. 🛜
