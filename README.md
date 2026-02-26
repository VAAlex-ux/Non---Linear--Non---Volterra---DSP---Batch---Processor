# Non-Linear-Non-Volterra-DSP-Batch-Processor
A new instant audio web batch processor based on Non - Linear Non - Volterra DSP theory. 

# Only the Front - End will be posted.


<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Instant Audio Web Batch Processor</title>
<style>
  body { font-family: Arial; background: #121212; color: #fff; padding: 20px;
  /* Flexbox centering */
    display: flex;
    justify-content: center;   /* center horizontally */
    align-items: center;   /* optional: top-aligned vertically */
    min-height: 100vh;         /* ensures full viewport height */
  }

  .container {
    width: 100%;  /* let it take full width */
    max-width: 900px; /* but not wider than 900px */
    display: flex;
    flex-direction: column; /* stack items vertically */
    align-items: center;    /* center items horizontally inside container */
    gap: 15px;              /* spacing between elements */
    padding: 0 20px;      /* small space from the edges */
    box-sizing: border-box; /* ensures padding doesn't increase width */
  }

  .slider-container {
    display: flex;          /* flex layout */
    align-items: center;    /* vertically align items */
    justify-content: flex-start; /* left align */
    gap: 10px;              /* spacing between label, slider, value */
  }

  .slider-container label {
    width: 200px;           /* fixed width for all labels */
    text-align: right;      /* optional: right-align labels */
  }

  .slider-container input[type=range] {
    flex: 1;                /* slider takes remaining space */
  }

  .slider-container span {
    width: 50px;            /* fixed width for value display */
    text-align: left;
  }

  .button-row {
    display: flex;                /* horizontal layout */
    justify-content: center;      /* center buttons in the row */
    gap: 20px;                    /* spacing between buttons */
    margin-top: 20px;             /* spacing above the buttons row */
  }

  .button-row button {
    padding: 10px 20px;
    font-size: 16px;
    background: #0a0;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background 0.2s;
  }

  .button-row button:hover {
    background: #0f0;  /* hover effect */
  }

  canvas {
    max-width: 100%;
    height: auto;
    border: 1px solid #444; /* scale canvas so this it is not fixed at 800px just to see the border */
  }

  h2 { color: #0f0; }
  .slider-container { margin: 10px 0; }
  label { display: inline-block; width: 160px; }
  input[type=range] { width: 300px; }
  button { background: #0a0; color: #fff; padding: 10px 20px; border: none; font-size: 16px; cursor: pointer; }
</style>
</head>

<body>
<div class="container">

<h2>Instant Audio Web Batch Processor</h2>
<div>Upload Files - Get Hundreds of Variations</div>
<div>Based on Non - Linear Non - Volterra DSP Theory</div>

<canvas id="waveCanvas" width="800" height="300"></canvas>

<!-- File Upload -->
<div>
  <label>Upload Audio File</label>
  <input type="file" id="fileUpload" multiple>
</div>

<!-- Sampling Frequency -->
<div class="slider-container">
  <label for="fsSlider">Sampling Frequency (Hz)</label>
  <input type="range" id="fsSlider" min="8000" max="96000" step="10" value="44100">
  <span id="fsVal">44100</span>
</div>

<!-- RR_COUNT -->
<div class="slider-container">
  <label for="rrCount">Variations / Sound</label>
  <input type="range" id="rrCount" min="1" max="100" value="10">
  <span id="rrVal">10</span>
</div>

<!-- Tnum -->
<div class="slider-container">
  <label for="Tnum">Time Segments (s)</label>
  <input type="range" id="Tnum" min="2" max="64" value="8">
  <span id="TnumVal">8</span>
</div>

<!-- DSP Parameters -->
<div class="slider-container"><label for="mutation">Mutation Factor</label><input type="range" id="mutation" min="1" max="10" step="0.01" value="5"><span id="mutVal">5</span></div>
<div class="slider-container"><label for="glitch">Glitch Factor</label><input type="range" id="glitch" min="1" max="100" step="0.01" value="50"><span id="gliVal">50</span></div>
<div class="slider-container"><label for="resonance">Resonance Factor</label><input type="range" id="resonance" min="1" max="10" step="0.01" value="5"><span id="resVal">5</span></div>
<div class="slider-container"><label for="crush">Crush Factor</label><input type="range" id="crush" min="1" max="10" step="0.01" value="5"><span id="cruVal">5</span></div>
<div class="slider-container"><label for="evolution">File Extension Scale</label><input type="range" id="evolution" min="0" max="10" step="0.01" value="5"><span id="evoVal">5</span></div>

<!-- Dynamic fc_base_points -->
<div class="slider-container"><label for="fc_Base">Base Cutoff (Hz)</label><input type="range" id="fc_Base" min="20" max="5000" step="0.01" value="3000"><span id="fcBase">3000</span></div>
<div class="slider-container"><label for="fc_LowMid">LowMid Cutoff (Hz)</label><input type="range" id="fc_LowMid" min="20" max="5000" step="0.01" value="3000"><span id="fcLowMid">3000</span></div>
<div class="slider-container"><label for="fc_HighMid">HighMid Cutoff (Hz)</label><input type="range" id="fc_HighMid" min="20" max="5000" step="0.01" value="3000"><span id="fcHighMid">3000</span></div>
<div class="slider-container"><label for="fc_Treble">Treble Cutoff (Hz)</label><input type="range" id="fc_Treble" min="20" max="5000" step="0.01" value="3000"><span id="fcTreble">3000</span></div>

<!-- Dynamic Normalization Sound Smoother Factors -->
<div class="slider-container"><label for="N1">Base Cutoff Smoother</label><input type="range" id="N1" min="0.1" max="2" step="0.01" value="0.5"><span id="n1">0.5</span></div>
<div class="slider-container"><label for="N2">LowMid Cutoff Smoother</label><input type="range" id="N2" min="0.1" max="2" step="0.01" value="0.5"><span id="n2">0.5</span></div>
<div class="slider-container"><label for="N3">HighMid Cutoff Smoother</label><input type="range" id="N3" min="0.1" max="2" step="0.01" value="0.5"><span id="n3">0.5</span></div>
<div class="slider-container"><label for="N4">Treble Cutoff Smoother</label><input type="range" id="N4" min="0.1" max="2" step="0.01" value="0.5"><span id="n4">0.5</span></div>

<!-- Buttons -->
<div class="button-row">
  <button id="toggleView">Toggle View</button>
  <button id="startPreview">Start Preview</button>
  <button id="processBtn">Process Batch</button> 
</div>

<!-- Result Gallery (Hidden by default) -->
<div id="resultContainer" style="margin-top:30px; display:none; border-top: 1px solid #444; padding-top: 20px;">
    <h2 style="color: #0f0;">Generated Variations</h2>
    <p style="color: #888;">Windows Safe: Download files individually to avoid ZIP corruption.</p>
    <button id="downloadAllBtn" style="background:#007bff; margin-bottom:20px;">Download All (Sequential)</button>
    <ul id="fileList" style="list-style:none; padding:0;"></ul>
</div>

<script>
const sliders = ['mutation','glitch','resonance','crush','evolution'];
const fcSliders = ['Base','LowMid','HighMid','Treble'];

let animationFrameId;
let shaper, bitCrusher;
let baseFilter, lowMidFilter, highMidFilter, trebleFilter;
let engineReady = false;
let sourceStarted = false;
let audioCtx = null;
let audioSource = null;
let audioBuffer = null; 
let masterGain = null;
let analyser = null;
let isPlaying = false;  // Tracks if audio is currently playing

const canvas = document.getElementById("waveCanvas");
const ctx = canvas.getContext("2d");
const WIDTH = canvas.width;
const HEIGHT = canvas.height;

let currentView = "time";

function drawTimeGrid() {

    ctx.strokeStyle = "#222";
    ctx.lineWidth = 1;

    const divisions = 10;
    const stepX = WIDTH / divisions;
    const stepY = HEIGHT / divisions;

    // Vertical lines
    for (let i = 0; i <= divisions; i++) {
        const x = i * stepX;
        ctx.beginPath();
        ctx.moveTo(x, 0);
        ctx.lineTo(x, HEIGHT);
        ctx.stroke();
    }

    // Horizontal lines
    for (let i = 0; i <= divisions; i++) {
        const y = i * stepY;
        ctx.beginPath();
        ctx.moveTo(0, y);
        ctx.lineTo(WIDTH, y);
        ctx.stroke();
    }

    // Center line (0 amplitude)
    ctx.strokeStyle = "#444";
    ctx.lineWidth = 2;
    ctx.beginPath();
    ctx.moveTo(0, HEIGHT / 2);
    ctx.lineTo(WIDTH, HEIGHT / 2);
    ctx.stroke();
}

function drawFrequencyGrid() {

    ctx.strokeStyle = "#222";
    ctx.lineWidth = 1;

    const freqs = [20, 50, 100, 200, 500, 1000, 2000, 5000, 10000, 20000];

    const minLog = Math.log10(20);
    const maxLog = Math.log10(audioCtx.sampleRate / 2);

    freqs.forEach(freq => {

        if (freq > audioCtx.sampleRate / 2) return;

        const logPos = (Math.log10(freq) - minLog) / (maxLog - minLog);
        const x = logPos * WIDTH;

        ctx.beginPath();
        ctx.moveTo(x, 0);
        ctx.lineTo(x, HEIGHT);
        ctx.stroke();

        // Label
        ctx.fillStyle = "#888";
        ctx.font = "12px Arial";
        ctx.fillText(freq + "Hz", x + 4, HEIGHT - 5);
    });

    // dB horizontal lines
    const dbLevels = [-60, -40, -20, -10, 0];

    dbLevels.forEach(db => {

        const y = HEIGHT - ((db + 60) / 60) * HEIGHT;

        ctx.beginPath();
        ctx.moveTo(0, y);
        ctx.lineTo(WIDTH, y);
        ctx.stroke();

        ctx.fillStyle = "#888";
        ctx.fillText(db + "dB", WIDTH - 50, y - 2);
    });
}


function draw() {

  // GUARD: If the system is resetting or context is null, just loop without drawing
    if (!engineReady || !analyser || !audioCtx) {
        animationFrameId = requestAnimationFrame(draw);
        return; 
    }

    animationFrameId = requestAnimationFrame(draw);

    ctx.fillStyle = "black";
    ctx.fillRect(0, 0, WIDTH, HEIGHT);

    // Only draw if we actually have data
    if (currentView === "time") {
        drawTimeGrid();
        drawTime();
    } else {
        drawFrequencyGrid();
        drawFrequency();
    }
}

function drawTime() {

    const bufferLength = analyser.frequencyBinCount;
    const dataArray = new Uint8Array(bufferLength);

    analyser.getByteTimeDomainData(dataArray);

    ctx.strokeStyle = "#00ffcc";
    ctx.lineWidth = 2;

    ctx.beginPath();

    const sliceWidth = WIDTH / bufferLength;
    let x = 0;

    for (let i = 0; i < bufferLength; i++) {

        const v = (dataArray[i] - 128) / 128.0;

        const y = HEIGHT / 2 + v * HEIGHT * 0.45;

        if (i === 0) ctx.moveTo(x, y);
        else ctx.lineTo(x, y);

        x += sliceWidth;
    }

    ctx.stroke();
}

function drawFrequency() {
    const bufferLength = analyser.frequencyBinCount;
    const dataArray = new Uint8Array(bufferLength);
    analyser.getByteFrequencyData(dataArray);
    
    const minLog = Math.log10(20);
    const maxLog = Math.log10(audioCtx.sampleRate / 2);

    for (let i = 1; i < bufferLength; i++) {
        const freq = i * audioCtx.sampleRate / analyser.fftSize;
        if (freq < 20) continue;
        const logPos = (Math.log10(freq) - minLog) / (maxLog - minLog);
        if (logPos < 0 || logPos > 1) continue;
        const x = logPos * WIDTH;
        const magnitude = Math.max(dataArray[i] / 255, 0.0001);
        const db = 20 * Math.log10(Math.max(magnitude,0.0001));
        const normalized = (db + 60) / 60;
        const barHeight = Math.max(0, normalized * HEIGHT);

        ctx.fillStyle = "lime";
        ctx.fillRect(x, HEIGHT - barHeight, 2, barHeight);
      }
}

// Handle new file uploads
document.getElementById('fileUpload').addEventListener('change', async () => {
    if (audioSource) {
        try { audioSource.stop(); } catch (e) {}
        audioSource.disconnect();
        audioSource = null;
    }

    // Nullify old buffer to force decoding new file
    audioBuffer = null;

    // Reset preview button
    isPlaying = false;
    document.getElementById('startPreview').innerText = "Start Preview";

    // Optional: stop visualization
    // engineReady = false;

    console.log("New file uploaded, old playback stopped. Ready to preview new file.");
});

async function initAudio() {
    const fileInput = document.getElementById("fileUpload");
    if (!fileInput.files.length) {
        alert("Please upload an audio file first.");
        return;
    }

    // 1. Create Context ONLY if it doesn't exist
    if (!audioCtx) {
        const Fs = parseInt(document.getElementById("fsSlider").value);
        audioCtx = new (window.AudioContext || window.webkitAudioContext)({ sampleRate: Fs });
    }

    // 2. Always resume (handles browser auto-play blocks)
    if (audioCtx.state === 'suspended') await audioCtx.resume();

    // 3. KILL OLD SOURCE: Stops sounds from stacking
    if (audioSource) {
        try { audioSource.stop(); } catch(e) {}
        audioSource.disconnect();
        audioSource = null;
    }

    // 4. DECODE ONLY ONCE: Optimization so clicks are instant
    if (!audioBuffer) {
        const arrayBuffer = await fileInput.files[0].arrayBuffer();
        audioBuffer = await audioCtx.decodeAudioData(arrayBuffer);
    }

    // 5. CREATE NEW SOURCE: Mandatory for every "Play" action
    audioSource = audioCtx.createBufferSource();
    audioSource.buffer = audioBuffer;
    audioSource.loop = true;

    // 6. INITIALIZE DSP NODES ONLY ONCE
    if (!shaper) {
        // Load Worklet
        await audioCtx.audioWorklet.addModule("bitcrusher-processor.js");
        
        // Create Nodes
        shaper = audioCtx.createWaveShaper();
        bitCrusher = new AudioWorkletNode(audioCtx, "bitcrusher-processor");
        masterGain = audioCtx.createGain();
        analyser = audioCtx.createAnalyser();
        analyser.fftSize = 2048;

        baseFilter = audioCtx.createBiquadFilter();
        lowMidFilter = audioCtx.createBiquadFilter();
        highMidFilter = audioCtx.createBiquadFilter();
        trebleFilter = audioCtx.createBiquadFilter();

        baseFilter.type = "lowpass";
        lowMidFilter.type = "bandpass";
        highMidFilter.type = "bandpass";
        trebleFilter.type = "highpass";

        // PARALLEL CONNECTION (The working fix)
        [baseFilter, lowMidFilter, highMidFilter, trebleFilter].forEach(f => {
            shaper.connect(f);
            f.connect(bitCrusher);
        });
        bitCrusher.connect(masterGain);
        masterGain.connect(audioCtx.destination);
        masterGain.connect(analyser);
    }

    // 7. ALWAYS RE-CONNECT THE NEW SOURCE TO THE SHAPER
    audioSource.connect(shaper);

    // 8. UPDATE AND START
    updateAllControls();
    audioSource.start(0);
    sourceStarted = true;

    if (!engineReady) {
        engineReady = true;
        requestAnimationFrame(draw);
    }

    isPlaying = true;
    document.getElementById('startPreview').innerText = "Stop Preview";
}

function makeDistortionCurve(amount) {
    const k = amount;
    const n_samples = audioCtx ? audioCtx.sampleRate : 44100;
    const curve = new Float32Array(n_samples);
    const deg = Math.PI / 180;

    for (let i = 0; i < n_samples; ++i) {
        const x = i * 2 / n_samples - 1;
        curve[i] = (3 + k) * x * 20 * deg /
                   (Math.PI + k * Math.abs(x) + 0.0001);
    }
    return curve;
}


function updateAllControls() {

    if (!audioCtx) return;

    // ===== Mutation =====
    const mutation = parseFloat(document.getElementById("mutation").value);
    shaper.curve = makeDistortionCurve(mutation);

    // ===== Glitch =====
    const glitch = parseFloat(document.getElementById("glitch").value);

    if (bitCrusher && bitCrusher.parameters) {
      bitCrusher.parameters.get("glitch")
      .linearRampToValueAtTime(
        glitch / 100,
        audioCtx.currentTime + 0.05
      );
    }

    // ===== Resonance =====
    const resonance = parseFloat(document.getElementById("resonance").value);
    baseFilter.Q.value = resonance;
    lowMidFilter.Q.value = resonance;
    highMidFilter.Q.value = resonance;
    trebleFilter.Q.value = resonance;

    // ===== Bit Crusher =====
    const bits = Math.max(1,Math.floor(parseFloat(document.getElementById("crush").value)));
    if (bitCrusher && bitCrusher.parameters) {
      bitCrusher.parameters.get("bits")
      .linearRampToValueAtTime(
        bits,
        audioCtx.currentTime + 0.05
      );
    }

    // ===== Evolution =====
    const evolution = parseFloat(document.getElementById("evolution").value);

    baseFilter.frequency.linearRampToValueAtTime(parseFloat(document.getElementById("fc_Base").value), 
    audioCtx.currentTime + 0.05);

    lowMidFilter.frequency.linearRampToValueAtTime(parseFloat(document.getElementById("fc_LowMid").value), 
    audioCtx.currentTime + 0.05);

    highMidFilter.frequency.linearRampToValueAtTime(parseFloat(document.getElementById("fc_HighMid").value),
    audioCtx.currentTime + 0.05);

    trebleFilter.frequency.linearRampToValueAtTime(parseFloat(document.getElementById("fc_Treble").value),
    audioCtx.currentTime + 0.05);
}

document.getElementById("toggleView")
.addEventListener("click", () => {
    // Simply flip the state. The draw() loop handles the rest.
    currentView = currentView === "time" ? "freq" : "time";
    console.log("View mode changed to:", currentView);
});

document.getElementById("fsSlider").addEventListener("change", async() => {
    const newFs = document.getElementById("fsSlider").value;
    document.getElementById("fsVal").innerText = newFs;

    // 1. Stop the animation loop immediately to prevent it from calling a null analyser
    if (animationFrameId) {
        cancelAnimationFrame(animationFrameId);
        animationFrameId = null;
    }

    // 2. Kill the Audio Source
    if (audioSource) {
        try { audioSource.stop(); } catch(e) {}
        audioSource.disconnect();
        audioSource = null;
    }

    // 3. Close and NULL the context (Mandatory to change Sample Rate)
    if (audioCtx) {
        await audioCtx.close();
        audioCtx = null;
    }

    // 4. Nullify all DSP nodes so initAudio() knows it must rebuild them
    shaper = null;
    bitCrusher = null;
    baseFilter = null;
    lowMidFilter = null;
    highMidFilter = null;
    trebleFilter = null;
    analyser = null;
    
    // 5. Reset State Flags
    engineReady = false;
    sourceStarted = false;

    console.log("Audio System Hard Reset for " + newFs + "Hz. Click 'Start Preview' to rebuild.");
});

document.getElementById("startPreview").addEventListener("click", async () => {
  if (!isPlaying) {
        // Start playback
        await initAudio();
        document.getElementById("startPreview").innerText = "Stop Preview";
        isPlaying = true;
    } else {
        // Stop playback
        if (audioSource) {
            try {
                audioSource.stop();
            } catch(e) {}
            audioSource.disconnect();
            audioSource = null;
        }
        isPlaying = false;
        document.getElementById("startPreview").innerText = "Start Preview";
    }
});

document.querySelectorAll(
    "#fc_Base, #fc_LowMid, #fc_HighMid, #fc_Treble, " +
    "#mutation, #glitch, #resonance, #crush, #evolution"
).forEach(slider => 
    slider.addEventListener("input", updateAllControls)
);


// Fs, RR_COUNT, Tnum
document.getElementById('fsSlider').addEventListener('input', () => {
  document.getElementById('fsVal').innerText = document.getElementById('fsSlider').value;
//  updateFcSliderRanges(document.getElementById('fsSlider').value);
});
document.getElementById('rrCount').addEventListener('input', () => {
  document.getElementById('rrVal').innerText = document.getElementById('rrCount').value;
});
document.getElementById('Tnum').addEventListener('input', () => {
  document.getElementById('TnumVal').innerText =
    document.getElementById('Tnum').value;
});

// N1, N2, N3, N4
document.getElementById('N1').addEventListener('input', () => {
  document.getElementById('n1').innerText = document.getElementById('N1').value;
});
document.getElementById('N2').addEventListener('input', () => {
  document.getElementById('n2').innerText = document.getElementById('N2').value;
});
document.getElementById('N3').addEventListener('input', () => {
  document.getElementById('n3').innerText = document.getElementById('N3').value;
});
document.getElementById('N4').addEventListener('input', () => {
  document.getElementById('n4').innerText = document.getElementById('N4').value;
});

// sliders = ['mutation','glitch','resonance','crush','evolution']
document.getElementById('mutation').addEventListener('input', () => {
  document.getElementById('mutVal').innerText = document.getElementById('mutation').value;
});
document.getElementById('glitch').addEventListener('input', () => {
  document.getElementById('gliVal').innerText = document.getElementById('glitch').value;
});
document.getElementById('resonance').addEventListener('input', () => {
  document.getElementById('resVal').innerText = document.getElementById('resonance').value;
});
document.getElementById('crush').addEventListener('input', () => {
  document.getElementById('cruVal').innerText = document.getElementById('crush').value;
});
document.getElementById('evolution').addEventListener('input', () => {
  document.getElementById('evoVal').innerText = document.getElementById('evolution').value;
});

// fcSliders = ['Base','LowMid','HighMid','Treble']
document.getElementById('fc_Base').addEventListener('input', () => {
  document.getElementById('fcBase').innerText = document.getElementById('fc_Base').value;
});
document.getElementById('fc_LowMid').addEventListener('input', () => {
  document.getElementById('fcLowMid').innerText = document.getElementById('fc_LowMid').value;
});
document.getElementById('fc_HighMid').addEventListener('input', () => {
  document.getElementById('fcHighMid').innerText = document.getElementById('fc_HighMid').value;
});
document.getElementById('fc_Treble').addEventListener('input', () => {
  document.getElementById('fcTreble').innerText = document.getElementById('fc_Treble').value;
});

// Process Button
document.getElementById('processBtn').addEventListener('click', async () => {
  const files = document.getElementById('fileUpload').files;
  if(files.length===0){ alert("Upload at least one file"); return; }

  const processBtn = document.getElementById('processBtn');
  processBtn.innerText = "Processing...";
  processBtn.disabled = true;

  const formData = new FormData();
  for(let f of files) formData.append('audioFiles', f);

  formData.append('Fs', document.getElementById('fsSlider').value);
  formData.append('RR_COUNT', document.getElementById('rrCount').value);
  formData.append('Tnum', document.getElementById('Tnum').value);
  formData.append('N1', document.getElementById('N1').value);
  formData.append('N2', document.getElementById('N2').value);
  formData.append('N3', document.getElementById('N3').value);
  formData.append('N4', document.getElementById('N4').value);
  sliders.forEach(s => formData.append(s, document.getElementById(s).value));
  fcSliders.forEach(fcs => formData.append(`fc_${fcs}`, document.getElementById(`fc_${fcs}`).value));

  try {
    const res = await fetch('/process-dsp', { method:'POST', body: formData, signal: AbortSignal.timeout(120000) });

    if (res.ok) {
      // Once processed, fetch the list of new files from the server
      const listRes = await fetch('/list-files');
      const generatedFiles = await listRes.json();
      renderGallery(generatedFiles);
    } else {
    // This will now tell you the SPECIFIC reason (e.g., "Octave not found")
    const errorText = await res.text();
    alert("Server Error: " + errorText);
    }
  } catch (err) {
    console.error(err);
  } finally {
    processBtn.innerText = "Process Batch";
    processBtn.disabled = false;
  }
});

// --- New Function: Render the Result Gallery ---
function renderGallery(files) {
    const container = document.getElementById('resultContainer');
    const list = document.getElementById('fileList');
    list.innerHTML = ''; // Clear old results
    container.style.display = 'block';

    files.forEach(file => {
        const li = document.createElement('li');
        li.style.cssText = "background:#1e1e1e; margin-bottom:10px; padding:15px; border-radius:5px; display:flex; align-items:center; justify-content:space-between;";
        
        li.innerHTML = `
            <span style="font-weight:bold; color:#0f0; flex:1;">${file.name}</span>
            <audio controls src="${file.url}" style="height:30px; margin: 0 20px;"></audio>
            <a href="${file.url}" download="${file.name}" style="background:#0a0; color:white; padding:5px 15px; text-decoration:none; border-radius:3px; font-size:14px;">Download</a>
        `;
        list.appendChild(li);
    });

    // Setup "Download All" with Method 4 (Sequential Delay)
    document.getElementById('downloadAllBtn').onclick = () => downloadSequentially(files);
}

// --- New Function: Method 4 - Sequential Downloads ---
async function downloadSequentially(files) {
    for (let i = 0; i < files.length; i++) {
        const file = files[i];
        const a = document.createElement('a');
        a.href = file.url;
        a.download = file.name;
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
        
        // Wait 400ms between downloads to ensure Windows handles each file write correctly
        await new Promise(resolve => setTimeout(resolve, 400));
    }
}
</script>
</div>
</body>
</html>
