# -Birthchart-details-for-FREE
Make sure only few people know this... only BADDIES
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Vedic Birth Chart</title>
    <style>
        :root {
            --bg-color: #f8fafc;
            --card-bg: #ffffff;
            --text-color: #1e293b;
            --border-color: #cbd5e1;
            --accent-color: #4f46e5;
            --accent-hover: #4338ca;
            --chart-line: #334155;
        }

        body {
            font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        h1 {
            margin-bottom: 5px;
            color: var(--text-color);
        }

        p.subtitle {
            margin-top: 0;
            margin-bottom: 30px;
            color: #64748b;
        }

        .container {
            display: flex;
            flex-direction: row;
            gap: 40px;
            max-width: 1100px;
            width: 100%;
            justify-content: center;
            align-items: flex-start;
        }

        @media (max-width: 850px) {
            .container {
                flex-direction: column;
                align-items: center;
            }
        }

        /* Input Panel Styles */
        .input-panel {
            background: var(--card-bg);
            padding: 24px;
            border-radius: 12px;
            box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05), 0 2px 4px -1px rgba(0,0,0,0.03);
            width: 340px;
            border: 1px solid var(--border-color);
        }

        .input-group {
            margin-bottom: 16px;
        }

        label {
            display: block;
            font-weight: 600;
            margin-bottom: 6px;
            font-size: 0.9rem;
        }

        select, input[type="text"] {
            width: 100%;
            padding: 8px 12px;
            border: 1px solid var(--border-color);
            border-radius: 6px;
            background-color: #fff;
            box-sizing: border-box;
            font-size: 0.95rem;
        }

        button {
            width: 100%;
            padding: 12px;
            background-color: var(--accent-color);
            color: white;
            border: none;
            border-radius: 6px;
            font-weight: 600;
            cursor: pointer;
            transition: background 0.2s;
            font-size: 1rem;
            margin-top: 10px;
        }

        button:hover {
            background-color: var(--accent-hover);
        }

        /* Chart Output Panel */
        .chart-panel {
            display: flex;
            flex-direction: column;
            align-items: center;
            background: var(--card-bg);
            padding: 24px;
            border-radius: 12px;
            box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05), 0 2px 4px -1px rgba(0,0,0,0.03);
            border: 1px solid var(--border-color);
        }

        /* North Indian SVG Grid Map coordinates */
        svg {
            background-color: #fff;
            border: 2px solid var(--chart-line);
            border-radius: 4px;
        }

        .house-text {
            font-size: 11px;
            fill: #94a3b8;
            font-weight: bold;
        }

        .sign-text {
            font-size: 14px;
            fill: var(--accent-color);
            font-weight: bold;
        }

        .planet-text {
            font-size: 13px;
            fill: #0f172a;
            font-weight: 500;
        }
    </style>
</head>
<body>

    <h1>Vedic Birth Chart Engine</h1>
    <p class="subtitle">Assign signs to your planets and set your Lagna (Ascendant) to visualize the house overlays.</p>

    <div class="container">
        <div class="input-panel">
            <div class="input-group">
                <label for="lagnaSelect">1st House / Ascendant Sign</label>
                <select id="lagnaSelect">
                    <option value="1">1 - Aries (Mesha)</option>
                    <option value="2">2 - Taurus (Vrishabha)</option>
                    <option value="3">3 - Gemini (Mithuna)</option>
                    <option value="4">4 - Cancer (Karka)</option>
                    <option value="5">5 - Leo (Simha)</option>
                    <option value="6">6 - Virgo (Kanya)</option>
                    <option value="7">7 - Libra (Tula)</option>
                    <option value="8">8 - Scorpio (Vrishchika)</option>
                    <option value="9">9 - Sagittarius (Dhanu)</option>
                    <option value="10">10 - Capricorn (Makara)</option>
                    <option value="11">11 - Aquarius (Kumbha)</option>
                    <option value="12">12 - Pisces (Meena)</option>
                </select>
            </div>

            <hr style="border: 0; border-top: 1px solid var(--border-color); margin: 20px 0;">
            <h3 style="margin-top:0; font-size: 1rem;">Assign Planet Positions (Signs)</h3>

            <div id="planetInputsContainer"></div>

            <button onclick="renderChart()">Update Visual Chart</button>
        </div>

        <div class="chart-panel">
            <svg id="kundliSvg" width="400" height="400" viewBox="0 0 400 400">
                <line x1="0" y1="0" x2="400" y2="0" stroke="#334155" stroke-width="3"/>
                <line x1="400" y1="0" x2="400" y2="400" stroke="#334155" stroke-width="3"/>
                <line x1="400" y1="400" x2="0" y2="400" stroke="#334155" stroke-width="3"/>
                <line x1="0" y1="400" x2="0" y2="0" stroke="#334155" stroke-width="3"/>

                <line x1="0" y1="0" x2="400" y2="400" stroke="#334155" stroke-width="2"/>
                <line x1="400" y1="0" x2="0" y2="400" stroke="#334155" stroke-width="2"/>

                <line x1="200" y1="0" x2="0" y2="200" stroke="#334155" stroke-width="2"/>
                <line x1="0" y1="200" x2="200" y2="400" stroke="#334155" stroke-width="2"/>
                <line x1="200" y1="400" x2="400" y2="200" stroke="#334155" stroke-width="2"/>
                <line x1="400" y1="200" x2="200" y2="0" stroke="#334155" stroke-width="2"/>

                <g id="houseLabels"></g>
                <g id="signLabels"></g>
                <g id="planetLabels"></g>
            </svg>
        </div>
    </div>

    <script>
        // List of planets to map
        const planets = ["Sun", "Moon", "Mars", "Merc", "Jup", "Ven", "Sat", "Rahu", "Ketu"];
        
        // Setup initial mock sign structure for planets
        const initialPlacements = {
            "Sun": 1, "Moon": 4, "Mars": 10, "Merc": 1, "Jup": 4, "Ven": 7, "Sat": 11, "Rahu": 3, "Ketu": 9
        };

        // Static geometric anchor points for center points of each of the 12 North Indian Houses
        const houseAnchors = {
            1:  { hX: 200, hY: 30,  sX: 200, sY: 120, pX: 200, pY: 75 },
            2:  { hX: 95,  hY: 30,  sX: 95,  sY: 85,  pX: 95,  pY: 55 },
            3:  { hX: 30,  hY: 95,  sX: 85,  sY: 95,  pX: 55,  pY: 95 },
            4:  { hX: 30,  hY: 200, sX: 120, sY: 200, pX: 75,  pY: 200 },
            5:  { hX: 30,  hY: 305, sX: 85,  sY: 305, pX: 55,  pY: 305 },
            6:  { hX: 95,  hY: 370, sX: 95,  sY: 315, pX: 95,  pY: 345 },
            7:  { hX: 200, hY: 370, sX: 200, sY: 280, pX: 200, pY: 325 },
            8:  { hX: 305, hY: 370, sX: 305, sY: 315, pX: 305, pY: 345 },
            9:  { hX: 370, hY: 305, sX: 315, sY: 305, pX: 345, pY: 305 },
            10: { hX: 370, hY: 200, sX: 280, sY: 200, pX: 325, pY: 200 },
            11: { hX: 370, hY: 95,  sX: 315, sY: 95,  pX: 345, pY: 95 },
            12: { hX: 305, hY: 30,  sX: 305, sY: 85,  pX: 305, pY: 55 }
        };

        // Generate drop-downs for all planets on load
        const container = document.getElementById('planetInputsContainer');
        planets.forEach(p => {
            const div = document.createElement('div');
            div.className = 'input-group';
            div.innerHTML = `
                <label>${p}</label>
                <select id="select_${p}">
                    ${Array.from({length: 12}, (_, i) => `<option value="${i+1}" ${initialPlacements[p] === i+1 ? 'selected':''}>Sign ${i+1}</option>`).join('')}
                </select>
            `;
            container.appendChild(div);
        });

        function renderChart() {
            const lagnaSign = parseInt(document.getElementById('lagnaSelect').value);
            
            const houseLabelsGroup = document.getElementById('houseLabels');
            const signLabelsGroup = document.getElementById('signLabels');
            const planetLabelsGroup = document.getElementById('planetLabels');

            // Clear previous loops
            houseLabelsGroup.innerHTML = '';
            signLabelsGroup.innerHTML = '';
            planetLabelsGroup.innerHTML = '';

            // Setup a mapping collection array to capture what planets map to what house ID index numbers
            let housePlanetsMap = { 1:[], 2:[], 3:[], 4:[], 5:[], 6:[], 7:[], 8:[], 9:[], 10:[], 11:[], 12:[] };

            for (let houseNum = 1; houseNum <= 12; houseNum++) {
                // Formula to calculate sign mapping dynamically inside house structures
                let activeSign = (lagnaSign + houseNum - 1) % 12;
                if (activeSign === 0) activeSign = 12;

                const coords = houseAnchors[houseNum];

                // 1. Plot Small House ID numbers reference tracking
                houseLabelsGroup.innerHTML += `<text x="${coords.hX}" y="${coords.hY}" text-anchor="middle" class="house-text">H${houseNum}</text>`;
                
                // 2. Plot Dynamic Sign Numbers inside the diamond quadrants
                signLabelsGroup.innerHTML += `<text x="${coords.sX}" y="${coords.sY}" text-anchor="middle" dominant-baseline="central" class="sign-text">${activeSign}</text>`;

                // Check which planets match this specific calculated active zodiac sign
                planets.forEach(p => {
                    const chosenPlanetSign = parseInt(document.getElementById(`select_${p}`).value);
                    if (chosenPlanetSign === activeSign) {
                        housePlanetsMap[houseNum].push(p);
                    }
                });
            }

            // 3. Render Planet Strings cleanly inside their dynamic boundaries 
            for (let houseNum = 1; houseNum <= 12; houseNum++) {
                const plist = housePlanetsMap[houseNum];
                if (plist.length > 0) {
                    const coords = houseAnchors[houseNum];
                    
                    // Split layout strings adjustments dynamically for stacked viewing configurations 
                    if(houseNum === 1 || houseNum === 7 || houseNum === 4 || houseNum === 10) {
                        // Diamond structures process text wrapped lines vertically split
                        plist.forEach((planetName, index) => {
                            planetLabelsGroup.innerHTML += `<text x="${coords.pX}" y="${coords.pY - 10 + (index * 14)}" text-anchor="middle" class="planet-text">${planetName}</text>`;
                        });
                    } else {
                        // Side Triangles draw inline space separation structures
                        let planetStringLine = plist.join(" ");
                        planetLabelsGroup.innerHTML += `<text x="${coords.pX}" y="${coords.pY}" text-anchor="middle" dominant-baseline="central" class="planet-text">${planetStringLine}</text>`;
                    }
                }
            }
        }

        // Run execution setup visually on first loading lifecycle event execution
        renderChart();
    </script>
</body>
</html>
