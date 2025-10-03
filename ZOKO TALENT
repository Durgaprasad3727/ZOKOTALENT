rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /contests/{contestId} {
      allow read: if true;
      allow write: if request.auth != null && request.auth.token.admin == true;
    }
    match /entries/{entryId} {
      allow read: if true;
      allow create: if request.auth != null && request.resource.data.userId == request.auth.uid;
      allow update: if request.auth != null && request.auth.token.admin == true;
      allow delete: if request.auth != null && (request.auth.token.admin == true || resource.data.userId == request.auth.uid);
    }
    match /payments/{paymentId} {
      allow read: if request.auth != null;
      allow create: if request.auth != null && request.resource.data.userId == request.auth.uid;
      allow update: if request.auth != null && request.auth.token.admin == true;
    }
    match /votes/{voteId} {
      allow create: if request.auth != null && request.resource.data.userId == request.auth.uid;
      allow read: if true;
    }
    match /users/{userId} {
      allow read: if true;
      allow write: if request.auth != null && request.auth.uid == userId;
    }
  }
}

<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Zoko Talent — Mockup Preview</title>
<style>
  :root{--green:#4CAF50;--blue:#1A237E;--muted:#666}
  body{font-family:Inter,system-ui,Arial;background:#f6f8fb;margin:0;color:#111}
  header{background:var(--green);color:#fff;padding:28px 36px;display:flex;align-items:center;justify-content:space-between}
  .logo{font-weight:800;letter-spacing:1px}
  main{max-width:1100px;margin:28px auto;padding:0 16px}
  .hero{background:#fff;padding:28px;border-radius:10px;display:flex;gap:20px;align-items:center}
  .hero h1{margin:0;font-size:34px}
  .hero p{margin:6px 0;color:var(--muted)}
  .card{background:#fff;padding:16px;border-radius:10px;box-shadow:0 6px 18px rgba(12,14,20,0.05)}
  .contest-grid{display:grid;grid-template-columns:1fr 360px;gap:18px;margin-top:18px}
  .contest-info h2{margin:0}
  .meta{color:var(--muted);margin-top:6px}
  .countdown{background:var(--green);color:white;padding:16px;border-radius:8px;text-align:center}
  .countdown h3{margin:0;font-size:18px}
  .qr{margin-top:12px;padding:12px;border-radius:8px;background:#fff;border:1px solid #eee;text-align:center}
  .btn{background:var(--green);color:#fff;padding:8px 12px;border-radius:8px;border:none;cursor:pointer}
  .btn-muted{background:#eee;color:#333;padding:8px 12px;border-radius:8px;border:none;cursor:pointer}
  .gallery{display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:12px;margin-top:16px}
  .entry{background:#fff;border-radius:8px;overflow:hidden;border:1px solid #eee}
  .entry img, .entry video{width:100%;height:160px;object-fit:cover;display:block}
  .entry .meta{padding:8px;display:flex;justify-content:space-between;align-items:center}
  .small{font-size:13px;color:var(--muted)}
  .leader{margin-top:16px}
  footer{margin:28px 0;text-align:center;color:var(--muted)}
  .admin{margin-top:18px;padding:12px;border-radius:8px;background:#fff;border:1px dashed #ddd}
  .badge{background:gold;padding:4px 8px;border-radius:6px;font-weight:600}
  input[type=file]{border:none}
  .flex{display:flex;gap:8px;align-items:center}
  .muted{color:var(--muted)}
  .pill{padding:6px 10px;border-radius:999px;background:#f3f6f4;color:#085; font-weight:700}
  @media(max-width:880px){ .contest-grid{grid-template-columns:1fr} .hero{flex-direction:column;align-items:flex-start} }
</style>
</head>
<body>

<header>
  <div style="display:flex;align-items:center;gap:14px">
    <div style="background:#fff;padding:6px 10px;border-radius:8px;color:var(--green);font-weight:800" class="logo">ZOKO</div>
    <div style="color:#fff;font-weight:600">Talent</div>
  </div>
  <nav style="color:#fff;display:flex;gap:14px;align-items:center">
    <a href="#" style="color:#fff;text-decoration:none">Contests</a>
    <a href="#" style="color:#fff;text-decoration:none">Profile</a>
    <button class="btn" onclick="openAdmin()">Admin</button>
  </nav>
</header>

<main>
  <div class="hero card">
    <div style="flex:1">
      <h1>Unleash Your Skills, Win Rewards</h1>
      <p>Storytelling • Cooking • Fancy Dress • Fashion — Compete, get voted, and win prizes</p>
      <div style="margin-top:12px">
        <button class="btn" onclick="scrollToContest()">Join Contest</button>
        <button class="btn-muted" style="margin-left:8px" onclick="alert('Create Contest — admin only in real app')">Create Contest</button>
      </div>
    </div>
    <div style="width:320px;text-align:right">
      <div style="background:#f1fff4;padding:12px;border-radius:8px;color:var(--green)">
        <div style="font-size:12px">Featured</div>
        <div style="font-weight:700;margin-top:6px">Fancy Dress: Retro Challenge</div>
        <div class="small" style="margin-top:6px">Prize ₹1000 • Ends in <span id="top-count">--</span></div>
      </div>
    </div>
  </div>

  <!-- Contest area -->
  <div id="contest-area" class="contest-grid">
    <div>

      <div class="card contest-info">
        <h2>Storytelling — Short Story Stars</h2>
        <div class="meta">Category: Storytelling • Prize: ₹700 • Fee: ₹30</div>
        <div style="margin-top:12px">
          <div class="small"><strong>Start:</strong> Oct 5, 2025 • <strong>End:</strong> Oct 12, 2025</div>
          <div style="margin-top:8px">FAQ: Submit a recorded story or text (max 5 minutes or 800 words). One entry per user.</div>
        </div>
        <div style="margin-top:12px;">
          <button class="btn" onclick="openContest('story')">Join Storytelling</button>
        </div>
      </div>

      <div style="margin-top:12px" class="card contest-info">
        <h2>Best Healthy Snack</h2>
        <div class="meta">Category: Cooking • Prize: ₹500 • Fee: ₹50</div>
        <div style="margin-top:12px">
          <div class="small"><strong>Start:</strong> Oct 1, 2025 • <strong>End:</strong> Oct 10, 2025</div>
          <div style="margin-top:8px">FAQ: Submit a photo and short recipe. One entry per user.</div>
        </div>
        <div style="margin-top:12px;">
          <button class="btn" onclick="openContest('cook')">Join Cooking</button>
        </div>
      </div>

      <div style="margin-top:12px" class="card contest-info">
        <h2>Fancy Dress: Retro Challenge</h2>
        <div class="meta">Category: Fancy Dress • Prize: ₹1000 • Fee: ₹40</div>
        <div style="margin-top:12px">
          <div class="small"><strong>Start:</strong> Sep 28, 2025 • <strong>End:</strong> Oct 8, 2025</div>
          <div style="margin-top:8px">FAQ: Costume creativity counts. Kids and Adults categories available.</div>
        </div>
        <div style="margin-top:12px;">
          <button class="btn" onclick="openContest('fancy')">Join Fancy Dress</button>
        </div>
      </div>

      <div style="margin-top:12px" class="card contest-info">
        <h2>Stylish Dressing — Fashion Star</h2>
        <div class="meta">Category: Fashion • Prize: ₹1500 • Fee: ₹60</div>
        <div style="margin-top:12px">
          <div class="small"><strong>Start:</strong> Oct 3, 2025 • <strong>End:</strong> Oct 15, 2025</div>
          <div style="margin-top:8px">FAQ: Show your best styled outfit. Short video or image allowed.</div>
        </div>
        <div style="margin-top:12px;">
          <button class="btn" onclick="openContest('fashion')">Join Fashion</button>
        </div>
      </div>

    <div>
      <div class="card contest-info">
        <h2>Best Healthy Snack</h2>
        <div class="meta">Category: Cooking • Prize: ₹500 • Fee: ₹50</div>
        <div style="margin-top:12px">
          <div class="small"><strong>Start:</strong> Oct 1, 2025 • <strong>End:</strong> Oct 10, 2025</div>
          <div style="margin-top:8px">FAQ: Submit a photo and short recipe. One entry per user.</div>
        </div>

        <div style="margin-top:12px" id="statusBox"></div>

        <div style="margin-top:12px;">
          <button class="btn" onclick="openContest()">Join Contest</button>
        </div>

        <div style="margin-top:16px" class="leader card">
          <h3 style="margin:0 0 8px 0">Recent Winners</h3>
          <div style="display:flex;gap:8px">
            <div style="flex:1;padding:8px;border-radius:8px;background:#fff;text-align:center">
              <div class="badge">1</div>
              <div style="margin-top:6px;font-weight:700">Anna Smith</div>
              <div class="small">₹1000</div>
            </div>
            <div style="flex:1;padding:8px;border-radius:8px;background:#fff;text-align:center">
              <div class="badge">2</div>
              <div style="margin-top:6px;font-weight:700">John Doe</div>
              <div class="small">₹500</div>
            </div>
            <div style="flex:1;padding:8px;border-radius:8px;background:#fff;text-align:center">
              <div class="badge">3</div>
              <div style="margin-top:6px;font-weight:700">Mary Johnson</div>
              <div class="small">₹300</div>
            </div>
          </div>
        </div>

      </div>

      <div style="margin-top:12px" class="card">
        <h3 style="margin-top:0">Gallery Preview</h3>
        <div class="gallery" id="gallery">
          <!-- entries inserted by JS -->
        </div>
      </div>
    </div>

    <aside>
      <div class="card countdown">
        <h3>Time left to participate</h3>
        <div id="countdownLarge" style="font-size:22px;margin-top:8px;font-weight:800">--</div>
        <div style="margin-top:12px">
          <button class="btn" onclick="openContest()">Join Contest</button>
        </div>
      </div>

      <div class="qr card">
        <div style="font-weight:700">Pay via UPI</div>
        <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAANwAAADcAQMAAABi5qhEAAAABlBMVEX///8AAABVwtN+AAABGElEQVR4nO3QMQEAAADCIPunNscKAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPwF6n0AAXr+z3gAAAAASUVORK5CYII=" alt="QR" style="width:160px;height:160px;background:#eee;display:block;margin:12px auto">
        <div class="small">UPI ID: <strong>thannirudurgaprasad-10@okaxis</strong></div>
        <div style="margin-top:10px;font-size:13px;color:var(--muted)">Or click Pay to simulate payment</div>
        <div style="margin-top:8px">
          <button class="btn" onclick="mockPay()">Simulate Pay ₹50</button>
        </div>
      </div>

      <div style="margin-top:12px" class="card">
        <h4 style="margin:0 0 8px 0">Leaderboard (Top)</h4>
        <ol id="miniLeaderboard" style="padding-left:18px;margin:0">
          <!-- filled by JS -->
        </ol>
      </div>
    </aside>
  </div>

  <!-- Contest modal / details -->
  <div id="contestModal" style="display:none;position:fixed;inset:0;background:rgba(0,0,0,0.5);z-index:999;align-items:center;justify-content:center;">
    <div style="width:95%;max-width:880px;background:#fff;border-radius:10px;padding:18px;position:relative;">
      <button onclick="closeContest()" style="position:absolute;right:14px;top:10px;border:none;background:#eee;padding:6px;border-radius:6px">Close</button>
      <div style="display:flex;gap:14px;flex-wrap:wrap">
        <div style="flex:1;min-width:300px">
          <h2 style="margin-top:0">Best Healthy Snack — Join</h2>
          <div class="small">Category: Cooking • Prize: ₹500 • Fee: ₹50</div>
          <div style="margin-top:12px">
            <div id="paySection">
              <div style="margin-bottom:8px" class="small">Scan QR or click simulate pay</div>
              <img src="" id="qrLarge" style="width:180px;height:180px;background:#eee;display:block;margin-bottom:8px" alt="QR">
              <div>
                <button class="btn" onclick="mockPay()">Simulate Pay ₹50</button>
                <button class="btn-muted" onclick="markPaidManually()">I have paid (manual)</button>
              </div>
            </div>

            <div id="uploadArea" style="display:none;margin-top:14px">
              <div class="small" style="margin-bottom:8px">Upload your entry (JPG/PNG/MP4). Entry will be visible after admin approval.</div>
              <input type="file" id="entryFile"><br>
              <input id="captionInput" class="small" placeholder="Caption (optional)" style="width:100%;padding:8px;margin-top:8px"/>
              <div style="margin-top:8px">
                <button class="btn" onclick="submitMockEntry()">Upload Entry</button>
              </div>
            </div>
          </div>
        </div>

        <div style="width:320px">
          <div class="card small" style="padding:12px">
            <strong>Contest Rules</strong>
            <ul style="padding-left:18px;color:var(--muted)">
              <li>One entry per user</li>
              <li>Appropriate content only</li>
              <li>Admin will approve entries</li>
            </ul>
            <div style="margin-top:8px">FAQ: <span class="small muted">When will winners be announced? Within 3 days after closing.</span></div>
          </div>

          <div style="margin-top:10px" class="card">
            <strong>Recent Top</strong>
            <div id="detailTop" style="margin-top:8px"></div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Admin Panel (simple) -->
  <div id="adminPanel" style="display:none;position:fixed;right:12px;bottom:12px;width:360px;z-index:9999">
    <div class="admin">
      <div style="display:flex;justify-content:space-between;align-items:center">
        <strong>Admin</strong>
        <button onclick="closeAdmin()" style="background:#eee;border:none;padding:6px;border-radius:6px">Close</button>
      </div>

      <div style="margin-top:8px">
        <div style="font-size:13px;margin-bottom:6px">Pending uploads</div>
        <div id="pendingList" style="max-height:160px;overflow:auto"></div>
      </div>

      <div style="margin-top:10px">
        <div style="font-size:13px;margin-bottom:6px">Pending payments (manual)</div>
        <div id="pendingPayments" style="max-height:120px;overflow:auto"></div>
      </div>

      <div style="margin-top:10px">
        <button class="btn" onclick="approveAllMock()">Approve All (mock)</button>
        <button class="btn-muted" style="margin-left:6px" onclick="awardWinnersMock()">Award Top 10</button>
      </div>
    </div>
  </div>

  <footer>
    Zoko Talent — Mockup • This preview is static and simulates app flows. For full product we integrate Firebase & Razorpay.
  </footer>
</main>

<script>
/* ---------- MOCK DATA & STATE ---------- */
let mockEntries = [
  { id:'e1', name:'Aisha', caption:'Healthy oats cookie', file:'https://images.unsplash.com/photo-1546069901-ba9599a7e63c?w=800&q=60', votes:5, approved:true },
  { id:'e2', name:'Ravi', caption:'Spicy chickpea bites', file:'https://images.unsplash.com/photo-1543353071-873f17a7a088?w=800&q=60', votes:12, approved:true },
  { id:'e3', name:'Maya', caption:'Quick energy bars', file:'https://images.unsplash.com/photo-1551218808-94e220e084d2?w=800&q=60', votes:7, approved:true },
  { id:'e4', name:'Liam', caption:'Baked samosa twist', file:'https://images.unsplash.com/photo-1604908553740-8a7f3df5b1b1?w=800&q=60', votes:2, approved:false }
];
let mockPaid = false;
let pendingUploads = []; // unapproved
let pendingPayments = []; // manual payments

/* ---------- UTILITY ---------- */
let currentContestType = 'cook';
function updateModalForType(type){
  const map = {
    'story': {title:'Storytelling — Short Story Stars', fee:30},
    'cook': {title:'Best Healthy Snack', fee:50},
    'fancy': {title:'Fancy Dress: Retro Challenge', fee:40},
    'fashion': {title:'Stylish Dressing — Fashion Star', fee:60}
  };
  const info = map[type] || map['cook'];
  document.querySelector('#contestModal h2').innerText = info.title + ' — Join';
  document.querySelector('#contestModal .small').innerText = 'Category: ' + (type || 'Cooking') + ' • Fee: ₹' + info.fee;
}

function $(id){ return document.getElementById(id) }
function nowPlus(days=3){ return Date.now() + days*24*60*60*1000 }

/* ---------- COUNTDOWN ---------- */
const contestEnd = new Date();
contestEnd.setDate(contestEnd.getDate()+3);
function updateCountdown(){
  const d = contestEnd - new Date();
  if (d<=0) { $('countdownLarge').innerText='Closed'; $('top-count').innerText='Closed'; $('statusBox').innerHTML = '<div class="small">Contest closed</div>'; return; }
  const days = Math.floor(d/86400000); const hours = Math.floor((d%86400000)/3600000);
  const mins = Math.floor((d%3600000)/60000); const secs = Math.floor((d%60000)/1000);
  $('countdownLarge').innerText = `${days}d ${hours}h ${mins}m ${secs}s`;
  $('top-count').innerText = `${days}d ${hours}h ${mins}m`;
}
setInterval(updateCountdown,1000); updateCountdown();

/* ---------- RENDER GALLERY ---------- */
function renderGallery(){
  const g = $('gallery'); g.innerHTML = '';
  const visible = mockEntries.filter(e=>e.approved).sort((a,b)=>b.votes-a.votes);
  visible.forEach(e=>{
    const div = document.createElement('div'); div.className='entry';
    div.innerHTML = `
      ${e.file.endsWith('.mp4') ? `<video src="${e.file}" controls></video>` : `<img src="${e.file}" alt="entry"/>`}
      <div class="meta"><div><strong>${e.name}</strong><div class="small">${e.caption||''}</div></div>
      <div><span style="font-weight:700">${e.votes}</span> <button class="btn-muted" onclick="vote('${e.id}',this)">Vote</button></div></div>
    `;
    g.appendChild(div);
  });
  renderMiniLeaderboard();
}
function renderMiniLeaderboard(){
  const lb = $('miniLeaderboard'); lb.innerHTML='';
  const top = mockEntries.filter(e=>e.approved).sort((a,b)=>b.votes-a.votes).slice(0,5);
  top.forEach(t=>{
    const li = document.createElement('li'); li.innerText = `${t.name} — ${t.votes} votes`; lb.appendChild(li);
  });
  // detail top
  const dt = $('detailTop'); dt.innerHTML = top.slice(0,3).map((t,idx)=>`<div class="small"><strong>#${idx+1}</strong> ${t.name} — ${t.votes}</div>`).join('');
}
renderGallery();

/* ---------- MOCK PAY ---------- */
function mockPay(){
  // create a "pending" payment then mark paid after 1s
  const id = 'p_'+Date.now();
  pendingPayments.push({ id, user:'you@example.com', amount:50, contest:'besthealthy', status:'PENDING' });
  renderPendingPayments();
  // simulate server webhook later
  setTimeout(()=> {
    // mark paid
    const p = pendingPayments.find(x=>x.id===id);
    if (p) { p.status='PAID'; mockPaid = true; alert('Payment simulated OK — your payment marked PAID'); renderPendingPayments(); }
  }, 900);
}

function renderPendingPayments(){
  const el = $('pendingPayments'); el.innerHTML='';
  pendingPayments.forEach(p=>{
    const div = document.createElement('div'); div.style.borderBottom='1px solid #eee'; div.style.padding='6px 0';
    div.innerHTML = `<div style="display:flex;justify-content:space-between"><div><strong>${p.user}</strong> • ₹${p.amount}</div><div class="small">${p.status}</div></div>`;
    el.appendChild(div);
  });
}

/* ---------- MOCK CONTEST MODAL ---------- */
function openContest(type){ currentContestType = type || 'cook'; $('contestModal').style.display='flex'; checkUserPaidUI(); updateModalForType(type); }
function closeContest(){ $('contestModal').style.display='none' }

function checkUserPaidUI(){
  const uploadArea = $('uploadArea'); const paySection = $('paySection');
  if (mockPaid) { uploadArea.style.display='block'; paySection.style.display='none'; }
  else { uploadArea.style.display='block'; paySection.style.display='block'; /* allow manual too */ }
}
function markPaidManually(){
  // admin will verify later in real app. For mock, mark pendingPayments and set paid flag
  const id = 'manual_'+Date.now();
  pendingPayments.push({ id, user:'you@example.com', amount:50, contest:'besthealthy', status:'MANUAL_PENDING' });
  renderPendingPayments();
  alert('Marked as “I have paid”. Admin must verify. In this mock, open Admin panel and click Verify.');
}

/* ---------- MOCK SUBMIT ENTRY ---------- */
function submitMockEntry(){
  const fileInput = $('entryFile');
  const caption = $('captionInput').value || '';
  if (!fileInput.files || fileInput.files.length===0) return alert('Choose a file first (mock: reads file name only)');
  const f = fileInput.files[0];
  // create object URL preview and push to pendingUploads
  const id = 'u'+Date.now();
  const url = URL.createObjectURL(f);
  pendingUploads.push({ id, name:'You', caption, file:url, votes:0, approved:false });
  renderPendingUploads();
  alert('Entry submitted! It will appear in Gallery after admin approves (mock). Close modal and open Admin to approve.');
  closeContest();
}

/* ---------- VOTING (client-side mock, 1 per session) ---------- */
const votedSet = new Set();
function vote(entryId, btn){
  if (votedSet.has(entryId)) { alert('You already voted in this session (mock restriction).'); return; }
  // find entry
  const e = mockEntries.find(x=>x.id===entryId);
  if (e) { e.votes++; votedSet.add(entryId); renderGallery(); }
  else {
    // maybe in pendingUploads
    const p = pendingUploads.find(x=>x.id===entryId);
    if (p) { p.votes++; votedSet.add(entryId); renderPendingUploads(); }
  }
}

/* ---------- PENDING UPLOADS UI ---------- */
function renderPendingUploads(){
  const el = $('pendingList'); el.innerHTML='';
  pendingUploads.forEach(u=>{
    const div = document.createElement('div'); div.style.padding='8px'; div.style.borderBottom='1px solid #eee';
    div.innerHTML = `<div><strong>${u.name}</strong> • ${u.caption}</div><div style="margin-top:6px"><button class="btn" onclick="approveMock('${u.id}')">Approve</button> <button class="btn-muted" onclick="rejectMock('${u.id}')">Reject</button></div>`;
    el.appendChild(div);
  });
}
function approveMock(id){
  const idx = pendingUploads.findIndex(x=>x.id===id);
  if (idx===-1) return;
  const item = pendingUploads.splice(idx,1)[0];
  item.approved = true; item.id = 'm'+Date.now();
  mockEntries.push(item);
  renderPendingUploads(); renderGallery();
}
function rejectMock(id){ if (!confirm('Reject this upload?')) return; pendingUploads = pendingUploads.filter(x=>x.id!==id); renderPendingUploads(); }

/* ---------- ADMIN TOOLS ---------- */
function openAdmin(){ $('adminPanel').style.display='block'; renderPendingUploads(); renderPendingPayments(); }
function closeAdmin(){ $('adminPanel').style.display='none' }
function approveAllMock(){ pendingUploads.forEach(u=>{ u.approved=true; u.id='m'+Date.now()+Math.random(); mockEntries.push(u); }); pendingUploads=[]; renderPendingUploads(); renderGallery(); alert('All pending approved (mock)'); }
function awardWinnersMock(){
  // find top 10 by votes and tag as winners
  const winners = mockEntries.filter(e=>e.approved).sort((a,b)=>b.votes-a.votes).slice(0,10);
  winners.forEach((w,idx)=>{ w.rank = idx+1; });
  alert('Top winners awarded (mock). Check leaderboard.');
  renderGallery();
}

/* ---------- INIT: pending lists empty ---------- */
renderPendingUploads(); renderPendingPayments();

/* ---------- For demo: insert one unapproved file to pendingUploads ---------- */
pendingUploads.push({ id:'p0', name:'Kavya', caption:'Fusion salad', file:'https://images.unsplash.com/photo-1510626176961-4b57e53f7d2b?w=800&q=60', votes:0, approved:false });
renderPendingUploads();

</script>
</body>
</html>


Zoko Talent — Preview & Starter Package
======================================

Contents:
- index.html : interactive static mockup (open in browser)
- client/: sample React component stubs and firebase config templates
- server/: sample Node Express Razorpay server (create-order + webhook)
- functions/: sample Firebase Cloud Function webhook example
- firestore.rules : suggested Firestore security rules

How to use:
1. Download and unzip this package.
2. Open index.html in a browser to see the mockup preview.
3. For a working app, follow instructions in client/README.md to scaffold a React app and plug in Firebase keys.
4. To enable payments, deploy the server or Cloud Function and configure Razorpay credentials and webhook.

If you want, I can also create a full GitHub repo for this package and push the files there — you'll need to provide a connected GitHub account or I can give you instructions to create the repo locally and push.
