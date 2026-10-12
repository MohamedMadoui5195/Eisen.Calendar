<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#071226">
<meta name="description" content="Eisen Calendar - تقويم ذكي لتنظيم المواعيد بالتاريخين الميلادي والهجري.">
<title>Eisen Calendar</title>
<style>
:root{--bg:#050b18;--panel:#0b1730;--panel2:#101f3d;--line:#203454;--text:#edf4ff;--muted:#94a8c8;--blue:#438cff;--cyan:#4bd8e8;--gold:#f4c66b;--danger:#ff6f83;--radius:20px}
*{box-sizing:border-box}
body{margin:0;background:radial-gradient(ellipse at top,#10244a 0,#071226 38%,#040914 100%);color:var(--text);font-family:system-ui,-apple-system,"Segoe UI",Tahoma,Arial,sans-serif;min-height:100vh}
button,input,select,textarea{font:inherit}
button{cursor:pointer}
.app{max-width:1180px;margin:auto;padding:18px 16px 96px}
.topbar{display:flex;align-items:center;justify-content:space-between;gap:12px;margin-bottom:20px}
.brand{display:flex;align-items:center;gap:12px}
.brand-icon{width:48px;height:48px;border-radius:16px;background:linear-gradient(135deg,#2d7dff,#36d7e7);display:grid;place-items:center;color:#fff;font-size:25px;font-weight:900;box-shadow:0 8px 28px #267eff35}
.brand h1{font-size:21px;margin:0;letter-spacing:.2px}.brand p{margin:3px 0 0;color:var(--muted);font-size:12px}
.icon-btn,.btn{border:1px solid var(--line);color:var(--text);background:#112344;border-radius:13px;padding:10px 13px}
.icon-btn{width:43px;height:43px;padding:0;font-size:18px}
.btn.primary{background:linear-gradient(135deg,#2877ff,#28b8d8);border:0;color:#fff;font-weight:750}
.btn.ghost{background:transparent}
.btn.danger{color:#ff9aa8}
.welcome{padding:25px;border:1px solid #27436c;border-radius:24px;background:linear-gradient(115deg,#11284b,#0b1730 65%,#101c39);position:relative;overflow:hidden;margin-bottom:18px}
.welcome:after{content:"";position:absolute;width:180px;height:180px;border-radius:50%;background:#347eff15;left:-35px;top:-65px;pointer-events:none}
.eyebrow{color:#73dcf1;font-size:12px;font-weight:800;letter-spacing:1px}
.welcome h2{font-size:clamp(23px,4vw,34px);margin:9px 0}.welcome p{color:#b8c9e5;max-width:640px;line-height:1.7;margin:0}
.stats{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:12px;margin-bottom:18px}
.stat,.panel,.tool-card{background:linear-gradient(145deg,#0e1c36,#09142a);border:1px solid var(--line);border-radius:var(--radius)}
.stat{padding:15px;min-width:0}.stat-label{color:var(--muted);font-size:12px}.stat-value{font-size:17px;font-weight:800;margin-top:8px;overflow-wrap:anywhere}.stat-sub{font-size:11px;color:#7f96ba;margin-top:5px}
.layout{display:grid;grid-template-columns:minmax(0,1.5fr) minmax(290px,1fr);gap:16px;align-items:start}
.panel{padding:17px;min-width:0;margin-bottom:16px}
.panel-head{display:flex;justify-content:space-between;align-items:center;gap:10px;margin-bottom:15px}
.panel h3{font-size:16px;margin:0}.hint{font-size:12px;color:var(--muted);margin:5px 0 0}
.month-controls{display:flex;align-items:center;gap:8px}.month-title{min-width:125px;text-align:center;font-weight:800}
.weekdays,.calendar-grid{display:grid;grid-template-columns:repeat(7,minmax(0,1fr));gap:5px}
.weekday{text-align:center;color:#8fa6c8;font-size:11px;padding:8px 0}
.day{position:relative;min-height:66px;border:1px solid transparent;border-radius:12px;background:#0c1a33;color:var(--text);display:flex;flex-direction:column;align-items:center;justify-content:center;gap:3px;padding:5px 1px}
.day:hover{border-color:#3e75c3}.day.outside{opacity:.4}.day.today{border-color:#47bde0;background:#102d4a}.day.selected{background:linear-gradient(135deg,#226be1,#167eac);border-color:#76d8f4;box-shadow:0 5px 18px #1678d533}.day .greg{font-size:15px;font-weight:800}.day .hijri{font-size:9px;color:#a7c5e9}.day .dot{width:5px;height:5px;border-radius:50%;background:var(--cyan);position:absolute;bottom:4px}.day.holiday .dot{background:var(--gold)}
.legend{display:flex;gap:13px;flex-wrap:wrap;color:var(--muted);font-size:11px;margin-top:13px}.legend span{display:flex;align-items:center;gap:6px}.legend i{width:7px;height:7px;border-radius:50%;display:inline-block;background:var(--cyan)}.legend .gold{background:var(--gold)}
.selected-date{border-radius:15px;background:#102344;padding:13px;margin-bottom:12px}.selected-date strong{display:block;font-size:16px}.selected-date small{display:block;color:var(--muted);margin-top:5px}
.event-list{display:flex;flex-direction:column;gap:9px}.event{display:flex;align-items:stretch;gap:10px;border:1px solid #203554;background:#0a162c;border-radius:13px;padding:11px;min-width:0}.event-bar{width:4px;flex:0 0 4px;border-radius:6px;background:var(--blue)}.event-bar.islamic{background:var(--gold)}.event-content{flex:1;min-width:0}.event-content strong{font-size:13px;display:block;overflow-wrap:anywhere}.event-content small{font-size:11px;color:var(--muted);display:block;line-height:1.7;margin-top:4px;overflow-wrap:anywhere}.event-actions{display:flex;align-items:center;gap:5px}.event-actions button{border:1px solid #2b4163;background:#10213c;color:#dbeaff;border-radius:8px;width:29px;height:29px}.empty{border:1px dashed #29405f;border-radius:13px;padding:18px;text-align:center;color:var(--muted);font-size:13px}
.tools-grid{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:10px}.tool-card{padding:14px;text-align:right;cursor:pointer;color:var(--text);transition:border-color .15s}.tool-card:hover{border-color:#428de6}.tool-icon{width:37px;height:37px;border-radius:12px;display:grid;place-items:center;background:#142e55;font-size:19px;margin-bottom:10px}.tool-card strong{display:block;font-size:13px}.tool-card small{display:block;color:var(--muted);font-size:11px;line-height:1.5;margin-top:5px}
.page{display:none}.page.active{display:block}
.search-row{display:flex;gap:8px}.field{width:100%;background:#071226;border:1px solid #2a4164;border-radius:12px;color:var(--text);padding:12px;outline:none;min-width:0}.field:focus{border-color:#4c9bff;box-shadow:0 0 0 3px #438cff18}label{display:block;color:#b7c8e3;font-size:12px;margin-bottom:7px}.form-grid{display:grid;grid-template-columns:1fr 1fr;gap:13px}.form-group{min-width:0}.form-group.full{grid-column:1/-1}.form-actions{display:flex;gap:9px;flex-wrap:wrap;margin-top:17px}
.modal{display:none;position:fixed;inset:0;background:#020611d9;z-index:30;align-items:center;justify-content:center;padding:15px;overflow-y:auto}.modal.open{display:flex}.modal-box{width:min(540px,100%);max-height:92vh;overflow:auto;background:#0b1730;border:1px solid #2c456b;border-radius:22px;padding:20px;box-shadow:0 25px 80px #0009}.modal-head{display:flex;align-items:center;justify-content:space-between;gap:12px;margin-bottom:18px}.modal-head h3{margin:0;font-size:18px}
.note{color:var(--muted);font-size:11px;line-height:1.7;margin-top:14px}.settings-section{border-top:1px solid var(--line);padding-top:16px;margin-top:16px}
.toast{position:fixed;z-index:50;bottom:88px;left:50%;transform:translate(-50%,20px);opacity:0;pointer-events:none;background:#eaf6ff;color:#071226;padding:11px 17px;border-radius:12px;box-shadow:0 8px 30px #0005;font-size:13px;transition:.2s;max-width:calc(100% - 30px);text-align:center}.toast.show{opacity:1;transform:translate(-50%,0)}
.bottom-nav{position:fixed;z-index:20;bottom:0;left:0;right:0;display:flex;justify-content:center;background:#061022ee;backdrop-filter:blur(15px);border-top:1px solid #1b3152;padding:8px 7px calc(8px + env(safe-area-inset-bottom));gap:4px}.nav-btn{flex:1;max-width:170px;border:0;background:transparent;color:#8097b9;padding:7px 4px;border-radius:12px;font-size:11px}.nav-btn span{display:block;font-size:19px;margin-bottom:3px}.nav-btn.active{color:#fff;background:#16325a}
footer{text-align:center;color:#647b9f;font-size:11px;padding:12px 0 0}
@media(max-width:800px){.stats{grid-template-columns:repeat(2,minmax(0,1fr))}.layout{grid-template-columns:1fr}.tools-grid{grid-template-columns:repeat(3,minmax(0,1fr))}.day{min-height:58px}.app{padding:13px 11px 100px}}
@media(max-width:430px){.welcome{padding:20px}.panel{padding:12px}.day{min-height:49px;border-radius:9px}.day .greg{font-size:13px}.day .hijri{font-size:8px}.month-title{min-width:100px;font-size:13px}.tools-grid{grid-template-columns:1fr 1fr}.brand h1{font-size:18px}.form-grid{grid-template-columns:1fr}.form-group.full{grid-column:auto}.search-row{flex-direction:column}}
</style>
</head>
<body>
<div class="app">
<header class="topbar">
  <div class="brand"><div class="brand-icon">E</div><div><h1>Eisen Calendar</h1><p id="brandSubtitle">تقويمك الذكي، كل أيامك في مكان واحد</p></div></div>
  <button class="icon-btn" id="settingsButton" aria-label="الإعدادات">⚙</button>
</header>

<section class="welcome">
  <div class="eyebrow">EISEN · CALENDAR</div>
  <h2 id="greeting">نظّم وقتك، وامتلك يومك.</h2>
  <p id="welcomeText">التاريخان الميلادي والهجري، والمواعيد والأحداث في مكان واحد.</p>
  <div style="margin-top:17px"><button class="btn primary" id="addEventButton">＋ <span id="addEventText">إضافة موعد</span></button></div>
</section>

<section class="stats">
  <div class="stat"><div class="stat-label" id="statGregorianLabel">التاريخ الميلادي</div><div class="stat-value" id="statGregorian">—</div><div class="stat-sub" id="statGregorianSub">التقويم الميلادي</div></div>
  <div class="stat"><div class="stat-label" id="statHijriLabel">التاريخ الهجري</div><div class="stat-value" id="statHijri">—</div><div class="stat-sub" id="statHijriSub">قد يختلف حسب رؤية الهلال</div></div>
  <div class="stat"><div class="stat-label" id="statEventsLabel">المواعيد المحفوظة</div><div class="stat-value" id="statEvents">0</div><div class="stat-sub" id="statEventsSub">على هذا الجهاز</div></div>
  <div class="stat"><div class="stat-label" id="statMonthLabel">الشهر المعروض</div><div class="stat-value" id="statMonth">—</div><div class="stat-sub" id="statMonthSub">خطط لأيامك القادمة</div></div>
</section>

<div class="layout">
<main>
<section class="panel">
  <div class="panel-head"><div><h3 id="calendarHeading">التقويم</h3><p class="hint" id="calendarHint">اختر يومًا لعرض تفاصيله</p></div>
  <div class="month-controls"><button class="icon-btn" id="prevMonth" aria-label="الشهر السابق">‹</button><div class="month-title" id="monthTitle"></div><button class="icon-btn" id="nextMonth" aria-label="الشهر التالي">›</button></div></div>
  <div class="weekdays" id="weekdays"></div><div class="calendar-grid" id="calendarDays"></div>
  <div class="legend"><span><i></i><b id="legendEvent">موعد محفوظ</b></span><span><i class="gold"></i><b id="legendHoliday">مناسبة إسلامية</b></span><span>◉ <b id="legendToday">اليوم</b></span></div>
  <div style="margin-top:13px"><button class="btn ghost" id="todayButton">↩ <span id="todayButtonText">العودة إلى اليوم</span></button></div>
</section>

<section class="panel">
  <div class="panel-head"><div><h3 id="detailsHeading">تفاصيل اليوم</h3><p class="hint" id="selectedHint">اليوم المحدد في التقويم</p></div><button class="btn primary" id="quickAddButton">＋ <span id="quickAddText">إضافة</span></button></div>
  <div class="selected-date"><strong id="selectedWeekday">—</strong><small id="selectedGregorian">—</small><small id="selectedHijri">—</small></div>
  <div class="event-list" id="dayEvents"></div>
</section>

<section class="panel">
  <div class="panel-head"><div><h3 id="upcomingHeading">المواعيد القادمة</h3><p class="hint" id="upcomingHint">الأحداث المحفوظة في تقويمك</p></div></div>
  <div class="event-list" id="upcomingEvents"></div>
</section>
</main>

<aside>
<section class="panel">
  <div class="panel-head"><div><h3 id="toolsHeading">أدوات التقويم</h3><p class="hint" id="toolsHint">كل ما تحتاجه لتنظيم وقتك</p></div></div>
  <div class="tools-grid">
    <button class="tool-card" id="toolAdd"><span class="tool-icon">＋</span><strong id="quickAddTitle">موعد جديد</strong><small id="quickAddSub">أضف حدثًا إلى تقويمك</small></button>
    <button class="tool-card" data-quick-search><span class="tool-icon">⌕</span><strong id="quickSearchTitle">البحث</strong><small id="quickSearchSub">ابحث في أحداثك</small></button>
    <button class="tool-card" data-quick-islamic><span class="tool-icon">☾</span><strong id="quickIslamicTitle">المناسبات الإسلامية</strong><small id="quickIslamicSub">رمضان والأعياد وغيرها</small></button>
  </div>
</section>

<section class="panel page" data-page="search" id="searchPage">
  <div class="panel-head"><div><h3 id="searchHeading">البحث عن موعد</h3><p class="hint" id="searchHint">ابحث بالعنوان أو الوصف</p></div></div>
  <div class="search-row"><input class="field" id="searchInput" type="search" placeholder="اكتب اسم الموعد..."><button class="btn primary" id="searchButton">بحث</button></div>
  <div class="event-list" id="searchResults" style="margin-top:13px"></div>
</section>

<section class="panel page" data-page="islamic" id="islamicPage">
  <div class="panel-head"><div><h3 id="islamicHeading">المناسبات الإسلامية</h3><p class="hint" id="islamicHint">تواريخ تقريبية حسب التقويم الهجري</p></div></div>
  <div class="event-list" id="islamicEvents"></div>
  <p class="note" id="islamicNote">قد تختلف تواريخ المناسبات الهجرية يومًا بحسب رؤية الهلال والجهة الرسمية في بلدك.</p>
</section>
</aside>
</div>
<footer id="footerText">وقتك، منظّم بطريقتك · Eisen Calendar</footer>
</div>

<div class="modal" id="eventModal" role="dialog" aria-modal="true" aria-labelledby="eventModalTitle">
<div class="modal-box">
  <div class="modal-head"><h3 id="eventModalTitle">إضافة موعد جديد</h3><button class="icon-btn" id="cancelEventButton" aria-label="إغلاق">×</button></div>
  <form id="eventForm">
    <input type="hidden" id="eventId">
    <div class="form-grid">
      <div class="form-group full"><label id="eventTitleLabel" for="eventTitle">عنوان الموعد *</label><input class="field" id="eventTitle" maxlength="140" required placeholder="مثال: اجتماع مهم"></div>
      <div class="form-group"><label id="eventDateLabel" for="eventDate">التاريخ *</label><input class="field" id="eventDate" type="date" required></div>
      <div class="form-group"><label id="eventTimeLabel" for="eventTime">الوقت</label><input class="field" id="eventTime" type="time"></div>
      <div class="form-group full"><label id="eventCategoryLabel" for="eventCategory">نوع الموعد</label><select class="field" id="eventCategory"></select></div>
      <div class="form-group full"><label id="eventDescriptionLabel" for="eventDescription">ملاحظات</label><textarea class="field" id="eventDescription" rows="3" maxlength="1200" placeholder="تفاصيل إضافية..."></textarea></div>
    </div>
    <div class="form-actions"><button class="btn primary" type="submit" id="saveEventButton">حفظ الموعد</button><button class="btn ghost" type="button" id="cancelEventText">إلغاء</button></div>
    <p class="note" id="storageNote">تُحفظ المواعيد محليًا على هذا الجهاز، ولا تتم مزامنتها مع أجهزة أخرى.</p>
  </form>
</div>
</div>

<div class="modal" id="settingsModal" role="dialog" aria-modal="true" aria-labelledby="settingsTitle">
<div class="modal-box">
  <div class="modal-head"><h3 id="settingsTitle">إعدادات Eisen Calendar</h3><button class="icon-btn" id="closeSettingsButton" aria-label="إغلاق">×</button></div>
  <div class="form-group"><label id="languageLabel" for="languageSelect">لغة التطبيق</label><select class="field" id="languageSelect"><option value="ar">العربية</option><option value="en">English</option><option value="fr">Français</option></select></div>
  <div class="settings-section">
    <div class="form-group"><label id="weekStartLabel" for="weekStartSelect">بداية الأسبوع</label><select class="field" id="weekStartSelect"><option value="6">السبت</option><option value="0">الأحد</option><option value="1">الاثنين</option></select></div>
    <div class="form-group" style="margin-top:13px"><label id="hijriAdjustmentLabel" for="hijriAdjustment">تعديل التاريخ الهجري</label><select class="field" id="hijriAdjustment"><option value="-2">−2</option><option value="-1">−1</option><option value="0">0</option><option value="1">+1</option><option value="2">+2</option></select></div>
  </div>
  <div class="settings-section">
    <button class="btn" id="exportButton" style="width:100%;text-align:start">⇩ <span id="exportText">تصدير المواعيد</span></button>
    <div style="height:9px"></div>
    <label id="importLabel" for="importFile">استعادة المواعيد من ملف JSON</label><input class="field" id="importFile" type="file" accept=".json,application/json">
  </div>
  <p class="note" id="settingsNote">التقويم الهجري المعروض يعتمد على حساب المتصفح، وقد يختلف عن التقويم الرسمي المحلي.</p>
  <div class="form-actions"><button class="btn primary" id="saveSettingsButton">حفظ الإعدادات</button><button class="btn ghost" id="closeSettingsText">إغلاق</button></div>
</div>
</div>

<nav class="bottom-nav" aria-label="التنقل">
<button class="nav-btn active" data-nav="calendar"><span>▦</span><b id="navCalendar">التقويم</b></button>
<button class="nav-btn" data-nav="search"><span>⌕</span><b id="navSearch">البحث</b></button>
<button class="nav-btn" data-nav="islamic"><span>☾</span><b id="navIslamic">المناسبات</b></button>
<button class="nav-btn" data-settings><span>⚙</span><b id="navSettings">الإعدادات</b></button>
</nav>
<div class="toast" id="toast" role="status" aria-live="polite"></div>

<script>
"use strict";
const $=id=>document.getElementById(id);
const STORAGE_EVENTS="eisen_calendar_events_v1";
const STORAGE_SETTINGS="eisen_calendar_settings_v1";

const translations={
ar:{
dir:"rtl",subtitle:"تقويمك الذكي، كل أيامك في مكان واحد",greeting:"نظّم وقتك، وامتلك يومك.",welcomeText:"التاريخان الميلادي والهجري، والمواعيد والأحداث في مكان واحد.",
today:"اليوم",gregorian:"التاريخ الميلادي",gregSub:"التقويم الميلادي",hijri:"التاريخ الهجري",hijriSub:"قد يختلف حسب رؤية الهلال",saved:"المواعيد المحفوظة",savedSub:"الأحداث على هذا الجهاز",month:"الشهر المعروض",monthSub:"خطط لأيامك القادمة",calendar:"التقويم",calendarHint:"اختر يومًا لعرض تفاصيله",todayLegend:"اليوم",eventLegend:"موعد محفوظ",holidayLegend:"مناسبة إسلامية",details:"تفاصيل اليوم",selectedHint:"اليوم المحدد في التقويم",add:"إضافة",upcoming:"المواعيد القادمة",upcomingHint:"الأحداث المحفوظة في تقويمك",tools:"أدوات التقويم",toolsHint:"كل ما تحتاجه لتنظيم وقتك",newEvent:"موعد جديد",newEventSub:"أضف حدثًا إلى تقويمك",search:"البحث",searchSub:"ابحث في أحداثك",islamic:"المناسبات الإسلامية",islamicSub:"رمضان والأعياد وغيرها",searchHeading:"البحث عن موعد",searchHint:"ابحث بالعنوان أو الوصف",searchPlaceholder:"اكتب اسم الموعد...",searchButton:"بحث",islamicHint:"تواريخ تقريبية حسب التقويم الهجري",islamicNote:"قد تختلف تواريخ المناسبات الهجرية يومًا بحسب رؤية الهلال والجهة الرسمية في بلدك.",footer:"وقتك، منظّم بطريقتك · Eisen Calendar",navSettings:"الإعدادات",addTitle:"إضافة موعد جديد",editTitle:"تعديل الموعد",titleLabel:"عنوان الموعد *",dateLabel:"التاريخ *",timeLabel:"الوقت",categoryLabel:"نوع الموعد",descriptionLabel:"ملاحظات",saveEvent:"حفظ الموعد",cancel:"إلغاء",storageNote:"تُحفظ المواعيد محليًا على هذا الجهاز، ولا تتم مزامنتها مع أجهزة أخرى.",settingsTitle:"إعدادات Eisen Calendar",language:"لغة التطبيق",weekStart:"بداية الأسبوع",hijriAdjustment:"تعديل التاريخ الهجري",export:"تصدير المواعيد",import:"استعادة المواعيد من ملف JSON",settingsNote:"التقويم الهجري المعروض يعتمد على حساب المتصفح، وقد يختلف عن التقويم الرسمي المحلي.",saveSettings:"حفظ الإعدادات",close:"إغلاق",personal:"شخصي",work:"عمل",family:"عائلي",religious:"ديني",other:"أخرى",noEvents:"لا توجد مواعيد في هذا اليوم.",noUpcoming:"لا توجد مواعيد قادمة. أضف موعدك الأول!",noSearch:"لم يتم العثور على مواعيد مطابقة.",noIslamic:"لا تتوفر مناسبات في هذه الفترة.",savedToast:"تم حفظ الموعد بنجاح.",deleted:"تم حذف الموعد.",confirmDelete:"هل تريد حذف هذا الموعد؟",settingsSaved:"تم حفظ الإعدادات.",exported:"تم تصدير نسخة احتياطية.",imported:"تم استيراد المواعيد.",invalidFile:"ملف غير صالح أو لا يحتوي على مواعيد صحيحة.",titleRequired:"يرجى كتابة عنوان الموعد.",searchEmpty:"اكتب كلمة للبحث.",months:["يناير","فبراير","مارس","أبريل","مايو","يونيو","يوليو","أغسطس","سبتمبر","أكتوبر","نوفمبر","ديسمبر"],weekdays:["الأحد","الاثنين","الثلاثاء","الأربعاء","الخميس","الجمعة","السبت"],hijriMonths:["محرم","صفر","ربيع الأول","ربيع الآخر","جمادى الأولى","جمادى الآخرة","رجب","شعبان","رمضان","شوال","ذو القعدة","ذو الحجة"],islamicNames:["رأس السنة الهجرية","عاشوراء","المولد النبوي","الإسراء والمعراج","النصف من شعبان","أول رمضان","عيد الفطر","يوم عرفة","عيد الأضحى"],todayAction:"العودة إلى اليوم"},
en:{
dir:"ltr",subtitle:"Your smart calendar, all your days in one place",greeting:"Organize your time. Own your day.",welcomeText:"Gregorian and Hijri dates, events and appointments in one place.",today:"Today",gregorian:"Gregorian date",gregSub:"Gregorian calendar",hijri:"Hijri date",hijriSub:"May vary by moon sighting",saved:"Saved appointments",savedSub:"Events on this device",month:"Displayed month",monthSub:"Plan your upcoming days",calendar:"Calendar",calendarHint:"Select a day to see its details",todayLegend:"Today",eventLegend:"Saved event",holidayLegend:"Islamic occasion",details:"Day details",selectedHint:"Selected calendar day",add:"Add",upcoming:"Upcoming events",upcomingHint:"Events saved in your calendar",tools:"Calendar tools",toolsHint:"Everything you need to organize your time",newEvent:"New event",newEventSub:"Add an event to your calendar",search:"Search",searchSub:"Search your events",islamic:"Islamic occasions",islamicSub:"Ramadan, Eid and more",searchHeading:"Find an event",searchHint:"Search by title or description",searchPlaceholder:"Enter an event name...",searchButton:"Search",islamicHint:"Approximate dates based on the Hijri calendar",islamicNote:"Islamic dates may vary by a day depending on moon sighting and local authorities.",footer:"Your time, organized your way · Eisen Calendar",navSettings:"Settings",addTitle:"Add a new event",editTitle:"Edit event",titleLabel:"Event title *",dateLabel:"Date *",timeLabel:"Time",categoryLabel:"Event type",descriptionLabel:"Notes",saveEvent:"Save event",cancel:"Cancel",storageNote:"Events are saved locally on this device and are not synced across devices.",settingsTitle:"Eisen Calendar settings",language:"App language",weekStart:"Week starts on",hijriAdjustment:"Hijri date adjustment",export:"Export events",import:"Restore events from JSON",settingsNote:"The Hijri calendar is calculated by your browser and may differ from local official calendars.",saveSettings:"Save settings",close:"Close",personal:"Personal",work:"Work",family:"Family",religious:"Religious",other:"Other",noEvents:"No events on this day.",noUpcoming:"No upcoming events. Add your first event!",noSearch:"No matching events found.",noIslamic:"No occasions available in this period.",savedToast:"Event saved successfully.",deleted:"Event deleted.",confirmDelete:"Delete this event?",settingsSaved:"Settings saved.",exported:"Backup exported.",imported:"Events imported.",invalidFile:"Invalid file or no valid events found.",titleRequired:"Please enter an event title.",searchEmpty:"Enter a search term.",months:["January","February","March","April","May","June","July","August","September","October","November","December"],weekdays:["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"],hijriMonths:["Muharram","Safar","Rabi I","Rabi II","Jumada I","Jumada II","Rajab","Shaban","Ramadan","Shawwal","Dhul Qadah","Dhul Hijjah"],islamicNames:["Islamic New Year","Ashura","Mawlid al-Nabi","Isra and Mi'raj","Mid-Sha'ban","First day of Ramadan","Eid al-Fitr","Day of Arafah","Eid al-Adha"],todayAction:"Return to today"},
fr:{
dir:"ltr",subtitle:"Votre calendrier intelligent, tous vos jours au même endroit",greeting:"Organisez votre temps.",welcomeText:"Dates grégoriennes et hégiriennes, événements et rendez-vous.",today:"Aujourd'hui",gregorian:"Date grégorienne",gregSub:"Calendrier grégorien",hijri:"Date hégirienne",hijriSub:"Peut varier selon l'observation lunaire",saved:"Rendez-vous enregistrés",savedSub:"Événements sur cet appareil",month:"Mois affiché",monthSub:"Planifiez les jours à venir",calendar:"Calendrier",calendarHint:"Choisissez un jour pour voir les détails",todayLegend:"Aujourd'hui",eventLegend:"Événement enregistré",holidayLegend:"Fête islamique",details:"Détails du jour",selectedHint:"Jour sélectionné",add:"Ajouter",upcoming:"Événements à venir",upcomingHint:"Événements de votre calendrier",tools:"Outils du calendrier",toolsHint:"Tout pour organiser votre temps",newEvent:"Nouveau rendez-vous",newEventSub:"Ajouter un événement",search:"Recherche",searchSub:"Rechercher vos événements",islamic:"Fêtes islamiques",islamicSub:"Ramadan, Aïd et plus",searchHeading:"Rechercher un événement",searchHint:"Par titre ou description",searchPlaceholder:"Nom de l'événement...",searchButton:"Rechercher",islamicHint:"Dates approximatives selon le calendrier hégirien",islamicNote:"Les dates peuvent varier selon l'observation lunaire et les autorités locales.",footer:"Votre temps, organisé à votre façon · Eisen Calendar",navSettings:"Paramètres",addTitle:"Ajouter un événement",editTitle:"Modifier l'événement",titleLabel:"Titre *",dateLabel:"Date *",timeLabel:"Heure",categoryLabel:"Type",descriptionLabel:"Notes",saveEvent:"Enregistrer",cancel:"Annuler",storageNote:"Les événements sont enregistrés sur cet appareil, sans synchronisation.",settingsTitle:"Paramètres Eisen Calendar",language:"Langue",weekStart:"Début de la semaine",hijriAdjustment:"Ajustement de la date hégirienne",export:"Exporter les événements",import:"Restaurer depuis un fichier JSON",settingsNote:"Le calendrier hégirien est calculé par le navigateur et peut différer du calendrier officiel local.",saveSettings:"Enregistrer",close:"Fermer",personal:"Personnel",work:"Travail",family:"Famille",religious:"Religieux",other:"Autre",noEvents:"Aucun événement ce jour.",noUpcoming:"Aucun événement à venir. Ajoutez votre premier rendez-vous !",noSearch:"Aucun résultat.",noIslamic:"Aucune occasion disponible pour cette période.",savedToast:"Événement enregistré.",deleted:"Événement supprimé.",confirmDelete:"Supprimer cet événement ?",settingsSaved:"Paramètres enregistrés.",exported:"Sauvegarde exportée.",imported:"Événements importés.",invalidFile:"Fichier invalide ou aucun événement valide.",titleRequired:"Veuillez saisir un titre.",searchEmpty:"Saisissez un terme.",months:["Janvier","Février","Mars","Avril","Mai","Juin","Juillet","Août","Septembre","Octobre","Novembre","Décembre"],weekdays:["Dimanche","Lundi","Mardi","Mercredi","Jeudi","Vendredi","Samedi"],hijriMonths:["Mouharram","Safar","Rabi I","Rabi II","Joumada I","Joumada II","Rajab","Chaabane","Ramadan","Chawwal","Dhou al-Qi'da","Dhou al-Hijja"],islamicNames:["Nouvel an hégirien","Achoura","Mawlid","Isra et Mi'raj","Mi-Chaabane","Premier jour du Ramadan","Aïd el-Fitr","Jour d'Arafat","Aïd el-Adha"],todayAction:"Revenir à aujourd'hui"}
};

const today=new Date();
let viewDate=new Date(today.getFullYear(),today.getMonth(),1);
let selectedDate=dateKey(today);
let settings=loadSettings();
let events=loadEvents();
let toastTimer;

function dateKey(d){return `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,"0")}-${String(d.getDate()).padStart(2,"0")}`}
function parseKey(key){const [y,m,d]=key.split("-").map(Number);return new Date(y,m-1,d,12)}
function shiftDate(d,n){const x=new Date(d.getFullYear(),d.getMonth(),d.getDate(),12);x.setDate(x.getDate()+n);return x}
function loadSettings(){try{const s=JSON.parse(localStorage.getItem(STORAGE_SETTINGS)||"{}");return{lang:["ar","en","fr"].includes(s.lang)?s.lang:"ar",weekStart:[0,1,6].includes(Number(s.weekStart))?Number(s.weekStart):6,hijriAdjustment:Math.max(-2,Math.min(2,Number(s.hijriAdjustment)||0))}}catch{return{lang:"ar",weekStart:6,hijriAdjustment:0}}}
function loadEvents(){try{const x=JSON.parse(localStorage.getItem(STORAGE_EVENTS)||"[]");if(!Array.isArray(x))return[];return x.filter(e=>e&&typeof e.id==="string"&&typeof e.title==="string"&&/^\d{4}-\d{2}-\d{2}$/.test(e.date)).map(e=>({...e,category:["personal","work","family","religious","other"].includes(e.category)?e.category:"other"}))}catch{return[]}}
function persistEvents(){try{localStorage.setItem(STORAGE_EVENTS,JSON.stringify(events));return true}catch{showToast("تعذر الحفظ. قد تكون مساحة التخزين ممتلئة.");return false}}
function T(){return translations[settings.lang]||translations.ar}
function safeText(s){return String(s??"").replace(/[&<>"']/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]))}
function formatDate(d,options={}){return new Intl.DateTimeFormat(settings.lang==="ar"?"ar-DZ":settings.lang==="fr"?"fr-FR":"en-GB",options).format(d)}
function hijriParts(date){try{const d=shiftDate(date,settings.hijriAdjustment);const parts=new Intl.DateTimeFormat("en-u-ca-islamic-umalqura-nu-latn",{day:"numeric",month:"numeric",year:"numeric"}).formatToParts(d);const o={};parts.forEach(p=>{if(p.type!=="literal")o[p.type]=Number(p.value)});if(o.day&&o.month&&o.year)return o}catch{}try{const parts=new Intl.DateTimeFormat("en-u-ca-islamic-nu-latn",{day:"numeric",month:"numeric",year:"numeric"}).formatToParts(shiftDate(date,settings.hijriAdjustment));const o={};parts.forEach(p=>{if(p.type!=="literal")o[p.type]=Number(p.value)});return o}catch{return null}}
function hijriText(date,short=false){
  const h=hijriParts(date);
  if(!h) return "—";
  const month=T().hijriMonths[h.month-1]||String(h.month);
  const suffix = (settings.lang==='ar') ? 'هـ' : 'AH';
  return short? String(h.day) : `${h.day} ${month} ${h.year} ${suffix}`;
}
function dateLabel(key){return formatDate(parseKey(key),{year:"numeric",month:"long",day:"numeric"})}
function isSameMonth(a,b){return a.getFullYear()===b.getFullYear()&&a.getMonth()===b.getMonth()}
function getIslamicHolidays(year){const names=T().islamicNames,results=[];let seen=new Set();const start=new Date(year,0,1,12),end=new Date(year+1,0,1,12);for(let d=new Date(start);d<end;d=shiftDate(d,1)){const h=hijriParts(d);if(!h)continue;if(h.day===1){const index=({1:0,9:5,10:6,12:7})[h.month];if(index!==undefined){const key=`${h.month}-${h.year}`;if(!seen.has(key)){seen.add(key);results.push({id:`holiday-${dateKey(d)}-${index}`,date:dateKey(d),title:names[index],category:"religious",islamic:true})}}}const occasions=[[1,10,1],[3,12,2],[7,27,3],[8,15,4],[12,9,7],[12,10,8]];for(const [m,day,index] of occasions){if(h.month===m&&h.day===day)results.push({id:`holiday-${dateKey(d)}-${index}`,date:dateKey(d),title:names[index],category:"religious",islamic:true})}}const unique=new Map();results.forEach(e=>unique.set(e.id,e));return[...unique.values()].sort((a,b)=>a.date.localeCompare(b.date))}
function allEvents(){const years=[viewDate.getFullYear()-1,today.getFullYear(),viewDate.getFullYear(),viewDate.getFullYear()+1];const holidays=[...new Set(years)].flatMap(getIslamicHolidays);return[...events,...holidays]}
function dayEvents(key){return allEvents().filter(e=>e.date===key).sort((a,b)=>(a.time||"").localeCompare(b.time||""))}
function eventMarkup(e,withDate=false){return `<div class="event"><div class="event-bar ${e.islamic?"islamic":""}"></div><div class="event-content"><strong>${safeText(e.title)}</strong><small>${withDate?safeText(dateLabel(e.date))+" · ":""}${e.time?safeText(e.time)+" · ":""}${safeText(T()[e.category]||e.category||"")}${e.description?"<br>"+safeText(e.description):""}</small></div>${e.islamic?"":`<div class="event-actions"><button type="button" data-edit="${safeText(e.id)}" aria-label="Edit">✎</button><button type="button" data-delete="${safeText(e.id)}" aria-label="Delete">×</button></div>`}</div>`}
function showToast(msg){$("toast").textContent=msg;$("toast").classList.add("show");clearTimeout(toastTimer);toastTimer=setTimeout(()=>$("toast").classList.remove("show"),2600)}
function renderStatic(){const t=T();document.documentElement.lang=settings.lang;document.documentElement.dir=t.dir;const map={brandSubtitle:"subtitle",greeting:"greeting",welcomeText:"welcomeText",addEventText:"add",statGregorianLabel:"gregorian",statGregorianSub:"gregSub",statHijriLabel:"hijri",statHijriSub:"hijriSub",statEventsLabel:"saved",statEventsSub:"savedSub",statMonthLabel:"month",statMonthSub:"monthSub",calendarHeading:"calendar",calendarHint:"calendarHint",legendToday:"todayLegend",legendEvent:"eventLegend",legendHoliday:"holidayLegend",detailsHeading:"details",selectedHint:"selectedHint",quickAddText:"add",upcomingHeading:"upcoming",upcomingHint:"upcomingHint",toolsHeading:"tools",toolsHint:"toolsHint",quickAddTitle:"newEvent",quickAddSub:"newEventSub",quickSearchTitle:"search",quickSearchSub:"searchSub",quickIslamicTitle:"islamic",quickIslamicSub:"islamicSub",searchHeading:"searchHeading",searchHint:"searchHint",searchButton:"searchButton",islamicHeading:"islamic",islamicHint:"islamicHint",islamicNote:"islamicNote",footerText:"footer",navCalendar:"calendar",navSearch:"search",navIslamic:"islamic",navSettings:"navSettings",eventTitleLabel:"titleLabel",eventDateLabel:"dateLabel",eventTimeLabel:"timeLabel",eventCategoryLabel:"categoryLabel",eventDescriptionLabel:"descriptionLabel",saveEventButton:"saveEvent",cancelEventText:"cancel",storageNote:"storageNote",settingsTitle:"settingsTitle",languageLabel:"language",weekStartLabel:"weekStart",hijriAdjustmentLabel:"hijriAdjustment",exportText:"export",importLabel:"import",settingsNote:"settingsNote",saveSettingsButton:"saveSettings",closeSettingsText:"close",todayButtonText:"todayAction"};for(const[id,key]of Object.entries(map))$(id).textContent=t[key];$("searchInput").placeholder=t.searchPlaceholder;$("eventTitle").placeholder=settings.lang==="en"?"e.g. Important meeting":settings.lang==="fr"?"Ex. réunion importante":"مثال: اجتماع مهم";$("eventDescription").placeholder=settings.lang==="en"?"Additional details...":settings.lang==="fr"?"Détails supplémentaires...":"تفاصيل إضافية...";$("languageSelect").value=settings.lang;$("weekStartSelect").value=String(settings.weekStart);$("hijriAdjustment").value=String(settings.hijriAdjustment);$("eventCategory").innerHTML=Object.entries({personal:t.personal,work:t.work,family:t.family,religious:t.religious,other:t.other}).map(([v,label])=>`<option value="${v}">${safeText(label)}</option>`).join("");}
function renderHeader(){const t=T();$("statGregorian").textContent=formatDate(today,{day:"numeric",month:"short",year:"numeric"});$("statHijri").textContent=hijriText(today);$("statEvents").textContent=events.length;$("statMonth").textContent=t.months[viewDate.getMonth()]}
function renderWeekdays(){const t=T();$("weekdays").innerHTML=Array.from({length:7},(_,i)=>{const index=(settings.weekStart+i)%7;return`<div class="weekday">${safeText(t.weekdays[index].slice(0,settings.lang==="ar"?2:3))}</div>`}).join("")}
function renderCalendar(){const t=T();renderWeekdays();$("monthTitle").textContent=`${t.months[viewDate.getMonth()]} ${viewDate.getFullYear()}`;const first=new Date(viewDate.getFullYear(),viewDate.getMonth(),1,12);const offset=(first.getDay()-settings.weekStart+7)%7;const start=shiftDate(first,-offset);let html="";for(let i=0;i<42;i++){const d=shiftDate(start,i),key=dateKey(d),same=isSameMonth(d,viewDate),list=dayEvents(key);html+=`<button class="day ${same?"":"outside"} ${key===dateKey(today)?"today":""} ${key===selectedDate?"selected":""} ${list.some(e=>!e.islamic)?"event-day":""} ${list.some(e=>e.islamic)?"holiday":""}" data-date="${key}" aria-label="${safeText(dateLabel(key))}"><span class="greg">${d.getDate()}</span><span class="hijri">${safeText(hijriText(d,true))}</span>${list.length?'<i class="dot"></i>':""}</button>`}$("calendarDays").innerHTML=html}
function renderSelected(){const d=parseKey(selectedDate),list=dayEvents(selectedDate);$("selectedWeekday").textContent=formatDate(d,{weekday:"long"});$("selectedGregorian").textContent=dateLabel(selectedDate);$("selectedHijri").textContent=hijriText(d);$("dayEvents").innerHTML=list.length?list.map(e=>eventMarkup(e)).join(""):`<div class="empty">${safeText(T().noEvents)}</div>`}
function renderUpcoming(){const list=allEvents().filter(e=>e.date>=dateKey(today)).sort((a,b)=>a.date.localeCompare(b.date)||(a.time||"").localeCompare(b.time||"")).filter((e,i,a)=>a.findIndex(x=>x.id===e.id&&x.date===e.date&&x.title===e.title)===i);$("upcomingEvents").innerHTML=list.length?list.slice(0,6).map(e=>eventMarkup(e,true)).join(""):`<div class="empty">${safeText(T().noUpcoming)}</div>`}
function renderSearch(){const t=T(),query=$("searchInput").value.trim().toLocaleLowerCase();if(!query){$("searchResults").innerHTML="";return}const results=events.filter(e=>e.title.toLocaleLowerCase().includes(query)||(e.description||"").toLocaleLowerCase().includes(query)).sort((a,b)=>a.date.localeCompare(b.date));$("searchResults").innerHTML=results.length?results.map(e=>eventMarkup(e,true)).join(""):`<div class="empty">${safeText(t.noSearch)}</div>`}
function renderIslamic(){const list=getIslamicHolidays(viewDate.getFullYear()).filter(e=>e.date>=dateKey(today)).slice(0,12);$("islamicEvents").innerHTML=list.length?list.map(e=>eventMarkup(e,true)).join(""):`<div class="empty">${safeText(T().noIslamic)}</div>`}
function renderAll(){renderStatic();renderHeader();renderCalendar();renderSelected();renderUpcoming();renderSearch();renderIslamic()}
function openModal(id=null){const t=T();$("eventForm").reset();$("eventId").value="";$("eventDate").value=selectedDate;$("eventCategory").value="personal";$("eventModalTitle").textContent=t.addTitle;if(id){const e=events.find(item=>item.id===id);if(!e)return;$("eventId").value=e.id;$("eventTitle").value=e.title;$("eventDate").value=e.date;$("eventTime").value=e.time||"";$("eventCategory").value=e.category||"personal";$("eventDescription").value=e.description||"";$("eventModalTitle").textContent=t.editTitle}$("eventModal").classList.add("open");$("eventTitle").focus()}
function closeModal(){$("eventModal").classList.remove("open")}
function saveEvent(e){e.preventDefault();const t=T(),title=$("eventTitle").value.trim(),date=$("eventDate").value;if(!title){showToast(t.titleRequired);$("eventTitle").focus();return}if(!date){$("eventDate").focus();return}const id=$("eventId").value,existing=id?events.find(e=>e.id===id):null;const event={id:id||(crypto.randomUUID?crypto.randomUUID():"event-"+Date.now()+"-"+Math.random().toString(36).slice(2)),title,date,time:$("eventTime").value,category:$("eventCategory").value,description:$("eventDescription").value.trim(),createdAt:existing?.createdAt||new Date().toISOString()};if(existing)events=events.map(e=>e.id===id?event:e);else events.push(event);if(!persistEvents())return;selectedDate=date;const d=parseKey(date);viewDate=new Date(d.getFullYear(),d.getMonth(),1);closeModal();renderAll();showToast(t.savedToast)}
function deleteEvent(id){const t=T();if(!confirm(t.confirmDelete))return;const old=events;events=events.filter(e=>e.id!==id);if(persistEvents()){renderAll();showToast(t.deleted)}else events=old}
function changeMonth(amount){viewDate=new Date(viewDate.getFullYear(),viewDate.getMonth()+amount,1);renderAll()}
function goToday(){viewDate=new Date(today.getFullYear(),today.getMonth(),1);selectedDate=dateKey(today);renderAll()}
function selectDate(key){selectedDate=key;const d=parseKey(key);if(!isSameMonth(d,viewDate))viewDate=new Date(d.getFullYear(),d.getMonth(),1);renderAll()}
function switchPage(page){document.querySelectorAll("[data-page]").forEach(el=>el.classList.toggle("active",el.dataset.page===page));document.querySelectorAll("[data-nav]").forEach(el=>el.classList.toggle("active",el.dataset.nav===page));if(page==="search")$("searchInput").focus();if(page==="islamic")renderIslamic()}
function openSettings(){$("settingsModal").classList.add("open")}
function closeSettings(){$("settingsModal").classList.remove("open")}
function saveSettings(){const t=T();settings.lang=$("languageSelect").value;settings.weekStart=Number($("weekStartSelect").value);settings.hijriAdjustment=Math.max(-2,Math.min(2,Number($("hijriAdjustment").value)||0));try{localStorage.setItem(STORAGE_SETTINGS,JSON.stringify(settings))}catch{showToast("تعذر حفظ الإعدادات على هذا الجهاز.");return}closeSettings();renderAll();showToast(t.settingsSaved)}
function exportEvents(){const t=T(),backup={app:"Eisen Calendar",version:1,exportedAt:new Date().toISOString(),settings,events};const blob=new Blob([JSON.stringify(backup,null,2)],{type:"application/json;charset=utf-8"});const url=URL.createObjectURL(blob),a=document.createElement("a");a.href=url;a.download="eisen-calendar-backup.json";document.body.appendChild(a);a.click();a.remove();setTimeout(()=>URL.revokeObjectURL(url),1000);showToast(t.exported)}
function importEvents(file){const t=T();if(!file)return;const reader=new FileReader();reader.onload=()=>{try{const data=JSON.parse(reader.result),imported=Array.isArray(data)?data:data.events;if(!Array.isArray(imported))throw Error("Invalid backup");const valid=imported.filter(e=>e&&typeof e.title==="string"&&e.title.trim()&&/^\d{4}-\d{2}-\d{2}$/.test(e.date)&&!Number.isNaN(parseKey(e.date).getTime())&&dateKey(parseKey(e.date))===e.date).map(e=>({id:typeof e.id==="string"&&e.id?e.id:"event-"+Date.now()+"-"+Math.random().toString(36).slice(2),title:e.title.trim(),date:e.date,time:typeof e.time==="string"?e.time:"",category:["personal","work","family","religious","other"].includes(e.category)?e.category:"other",description:typeof e.description==="string"?e.description:"",createdAt:e.createdAt||new Date().toISOString()}));if(!valid.length){showToast(t.invalidFile);return}const merged=new Map(events.map(e=>[e.id,e]));valid.forEach(e=>{let id=e.id;if(merged.has(id))id="import-"+Date.now()+"-"+Math.random().toString(36).slice(2);merged.set(id,{...e,id})});const old=events;events=[...merged.values()];if(!persistEvents()){events=old;return}renderAll();showToast(t.imported)}catch{showToast(t.invalidFile)}$("importFile").value=""};reader.onerror=()=>{showToast(t.invalidFile);$("importFile").value=""};reader.readAsText(file)}
function initializeCalendar(){renderAll();$("prevMonth").addEventListener("click",()=>changeMonth(-1));$("nextMonth").addEventListener("click",()=>changeMonth(1));$("todayButton").addEventListener("click",goToday);$("addEventButton").addEventListener("click",()=>openModal());$("quickAddButton").addEventListener("click",()=>openModal());$("toolAdd").addEventListener("click",()=>openModal());$("eventForm").addEventListener("submit",saveEvent);$("cancelEventButton").addEventListener("click",closeModal);$("cancelEventText").addEventListener("click",closeModal);$("closeSettingsButton").addEventListener("click",closeSettings);$("closeSettingsText").addEventListener("click",closeSettings);$("settingsButton").addEventListener("click",openSettings);$("saveSettingsButton").addEventListener("click",saveSettings);$("exportButton").addEventListener("click",exportEvents);$("importFile").addEventListener("change",e=>importEvents(e.target.files[0]));$("searchButton").addEventListener("click",()=>{if(!$("searchInput").value.trim()){showToast(T().searchEmpty);$("searchInput").focus();return}renderSearch()});$("searchInput").addEventListener("keydown",e=>{if(e.key==="Enter"){e.preventDefault();if(!$("searchInput").value.trim()){showToast(T().searchEmpty);return}renderSearch()}});$("searchInput").addEventListener("input",renderSearch);document.addEventListener("click",e=>{const dateButton=e.target.closest("[data-date]");if(dateButton){selectDate(dateButton.dataset.date);return}const editButton=e.target.closest("[data-edit]");if(editButton){openModal(editButton.dataset.edit);return}const deleteButton=e.target.closest("[data-delete]");if(deleteButton){deleteEvent(deleteButton.dataset.delete);return}const nav=e.target.closest("[data-nav]");if(nav){switchPage(nav.dataset.nav);return}if(e.target.closest("[data-quick-search]")){switchPage("search");return}if(e.target.closest("[data-quick-islamic]")){switchPage("islamic");return}if(e.target.closest("[data-settings]"))openSettings()});$("eventModal").addEventListener("click",e=>{if(e.target===$("eventModal"))closeModal()});$("settingsModal").addEventListener("click",e=>{if(e.target===$("settingsModal"))closeSettings()});document.addEventListener("keydown",e=>{if(e.key==="Escape"){closeModal();closeSettings()}})}
if(document.readyState==="loading")document.addEventListener("DOMContentLoaded",initializeCalendar);else initializeCalendar();
</script>
</body>
</html>
