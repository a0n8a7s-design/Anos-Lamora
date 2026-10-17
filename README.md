# Anos-Lamora

<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#101010">
<title>أنا ولمورة</title>
<style>
*{box-sizing:border-box}
body{
 margin:0;background:#0c0c0e;color:#f8f1e5;
 font-family:system-ui,Tahoma,sans-serif;padding:18px;
 padding-bottom:90px
}
header{text-align:center;padding:20px 0}
h1,h2{color:#e7c27c}
h1{font-size:32px}
p{line-height:1.8}
.card{
 background:#19191c;border:1px solid #423725;
 border-radius:18px;padding:17px;margin:12px 0
}
button,input,textarea{font:inherit;border-radius:11px;padding:12px}
button{
 border:0;background:#e7c27c;color:#18130a;
 font-weight:bold;cursor:pointer
}
input,textarea{
 width:100%;background:#101012;color:white;
 border:1px solid #51452f;margin:7px 0
}
nav{
 position:fixed;bottom:0;left:0;right:0;
 background:#151517;display:flex;gap:5px;
 padding:8px;justify-content:space-around
}
nav button{
 flex:1;padding:10px 3px;background:transparent;
 color:#e7c27c;font-size:12px
}
.page{display:none}
.page.active{display:block}
.gold{font-size:29px;color:#e7c27c;font-weight:bold}
.muted{color:#b8b0a2;font-size:14px}
.entry{
 padding:12px;margin:8px 0;background:#242326;
 border-radius:12px;overflow-wrap:anywhere
}
</style>
</head>
<body>

<header>
 <div style="font-size:38px;color:#e7c27c">♥</div>
 <h1 id="heading">أنا ولمورة</h1>
 <p class="muted">مساحتنا الصغيرة وذكرياتنا الكبيرة</p>
</header>

<section id="home" class="page active">
 <div class="card">
  <h2>رحلتنا معًا</h2>
  <div class="gold" id="days">♡</div>
  <p class="muted">عدد الأيام منذ تاريخ البداية</p>
 </div>

 <div class="card">
  <h2>رسالة اليوم 💌</h2>
  <p id="message">بعض التفاصيل الصغيرة تصبح ذكريات جميلة.</p>
  <button onclick="newMessage()">رسالة أخرى</button>
 </div>

 <div class="card">
  <h2>شعلة الحماسة 🔥</h2>
  <div class="gold" id="points">0</div>
  <p class="muted">نقاط التحديات على هذا الجهاز</p>
  <button onclick="addPoints()">أنجزنا تحديًا +5</button>
 </div>
</section>

<section id="memories" class="page">
 <div class="card">
  <h2>ذكرياتنا ✨</h2>
  <textarea id="memory" placeholder="اكتب ذكرى جميلة..."></textarea>
  <button onclick="saveMemory()">حفظ الذكرى</button>
  <div id="memoryList"></div>
 </div>
</section>

<section id="games" class="page">
 <div class="card">
  <h2>تحدّي اليوم 🎲</h2>
  <p id="challenge">اكتب شيئًا جميلًا تقدّره في يومك.</p>
  <button onclick="newChallenge()">تحدٍّ جديد</button>
 </div>
 <div class="card">
  <h2>سؤال لنا 💫</h2>
  <p id="question">ما الشيء الذي يجعلك سعيدًا في يوم عادي؟</p>
  <button onclick="newQuestion()">سؤال آخر</button>
 </div>
</section>

<section id="settings" class="page">
 <div class="card">
  <h2>تخصيص التطبيق ⚙️</h2>
  <label>اسمك</label>
  <input id="myName" placeholder="أنا">
  <label>اسم الطرف الآخر</label>
  <input id="herName" placeholder="لمورة">
  <label>تاريخ البداية</label>
  <input id="startDate" type="date">
  <button onclick="saveSettings()">حفظ الإعدادات</button>
  <p class="muted">تُحفظ هذه البيانات على هاتفك فقط في هذه النسخة.</p>
 </div>
</section>

<nav>
 <button onclick="show('home')">الرئيسية</button>
 <button onclick="show('memories')">الذكريات</button>
 <button onclick="show('games')">الألعاب</button>
 <button onclick="show('settings')">الإعدادات</button>
</nav>

<script>
const $=id=>document.getElementById(id);
const get=(key,def)=> {
 try{return JSON.parse(localStorage.getItem(key)) ?? def}
 catch{return def}
};
const put=(key,value)=>localStorage.setItem(key,JSON.stringify(value));

let memories=get("memories",[]);
let points=get("points",0);

function show(id){
 document.querySelectorAll(".page").forEach(p=>{
  p.classList.toggle("active",p.id===id);
 });
 if(id==="memories")renderMemories();
}

const messages=[
 "وجودك يجعل التفاصيل الصغيرة أجمل ♥",
 "أتمنى أن يحمل يومك شيئًا يسعد قلبك.",
 "الذكريات الجميلة تبدأ أحيانًا بلحظة بسيطة.",
 "لا تنسَ أن تمنح نفسك وقتًا للراحة."
];
function newMessage(){
 $("message").textContent=messages[Math.floor(Math.random()*messages.length)];
}

const challenges=[
 "اكتب ثلاثة أشياء جميلة حدثت اليوم.",
 "تذكّر موقفًا جعلك تبتسم.",
 "حدّد هدفًا صغيرًا لهذا الأسبوع.",
 "خذ خمس دقائق للراحة والتركيز.",
 "اكتب رسالة تقدير لشخص مهم في حياتك."
];
function newChallenge(){
 $("challenge").textContent=challenges[Math.floor(Math.random()*challenges.length)];
}

const questions=[
 "ما الشيء الذي يجعلك سعيدًا في يوم عادي؟",
 "ما المهارة التي تريد تعلّمها؟",
 "ما الذكرى التي تحب الاحتفاظ بها؟",
 "ما هدفك الأهم لهذا الشهر؟"
];
function newQuestion(){
 $("question").textContent=questions[Math.floor(Math.random()*questions.length)];
}

function addPoints(){
 points+=5;
 put("points",points);
 $("points").textContent=points;
}

function saveMemory(){
 const text=$("memory").value.trim();
 if(!text)return alert("اكتب الذكرى أولًا.");
 memories.push({text,date:new Date().toLocaleDateString("ar-IQ")});
 put("memories",memories);
 $("memory").value="";
 renderMemories();
}

function renderMemories(){
 $("memoryList").innerHTML="";
 memories.slice().reverse().forEach((m,index)=>{
  const el=document.createElement("div");
  el.className="entry";
  const content=document.createElement("p");
  content.textContent=m.text;
  const date=document.createElement("small");
  date.className="muted";
  date.textContent=m.date;
  const del=document.createElement("button");
  del.textContent="حذف";
  del.style.marginTop="8px";
  del.onclick=()=>{
   memories.splice(memories.length-1-index,1);
   put("memories",memories);
   renderMemories();
  };
  el.append(content,date,document.createElement("br"),del);
  $("memoryList").appendChild(el);
 });
}

function saveSettings(){
 const me=$("myName").value.trim()||"أنا";
 const her=$("herName").value.trim()||"لمورة";
 const date=$("startDate").value;
 put("settings",{me,her,date});
 updateSettings();
 alert("تم حفظ الإعدادات على هذا الجهاز.");
}

function updateSettings(){
 const s=get("settings",{me:"أنا",her:"لمورة",date:""});
 $("myName").value=s.me;
 $("herName").value=s.her;
 $("startDate").value=s.date;
 $("heading").textContent=s.me+" و"+s.her;
 if(s.date){
  const start=new Date(s.date+"T00:00:00");
  const days=Math.max(0,Math.floor((Date.now()-start.getTime())/86400000));
  $("days").textContent=days;
 }else $("days").textContent="♡";
 $("points").textContent=points;
}

updateSettings();
renderMemories();
</script>
</body>
</html>
