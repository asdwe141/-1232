<!doctype html>
<html lang="ko">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="referrer" content="no-referrer">
<meta http-equiv="Content-Security-Policy" content="default-src 'none'; script-src 'self' https://unpkg.com 'unsafe-inline'; style-src 'unsafe-inline'; img-src 'self' data:; media-src 'self' blob:; connect-src 'self' https://unpkg.com; worker-src 'self' blob:;">
<title>FIRE-CHECK | 실시간 QR 스캔</title>
<script defer src="https://unpkg.com/html5-qrcode@2.3.8/html5-qrcode.min.js"></script>
<style>
*{box-sizing:border-box}body{margin:0;background:#edf2f8;color:#172c43;font-family:-apple-system,BlinkMacSystemFont,'Noto Sans KR',sans-serif}
header{background:#132f4d;color:white;padding:17px 18px;font-weight:750;letter-spacing:.3px}header small{display:block;color:#bad1ea;font-weight:450;margin-top:4px}
main{max-width:530px;margin:24px auto;padding:0 14px 30px}
.card{background:#fff;border:1px solid #dce5ef;border-radius:16px;padding:19px;box-shadow:0 4px 18px #243c5610}
h1{font-size:20px;margin:0 0 8px}p{line-height:1.65;color:#49627a;font-size:14px}#reader{min-height:255px;background:#101927;border-radius:12px;overflow:hidden;margin:14px 0}#reader video{border-radius:10px}
#status{font-size:14px;line-height:1.65;min-height:26px;font-weight:600;color:#274d72}
button,a.link{display:block;width:100%;border:none;border-radius:10px;padding:13px 12px;margin-top:10px;text-align:center;font-size:15px;font-weight:650;text-decoration:none;cursor:pointer}
button.primary{background:#1761a0;color:white}button.secondary,a.link{background:#e7eff8;color:#17446e}
.tip{font-size:12px;color:#60758b;margin-top:16px}#error{font-size:13px;color:#b42318;white-space:pre-wrap;overflow-wrap:anywhere}
</style>
</head>
<body>
<header>FIRE-CHECK<small>소방시설 월간 점검 · 실시간 QR 스캐너</small></header>
<main><div class="card">
<h1>설비 QR코드 스캔</h1>
<p>스마트폰 후면 카메라를 설비 QR 라벨에 비추세요. 인식되면 별도 확인 없이 해당 설비의 점검표로 이동합니다.</p>
<div id="reader" aria-label="QR 카메라 영상"></div>
<div id="status" role="status" aria-live="polite">스캐너 준비 중…</div>
<div id="error"></div>
<button id="retry" class="primary" type="button">카메라 다시 시작</button>
<a class="link" id="returnLink" href="#">FIRE-CHECK로 돌아가기</a>
<p class="tip">HTTPS 및 카메라 권한이 필요합니다. QR 이미지와 카메라 영상은 서버로 업로드하지 않습니다. 최초 실행 시 카메라 권한을 허용하세요.</p>
</div></main>
<script>
'use strict';
const el = id => document.getElementById(id);
const params=new URLSearchParams(location.search);
let app=null;
try {
  const value=params.get('return')||'';
  app=new URL(value);
  if(app.protocol!=='https:' || app.hostname!=='script.google.com' ||
     !/^\/macros\/s\/[^/]+\/exec$/.test(app.pathname))throw Error('invalid app');
} catch(_){el('status').textContent='FIRE-CHECK 연결 주소가 올바르지 않습니다.';el('error').textContent='FIRE-CHECK 웹앱의 QR 버튼으로 접속해 주세요.';}
if(app){
  el('returnLink').href=app.origin+app.pathname;
} else {el('returnLink').style.display='none';}
let scanner=null,scanning=false,done=false;
function setError(message){el('error').textContent=message;}
async function stop(){
  if(!scanner)return;
  try{if(scanning){await scanner.stop();scanning=false;}}catch(_){}
  try{await scanner.clear();}catch(_){}
  scanner=null;
}
async function onDecoded(value){
  if(done || !app)return;
  let link;
  try {
    link=new URL(value.trim());
    if(link.origin!==app.origin || link.pathname!==app.pathname)return;
    const id=link.searchParams.get('eq')||'';
    if(!/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/i.test(id))return;
    done=true;
    el('status').textContent='QR 인식 완료! 해당 설비 점검표로 이동합니다.';
    // 스마트폰 탭을 그대로 점검 화면으로 이동: iframe 간 메시지·팝업 의존하지 않음.
    const target=new URL(app.origin+app.pathname);
    target.searchParams.set('eq',id);
    await stop();
    location.replace(target.href);
  }catch(_){return;}
}
async function start(){
  if(!app)return;
  if(!window.isSecureContext || !navigator.mediaDevices){setError('보안 HTTPS 페이지에서만 카메라 사용이 가능합니다.');return;}
  if(typeof Html5Qrcode==='undefined') {setError('QR 스캔 라이브러리를 불러오지 못했습니다. 네트워크/도메인 차단 여부를 확인하세요.');return;}
  done=false;
  await stop();
  setError('');
  el('status').textContent='후면 카메라를 여는 중…';
  scanner=new Html5Qrcode('reader',{formatsToSupport:[Html5QrcodeSupportedFormats.QR_CODE]});
  try{
    await scanner.start({facingMode:'environment'},{fps:10,qrbox:(w,h)=>({width:Math.min(260,Math.max(160,Math.floor(w*.75))),height:Math.min(260,Math.max(160,Math.floor(Math.min(w,h)*.75)))})},onDecoded,()=>{});
    scanning=true;
    el('status').textContent='설비 QR코드를 카메라 중앙에 비춰 주세요.';
  }catch(err){
    setError('카메라 실행 실패: '+(err && err.message ? err.message : String(err))+'\n브라우저 카메라 권한, HTTPS 접속, 다른 앱의 카메라 사용 여부를 확인하세요.');
    el('status').textContent='카메라를 실행할 수 없습니다.';
  }
}
el('retry').addEventListener('click',start);
window.addEventListener('pagehide',()=>{stop();});
window.addEventListener('load',()=>{if(app)start();});
</script>
</body>
</html>
