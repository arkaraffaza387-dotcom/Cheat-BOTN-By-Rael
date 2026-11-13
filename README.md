<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Battle of the Nations</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
html,body{width:100%;height:100%;overflow:hidden;background:#000}
#game{position:absolute;inset:0;width:100%;height:100%;border:none;z-index:1}
#bt{position:fixed;bottom:20px;right:20px;z-index:99999;width:60px;height:60px;border-radius:50%;background:linear-gradient(135deg,#da3633,#f0883e);border:2px solid #fff3;color:#fff;font-size:26px;cursor:pointer;box-shadow:0 4px 20px #000a;-webkit-tap-highlight-color:transparent}
#bt:active{transform:scale(.95)}
#bp{position:fixed;bottom:90px;right:10px;left:10px;z-index:99999;max-height:75vh;background:#0a0e14;border:1px solid #30363d;border-radius:12px;color:#e6edf3;font-family:system-ui,sans-serif;font-size:13px;display:none;flex-direction:column;overflow:hidden;box-shadow:0 8px 40px #000c}
#bp.open{display:flex}
#bh{padding:12px 14px;background:linear-gradient(90deg,#da3633,#9e2f2c);display:flex;justify-content:space-between;align-items:center}
#bh h3{font-size:13px;color:#fff}
#bx{background:none;border:none;color:#fff;font-size:22px;cursor:pointer}
#bb{padding:10px;overflow-y:auto;-webkit-overflow-scrolling:touch}
.bs{margin-bottom:10px;background:#161b22;border:1px solid #21262d;border-radius:8px;padding:8px 10px}
.bs h4{font-size:10px;text-transform:uppercase;color:#8b949e;margin-bottom:6px;letter-spacing:.5px}
.br{display:flex;gap:6px;margin-bottom:6px}
.bb{flex:1;padding:10px 8px;border-radius:6px;border:1px solid #30363d;background:#21262d;color:#e6edf3;font-size:12px;cursor:pointer;font-family:inherit;-webkit-tap-highlight-color:transparent}
.bb:active{opacity:.7}
.bb.p{background:#238636;border-color:#2ea043}
.bb.d{background:#da3633;border-color:#f85149}
.bb.w{background:#9e6a03;border-color:#d29922}
.bi{width:100%;background:#0d1117;border:1px solid #30363d;color:#e6edf3;border-radius:6px;padding:8px 10px;font-size:13px;margin-bottom:6px}
.bl{background:#000;border:1px solid #21262d;border-radius:6px;height:100px;overflow-y:auto;padding:8px;font-family:monospace;font-size:10px;line-height:1.5;color:#8b949e}
.bl .ok{color:#3fb950}.bl .err{color:#f85149}.bl .info{color:#58a6ff}.bl .warn{color:#d29922}
.cb{font-size:9px;padding:2px 6px;border-radius:10px;background:#484f58;color:#fff;margin-left:4px;text-transform:uppercase}
.cb.on{background:#238636}
</style>
</head>
<body>

<iframe id="game" src="./game.html" sandbox="allow-scripts allow-same-origin allow-forms allow-modals allow-popups allow-pointer-lock"></iframe>

<button id="bt">⚡</button>

<div id="bp">
  <div id="bh"><h3>⚡ BotN Cheat</h3><button id="bx">×</button></div>
  <div id="bb">
    <div class="bs"><h4>Auto Win <span id="awB" class="cb">off</span></h4>
      <div class="br"><button class="bb p" onclick="bAW(1)">▶ Start</button><button class="bb d" onclick="bAW(0)">■ Stop</button></div></div>
    <div class="bs"><h4>God Mode <span id="gmB" class="cb">off</span></h4>
      <div class="br"><button class="bb p" onclick="bGM(1)">Enable</button><button class="bb d" onclick="bGM(0)">Disable</button></div></div>
    <div class="bs"><h4>Boost Resources</h4>
      <div class="br"><button class="bb p" onclick="bBoostAll()">Boost All</button><button class="bb w" onclick="bBoostN('gold')">Gold</button></div>
      <div class="br"><button class="bb w" onclick="bBoostN('gem')">Gems</button><button class="bb w" onclick="bBoostN('level')">Level</button></div></div>
    <div class="bs"><h4>Auto Clicker <span id="acB" class="cb">off</span></h4>
      <div class="br"><button class="bb p" onclick="bAC(1)">▶ Start</button><button class="bb d" onclick="bAC(0)">■ Stop</button></div></div>
    <div class="bs"><h4>Ban Lokal</h4>
      <input class="bi" id="banT" placeholder="nama akun">
      <div class="br"><button class="bb d" onclick="bBan()">🚫 Ban</button><button class="bb w" onclick="bUnban()">♻ Unban</button></div></div>
    <div class="bs"><h4>Recon</h4>
      <div class="br"><button class="bb" onclick="bScan()">Scan Storage</button></div></div>
    <div class="bs"><h4>Log</h4><div class="bl" id="blg"></div></div>
  </div>
</div>

<script>
(function(){
var frame=document.getElementById('game'),btn=document.getElementById('bt'),panel=document.getElementById('bp'),logEl=document.getElementById('blg');
btn.onclick=function(){panel.classList.toggle('open');btn.textContent=panel.classList.contains('open')?'×':'⚡'};
document.getElementById('bx').onclick=function(){panel.classList.remove('open');btn.textContent='⚡'};
function L(m,t){var d=document.createElement('div');d.className=t||'info';d.textContent='['+new Date().toLocaleTimeString('id-ID',{hour12:false})+'] '+m;logEl.appendChild(d);logEl.scrollTop=logEl.scrollHeight}
function bdg(id,on){var e=document.getElementById(id);e.textContent=on?'on':'off';e.className='cb'+(on?' on':'')}
function LS(){try{return frame.contentWindow.localStorage}catch(e){return null}}
function DOC(){try{return frame.contentDocument}catch(e){return null}}
var CK=['gold','coin','money','cash','gem','diamond','level','exp','xp','power','troop','soldier','army','hp','health','resource','food','wood','iron','attack','defense'];
function walk(o,cb){if(!o||typeof o!=='object')return;for(var f in o){cb(o,f);if(typeof o[f]==='object')walk(o[f],cb)}}
var awT,acT,gmT;

window.bAW=function(on){if(!on){if(awT)clearInterval(awT);awT=null;bdg('awB',0);L('Auto-Win OFF','err');return}if(awT)return;var d=DOC();if(!d){L('Game belum siap','err');return}awT=setInterval(function(){try{d.querySelectorAll('button,[role=button],.btn').forEach(function(b){if(/attack|battle|fight|serang|war|win|menang/i.test(b.textContent||'')&&!b.disabled)b.click()})}catch(e){}},150);bdg('awB',1);L('Auto-Win ON','warn')};

window.bAC=function(on){if(!on){if(acT)clearInterval(acT);acT=null;bdg('acB',0);L('Clicker OFF','err');return}if(acT)return;var d=DOC();if(!d){L('Game belum siap','err');return}acT=setInterval(function(){try{d.querySelectorAll('button').forEach(function(b){if(!b.disabled)b.click()})}catch(e){}},200);bdg('acB',1);L('Clicker ON','warn')};

window.bGM=function(on){if(!on){if(gmT)clearInterval(gmT);gmT=null;bdg('gmB',0);L('God OFF','err');return}if(gmT)return;var ls=LS();if(!ls){L('Game belum siap','err');return}gmT=setInterval(function(){try{for(var i=0;i<ls.length;i++){var k=ls.key(i);try{var v=JSON.parse(ls.getItem(k));walk(v,function(o,f){var fl=f.toLowerCase();if(typeof o[f]==='number'&&(fl.indexOf('hp')!==-1||fl.indexOf('health')!==-1||fl.indexOf('defense')!==-1))o[f]=999999999});ls.setItem(k,JSON.stringify(v))}catch(e){}}}catch(e){}},500);bdg('gmB',1);L('God ON','warn')};

window.bBoostAll=function(){var ls=LS();if(!ls){L('Game belum siap','err');return}var n=0;for(var i=0;i<ls.length;i++){var k=ls.key(i);try{var v=JSON.parse(ls.getItem(k));walk(v,function(o,f){if(typeof o[f]==='number'&&CK.some(function(c){return f.toLowerCase().indexOf(c)!==-1})){o[f]=999999999;n++}});ls.setItem(k,JSON.stringify(v))}catch(e){}}L('Boosted '+n+' fields.','ok')};

window.bBoostN=function(nm){var ls=LS();if(!ls){L('Game belum siap','err');return}var n=0;for(var i=0;i<ls.length;i++){var k=ls.key(i);try{var v=JSON.parse(ls.getItem(k));walk(v,function(o,f){if(typeof o[f]==='number'&&f.toLowerCase().indexOf(nm)!==-1){o[f]=999999999;n++}});ls.setItem(k,JSON.stringify(v))}catch(e){}}L('Boosted '+nm+': '+n,'ok')};

window.bBan=function(){var ls=LS();if(!ls)return;var t=document.getElementById('banT').value.trim();if(!t)return;var a=JSON.parse(ls.getItem('__ban')||'[]');if(a.indexOf(t)===-1)a.push(t);ls.setItem('__ban',JSON.stringify(a));L('Banned '+t,'ok')};

window.bUnban=function(){var ls=LS();if(!ls)return;var t=document.getElementById('banT').value.trim();var a=(JSON.parse(ls.getItem('__ban')||'[]')).filter(function(x){return x!==t});ls.setItem('__ban',JSON.stringify(a));L('Unban '+t,'ok')};

window.bScan=function(){var ls=LS();if(!ls){L('Game belum siap','err');return}L('=== SCAN ===','info');for(var i=0;i<ls.length;i++){var k=ls.key(i);var v=ls.getItem(k);L(k+' => '+(v.length>60?v.slice(0,60)+'...':v),'ok')}};

frame.addEventListener('load',function(){setTimeout(function(){var ls=LS();if(ls){L('Cheat siap. Tap Scan Storage.','info')}else{L('Iframe blocked. Buka lewat github.io!','err')}},1000)});
L('Panel ready.','info');
})();
</script>
</body>
</html>
