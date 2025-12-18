<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>CBT COUPLE STUDY</title>

<style>
/* CSS DASAR */
*{margin:0;padding:0;box-sizing:border-box;user-select:none}
body{font-family:Arial,Helvetica,sans-serif;background:#f3f4f6;overflow:hidden}

:root{
  --ungu:#6a1b9a;
  --ungu-muda:#ede7f6;
  --kuning:#fbc02d;
  --hijau:#4caf50;
}

#main-container > div {
    position: fixed;
    top: 0; left: 0;
    width: 100vw; height: 100vh;
    background: #f3f4f6;
    z-index: 9999;
    overflow-y: auto;
}

/* LOGIN & MODAL PANEL */
#login, #modal{display:flex;align-items:center;justify-content:center}
.login-box, .modal-box{background:#fff;width:90%;max-width:380px;padding:30px;border-radius:12px;box-shadow:0 15px 40px rgba(0,0,0,.15);text-align:center}
.login-box h1, .modal-box h3{color:var(--ungu);margin-bottom:15px;font-size:24px}

.identitas-box {margin-bottom: 10px; display: flex; flex-direction: column; gap: 5px;}
.identitas-box input, .identitas-box select {
    width: 100%; padding: 12px; border-radius: 8px; border: 2px solid var(--ungu);
    outline: none; font-weight: bold; color: var(--ungu); background: #fff;
    text-align: left;
}
#namaInput { text-transform: uppercase; }
.identitas-box input::placeholder { color: #b39ddb; opacity: 1; text-transform: none; }

.token-display-box {background: var(--ungu-muda); padding: 15px; border-radius: 8px; border: 1px dashed var(--ungu); margin-bottom: 20px;}
.token-display-box p {font-size: 12px; color: #555; margin-bottom: 8px; font-weight: bold;}
.token-val {font-family: monospace; font-size: 18px; color: var(--ungu); letter-spacing: 1px; display: block; margin-bottom: 12px; font-weight: 900;}
.token-tools {display: flex; justify-content: center; gap: 8px;}
.btn-tool {background: var(--ungu); color: white; border: none; padding: 6px 12px; font-size: 11px; border-radius: 5px; cursor: pointer; font-weight: bold;}

.input-container {position: relative; width: 100%; margin-bottom: 5px;}
.token-in{width:100%;padding:14px;padding-right:110px; border-radius:8px;border:2px solid var(--ungu);outline:none; text-align:center; font-weight: bold; background: #fafafa !important;}
.token-in.caps {text-transform: uppercase;}

.input-actions {position: absolute; right: 8px; top: 50%; transform: translateY(-50%); display: flex; gap: 5px; z-index: 10;}
.btn-action {cursor: pointer; color: var(--ungu); font-size: 10px; font-weight: bold; background: var(--ungu-muda); padding: 5px 7px; border-radius: 4px; border: 1px solid var(--ungu);}

.error-text {color: #d32f2f; font-size: 12px; font-weight: bold; margin-bottom: 10px; display: none; text-align: center;}
.info-text {color: var(--hijau); font-size: 11px; font-weight: bold; margin-top: 5px; display: none;}

.btn-ungu{width:100%;padding:14px;border:none;border-radius:8px;background:var(--ungu);color:#fff;font-weight:bold;cursor:pointer;margin-top:5px}
.btn-ungu:disabled{background:#ccc; cursor:not-allowed}

/* UI UJIAN */
#ujian{display:none}
.header{background:#fff;padding:15px;display:flex;justify-content:space-between;border-bottom:1px solid #ddd;position:sticky;top:0;z-index:10}
.timer{color:var(--ungu);font-weight:bold} 
.list-btn{color:var(--ungu);font-weight:bold;cursor:pointer}
.content{padding:20px 20px 120px}
.soal-box{background:#fff;padding:25px;border-radius:12px;box-shadow:0 4px 12px rgba(0,0,0,.1);min-height:50vh}
.teks-soal-wrapper {margin:15px 0; font-size:17px; line-height:1.5; color: #333;}
.opsi label{display:block;border:1px solid #ccc;border-radius:8px;padding:14px;margin-top:10px;cursor:pointer}
.opsi span{display:block;padding:5px;border-radius:6px}
.opsi span.selected{background:var(--ungu-muda);font-weight:bold;border:1px solid var(--ungu)}
.opsi span.ragu{background:var(--kuning);font-weight:bold}
.nav{position:fixed;bottom:0;left:0;right:0;background:#fff;border-top:1px solid #ddd;padding:15px;display:none;justify-content:center;gap:20px;z-index:10000}
.nav button{padding:12px 25px;border:none;border-radius:8px;font-weight:bold;cursor:pointer;font-size:18px}
.prev,.next{background:var(--ungu);color:#fff}
.raguBtn{background:var(--kuning);font-size:14px !important}

/* SIDEBAR DAFTAR SOAL */
#daftarSoal{position:fixed;top:0;left:-300px;width:300px;height:100%;background:#fff;box-shadow:5px 0 15px rgba(0,0,0,.2);z-index:10001; transition:.3s; display: flex; flex-direction: column;}
.ds-header {padding: 20px; background: var(--ungu); color: white; position: relative;}
.ds-header h3 {font-size: 16px; margin-bottom: 5px;}
.ds-header p {font-size: 12px; opacity: 0.9;}
.ds-close {position: absolute; top: 15px; right: 15px; font-size: 24px; cursor: pointer; font-weight: bold;}
.ds-body {flex: 1; padding: 20px; overflow-y: auto; display: grid; grid-template-columns: repeat(5, 1fr); gap: 8px; align-content: start;}

#daftarSoal button{width:100%; aspect-ratio: 1/1; border:none; border-radius:8px; font-weight:bold; cursor:pointer; font-size: 14px;}
.belum{background:#e0e0e0; color: #757575;}
.terjawab{background:var(--ungu); color:#fff}
.raguSoal{background:var(--kuning); color: #000;}

#modal{position:fixed;inset:0;background:rgba(0,0,0,0.8);display:none;z-index:20000}
#hasil{display:none;padding:20px 15px;background:#f3f4f6}
.skor-box{background:var(--ungu);color:#fff;padding:30px;border-radius:12px;text-align:center;margin-bottom:25px}
.skor-box h1{font-size: 54px; margin: 10px 0;}
.table-title{color:var(--ungu); font-weight:bold; margin: 25px 0 10px; border-left: 5px solid var(--ungu); padding-left: 10px; font-size: 18px;}
table{width:100%; border-collapse:collapse; background:#fff; margin-bottom:20px; border-radius:8px; overflow:hidden;}
th{background:var(--ungu); color: white; padding:14px; text-align:left}
td{padding:14px; border:1px solid #eee; font-size:13px;}
.txt-green{color: #2e7d32; font-weight:bold}
.txt-red{color: #d32f2f; font-weight:bold}
.action-btns{display:flex; gap:10px; margin-top:30px; padding-bottom:60px}
.btn-coba{background:var(--kuning); color:#000; flex:1; padding:16px; border-radius:8px; border:none; font-weight:bold; cursor:pointer}
.btn-menu{background:var(--ungu); color:#fff; flex:1; padding:16px; border-radius:8px; border:none; font-weight:bold; cursor:pointer; text-decoration:none; text-align:center}
.check-container {display: flex; align-items: center; justify-content: center; gap: 10px; margin: 15px 0; font-size: 14px; font-weight: bold; color: var(--ungu);}
.missed-grid {display: grid; grid-template-columns: repeat(5, 1fr); gap: 8px; margin: 15px 0;}
.btn-missed {padding: 10px; background: #d32f2f; color: white; border: none; border-radius: 6px; font-weight: bold; cursor: pointer;}
</style>
</head>
<body oncontextmenu="return false" onselectstart="return false">

<div id="main-container">
    <div id="login">
      <div class="login-box">
        <h1>CBT COUPLE STUDY</h1> 
        <div class="identitas-box">
            <input type="text" id="namaInput" placeholder="NAMA LENGKAP" oninput="this.value = this.value.toUpperCase(); resetError('errorNama')">
            <div id="errorNama" class="error-text">Masukkan terlebih dahulu nama</div>
            <select id="kelasInput" onchange="resetError('errorKelas')">
                <option value="" disabled selected>Pilih kelas</option>
                <option value="10">Kelas 10</option>
                <option value="11">Kelas 11</option>
                <option value="12">Kelas 12</option>
            </select>
            <div id="errorKelas" class="error-text">Masukkan terlebih dahulu kelas</div>
        </div>
        <div class="token-display-box">
            <p>Token masuk</p>
            <b class="token-val">Memuat...</b>
            <div class="token-tools">
                <button class="btn-tool" onclick="generateRandomToken()">Ganti token</button>
                <button class="btn-tool" style="background:var(--hijau)" onclick="salinToken('infoSalinLogin')">Salin</button>
            </div>
            <div id="infoSalinLogin" class="info-text">Token berhasil disalin</div>
        </div>
        <div class="input-container">
            <input type="password" id="loginInput" class="token-in caps" placeholder="Klik Tempel" readonly>
            <div class="input-actions">
                <span class="btn-action" onclick="tempelToken('loginInput', 'errorLogin')">Tempel</span>
                <span class="btn-action" onclick="toggleViewToken(this)">Lihat</span>
            </div>
        </div>
        <div id="errorLogin" class="error-text">Token salah!</div>
        <button class="btn-ungu" onclick="MulaiUjian()">Mulai ujian</button>
      </div>
    </div>

    <div id="ujian">
      <div class="header">
        <span class="list-btn" onclick="ToggleList()">≡ Daftar Soal</span>
        <span class="timer" id="timer">01:30:00</span> 
      </div>
      <div class="content">
        <div class="soal-box">
          <div class="teks-soal-wrapper" id="teksSoal"></div>
          <div class="opsi" id="opsi"></div>
        </div>
      </div>
    </div>

    <div id="hasil"></div>
</div>

<div class="nav" id="nav">
  <button class="prev" onclick="Prev()"> < </button>
  <button class="raguBtn" onclick="TandaiRagu()">Ragu-ragu</button>
  <button class="next" id="btnNext" onclick="Next()"> > </button>
</div>

<div id="daftarSoal">
  <div class="ds-header">
      <span class="ds-close" onclick="ToggleList()">✕</span>
      <h3 id="ds-nama">NAMA SISWA</h3>
      <p id="ds-kelas">KELAS</p>
  </div>
  <div class="ds-body" id="listSoal"></div>
</div>

<div id="modal">
  <div class="modal-box" id="modalBox"></div>
</div>

<script>
const soal=[
 {q:"Ibukota Indonesia Adalah…",o:["Jakarta","Bandung","Surabaya","Yogyakarta","Medan"],a:0},
 {q:"Presiden Pertama Indonesia Adalah…",o:["Soeharto","Joko Widodo","Sukarno","Habibie","Megawati"],a:2},
 {q:"Proses Fotosintesis Pada Tumbuhan Terjadi Di…",o:["Akar","Batang","Daun","Bunga","Buah"],a:2},
 {q:"Unsur Gas Yang Paling Banyak Di Atmosfer Bumi Adalah…",o:["Oksigen","Hidrogen","Karbon Dioksida","Nitrogen","Argon"],a:3},
 {q:"Planet Terdekat Dengan Matahari Adalah…",o:["Bumi","Mars","Venus","Merkurius","Jupiter"],a:3},
 {q:"Lambang Negara Indonesia Adalah…",o:["Burung Garuda","Singa","Elang","Rajawali","Merak"],a:0},
 {q:"Sungai Terpanjang Di Dunia Adalah…",o:["Sungai Nil","Sungai Amazon","Sungai Mississippi","Sungai Yangtze","Sungai Mekong"],a:0},
 {q:"Zat Yang Membuat Kulit Manusia Gelap Adalah…",o:["Melanin","Hemoglobin","Klorofil","Karoten","Xantofil"],a:1},
 {q:"Organ Utama Sistem Peredaran Darah Adalah…",o:["Paru-Paru","Ginjal","Jantung","Hati","Lambung"],a:2},
 {q:"Hari Kemerdekaan Indonesia Diperingati Pada…",o:["17 Agustus 1945","20 Mei 1908","1 Juni 1945","10 November 1945","2 September 1945"],a:0},
 {q:"Benua Terkecil Di Dunia Adalah…",o:["Asia","Afrika","Eropa","Australia","Amerika"],a:3},
 {q:"Alat Musik Tradisional Dari Jawa Barat Yang Terbuat Dari Bambu Adalah…",o:["Angklung","Sasando","Gamelan","Kolintang","Kecapi"],a:0},
 {q:"Presiden RI Saat Ini (2025) Adalah…",o:["Susilo Bambang Yudhoyono","Megawati Soekarnoputri","Joko Widodo","Prabowo Subianto","Basuki Tjahaja Purnama"],a:2},
 {q:"Sifat Air Yang Membuatnya Mampu Menopang Serangga Kecil Di Permukaan Adalah…",o:["Viskositas","Tegangan Permukaan","Kapilaritas","Koagulasi","Osmosis"],a:1},
 {q:"Bahasa Resmi PBB Adalah…",o:["Inggris, Prancis, Spanyol, Rusia, Cina, Arab","Inggris, Jerman, Jepang, Cina","Inggris, Prancis, Jerman, Arab","Inggris, Cina, India, Arab","Inggris, Spanyol, Rusia, Jepang"],a:0},
 {q:"Senyawa Yang Termasuk Karbohidrat Adalah…",o:["Glukosa","Asam Amino","Asam Lemak","Vitamin C","Protein"],a:0},
 {q:"Hukum Newton Pertama Dikenal Sebagai Hukum…",o:["Gravitasi","Aksi-Reaksi","Inersia","Momentum","Energi"],a:2},
 {q:"Negara Dengan Jumlah Penduduk Terbanyak Di Dunia Adalah…",o:["Amerika Serikat","India","China","Indonesia","Rusia"],a:2},
 {q:"Pulau Terbesar Di Indonesia Adalah…",o:["Sumatra","Kalimantan","Papua","Sulawesi","Jawa"],a:2},
 {q:"Unsur Yang Paling Ringan Adalah…",o:["Helium","Hidrogen","Oksigen","Nitrogen","Karbon"],a:1},
 {q:"Alat Yang Digunakan Untuk Mengukur Suhu Adalah…",o:["Barometer","Termometer","Anemometer","Hygrometer","Voltmeter"],a:1},
 {q:"Raja Majapahit Terkenal Dengan Sebutan…",o:["Raden Wijaya","Hayam Wuruk","Gajah Mada","Airlangga","Diponegoro"],a:1},
 {q:"Salah Satu Fungsi Hati Adalah…",o:["Menyaring Darah Dan Menghasilkan Empedu","Menghasilkan Insulin","Menyerap Nutrisi Dari Makanan","Membentuk Sel Darah Putih","Mengontrol Pernapasan"],a:0},
 {q: "Matahari Termasuk Jenis Bintang…",o:["Neutron","Raksasa Merah","Katai Putih","Katai Kuning","Supernova"],a:3},
 {q:"Negara Dengan Julukan Negeri Matahari Terbit Adalah…",o:["China","Korea Selatan","Jepang","Thailand","India"],a:2}
];

let activeToken = "", lastCopiedToken = "", i=0, jawaban=[], ragu=[], w=5400, timerInterval, cheatCount=0, cheatLog=[], isCheating=false, shuffledSoal=[], userName = "", userClass = "", startTimeExam = null; 

function create7CharToken() {
    const L = "ABCDEFGHIJKLMNOPQRSTUVWXYZ", N = "0123456789";
    let res = "";
    for(let j=0; j<7; j++) res += (j % 2 === 0) ? L.charAt(Math.floor(Math.random()*L.length)) : N.charAt(Math.floor(Math.random()*N.length));
    return res;
}

function generateRandomToken() {
    activeToken = "CBT-CS-" + create7CharToken();
    document.querySelectorAll('.token-val').forEach(el => el.innerText = activeToken);
}

function salinToken(infoId) {
    lastCopiedToken = activeToken;
    navigator.clipboard.writeText(activeToken).then(() => {
        const el = document.getElementById(infoId);
        if(el) { el.style.display = "block"; setTimeout(() => el.style.display = "none", 2000); }
    });
}

function tempelToken(inputId, errorId) {
    if(!lastCopiedToken) { showToast(errorId, "Salin terlebih dahulu token", "#d32f2f"); return; }
    document.getElementById(inputId).value = lastCopiedToken;
    resetError(errorId);
}

function showToast(id, msg, color) {
    const el = document.getElementById(id);
    if(el) { el.innerText = msg; el.style.color = color; el.style.display = "block"; setTimeout(() => el.style.display = "none", 3000); }
}

function resetError(id) { const err = document.getElementById(id); if(err) err.style.display = "none"; }
function toggleViewToken(btn) {
    const inp = btn.parentElement.previousElementSibling;
    inp.type = (inp.type === "password") ? "text" : "password";
    btn.innerText = (inp.type === "password") ? "Lihat" : "Tutup";
}

function MulaiUjian(){
    const inputToken = document.getElementById('loginInput'), nameIn = document.getElementById('namaInput').value, classIn = document.getElementById('kelasInput').value;
    if(!nameIn) { document.getElementById('errorNama').style.display = "block"; return; }
    if(!classIn) { document.getElementById('errorKelas').style.display = "block"; return; }
    if(inputToken.value.trim().toUpperCase() === activeToken){
        userName = nameIn; userClass = "KELAS " + classIn; startTimeExam = new Date();
        document.getElementById('ds-nama').innerText = userName;
        document.getElementById('ds-kelas').innerText = userClass;
        shuffledSoal = [...soal].sort(() => Math.random() - 0.5);
        document.getElementById('login').style.display="none";
        document.getElementById('ujian').style.display="block";
        document.getElementById('nav').style.display="flex";
        Render(); Daftar(); StartTimer();
        window.addEventListener('blur', () => DetectCheat('Pindah halaman'));
    } else {
        document.getElementById('errorLogin').style.display = "block";
        generateRandomToken();
    }
}

function StartTimer(){
    timerInterval = setInterval(() => {
        w--;
        let h=Math.floor(w/3600).toString().padStart(2,'0'), m=Math.floor((w%3600)/60).toString().padStart(2,'0'), s=(w%60).toString().padStart(2,'0');
        document.getElementById('timer').innerText = `${h}:${m}:${s}`;
        if(w<=0) Selesai(true);
    }, 1000);
}

function Render(){
    const s = shuffledSoal[i];
    document.getElementById('teksSoal').innerHTML = `<b>${i+1}.</b> ${s.q}`;
    const ob = document.getElementById('opsi'); ob.innerHTML = "";
    s.o.forEach((txt, idx) => {
        let stl = (jawaban[i] === idx) ? (ragu[i] ? "ragu" : "selected") : "";
        ob.innerHTML += `<label onclick="Pilih(${idx})"><span class="${stl}">${txt}</span></label>`;
    });
    const btnNext = document.getElementById('btnNext');
    if(i === shuffledSoal.length - 1) { btnNext.innerText = "Kirim"; btnNext.style.background = "var(--hijau)"; }
    else { btnNext.innerText = " > "; btnNext.style.background = "var(--ungu)"; }
}

function Pilih(idx){ jawaban[i]=idx; ragu[i]=false; Render(); Daftar(); }
function TandaiRagu(){ if(jawaban[i]!=null){ ragu[i]=!ragu[i]; Render(); Daftar(); }}
function Next(){ if(i === shuffledSoal.length-1) CekSelesai(); else { i++; Render(); }}
function Prev(){ if(i > 0){ i--; Render(); }}

function Daftar(){
    const l = document.getElementById('listSoal'); l.innerHTML = "";
    shuffledSoal.forEach((_, n) => {
        let c = (jawaban[n] != null) ? (ragu[n] ? "raguSoal" : "terjawab") : "belum";
        l.innerHTML += `<button class="${c}" onclick="Goto(${n})">${n+1}</button>`;
    });
}
function ToggleList(){ const d = document.getElementById('daftarSoal'); d.style.left = d.style.left === "0px" ? "-300px" : "0px"; }
function Goto(n){ i=n; Render(); ToggleList(); }

function CekSelesai(){
    let missed = []; shuffledSoal.forEach((_, n) => { if(jawaban[n] == null) missed.push(n+1); });
    const box = document.getElementById('modalBox'); document.getElementById('modal').style.display = "flex";
    if(missed.length > 0){
        let gridHtml = missed.map(no => `<button class="btn-missed" onclick="GotoM(${no-1})">${no}</button>`).join("");
        box.innerHTML = `<h3 style="color:#d32f2f">Penyerahan ditolak</h3><p style="font-size:14px; color:#555; margin-bottom:10px">Lengkapi seluruh jawaban terlebih dahulu.</p><div class="missed-grid">${gridHtml}</div><button class="btn-ungu" onclick="document.getElementById('modal').style.display='none'">Kembali berusaha</button>`;
    } else {
        generateRandomToken();
        box.innerHTML = `
            <h3>Konfirmasi penyerahan</h3>
            <p style="font-size:13px; color:#555; margin-bottom:15px">Gunakan token untuk memverifikasi pengiriman.</p>
            <div class="token-display-box">
                <p>Token verifikasi kirim</p>
                <b class="token-val">${activeToken}</b>
                <div class="token-tools">
                    <button class="btn-tool" onclick="generateRandomToken(); CekSelesai();">Ganti</button>
                    <button class="btn-tool" style="background:var(--hijau)" onclick="salinToken('infoSalinFinal')">Salin</button>
                </div>
                <div id="infoSalinFinal" class="info-text">Token berhasil disalin</div>
            </div>
            <div class="input-container">
                <input type="password" id="finalTokenInput" class="token-in caps" placeholder="Klik Tempel" readonly>
                <div class="input-actions">
                    <span class="btn-action" onclick="tempelToken('finalTokenInput', 'errorFinal')">Tempel</span>
                    <span class="btn-action" onclick="toggleViewToken(this)">Lihat</span>
                </div>
            </div>
            <div id="errorFinal" class="error-text">Token verifikasi salah!</div>
            <label class="check-container"><input type="checkbox" id="yakinCheck" onchange="toggleSubmitBtn()"> Saya yakin dengan jawaban saya</label>
            <button class="btn-ungu" id="submitFinal" disabled onclick="VerifyFinalSubmission()">Kirim jawaban</button>
            <p id="timeWarning" style="color:#d32f2f; font-size:12px; font-weight:bold; margin-top:5px; display:none;"></p>
            <button class="btn-ungu" onclick="document.getElementById('modal').style.display='none'">Batal</button>`;
        checkExamDuration();
    }
}

function checkExamDuration() {
    const diff = Math.floor((new Date() - startTimeExam) / 1000), limit = 180, btn = document.getElementById('submitFinal'), warning = document.getElementById('timeWarning');
    if (diff < limit) {
        btn.disabled = true;
        if(warning) { warning.style.display = "block"; warning.innerText = `Minimal pengerjaan 3 menit. Tunggu ${limit - diff} detik lagi.`; }
        setTimeout(checkExamDuration, 1000);
    } else { if(warning) warning.style.display = "none"; toggleSubmitBtn(); }
}

function toggleSubmitBtn() {
    const btn = document.getElementById('submitFinal'), chk = document.getElementById('yakinCheck'), diff = Math.floor((new Date() - startTimeExam) / 1000);
    if(btn && chk) btn.disabled = (!chk.checked || diff < 180);
}

function VerifyFinalSubmission() {
    if(document.getElementById('finalTokenInput').value.trim().toUpperCase() === activeToken) Selesai();
    else { document.getElementById('errorFinal').style.display = "block"; generateRandomToken(); CekSelesai(); }
}

function DetectCheat(tipe){
    if(isCheating || document.getElementById('ujian').style.display !== 'block') return;
    isCheating = true; clearInterval(timerInterval); cheatCount++;
    cheatLog.push({waktu: document.getElementById('timer').innerText, ket: tipe});
    if(cheatCount >= 5) { Selesai(true); return; }
    generateRandomToken();
    const box = document.getElementById('modalBox'); document.getElementById('modal').style.display = "flex";
    box.innerHTML = `
        <h3>Akun anda beku</h3><p style="font-size:13px; color:#d32f2f; margin-bottom:15px">Pelanggaran terdeteksi: ${cheatCount}/5</p>
        <div class="token-display-box">
            <p>Token pembuka blokir</p><b class="token-val">${activeToken}</b>
            <div class="token-tools">
                <button class="btn-tool" onclick="generateRandomToken(); DetectCheat('${tipe}')">Ganti</button>
                <button class="btn-tool" style="background:var(--hijau)" onclick="salinToken('infoSalinUnlock')">Salin</button>
            </div>
            <div id="infoSalinUnlock" class="info-text">Token berhasil disalin</div>
        </div>
        <div class="input-container">
            <input type="password" id="unlockInput" class="token-in caps" placeholder="Klik Tempel" readonly>
            <div class="input-actions"><span class="btn-action" onclick="tempelToken('unlockInput', 'errorUnlock')">Tempel</span><span class="btn-action" onclick="toggleViewToken(this)">Lihat</span></div>
        </div>
        <div id="errorUnlock" class="error-text">Token salah!</div><button class="btn-ungu" onclick="VerifyUnlock()">Buka akun</button>`;
}

function VerifyUnlock(){
    if(document.getElementById('unlockInput').value.trim().toUpperCase() === activeToken){ isCheating = false; document.getElementById('modal').style.display = "none"; StartTimer(); }
    else { document.getElementById('errorUnlock').style.display = "block"; generateRandomToken(); document.querySelector('#modalBox .token-val').innerText = activeToken; }
}

function GotoM(idx){ i = idx; Render(); document.getElementById('modal').style.display = 'none'; }

function Selesai(forced = false){
    clearInterval(timerInterval);
    let benar = 0; shuffledSoal.forEach((s, n) => { if(jawaban[n] === s.a) benar++; });
    let skorMurni = Math.round((benar / soal.length) * 100), penalti = cheatCount * 3, skorAkhir = Math.max(0, skorMurni - penalti);
    document.getElementById('ujian').style.display="none"; document.getElementById('nav').style.display="none"; document.getElementById('modal').style.display="none";
    let html = `<div class="skor-box"><h2>${userName} (${userClass})</h2><p>Hasil evaluasi akhir</p><h1>${skorAkhir}</h1><p style="font-size:12px">Skor Murni: ${skorMurni} | Penalti: -${penalti}</p></div><div class="table-title">Pembahasan</div><table><thead><tr><th>Soal</th><th>Jawaban</th><th>Kunci</th></tr></thead><tbody>`;
    shuffledSoal.forEach((s, n) => {
        let isB = jawaban[n] === s.a;
        html += `<tr><td><b>${n+1}.</b> ${s.q}</td><td class="${isB?'txt-green':'txt-red'}">${jawaban[n] != null ? s.o[jawaban[n]] : "-"}</td><td class="txt-green">${s.o[s.a]}</td></tr>`;
    });
    html += `</tbody></table>`;
    if(cheatLog.length > 0){
        html += `<div class="table-title">Riwayat Pelanggaran</div><table><thead><tr><th>Waktu</th><th>Keterangan</th></tr></thead><tbody>`;
        cheatLog.forEach(log => { html += `<tr><td>${log.waktu}</td><td>${log.ket}</td></tr>`; });
        html += `</tbody></table>`;
    }
    html += `<div class="action-btns"><button class="btn-coba" onclick="location.reload()">Coba lagi</button><a href="https://alamat-blogger-anda.blogspot.com" class="btn-menu">Menu Utama</a></div>`;
    document.getElementById('hasil').innerHTML = html; document.getElementById('hasil').style.display = "block";
}

window.addEventListener('DOMContentLoaded', generateRandomToken);
</script>
</body>
</html>
