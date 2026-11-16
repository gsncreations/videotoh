<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="shortcut icon" href="data:image/x-icon;," type="image/x-icon">
<title>GSN Creations - Video to C/C++ Header Converter</title>
<meta name="description" content="Convert any video (MP4, WebM, MOV) into a C/C++ .h animation array for Arduino, ESP32, ESP8266, STM32 and OLED/TFT displays. Runs 100% in your browser.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.5/font/bootstrap-icons.css">
<style>
:root{
  --bg:#f4f6fb; --card:#fff; --ink:#0f172a; --muted:#64748b; --line:#dbe2ec;
  --blue:#2563eb; --teal:#0d9488; --orange:#f97316; --green:#059669; --red:#dc2626; --amber:#d97706;
  --soft:#f1f5f9; --grad:linear-gradient(90deg,var(--blue),var(--teal));
  --radius:18px;
}
*{box-sizing:border-box}
html{scroll-behavior:smooth}
body{margin:0;font-family:'Inter',system-ui,sans-serif;background:var(--bg);color:var(--ink);min-height:100vh;line-height:1.5}
body::before{content:'';position:fixed;inset:0;z-index:-1;pointer-events:none;
  background:radial-gradient(circle at 8% 12%,rgba(249,115,22,.08),transparent 38%),radial-gradient(circle at 92% 85%,rgba(37,99,235,.08),transparent 40%)}
a{color:var(--blue)}
.wrap{max-width:1180px;margin:0 auto;padding:28px 18px 60px}

/* header */
.hero{text-align:center;padding:28px 10px 10px}
.logo{font-weight:800;font-size:clamp(2rem,5vw,3.2rem);letter-spacing:-1px;background:linear-gradient(90deg,var(--orange),var(--blue));-webkit-background-clip:text;background-clip:text;color:transparent}
.hero h1{margin:4px 0 8px;font-size:clamp(1.1rem,2.6vw,1.6rem);font-weight:700}
.hero p{margin:0 auto 18px;max-width:720px;color:var(--muted)}
.pills{display:flex;flex-wrap:wrap;gap:10px;justify-content:center;margin-bottom:22px}
.pill{display:inline-flex;align-items:center;gap:8px;padding:8px 16px;border-radius:999px;font-weight:600;font-size:.9rem;text-decoration:none;border:1px solid var(--line);background:#fff;color:var(--ink);cursor:pointer;font-family:inherit}
.pill.yt{color:#e00;background:rgba(255,0,0,.07);border-color:rgba(255,0,0,.2)}
.pill.yt:hover{background:rgba(255,0,0,.13)}
.pill.privacy{color:var(--green);background:rgba(5,150,105,.08);border-color:rgba(5,150,105,.25)}

/* stats */
.stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:14px;margin-bottom:22px}
.stat{background:var(--card);border:1px solid var(--line);border-radius:14px;padding:16px;text-align:center}
.stat b{display:block;font-size:1.55rem;font-weight:800;background:var(--grad);-webkit-background-clip:text;background-clip:text;color:transparent}
.stat span{font-size:.8rem;color:var(--muted)}

/* cards */
.card{background:var(--card);border:1px solid var(--line);border-radius:var(--radius);margin-bottom:22px;box-shadow:0 6px 24px rgba(15,23,42,.05);overflow:hidden}
.card>h2{margin:0;padding:16px 22px;font-size:1.05rem;font-weight:700;color:#fff;background:var(--grad);display:flex;align-items:center;gap:10px;position:relative}
.card>h2::before{content:'';position:absolute;left:0;top:0;bottom:0;width:5px;background:linear-gradient(var(--orange),#f59e0b)}
.card>h2 .step{background:rgba(255,255,255,.22);border-radius:8px;padding:1px 9px;font-size:.85rem}
.body{padding:22px}
.grid{display:grid;gap:22px}
.g2{grid-template-columns:1fr 1fr}
.g3{grid-template-columns:repeat(3,1fr)}
@media(max-width:860px){.g2,.g3{grid-template-columns:1fr}}

label.l{display:block;font-weight:600;font-size:.88rem;margin-bottom:6px}
.hint{font-size:.76rem;color:var(--muted);margin-top:4px}
input[type=number],input[type=text],input[type=url],select{width:100%;padding:10px 13px;border:2px solid var(--line);border-radius:12px;background:var(--soft);font:inherit;color:var(--ink);transition:.2s}
input:focus,select:focus{outline:none;border-color:var(--teal);background:#fff;box-shadow:0 0 0 3px rgba(13,148,136,.12)}
input[type=range]{width:100%;accent-color:var(--teal)}
.row{display:flex;gap:10px;align-items:center}
.row>*{flex:1}
.row .x{flex:0 0 auto;color:var(--muted);font-weight:700}
.field{margin-bottom:16px}
h3.sub{margin:0 0 14px;font-size:.95rem;display:flex;gap:8px;align-items:center}

/* switch */
.sw{display:flex;align-items:center;gap:12px;margin-bottom:10px;cursor:pointer;user-select:none;font-size:.9rem;font-weight:500}
.sw input{display:none}
.sw i{position:relative;width:46px;height:24px;border-radius:24px;background:var(--line);transition:.3s;flex:0 0 auto}
.sw i::after{content:'';position:absolute;left:4px;top:4px;width:16px;height:16px;border-radius:50%;background:#fff;transition:.3s}
.sw input:checked+i{background:var(--teal)}
.sw input:checked+i::after{transform:translateX(22px)}

/* buttons */
.btn{display:inline-flex;align-items:center;justify-content:center;gap:8px;border:none;border-radius:12px;padding:11px 22px;font:inherit;font-weight:600;cursor:pointer;transition:.25s;color:#fff;background:var(--grad)}
.btn:hover:not(:disabled){transform:translateY(-2px);box-shadow:0 10px 24px rgba(37,99,235,.28)}
.btn:disabled{opacity:.45;cursor:not-allowed}
.btn.sm{padding:7px 14px;font-size:.85rem;border-radius:10px}
.btn.out{background:#fff;color:var(--blue);border:2px solid var(--blue)}
.btn.out:hover:not(:disabled){background:var(--blue);color:#fff}
.btn.go{background:linear-gradient(90deg,var(--green),#10b981);font-size:1.1rem;padding:16px 30px;width:100%}
.btn.stop{background:linear-gradient(90deg,var(--red),#f43f5e)}
.btn-row{display:flex;gap:10px;flex-wrap:wrap}

/* drop zone */
.drop{border:2.5px dashed var(--line);border-radius:16px;background:var(--soft);padding:34px 18px;text-align:center;cursor:pointer;transition:.25s}
.drop:hover,.drop.over{border-color:var(--teal);background:#f0fdfa}
.drop i{font-size:2.6rem;color:var(--teal)}
.drop b{display:block;margin-top:6px}
.drop small{color:var(--muted)}

/* preview */
.stage{display:grid;grid-template-columns:1fr 1fr;gap:20px}
@media(max-width:860px){.stage{grid-template-columns:1fr}}
.pv{background:#0b1220;border-radius:14px;padding:14px;text-align:center;min-height:180px;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:10px}
.pv .cap{color:#94a3b8;font-size:.75rem;font-weight:600;letter-spacing:.6px;text-transform:uppercase}
.pv video,.pv canvas{max-width:100%;max-height:340px;border-radius:8px;background:#000}
#outCanvas{image-rendering:pixelated;image-rendering:crisp-edges}
.empty{color:#64748b;font-size:.9rem}
.timeline{margin-top:14px}
.chips{display:flex;gap:8px;flex-wrap:wrap;margin-top:8px}
.chip{background:var(--soft);border:1px solid var(--line);border-radius:999px;padding:3px 11px;font-size:.76rem;color:var(--muted);font-weight:600}

/* progress */
.prog{display:none;margin-top:14px}
.bar{height:12px;background:var(--soft);border-radius:12px;overflow:hidden;border:1px solid var(--line)}
.bar>div{height:100%;width:0;background:linear-gradient(90deg,var(--orange),var(--teal));transition:width .1s}
.prog small{display:block;margin-top:6px;color:var(--muted)}

/* estimate */
.est{display:grid;grid-template-columns:repeat(auto-fit,minmax(170px,1fr));gap:10px;margin-top:6px}
.est div{background:var(--soft);border:1px solid var(--line);border-radius:12px;padding:10px 12px;font-size:.82rem;color:var(--muted)}
.est b{display:block;color:var(--ink);font-size:1.05rem}
.est .warn b{color:var(--red)} .est .ok b{color:var(--green)} .est .mid b{color:var(--amber)}
.notice{border-radius:12px;padding:11px 14px;font-size:.85rem;margin-top:12px;display:none}
.notice.show{display:block}
.notice.warn{background:#fff7ed;border:1px solid #fed7aa;color:#9a3412}
.notice.err{background:#fef2f2;border:1px solid #fecaca;color:#991b1b}
.notice.info{background:#eff6ff;border:1px solid #bfdbfe;color:#1e40af}

/* code */
.codebox{position:relative;border-radius:14px;overflow:hidden;background:#0f172a;border:1px solid var(--line)}
.codebar{display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:8px;padding:10px 14px;background:#111c33;border-bottom:1px solid #1e293b}
.codebar span{color:#94a3b8;font-size:.8rem;font-family:'JetBrains Mono',monospace}
pre#code{margin:0;padding:20px;font-family:'JetBrains Mono',monospace;font-size:.82rem;line-height:1.5;color:#e2e8f0;max-height:520px;min-height:240px;overflow:auto;white-space:pre}
pre#code::-webkit-scrollbar{width:9px;height:9px}
pre#code::-webkit-scrollbar-thumb{background:var(--teal);border-radius:6px}

footer{text-align:center;color:var(--muted);font-size:.85rem;margin-top:40px}
footer .badge{display:inline-block;background:linear-gradient(90deg,var(--orange),#f59e0b);color:#fff;font-weight:700;border-radius:999px;padding:5px 16px;margin-bottom:8px}

/* modal */
.modal{position:fixed;inset:0;background:rgba(15,23,42,.55);display:none;align-items:center;justify-content:center;z-index:50;padding:16px}
.modal.open{display:flex}
.modal .box{background:#fff;border-radius:20px;max-width:760px;width:100%;max-height:90vh;overflow:auto}
.modal .box>header{background:var(--grad);color:#fff;padding:16px 22px;display:flex;justify-content:space-between;align-items:center;font-weight:700}
.modal .box>header button{background:none;border:none;color:#fff;font-size:1.4rem;cursor:pointer}
.modal .inner{padding:22px;display:grid;grid-template-columns:1fr 1fr;gap:18px}
@media(max-width:700px){.modal .inner{grid-template-columns:1fr}}
.modal h4{margin:0 0 8px;color:var(--teal)}
.modal p{margin:0 0 6px;font-size:.88rem;color:#334155}
.toast{position:fixed;bottom:22px;left:50%;transform:translateX(-50%) translateY(80px);background:#0f172a;color:#fff;padding:11px 20px;border-radius:12px;font-weight:600;font-size:.9rem;transition:.35s;z-index:99}
.toast.show{transform:translateX(-50%) translateY(0)}
</style>
</head>
<body>
<div class="wrap">

<!-- HERO -->
<div class="hero">
  <div class="logo">GSN CREATIONS</div>
  <h1>Video to C/C++ Header (.h) Converter</h1>
  <p>Turn any MP4 / WebM / MOV clip into a ready-to-flash animation array for Arduino, ESP32, ESP8266, STM32 and Raspberry Pi Pico &mdash; OLED, LCD and TFT displays. Everything runs locally in your browser.</p>
  <div class="pills">
    <a class="pill yt" href="https://www.youtube.com/@GSNcreation07" target="_blank" rel="noopener"><i class="bi bi-youtube"></i> Subscribe on YouTube</a>
    <span class="pill privacy"><i class="bi bi-shield-check"></i> Your video never leaves your device</span>
    <button class="pill" onclick="openHelp(true)"><i class="bi bi-question-circle"></i> Help Guide</button>
  </div>
</div>

<!-- STATS -->
<div class="stats">
  <div class="stat"><b id="sFrames">0</b><span>Frames</span></div>
  <div class="stat"><b id="sRes">128x64</b><span>Resolution</span></div>
  <div class="stat"><b id="sFps">10</b><span>FPS</span></div>
  <div class="stat"><b id="sDur">0.0s</b><span>Clip length</span></div>
  <div class="stat"><b id="sSize">0 KB</b><span>Output data</span></div>
</div>

<!-- STEP 1 -->
<div class="card">
  <h2><span class="step">1</span><i class="bi bi-camera-video-fill"></i> Load Video</h2>
  <div class="body grid g2">
    <div>
      <div class="drop" id="drop">
        <i class="bi bi-cloud-arrow-up-fill"></i>
        <b>Drop a video here or click to browse</b>
        <small>MP4 &middot; WebM &middot; MOV &middot; OGV &middot; anything your browser can play</small>
        <input type="file" id="file" accept="video/*" hidden>
      </div>
      <div class="field" style="margin-top:16px">
        <label class="l" for="urlIn">Or load from URL</label>
        <div class="row">
          <input type="url" id="urlIn" placeholder="https://example.com/clip.mp4">
          <button class="btn out sm" id="urlBtn" style="flex:0 0 auto"><i class="bi bi-cloud-download"></i> Load</button>
        </div>
        <div class="hint">The remote server must allow CORS, otherwise download the file and upload it instead.</div>
      </div>
      <div class="notice" id="loadMsg"></div>
    </div>
    <div>
      <h3 class="sub"><i class="bi bi-gear-wide-connected"></i> Output Configuration</h3>
      <div class="field">
        <label class="l">Display size (px)</label>
        <div class="row">
          <input type="number" id="W" value="128" min="1" max="1024">
          <span class="x">&times;</span>
          <input type="number" id="H" value="64" min="1" max="1024">
        </div>
        <div class="chips" id="sizeChips"></div>
      </div>
      <div class="field">
        <label class="l" for="colorMode">Colour mode</label>
        <select id="colorMode">
          <option value="mono" selected>Monochrome 1-bit (OLED / e-paper / Nokia LCD)</option>
          <option value="rgb565">Colour RGB565 16-bit (TFT / ST7789 / ILI9341)</option>
        </select>
      </div>
      <div class="field" id="scanField">
        <label class="l" for="drawMode">Pixel packing (mono)</label>
        <select id="drawMode">
          <option value="horizontal" selected>Horizontal &middot; MSB first (Adafruit GFX drawBitmap)</option>
          <option value="horizontal_lsb">Horizontal &middot; LSB first (U8g2 XBM)</option>
          <option value="vertical">Vertical pages &middot; LSB top (SSD1306 raw buffer)</option>
        </select>
      </div>
    </div>
  </div>
</div>

<!-- STEP 2 -->
<div class="card">
  <h2><span class="step">2</span><i class="bi bi-scissors"></i> Trim &amp; Sampling</h2>
  <div class="body">
    <div class="stage">
      <div class="pv"><div class="cap">Source video</div>
        <video id="vid" muted playsinline preload="auto" style="display:none"></video>
        <div class="empty" id="vidEmpty">Load a video to see it here</div>
      </div>
      <div class="pv"><div class="cap">Live frame preview (what the display will show)</div>
        <canvas id="liveCanvas" style="display:none;image-rendering:pixelated"></canvas>
        <div class="empty" id="liveEmpty">Preview appears after loading</div>
      </div>
    </div>
    <div class="timeline">
      <label class="l">Scrub position: <span id="scrubLbl">0.00s</span></label>
      <input type="range" id="scrub" min="0" max="1" step="0.01" value="0" disabled>
    </div>
    <div class="grid g3" style="margin-top:14px">
      <div><label class="l" for="tStart">Start time (s)</label><input type="number" id="tStart" value="0" min="0" step="0.1"></div>
      <div><label class="l" for="tEnd">End time (s)</label><input type="number" id="tEnd" value="0" min="0" step="0.1"></div>
      <div><label class="l" for="fps">Output FPS</label><input type="number" id="fps" value="10" min="1" max="60" step="1"></div>
    </div>
    <div class="btn-row" style="margin-top:6px">
      <button class="btn out sm" id="setStart" disabled><i class="bi bi-skip-start"></i> Set start = scrub</button>
      <button class="btn out sm" id="setEnd" disabled><i class="bi bi-skip-end"></i> Set end = scrub</button>
      <button class="btn out sm" id="fullClip" disabled><i class="bi bi-arrows-expand"></i> Full clip</button>
    </div>
    <div class="grid g3" style="margin-top:18px">
      <div>
        <label class="l" for="maxFrames">Max frames (safety cap)</label>
        <input type="number" id="maxFrames" value="120" min="1" max="2000">
        <div class="hint">Microcontrollers have very little flash. Keep this low.</div>
      </div>
      <div>
        <label class="l" for="board">Check size against board</label>
        <select id="board">
          <option value="30000">Arduino Uno / Nano (~30 KB)</option>
          <option value="253000">Arduino Mega (~250 KB)</option>
          <option value="400000">ESP8266 4MB (~400 KB usable)</option>
          <option value="1300000" selected>ESP32 default (~1.3 MB)</option>
          <option value="3000000">ESP32 large-app / 16MB (~3 MB)</option>
          <option value="1900000">Raspberry Pi Pico 2MB (~1.9 MB)</option>
          <option value="0">No limit</option>
        </select>
      </div>
      <div>
        <label class="l" for="layout">Array layout</label>
        <select id="layout">
          <option value="2d" selected>One 2D array [frames][bytes]</option>
          <option value="sep">Separate array per frame + pointer table</option>
        </select>
      </div>
    </div>
    <div class="est" id="est"></div>
    <div class="notice" id="estMsg"></div>
  </div>
</div>

<!-- STEP 3 -->
<div class="card">
  <h2><span class="step">3</span><i class="bi bi-sliders2"></i> Image Processing</h2>
  <div class="body">
    <div class="grid g3">
      <div>
        <div class="field">
          <label class="l">Threshold: <span id="thVal" style="color:var(--teal)">128</span></label>
          <input type="range" id="threshold" min="0" max="255" value="128">
          <div class="hint">Mono only. Pixels brighter than this turn on.</div>
        </div>
        <div class="field">
          <label class="l" for="dither">Dithering (mono)</label>
          <select id="dither">
            <option value="none">None (hard threshold)</option>
            <option value="fs" selected>Floyd&ndash;Steinberg (smooth photos)</option>
            <option value="bayer">Ordered Bayer 4&times;4 (retro look)</option>
          </select>
        </div>
      </div>
      <div>
        <div class="field">
          <label class="l">Brightness: <span id="brVal" style="color:var(--teal)">0</span></label>
          <input type="range" id="bright" min="-100" max="100" value="0">
        </div>
        <div class="field">
          <label class="l">Contrast: <span id="coVal" style="color:var(--teal)">0</span></label>
          <input type="range" id="contrast" min="-100" max="100" value="0">
        </div>
      </div>
      <div>
        <div class="field">
          <label class="l" for="scaleMode">Scaling</label>
          <select id="scaleMode">
            <option value="fit">Fit (keep aspect, letterbox)</option>
            <option value="fill">Fill (keep aspect, crop)</option>
            <option value="stretch">Stretch to display</option>
          </select>
        </div>
        <label class="sw"><input type="checkbox" id="invert"><i></i>Invert colours</label>
      </div>
    </div>
    <hr style="border:none;border-top:1px solid var(--line);margin:8px 0 18px">
    <h3 class="sub"><i class="bi bi-arrow-repeat"></i> Transformations</h3>
    <div class="grid g3">
      <div>
        <label class="sw"><input type="checkbox" id="flipH"><i></i>Flip horizontal</label>
        <label class="sw"><input type="checkbox" id="flipV"><i></i>Flip vertical</label>
      </div>
      <div>
        <label class="l" for="rot">Rotation</label>
        <select id="rot"><option value="0">0&deg;</option><option value="90">90&deg;</option><option value="180">180&deg;</option><option value="270">270&deg;</option></select>
      </div>
      <div>
        <label class="l">Quick presets</label>
        <div class="btn-row">
          <button class="btn out sm" onclick="preset('oled')">OLED 128&times;64</button>
          <button class="btn out sm" onclick="preset('oled32')">OLED 128&times;32</button>
          <button class="btn out sm" onclick="preset('tft')">TFT 240&times;240</button>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- STEP 4 -->
<div class="card">
  <h2><span class="step">4</span><i class="bi bi-code-square"></i> Code Output</h2>
  <div class="body">
    <div class="grid g2">
      <div class="field"><label class="l" for="varName">Animation name</label><input type="text" id="varName" value="myVideo"><div class="hint">Used for the array and macro names.</div></div>
      <div class="field"><label class="l" for="platform">Target platform</label>
        <select id="platform">
          <option value="arduino" selected>Arduino AVR (PROGMEM)</option>
          <option value="esp">ESP8266 / ESP32 (PROGMEM)</option>
          <option value="pico">Pico / STM32 / generic ARM (const)</option>
          <option value="plain">Plain C/C++ (const)</option>
        </select></div>
    </div>

    <button class="btn go" id="convertBtn" disabled><i class="bi bi-magic"></i> Convert Video to C/C++ Array</button>
    <button class="btn stop" id="cancelBtn" style="display:none;width:100%;margin-top:10px"><i class="bi bi-x-octagon"></i> Cancel</button>
    <div class="prog" id="prog"><div class="bar"><div id="barIn"></div></div><small id="progTxt">Starting&hellip;</small></div>

    <div class="stage" style="margin-top:22px" id="resultStage" hidden>
      <div class="pv"><div class="cap">Converted animation</div>
        <canvas id="outCanvas"></canvas>
        <div class="btn-row" style="justify-content:center">
          <button class="btn sm" id="pPrev"><i class="bi bi-chevron-left"></i></button>
          <button class="btn sm" id="pPlay"><i class="bi bi-pause-fill"></i> Pause</button>
          <button class="btn sm" id="pNext"><i class="bi bi-chevron-right"></i></button>
        </div>
        <div class="cap" id="pCnt">Frame 0/0</div>
      </div>
      <div>
        <h3 class="sub"><i class="bi bi-info-circle"></i> Result summary</h3>
        <div class="est" id="resEst"></div>
        <div class="field" style="margin-top:14px">
          <label class="l">Preview zoom: <span id="zmVal">4</span>&times;</label>
          <input type="range" id="zoom" min="1" max="8" value="3">
        </div>
        <label class="sw"><input type="checkbox" id="oledTint" checked><i></i>Blue OLED tint (mono preview)</label>
      </div>
    </div>

    <div class="codebox" style="margin-top:22px">
      <div class="codebar">
        <span id="codeInfo">// nothing generated yet</span>
        <div class="btn-row">
          <button class="btn sm" id="saveBtn" disabled><i class="bi bi-file-earmark-arrow-down"></i> Save .h</button>
          <button class="btn sm" id="copyBtn" disabled><i class="bi bi-clipboard"></i> Copy</button>
          <button class="btn sm out" id="clearBtn" style="background:transparent;color:#cbd5e1;border-color:#334155"><i class="bi bi-x-circle"></i> Clear</button>
        </div>
      </div>
<pre id="code">// 1. Load a video
// 2. Pick your display size, trim and FPS
// 3. Click "Convert Video to C/C++ Array"
//
// Output is ready for Arduino, ESP32, ESP8266, STM32, Pico.</pre>
    </div>
    <div class="notice info show" style="margin-top:12px" id="truncNote" hidden></div>
  </div>
</div>

<footer>
  <span class="badge">GSN Creations</span>
  <p>Professional Video &amp; GIF to C/C++ converter for embedded systems.<br>
  Built with <i class="bi bi-heart-fill" style="color:#e11d48"></i> by GSN Creations &middot;
  <a href="https://www.youtube.com/@GSNcreation07" target="_blank" rel="noopener">youtube.com/@GSNcreation07</a></p>
</footer>
</div>

<!-- HELP -->
<div class="modal" id="help" onclick="if(event.target===this)openHelp(false)">
  <div class="box">
    <header><span><i class="bi bi-book"></i> GSN Video Converter Guide</span><button onclick="openHelp(false)" aria-label="Close">&times;</button></header>
    <div class="inner">
      <div><h4>1. Load</h4><p>Drop a video file or paste a URL. Nothing is uploaded; processing happens in your browser.</p></div>
      <div><h4>2. Trim &amp; FPS</h4><p>Pick start and end time. 8&ndash;15 FPS is plenty for small OLEDs and keeps flash usage low.</p></div>
      <div><h4>3. Process</h4><p>Use Floyd&ndash;Steinberg dithering for photo-like video, or plain threshold for line art. Adjust brightness and contrast until the live preview looks good.</p></div>
      <div><h4>4. Convert</h4><p>Click Convert, check the animation preview, then save the .h file into your sketch folder and <code>#include</code> it.</p></div>
      <div><h4>Memory tips</h4><p>128&times;64 mono = 1024 bytes/frame. 100 frames = 100 KB. An Uno only has ~30 KB, so use fewer frames or a smaller size.</p></div>
      <div><h4>Packing modes</h4><p>Horizontal MSB works with Adafruit <code>drawBitmap()</code>. Vertical pages matches the raw SSD1306 buffer. Horizontal LSB matches U8g2 XBM.</p></div>
    </div>
  </div>
</div>
<div class="toast" id="toast"></div>

<script>
'use strict';
const $ = id => document.getElementById(id);
const vid = $('vid');
let objectUrl = null, videoName = 'myVideo', videoReady = false;
let result = null;          // {frames:[typed arrays], w,h,mode, delays}
let fullCode = '';
let playTimer = null, playIdx = 0, playing = true, cancelFlag = false, busy = false;

/* ------------ helpers ------------ */
function toast(msg){const t=$('toast');t.textContent=msg;t.classList.add('show');clearTimeout(toast._t);toast._t=setTimeout(()=>t.classList.remove('show'),2200);}
function openHelp(o){$('help').classList.toggle('open',o);}
function showNote(id,cls,msg){const n=$(id);n.className='notice show '+cls;n.innerHTML=msg;}
function hideNote(id){$(id).className='notice';}
function fmtBytes(b){if(b<1024)return b+' B';if(b<1048576)return (b/1024).toFixed(1)+' KB';return (b/1048576).toFixed(2)+' MB';}
function sanitize(n){n=n.replace(/\.[^.]+$/,'').replace(/[^a-zA-Z0-9_]/g,'_');if(!n)n='myVideo';if(/^\d/.test(n))n='_'+n;return n;}
const nextTick = () => new Promise(r=>setTimeout(r,0));
const cfg = () => ({
  w:Math.max(1,Math.min(1024,parseInt($('W').value)||128)),
  h:Math.max(1,Math.min(1024,parseInt($('H').value)||64)),
  mode:$('colorMode').value, pack:$('drawMode').value,
  th:parseInt($('threshold').value), dither:$('dither').value,
  br:parseInt($('bright').value), co:parseInt($('contrast').value),
  scale:$('scaleMode').value, invert:$('invert').checked,
  fh:$('flipH').checked, fv:$('flipV').checked, rot:parseInt($('rot').value),
  fps:Math.max(1,Math.min(60,parseInt($('fps').value)||10)),
  t0:parseFloat($('tStart').value)||0, t1:parseFloat($('tEnd').value)||0,
  maxFrames:Math.max(1,parseInt($('maxFrames').value)||120),
  layout:$('layout').value, platform:$('platform').value, name:$('varName').value.trim()||'myVideo'
});

/* ------------ size chips / presets ------------ */
[['128×64',128,64],['128×32',128,32],['96×64',96,64],['64×48',64,48],['84×48',84,48],['240×240',240,240],['320×240',320,240]].forEach(([l,w,h])=>{
  const c=document.createElement('span');c.className='chip';c.style.cursor='pointer';c.textContent=l;
  c.onclick=()=>{$('W').value=w;$('H').value=h;refreshAll();};$('sizeChips').appendChild(c);
});
function preset(t){
  if(t==='oled'){$('W').value=128;$('H').value=64;$('colorMode').value='mono';$('drawMode').value='horizontal';$('dither').value='fs';}
  if(t==='oled32'){$('W').value=128;$('H').value=32;$('colorMode').value='mono';$('drawMode').value='horizontal';$('dither').value='fs';}
  if(t==='tft'){$('W').value=240;$('H').value=240;$('colorMode').value='rgb565';$('maxFrames').value=20;$('fps').value=8;$('platform').value='esp';}
  refreshAll();
}

/* ------------ loading ------------ */
const drop=$('drop'),fileIn=$('file');
drop.onclick=()=>fileIn.click();
['dragenter','dragover'].forEach(e=>drop.addEventListener(e,ev=>{ev.preventDefault();drop.classList.add('over');}));
['dragleave','drop'].forEach(e=>drop.addEventListener(e,ev=>{ev.preventDefault();drop.classList.remove('over');}));
drop.addEventListener('drop',ev=>{const f=ev.dataTransfer.files[0];if(f)loadFile(f);});
fileIn.onchange=()=>{if(fileIn.files[0])loadFile(fileIn.files[0]);};
$('urlBtn').onclick=loadUrl;
$('urlIn').addEventListener('keydown',e=>{if(e.key==='Enter')loadUrl();});

function loadFile(f){
  if(!f.type.startsWith('video/')&&!/\.(mp4|webm|mov|ogv|mkv|m4v)$/i.test(f.name)){showNote('loadMsg','err','Please choose a video file.');return;}
  if(objectUrl)URL.revokeObjectURL(objectUrl);
  objectUrl=URL.createObjectURL(f);videoName=sanitize(f.name);
  vid.removeAttribute('crossorigin');
  startLoad(objectUrl);
}
function loadUrl(){
  const u=$('urlIn').value.trim();if(!u){showNote('loadMsg','err','Enter a video URL first.');return;}
  videoName=sanitize((u.split('?')[0].split('/').pop()||'myVideo'));
  vid.crossOrigin='anonymous';startLoad(u);
}
function startLoad(src){
  videoReady=false;stopPlayback();clearResult();
  showNote('loadMsg','info','<i class="bi bi-hourglass-split"></i> Loading video&hellip;');
  vid.onloadedmetadata=()=>{
    if(!isFinite(vid.duration)||vid.duration<=0){showNote('loadMsg','err','Could not read video duration.');return;}
    videoReady=true;
    vid.style.display='block';$('vidEmpty').style.display='none';
    vid.controls=false;
    $('varName').value=videoName;
    $('tStart').value=0;$('tEnd').value=Math.min(vid.duration,10).toFixed(2);
    $('tEnd').max=vid.duration.toFixed(2);$('tStart').max=vid.duration.toFixed(2);
    const s=$('scrub');s.max=vid.duration;s.value=0;s.disabled=false;
    ['setStart','setEnd','fullClip','convertBtn'].forEach(i=>$(i).disabled=false);
    showNote('loadMsg','info',`<i class="bi bi-check-circle"></i> Loaded <b>${vid.videoWidth}&times;${vid.videoHeight}</b>, ${vid.duration.toFixed(2)}s.`);
    seekTo(0).then(()=>{updateLive();refreshAll();});
  };
  vid.onerror=()=>{showNote('loadMsg','err','Unable to load this video. The format may be unsupported or the URL blocks CORS.');};
  vid.src=src;vid.load();
}

function seekTo(t){
  return new Promise(res=>{
    let done=false;const fin=()=>{if(done)return;done=true;vid.removeEventListener('seeked',fin);clearTimeout(to);res();};
    const to=setTimeout(fin,4000);
    vid.addEventListener('seeked',fin);
    vid.currentTime=Math.max(0,Math.min(t,Math.max(0,vid.duration-0.001)));
  });
}

/* scrub + trim */
$('scrub').oninput=async()=>{const t=parseFloat($('scrub').value);$('scrubLbl').textContent=t.toFixed(2)+'s';await seekTo(t);updateLive();};
$('setStart').onclick=()=>{$('tStart').value=parseFloat($('scrub').value).toFixed(2);refreshAll();};
$('setEnd').onclick=()=>{$('tEnd').value=parseFloat($('scrub').value).toFixed(2);refreshAll();};
$('fullClip').onclick=()=>{$('tStart').value=0;$('tEnd').value=vid.duration.toFixed(2);refreshAll();};

/* ------------ image pipeline ------------ */
const work=document.createElement('canvas');
const wctx=work.getContext('2d',{willReadFrequently:true});
const BAYER=[[0,8,2,10],[12,4,14,6],[3,11,1,9],[15,7,13,5]];

function drawSource(c){
  work.width=c.w;work.height=c.h;
  wctx.fillStyle='#000';wctx.fillRect(0,0,c.w,c.h);
  const sw=vid.videoWidth,sh=vid.videoHeight;
  const swap=(c.rot===90||c.rot===270);
  const ew=swap?sh:sw, eh=swap?sw:sh;           // effective (rotated) source size
  let sx,sy;
  if(c.scale==='stretch'){sx=c.w/ew;sy=c.h/eh;}
  else if(c.scale==='fill'){sx=sy=Math.max(c.w/ew,c.h/eh);}
  else{sx=sy=Math.min(c.w/ew,c.h/eh);}
  wctx.save();
  wctx.imageSmoothingEnabled=true;wctx.imageSmoothingQuality='high';
  wctx.translate(c.w/2,c.h/2);
  if(c.fh)wctx.scale(-1,1);
  if(c.fv)wctx.scale(1,-1);
  if(c.rot)wctx.rotate(c.rot*Math.PI/180);
  // after rotation, local axes follow the source; apply scale per effective axis
  const lx=swap?sy:sx, ly=swap?sx:sy;
  wctx.drawImage(vid,-sw*lx/2,-sh*ly/2,sw*lx,sh*ly);
  wctx.restore();
  return wctx.getImageData(0,0,c.w,c.h);
}

// returns {bits:Uint8Array(w*h) 0/1}  or  {rgb:Uint16Array(w*h)}
function processFrame(c){
  const img=drawSource(c),d=img.data,n=c.w*c.h;
  const bf=c.co===0?1:(259*(c.co+255))/(255*(259-c.co)); // contrast factor
  const adj=v=>{v=bf*(v-128)+128+c.br;return v<0?0:v>255?255:v;};
  if(c.mode==='rgb565'){
    const out=new Uint16Array(n);
    for(let i=0,p=0;i<n;i++,p+=4){
      let r=adj(d[p]),g=adj(d[p+1]),b=adj(d[p+2]);
      if(c.invert){r=255-r;g=255-g;b=255-b;}
      out[i]=((r&0xF8)<<8)|((g&0xFC)<<3)|(b>>3);
    }
    return {rgb:out};
  }
  const g=new Float32Array(n);
  for(let i=0,p=0;i<n;i++,p+=4)g[i]=adj(0.299*d[p]+0.587*d[p+1]+0.114*d[p+2]);
  const bits=new Uint8Array(n);
  if(c.dither==='fs'){
    const W=c.w,H=c.h;
    for(let y=0;y<H;y++)for(let x=0;x<W;x++){
      const i=y*W+x,old=g[i],nw=old>=c.th?255:0,e=old-nw;bits[i]=nw?1:0;
      if(x+1<W)g[i+1]+=e*7/16;
      if(y+1<H){if(x>0)g[i+W-1]+=e*3/16;g[i+W]+=e*5/16;if(x+1<W)g[i+W+1]+=e/16;}
    }
  }else if(c.dither==='bayer'){
    for(let y=0;y<c.h;y++)for(let x=0;x<c.w;x++){
      const i=y*c.w+x,t=(BAYER[y&3][x&3]+0.5)/16*255+(c.th-128);
      bits[i]=g[i]>=t?1:0;
    }
  }else{for(let i=0;i<n;i++)bits[i]=g[i]>=c.th?1:0;}
  if(c.invert)for(let i=0;i<n;i++)bits[i]^=1;
  return {bits};
}

function packBits(bits,c){
  const W=c.w,H=c.h;let out;
  if(c.pack==='vertical'){
    const pages=Math.ceil(H/8);out=new Uint8Array(pages*W);
    for(let p=0;p<pages;p++)for(let x=0;x<W;x++){let b=0;
      for(let k=0;k<8;k++){const y=p*8+k;if(y<H&&bits[y*W+x])b|=1<<k;}
      out[p*W+x]=b;}
  }else{
    const bpr=Math.ceil(W/8);out=new Uint8Array(bpr*H);
    const msb=c.pack==='horizontal';
    for(let y=0;y<H;y++)for(let bx=0;bx<bpr;bx++){let b=0;
      for(let k=0;k<8;k++){const x=bx*8+k;if(x<W&&bits[y*W+x])b|=msb?(0x80>>k):(1<<k);}
      out[y*bpr+bx]=b;}
  }
  return out;
}
function frameBytes(c){
  if(c.mode==='rgb565')return c.w*c.h*2;
  return c.pack==='vertical'?Math.ceil(c.h/8)*c.w:Math.ceil(c.w/8)*c.h;
}

/* ------------ live preview ------------ */
function paintMono(canvas,bits,w,h,tint){
  canvas.width=w;canvas.height=h;
  const x=canvas.getContext('2d'),im=x.createImageData(w,h),o=im.data;
  const on=tint?[120,200,255]:[255,255,255];
  for(let i=0,p=0;i<w*h;i++,p+=4){const v=bits[i];o[p]=v?on[0]:0;o[p+1]=v?on[1]:0;o[p+2]=v?on[2]:0;o[p+3]=255;}
  x.putImageData(im,0,0);
}
function paintRGB(canvas,rgb,w,h){
  canvas.width=w;canvas.height=h;
  const x=canvas.getContext('2d'),im=x.createImageData(w,h),o=im.data;
  for(let i=0,p=0;i<w*h;i++,p+=4){const v=rgb[i];
    o[p]=((v>>11)&31)*255/31;o[p+1]=((v>>5)&63)*255/63;o[p+2]=(v&31)*255/31;o[p+3]=255;}
  x.putImageData(im,0,0);
}
function setZoom(canvas){
  const z=parseInt($('zoom').value);canvas.style.width=(canvas.width*z)+'px';canvas.style.height='auto';canvas.style.maxWidth='100%';
}
function updateLive(){
  if(!videoReady)return;
  const c=cfg();
  try{
    const r=processFrame(c),cv=$('liveCanvas');
    if(r.bits)paintMono(cv,r.bits,c.w,c.h,$('oledTint').checked);else paintRGB(cv,r.rgb,c.w,c.h);
    cv.style.display='block';$('liveEmpty').style.display='none';
    const z=Math.max(1,Math.floor(300/c.w));cv.style.width=(c.w*Math.min(z,6))+'px';cv.style.height='auto';cv.style.maxWidth='100%';
  }catch(e){
    showNote('loadMsg','err','Canvas is blocked (CORS). Download the video and upload it as a file instead.');
  }
}

/* ------------ estimates / stats ------------ */
function frameCountFor(c){
  const dur=Math.max(0,Math.min(c.t1,vid.duration||0)-c.t0);
  return Math.max(1,Math.min(c.maxFrames,Math.floor(dur*c.fps)||1));
}
function refreshAll(){
  const c=cfg();
  $('sRes').textContent=c.w+'x'+c.h;$('sFps').textContent=c.fps;
  $('scanField').style.opacity=c.mode==='mono'?1:.4;
  if(!videoReady){return;}
  const dur=Math.max(0,c.t1-c.t0),n=frameCountFor(c),fb=frameBytes(c),total=n*fb,lim=parseInt($('board').value);
  $('sFrames').textContent=n;$('sDur').textContent=(n/c.fps).toFixed(1)+'s';$('sSize').textContent=fmtBytes(total);
  const pct=lim?total/lim*100:0,cls=!lim?'ok':pct>100?'warn':pct>70?'mid':'ok';
  $('est').innerHTML=`<div><b>${n}</b>frames</div><div><b>${fmtBytes(fb)}</b>per frame</div><div class="${cls}"><b>${fmtBytes(total)}</b>total flash${lim?` (${pct.toFixed(0)}% of board)`:''}</div><div><b>${(1000/c.fps).toFixed(0)} ms</b>per frame delay</div>`;
  if(lim&&total>lim)showNote('estMsg','warn',`<i class="bi bi-exclamation-triangle"></i> This animation (${fmtBytes(total)}) is larger than the selected board's flash budget. Reduce frames, FPS or resolution.`);
  else if(dur*c.fps>c.maxFrames)showNote('estMsg','info',`Clip would need ${Math.floor(dur*c.fps)} frames; capped at ${c.maxFrames}. Shorten the range or raise the cap.`);
  else hideNote('estMsg');
  updateLive();
}
['W','H','colorMode','drawMode','fps','tStart','tEnd','maxFrames','board','layout','scaleMode','dither','rot','flipH','flipV','invert','oledTint'].forEach(id=>$(id).addEventListener('change',refreshAll));
['threshold','bright','contrast'].forEach(id=>$(id).addEventListener('input',()=>{
  $('thVal').textContent=$('threshold').value;$('brVal').textContent=$('bright').value;$('coVal').textContent=$('contrast').value;
  clearTimeout(refreshAll._t);refreshAll._t=setTimeout(refreshAll,40);
}));
['W','H','fps'].forEach(id=>$(id).addEventListener('input',()=>{clearTimeout(refreshAll._t);refreshAll._t=setTimeout(refreshAll,250);}));

/* ------------ conversion ------------ */
$('convertBtn').onclick=convert;
$('cancelBtn').onclick=()=>{cancelFlag=true;};
async function convert(){
  if(!videoReady||busy)return;
  const c=cfg();
  if(c.t1<=c.t0){showNote('estMsg','err','End time must be greater than start time.');return;}
  busy=true;cancelFlag=false;stopPlayback();
  $('convertBtn').style.display='none';$('cancelBtn').style.display='flex';
  $('prog').style.display='block';
  const n=frameCountFor(c),step=1/c.fps,frames=[],preview=[];
  try{
    for(let i=0;i<n;i++){
      if(cancelFlag)throw new Error('cancelled');
      const t=Math.min(c.t0+i*step,vid.duration-0.001);
      await seekTo(t);
      const r=processFrame(c);
      if(r.bits){frames.push(packBits(r.bits,c));preview.push(r.bits);}
      else{frames.push(r.rgb);preview.push(r.rgb);}
      $('barIn').style.width=((i+1)/n*100)+'%';
      $('progTxt').textContent=`Frame ${i+1} / ${n}  ·  t = ${t.toFixed(2)}s`;
      if(i%2===0)await nextTick();
    }
    const delay=Math.round(1000/c.fps);
    result={frames,preview,c,delays:new Array(n).fill(delay)};
    $('progTxt').textContent='Generating code…';await nextTick();
    fullCode=generateCode(result);
    showCode(fullCode);
    showResult();
    toast('Conversion complete ✔');
  }catch(e){
    if(e.message==='cancelled')toast('Cancelled');
    else showNote('estMsg','err','Conversion failed: '+e.message+'. If the video is from a URL, upload it as a file (CORS).');
  }
  busy=false;$('convertBtn').style.display='inline-flex';$('cancelBtn').style.display='none';
  setTimeout(()=>{$('prog').style.display='none';$('barIn').style.width='0';},700);
}

/* ------------ code generation ------------ */
function hex(v,w){return '0x'+v.toString(16).padStart(w,'0');}
function generateCode(res){
  const c=res.c,N=res.frames.length,U=c.name.toUpperCase(),nm=c.name,rgb=c.mode==='rgb565';
  const fb=frameBytes(c),type=rgb?'uint16_t':'uint8_t',per=rgb?c.w*c.h:fb;
  const pg=c.platform==='arduino'||c.platform==='esp';
  const attr=pg?' PROGMEM':'';
  const q=c.platform==='plain'?'':'const ';
  const L=[];
  L.push(`#ifndef ${U}_H`,`#define ${U}_H`,'');
  L.push('// =====================================================');
  L.push('// GSN Creations - Video to C/C++ Header Converter');
  L.push('// YouTube: https://www.youtube.com/@GSNcreation07');
  L.push('// =====================================================');
  L.push(`// Frames     : ${N}`,`// Size       : ${c.w}x${c.h}`,`// FPS        : ${c.fps}`);
  L.push(`// Colour     : ${rgb?'RGB565 (16-bit)':'Monochrome 1-bit, '+c.pack}`);
  if(!rgb)L.push(`// Dither     : ${c.dither}, threshold ${c.th}, invert ${c.invert?'yes':'no'}`);
  L.push(`// Data size  : ${fmtBytes(N*fb)}`,`// Generated  : ${new Date().toISOString().slice(0,10)}`);
  L.push('// =====================================================','');
  L.push('#include <stdint.h>');
  if(c.platform==='arduino')L.push('#include <avr/pgmspace.h>');
  else if(c.platform==='esp')L.push('#include <pgmspace.h>');
  L.push('');
  L.push(`#define ${U}_FRAME_COUNT ${N}`,`#define ${U}_WIDTH ${c.w}`,`#define ${U}_HEIGHT ${c.h}`,`#define ${U}_FPS ${c.fps}`,`#define ${U}_FRAME_SIZE ${per}  // ${rgb?'pixels (uint16_t)':'bytes'} per frame`,'');
  L.push('// Per-frame delay in milliseconds');
  L.push(`${q}uint16_t ${nm}_delays[${U}_FRAME_COUNT]${attr} = { ${res.delays.join(', ')} };`,'');
  const fmt=f=>{const parts=[],w=rgb?4:2;
    for(let i=0;i<f.length;i++)parts.push(hex(f[i],w));
    const lines=[];for(let i=0;i<parts.length;i+=16)lines.push('  '+parts.slice(i,i+16).join(', '));
    return lines.join(',\n');};
  if(c.layout==='2d'){
    L.push(`// Frame data - ${per} ${rgb?'pixels':'bytes'} per frame`);
    L.push(`${q}${type} ${nm}_frames[${U}_FRAME_COUNT][${U}_FRAME_SIZE]${attr} = {`);
    res.frames.forEach((f,i)=>{L.push(`  { // frame ${i}`);L.push(fmt(f).replace(/^/gm,'  '));L.push('  }'+(i<N-1?',':''));});
    L.push('};','');
  }else{
    res.frames.forEach((f,i)=>{
      L.push(`${q}${type} ${nm}_frame_${i}[${U}_FRAME_SIZE]${attr} = {`);L.push(fmt(f));L.push('};','');
    });
    L.push(`${q}${type}* ${nm}_frames[${U}_FRAME_COUNT]${attr} = {`);
    L.push('  '+res.frames.map((_,i)=>`${nm}_frame_${i}`).join(', '));L.push('};','');
    if(c.platform==='arduino'||c.platform==='esp')L.push(`// NOTE: pointers live in PROGMEM - read with (const ${type}*)pgm_read_ptr(&${nm}_frames[i])`,'');
  }
  L.push('/* =====================================================');
  L.push(' * USAGE EXAMPLE');
  L.push(' * =====================================================');
  const fp=c.layout==='2d'?`${nm}_frames[f]`:(pg?`(const ${type}*)pgm_read_ptr(&${nm}_frames[f])`:`${nm}_frames[f]`);
  if(rgb){
    L.push(' * TFT_eSPI / Adafruit_ST77xx:');
    L.push(` *   for(uint8_t f=0; f<${U}_FRAME_COUNT; f++){`);
    L.push(` *     tft.pushImage(0,0,${U}_WIDTH,${U}_HEIGHT,${fp});   // TFT_eSPI`);
    L.push(` *     // Adafruit: tft.drawRGBBitmap(0,0,${fp},${U}_WIDTH,${U}_HEIGHT);`);
    L.push(` *     delay(${nm}_delays[f]);`);
    L.push(' *   }');
  }else if(c.pack==='vertical'){
    L.push(' * Raw SSD1306 page buffer (e.g. SSD1306Ascii / custom driver):');
    L.push(` *   for(uint8_t f=0; f<${U}_FRAME_COUNT; f++){`);
    L.push(` *     memcpy_P(displayBuffer, ${fp}, ${U}_FRAME_SIZE);`);
    L.push(' *     displayUpdate();');
    L.push(` *     delay(${nm}_delays[f]);`);
    L.push(' *   }');
  }else if(c.pack==='horizontal_lsb'){
    L.push(' * U8g2:');
    L.push(` *   for(uint8_t f=0; f<${U}_FRAME_COUNT; f++){`);
    L.push(' *     u8g2.clearBuffer();');
    L.push(` *     u8g2.drawXBMP(0,0,${U}_WIDTH,${U}_HEIGHT,${fp});`);
    L.push(' *     u8g2.sendBuffer();');
    L.push(` *     delay(${nm}_delays[f]);`);
    L.push(' *   }');
  }else{
    L.push(' * Adafruit_SSD1306 / Adafruit_GFX:');
    L.push(` *   for(uint8_t f=0; f<${U}_FRAME_COUNT; f++){`);
    L.push(' *     display.clearDisplay();');
    L.push(` *     display.drawBitmap(0,0,${fp},${U}_WIDTH,${U}_HEIGHT,SSD1306_WHITE);`);
    L.push(' *     display.display();');
    L.push(` *     delay(${nm}_delays[f]);`);
    L.push(' *   }');
  }
  L.push(' */','',`#endif // ${U}_H`,'');
  return L.join('\n');
}

const SHOW_LIMIT=60000;
function showCode(code){
  const trunc=code.length>SHOW_LIMIT;
  $('code').textContent=trunc?code.slice(0,SHOW_LIMIT)+'\n\n// ... output truncated in the preview only ...\n// "Copy" and "Save .h" always use the COMPLETE file.':code;
  $('codeInfo').textContent=`// ${(code.length/1024).toFixed(0)} KB of source · ${result.frames.length} frames`;
  ['saveBtn','copyBtn'].forEach(i=>$(i).disabled=false);
  const tn=$('truncNote');
  if(trunc){tn.hidden=false;tn.className='notice info show';tn.innerHTML='<i class="bi bi-info-circle"></i> Large output: the preview shows only the beginning. Use <b>Save .h</b> or <b>Copy</b> to get the full file.';}
  else tn.hidden=true;
}
$('saveBtn').onclick=()=>{
  if(!fullCode)return;
  const a=document.createElement('a');
  a.href=URL.createObjectURL(new Blob([fullCode],{type:'text/plain'}));
  a.download=(result.c.name||'video')+'.h';document.body.appendChild(a);a.click();a.remove();
  setTimeout(()=>URL.revokeObjectURL(a.href),1000);toast('Saved '+a.download);
};
$('copyBtn').onclick=async()=>{
  try{await navigator.clipboard.writeText(fullCode);}
  catch(e){const t=document.createElement('textarea');t.value=fullCode;document.body.appendChild(t);t.select();document.execCommand('copy');t.remove();}
  toast('Full code copied ✔');
};
$('clearBtn').onclick=clearResult;

/* ------------ result preview ------------ */
function showResult(){
  const c=result.c,N=result.frames.length,fb=frameBytes(c);
  $('resultStage').hidden=false;
  $('sSize').textContent=fmtBytes(N*fb);
  $('resEst').innerHTML=`<div><b>${N}</b>frames</div><div><b>${c.w}×${c.h}</b>${c.mode==='mono'?'1-bit':'RGB565'}</div><div><b>${fmtBytes(fb)}</b>per frame</div><div><b>${fmtBytes(N*fb)}</b>total</div>`;
  playIdx=0;playing=true;$('pPlay').innerHTML='<i class="bi bi-pause-fill"></i> Pause';
  drawResultFrame();loopPlay();
}
function drawResultFrame(){
  if(!result)return;const c=result.c,cv=$('outCanvas'),f=result.preview[playIdx];
  if(c.mode==='mono')paintMono(cv,f,c.w,c.h,$('oledTint').checked);else paintRGB(cv,f,c.w,c.h);
  setZoom(cv);$('pCnt').textContent=`Frame ${playIdx+1}/${result.frames.length}`;
}
function loopPlay(){
  clearTimeout(playTimer);
  if(!playing||!result)return;
  playTimer=setTimeout(()=>{playIdx=(playIdx+1)%result.frames.length;drawResultFrame();loopPlay();},result.delays[playIdx]||100);
}
function stopPlayback(){clearTimeout(playTimer);}
$('pPlay').onclick=()=>{playing=!playing;$('pPlay').innerHTML=playing?'<i class="bi bi-pause-fill"></i> Pause':'<i class="bi bi-play-fill"></i> Play';if(playing)loopPlay();else stopPlayback();};
$('pPrev').onclick=()=>{if(!result)return;playing=false;stopPlayback();$('pPlay').innerHTML='<i class="bi bi-play-fill"></i> Play';playIdx=(playIdx-1+result.frames.length)%result.frames.length;drawResultFrame();};
$('pNext').onclick=()=>{if(!result)return;playing=false;stopPlayback();$('pPlay').innerHTML='<i class="bi bi-play-fill"></i> Play';playIdx=(playIdx+1)%result.frames.length;drawResultFrame();};
$('zoom').oninput=()=>{$('zmVal').textContent=$('zoom').value;if(result)drawResultFrame();};
$('oledTint').addEventListener('change',()=>{if(result)drawResultFrame();});

function clearResult(){
  stopPlayback();result=null;fullCode='';
  $('resultStage').hidden=true;$('truncNote').hidden=true;
  $('code').textContent='// 1. Load a video\n// 2. Pick your display size, trim and FPS\n// 3. Click "Convert Video to C/C++ Array"\n//\n// Output is ready for Arduino, ESP32, ESP8266, STM32, Pico.';
  $('codeInfo').textContent='// nothing generated yet';
  ['saveBtn','copyBtn'].forEach(i=>$(i).disabled=true);
}

refreshAll();
</script>
</body>
</html>
