<!DOCTYPE html>
<html lang="ku" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>SaleSnap — دروستکەرێ کارتا وەصلا بەرهەمی</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Noto+Naskh+Arabic:wght@400;500;600;700&display=swap" rel="stylesheet" />
  <style>
    body {
      font-family: 'Noto Naskh Arabic', -apple-system, BlinkMacSystemFont, sans-serif;
      background-color: #f3f5f8;
      color: #0f172a;
    }
    input[type="number"]::-webkit-inner-spin-button,
    input[type="number"]::-webkit-outer-spin-button {
      -webkit-appearance: none;
      margin: 0;
    }
    input[type="number"] {
      -moz-appearance: textfield;
    }
  </style>
</head>
<body class="min-h-screen pb-12">

  <!-- Top Header -->
  <header class="bg-white border-b border-slate-200 sticky top-0 z-30">
    <div class="max-w-5xl mx-auto px-4 py-3.5 flex items-center justify-between">
      <div class="flex items-center gap-2.5">
        <div class="w-9 h-9 rounded-xl bg-emerald-600 text-white flex items-center justify-center shadow-sm">
          <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M3 9a2 2 0 012-2h.93a2 2 0 001.664-.89l.812-1.22A2 2 0 0110.07 4h3.86a2 2 0 011.664.89l.812 1.22A2 2 0 0018.07 7H19a2 2 0 012 2v9a2 2 0 01-2 2H5a2 2 0 01-2-2V9z" />
            <path stroke-linecap="round" stroke-linejoin="round" d="M15 13a3 3 0 11-6 0 3 3 0 016 0z" />
          </svg>
        </div>
        <div>
          <h1 class="text-base font-bold tracking-tight text-slate-900 leading-tight">SaleSnap</h1>
          <p class="text-xs text-slate-500">دروستکەرێ وێنەی و وەصلا داخوازیا</p>
        </div>
      </div>

      <button id="resetBtn" type="button" class="text-xs font-semibold text-slate-600 hover:text-slate-900 bg-slate-100 hover:bg-slate-200 px-3 py-1.5 rounded-lg transition cursor-pointer">
        پاککرنا هەمیێ
      </button>
    </div>
  </header>

  <main class="max-w-5xl mx-auto px-4 pt-6 grid grid-cols-1 lg:grid-cols-12 gap-6 items-start">

    <!-- LEFT COLUMN: Photo Upload + Form -->
    <section class="lg:col-span-6 space-y-5">

      <!-- 1. Single Product Photo Upload -->
      <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-5">
        <div class="flex items-center justify-between mb-3">
          <span class="text-xs font-bold uppercase tracking-wider text-emerald-700 bg-emerald-50 px-2.5 py-1 rounded-md">
            ١. وێنەیێ بەرهەمی
          </span>
          <span class="text-xs text-slate-400">پەنجەی ل خانەی بدە یان وێنەی پێست بکە</span>
        </div>

        <div id="dropZone" class="relative rounded-xl border-2 border-dashed border-slate-300 hover:border-emerald-500 bg-slate-50 hover:bg-emerald-50/40 transition-all overflow-hidden">
          <!-- Single Direct Native File Input -->
          <input
            type="file"
            id="photoInput"
            accept="image/*"
            aria-label="وێنەیێ بەرهەمی هەلبژێرە"
            class="absolute inset-0 w-full h-full opacity-0 cursor-pointer z-20"
          />

          <!-- Empty State -->
          <div id="uploadPlaceholder" class="py-10 px-4 flex flex-col items-center justify-center text-center pointer-events-none select-none">
            <div class="w-12 h-12 rounded-full bg-white shadow-sm border border-slate-200 flex items-center justify-center text-emerald-600 mb-3">
              <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                <path stroke-linecap="round" stroke-linejoin="round" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
              </svg>
            </div>
            <p class="text-sm font-semibold text-slate-800">ل ڤێرێ بدە بو هەلبژارتن یان گرتنا وێنەیێ بەرهەمی</p>
            <p class="text-xs text-slate-500 mt-1">پشتەڤانیا JPG، PNG، WEBP، یان پێستکرنا ژ کلیبۆردێ دکەت</p>
          </div>

          <!-- Selected Image Preview -->
          <div id="uploadPreviewWrap" class="hidden relative bg-slate-900">
            <img id="uploadPreviewImg" alt="بەرهەمێ هەلبژارتی" class="w-full max-h-64 object-contain mx-auto pointer-events-none" />
            <div class="absolute bottom-3 left-3 z-30 flex gap-2">
              <button type="button" id="removePhotoBtn" class="bg-red-600/95 hover:bg-red-700 text-white text-xs font-semibold px-3 py-1.5 rounded-lg shadow cursor-pointer">
                لابرن
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- 2. Sale & Buyer Details -->
      <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-5 space-y-4">
        <div class="flex items-center justify-between">
          <span class="text-xs font-bold uppercase tracking-wider text-emerald-700 bg-emerald-50 px-2.5 py-1 rounded-md">
            ٢. پێزانینێن فروتنێ و کریاری
          </span>
        </div>

        <!-- Product Name -->
        <div>
          <label for="productName" class="block text-sm font-semibold text-slate-700 mb-1.5">ناڤێ بەرهەمی</label>
          <input
            type="text"
            id="productName"
            placeholder="بو نموونە: Samsung Galaxy S24 Ultra / کارتونا زەیتا زەیتوونا"
            class="w-full rounded-xl border border-slate-300 px-3.5 py-2.5 text-sm text-slate-900 placeholder-slate-400 focus:border-emerald-500 focus:ring-2 focus:ring-emerald-500/20 outline-none transition"
          />
        </div>

        <!-- Price per Box + Currency -->
        <div class="grid grid-cols-1 sm:grid-cols-12 gap-3">
          <div class="sm:col-span-8">
            <label for="boxPrice" class="block text-sm font-semibold text-slate-700 mb-1.5">بهایێ ئێک کارتۆنێ</label>
            <input
              type="text"
              inputmode="decimal"
              id="boxPrice"
              placeholder="بو نموونە: 25,000"
              class="w-full rounded-xl border border-slate-300 px-3.5 py-2.5 text-sm font-semibold text-slate-900 placeholder-slate-400 focus:border-emerald-500 focus:ring-2 focus:ring-emerald-500/20 outline-none transition"
            />
          </div>
          <div class="sm:col-span-4">
            <label for="currency" class="block text-sm font-semibold text-slate-700 mb-1.5">دراڤ</label>
            <select
              id="currency"
              class="w-full rounded-xl border border-slate-300 px-3 py-2.5 text-sm font-semibold text-slate-900 bg-white focus:border-emerald-500 focus:ring-2 focus:ring-emerald-500/20 outline-none transition"
            >
              <option value="IQD" selected>IQD (د.ع)</option>
              <option value="USD">USD ($)</option>
            </select>
          </div>
        </div>

        <!-- Amount of Boxes -->
        <div>
          <label for="boxAmount" class="block text-sm font-semibold text-slate-700 mb-1.5">هژمارا کارتۆنا</label>
          <div class="flex items-center gap-2">
            <button
              type="button"
              id="decreaseBoxBtn"
              aria-label="کێمکرنا کارتۆنا"
              class="w-11 h-11 rounded-xl border border-slate-300 bg-slate-50 hover:bg-slate-100 active:bg-slate-200 text-lg font-bold text-slate-700 flex items-center justify-center transition select-none cursor-pointer"
            >−</button>
            <input
              type="number"
              id="boxAmount"
              min="1"
              step="1"
              value="1"
              class="flex-1 text-center rounded-xl border border-slate-300 px-3.5 py-2.5 text-base font-bold text-slate-900 focus:border-emerald-500 focus:ring-2 focus:ring-emerald-500/20 outline-none transition"
            />
            <button
              type="button"
              id="increaseBoxBtn"
              aria-label="زێدەکرنا کارتۆنا"
              class="w-11 h-11 rounded-xl border border-slate-300 bg-slate-50 hover:bg-slate-100 active:bg-slate-200 text-lg font-bold text-slate-700 flex items-center justify-center transition select-none cursor-pointer"
            >+</button>
          </div>
        </div>

        <!-- Live Total Calculation Banner -->
        <div class="rounded-xl bg-emerald-50 border border-emerald-200 px-4 py-3 flex items-center justify-between">
          <div>
            <p class="text-xs font-semibold text-emerald-800">کویێ پارەی (هژمارا کارتۆنا × بهایێ کارتۆنێ)</p>
            <p id="formulaHint" class="text-xs text-emerald-600 mt-0.5">1 کارتۆن × 0 IQD</p>
          </div>
          <div class="text-left">
            <p id="totalDisplay" class="text-lg font-extrabold text-emerald-900 tracking-tight">0 IQD</p>
          </div>
        </div>

        <hr class="border-slate-100" />

        <!-- Buyer Name -->
        <div>
          <label for="buyerName" class="block text-sm font-semibold text-slate-700 mb-1.5">ناڤێ کریاری</label>
          <input
            type="text"
            id="buyerName"
            placeholder="بو نموونە: عەلی محەمەد"
            class="w-full rounded-xl border border-slate-300 px-3.5 py-2.5 text-sm text-slate-900 placeholder-slate-400 focus:border-emerald-500 focus:ring-2 focus:ring-emerald-500/20 outline-none transition"
          />
        </div>

        <!-- Iraqi Phone Number (+964) -->
        <div>
          <label for="buyerPhone" class="block text-sm font-semibold text-slate-700 mb-1.5">ژمارا تەلەفۆنا عێراقێ</label>
          <div dir="ltr" class="flex rounded-xl border border-slate-300 overflow-hidden focus-within:border-emerald-500 focus-within:ring-2 focus-within:ring-emerald-500/20 transition">
            <span class="inline-flex items-center gap-1.5 px-3.5 bg-slate-100 border-r border-slate-300 text-sm font-bold text-slate-700 select-none">
              <span>🇮🇶</span>
              <span>+964</span>
            </span>
            <input
              type="tel"
              inputmode="numeric"
              id="buyerPhone"
              maxlength="13"
              placeholder="750 123 4567"
              class="flex-1 px-3.5 py-2.5 text-sm font-semibold text-slate-900 placeholder-slate-400 outline-none text-left"
            />
          </div>
          <p class="text-[11px] text-slate-400 mt-1">سفرێ دەستپێکێ بخو دهێتە لابرن (بو نموونە: 0770... → +964 770...)</p>
        </div>
      </div>
    </section>

    <!-- RIGHT COLUMN: Live Receipt Preview + Save Button -->
    <section class="lg:col-span-6 space-y-4 lg:sticky lg:top-20">
      <div class="flex items-center justify-between">
        <span class="text-xs font-bold uppercase tracking-wider text-slate-600">
          ٣. دیتنا ڕاستەوخۆ یا کارتا هەڤبەرکری
        </span>
        <span id="previewDate" class="text-xs text-slate-400"></span>
      </div>

      <!-- Visual Preview Card -->
      <div class="bg-white rounded-2xl border border-slate-200 shadow-md overflow-hidden">
        <!-- Card Image Area -->
        <div class="bg-slate-900 relative flex items-center justify-center min-h-[220px] max-h-[320px] overflow-hidden">
          <img id="cardPreviewImg" alt="بەرهەم" class="hidden w-full max-h-[320px] object-contain" />
          <div id="cardPlaceholder" class="py-14 px-6 text-center text-slate-400">
            <svg xmlns="http://www.w3.org/2000/svg" class="w-10 h-10 mx-auto mb-2 opacity-50" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.6">
              <path stroke-linecap="round" stroke-linejoin="round" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
            </svg>
            <p class="text-xs font-medium">وێنەیێ بەرهەمی دێ ل ڤێرێ دیار بیت</p>
          </div>
        </div>

        <!-- Card Details Body -->
        <div class="p-5 space-y-4">
          <div class="flex items-start justify-between gap-3 border-b border-slate-100 pb-3.5">
            <div>
              <p class="text-[11px] font-bold uppercase tracking-wider text-emerald-600">بەرهەم</p>
              <h2 id="cardProductName" class="text-lg font-extrabold text-slate-900 mt-0.5">ناڤێ بەرهەمی</h2>
            </div>
            <span id="cardDateBadge" class="text-[11px] font-medium text-slate-500 bg-slate-100 px-2.5 py-1 rounded-md shrink-0"></span>
          </div>

          <!-- Boxes, Box Price, Total Money -->
          <div class="grid grid-cols-3 gap-2.5 bg-slate-50 rounded-xl p-3 border border-slate-100">
            <div>
              <p class="text-[11px] text-slate-500 font-medium">کارتۆن</p>
              <p id="cardBoxAmount" class="text-sm font-bold text-slate-900 mt-0.5">1 کارتۆن</p>
            </div>
            <div>
              <p class="text-[11px] text-slate-500 font-medium">بهایێ کارتۆنێ</p>
              <p id="cardBoxPrice" class="text-sm font-bold text-slate-900 mt-0.5">0 IQD</p>
            </div>
            <div class="text-left">
              <p class="text-[11px] text-emerald-700 font-semibold">کویێ پارەی</p>
              <p id="cardTotalMoney" class="text-sm font-extrabold text-emerald-700 mt-0.5">0 IQD</p>
            </div>
          </div>

          <!-- Buyer Info -->
          <div class="grid grid-cols-2 gap-3 pt-1">
            <div>
              <p class="text-[11px] text-slate-400 font-semibold uppercase tracking-wider">ناڤێ کریاری</p>
              <p id="cardBuyerName" class="text-sm font-bold text-slate-800 mt-0.5">—</p>
            </div>
            <div class="text-left">
              <p class="text-[11px] text-slate-400 font-semibold uppercase tracking-wider">ژمارا تەلەفۆنێ</p>
              <p id="cardBuyerPhone" dir="ltr" class="text-sm font-bold text-slate-800 mt-0.5">+964 —</p>
            </div>
          </div>
        </div>
      </div>

      <!-- Save & Share Action Buttons -->
      <div class="grid grid-cols-1 sm:grid-cols-2 gap-3 pt-1">
        <button
          type="button"
          id="saveBtn"
          class="w-full py-3.5 px-5 rounded-xl bg-emerald-600 hover:bg-emerald-700 active:bg-emerald-800 text-white font-bold text-sm shadow-sm flex items-center justify-center gap-2 transition cursor-pointer"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
          </svg>
          <span>خەزنکرنا وێنەی ب پێزانینا</span>
        </button>

        <button
          type="button"
          id="shareBtn"
          class="w-full py-3.5 px-5 rounded-xl bg-slate-900 hover:bg-slate-800 active:bg-slate-950 text-white font-bold text-sm shadow-sm flex items-center justify-center gap-2 transition cursor-pointer"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M8.684 13.342C8.886 12.938 9 12.482 9 12c0-.482-.114-.938-.316-1.342m0 2.684a3 3 0 110-2.684m0 2.684l6.632 3.316m-6.632-6l6.632-3.316m0 0a3 3 0 105.367-2.684 3 3 0 00-5.367 2.684zm0 9.316a3 3 0 105.368 2.684 3 3 0 00-5.368-2.684z" />
          </svg>
          <span>هنارتن بو کریاری</span>
        </button>
      </div>

      <p id="statusToast" class="hidden text-center text-xs font-semibold text-emerald-700 bg-emerald-50 border border-emerald-200 py-2 px-3 rounded-lg"></p>
    </section>

  </main>

  <script>
    const photoInput = document.getElementById('photoInput');
    const dropZone = document.getElementById('dropZone');
    const uploadPlaceholder = document.getElementById('uploadPlaceholder');
    const uploadPreviewWrap = document.getElementById('uploadPreviewWrap');
    const uploadPreviewImg = document.getElementById('uploadPreviewImg');
    const removePhotoBtn = document.getElementById('removePhotoBtn');

    const productNameInput = document.getElementById('productName');
    const boxPriceInput = document.getElementById('boxPrice');
    const currencySelect = document.getElementById('currency');
    const boxAmountInput = document.getElementById('boxAmount');
    const decreaseBoxBtn = document.getElementById('decreaseBoxBtn');
    const increaseBoxBtn = document.getElementById('increaseBoxBtn');
    const buyerNameInput = document.getElementById('buyerName');
    const buyerPhoneInput = document.getElementById('buyerPhone');

    const formulaHint = document.getElementById('formulaHint');
    const totalDisplay = document.getElementById('totalDisplay');

    const cardPreviewImg = document.getElementById('cardPreviewImg');
    const cardPlaceholder = document.getElementById('cardPlaceholder');
    const cardProductName = document.getElementById('cardProductName');
    const cardDateBadge = document.getElementById('cardDateBadge');
    const cardBoxAmount = document.getElementById('cardBoxAmount');
    const cardBoxPrice = document.getElementById('cardBoxPrice');
    const cardTotalMoney = document.getElementById('cardTotalMoney');
    const cardBuyerName = document.getElementById('cardBuyerName');
    const cardBuyerPhone = document.getElementById('cardBuyerPhone');

    const saveBtn = document.getElementById('saveBtn');
    const shareBtn = document.getElementById('shareBtn');
    const resetBtn = document.getElementById('resetBtn');
    const statusToast = document.getElementById('statusToast');

    let loadedImage = null;

    function getTodayFormatted() {
      const now = new Date();
      return now.toLocaleDateString('en-GB', { day: '2-digit', month: 'short', year: 'numeric' });
    }

    cardDateBadge.textContent = getTodayFormatted();

    function showToast(msg, isError = false) {
      statusToast.textContent = msg;
      statusToast.classList.remove('hidden', 'text-emerald-700', 'bg-emerald-50', 'border-emerald-200', 'text-red-700', 'bg-red-50', 'border-red-200');
      if (isError) {
        statusToast.classList.add('text-red-700', 'bg-red-50', 'border-red-200');
      } else {
        statusToast.classList.add('text-emerald-700', 'bg-emerald-50', 'border-emerald-200');
      }
      setTimeout(() => statusToast.classList.add('hidden'), 3500);
    }

    // Handle Image Loading
    function handleImageFile(file) {
      if (!file || !file.type.startsWith('image/')) return;
      const reader = new FileReader();
      reader.onload = (e) => {
        const img = new Image();
        img.onload = () => {
          loadedImage = img;
          uploadPreviewImg.src = e.target.result;
          uploadPlaceholder.classList.add('hidden');
          uploadPreviewWrap.classList.remove('hidden');

          cardPreviewImg.src = e.target.result;
          cardPreviewImg.classList.remove('hidden');
          cardPlaceholder.classList.add('hidden');
        };
        img.src = e.target.result;
      };
      reader.readAsDataURL(file);
    }

    photoInput.addEventListener('change', (e) => {
      if (e.target.files && e.target.files[0]) {
        handleImageFile(e.target.files[0]);
      }
    });

    // Drag & drop visual feedback
    dropZone.addEventListener('dragover', (e) => {
      e.preventDefault();
      dropZone.classList.add('border-emerald-500', 'bg-emerald-50/60');
    });
    dropZone.addEventListener('dragleave', () => {
      dropZone.classList.remove('border-emerald-500', 'bg-emerald-50/60');
    });
    dropZone.addEventListener('drop', (e) => {
      e.preventDefault();
      dropZone.classList.remove('border-emerald-500', 'bg-emerald-50/60');
      if (e.dataTransfer.files && e.dataTransfer.files[0]) {
        handleImageFile(e.dataTransfer.files[0]);
      }
    });

    // Clipboard paste support
    window.addEventListener('paste', (e) => {
      const items = e.clipboardData?.items;
      if (!items) return;
      for (const item of items) {
        if (item.type.startsWith('image/')) {
          handleImageFile(item.getAsFile());
          break;
        }
      }
    });

    removePhotoBtn.addEventListener('click', (e) => {
      e.stopPropagation();
      loadedImage = null;
      photoInput.value = '';
      uploadPreviewImg.src = '';
      uploadPreviewWrap.classList.add('hidden');
      uploadPlaceholder.classList.remove('hidden');

      cardPreviewImg.src = '';
      cardPreviewImg.classList.add('hidden');
      cardPlaceholder.classList.remove('hidden');
    });

    // Formatting Helpers
    function parseNumericValue(str) {
      const cleaned = String(str || '').replace(/[^0-9.]/g, '');
      const num = parseFloat(cleaned);
      return isNaN(num) ? 0 : num;
    }

    function formatMoney(num, currency) {
      const formatted = num.toLocaleString('en-US', {
        minimumFractionDigits: num % 1 === 0 ? 0 : 2,
        maximumFractionDigits: 2
      });
      return `${formatted} ${currency}`;
    }

    function formatBoxLabel(boxes) {
      return boxes === 1 ? '1 کارتۆن' : `${boxes} کارتۆن`;
    }

    function formatIraqiPhone(raw) {
      let digits = raw.replace(/\D/g, '');
      if (digits.startsWith('964')) digits = digits.slice(3);
      if (digits.startsWith('0')) digits = digits.slice(1);
      digits = digits.slice(0, 10);

      if (digits.length > 6) {
        return `${digits.slice(0, 3)} ${digits.slice(3, 6)} ${digits.slice(6)}`;
      } else if (digits.length > 3) {
        return `${digits.slice(0, 3)} ${digits.slice(3)}`;
      }
      return digits;
    }

    boxPriceInput.addEventListener('input', () => {
      const raw = boxPriceInput.value.replace(/[^0-9.]/g, '');
      const parts = raw.split('.');
      const intPart = parts[0] ? parseInt(parts[0], 10).toLocaleString('en-US') : '';
      boxPriceInput.value = parts.length > 1 ? `${intPart}.${parts[1].slice(0, 2)}` : intPart;
      updatePreview();
    });

    decreaseBoxBtn.addEventListener('click', () => {
      const current = Math.max(1, parseInt(boxAmountInput.value, 10) || 1);
      boxAmountInput.value = Math.max(1, current - 1);
      updatePreview();
    });

    increaseBoxBtn.addEventListener('click', () => {
      const current = Math.max(0, parseInt(boxAmountInput.value, 10) || 0);
      boxAmountInput.value = current + 1;
      updatePreview();
    });

    boxAmountInput.addEventListener('input', updatePreview);
    currencySelect.addEventListener('change', updatePreview);
    productNameInput.addEventListener('input', updatePreview);
    buyerNameInput.addEventListener('input', updatePreview);

    buyerPhoneInput.addEventListener('input', () => {
      buyerPhoneInput.value = formatIraqiPhone(buyerPhoneInput.value);
      updatePreview();
    });

    function updatePreview() {
      const product = productNameInput.value.trim() || 'ناڤێ بەرهەمی';
      const price = parseNumericValue(boxPriceInput.value);
      const boxes = Math.max(1, parseInt(boxAmountInput.value, 10) || 1);
      const currency = currencySelect.value;
      const total = price * boxes;

      const buyer = buyerNameInput.value.trim() || '—';
      const phone = buyerPhoneInput.value.trim();
      const fullPhone = phone ? `+964 ${phone}` : '+964 —';

      const formattedPrice = formatMoney(price, currency);
      const formattedTotal = formatMoney(total, currency);

      formulaHint.textContent = `${formatBoxLabel(boxes)} × ${formattedPrice}`;
      totalDisplay.textContent = formattedTotal;

      cardProductName.textContent = product;
      cardBoxAmount.textContent = formatBoxLabel(boxes);
      cardBoxPrice.textContent = formattedPrice;
      cardTotalMoney.textContent = formattedTotal;
      cardBuyerName.textContent = buyer;
      cardBuyerPhone.textContent = fullPhone;
    }

    // Generate High-Resolution Combined Receipt Canvas (RTL)
    function renderReceiptCanvas() {
      const width = 1080;
      const padding = 56;
      const innerWidth = width - padding * 2;

      // Determine image height proportionally
      let imgDrawHeight = 520;
      if (loadedImage) {
        const aspect = loadedImage.height / loadedImage.width;
        imgDrawHeight = Math.round(Math.min(760, Math.max(420, innerWidth * aspect)));
      }

      const detailsHeight = 520;
      const height = padding + imgDrawHeight + detailsHeight + padding;

      const canvas = document.createElement('canvas');
      canvas.width = width;
      canvas.height = height;
      const ctx = canvas.getContext('2d');

      // Outer background
      ctx.fillStyle = '#f1f5f9';
      ctx.fillRect(0, 0, width, height);

      // Card container
      const cardX = padding;
      const cardY = padding;
      const cardW = innerWidth;
      const cardH = height - padding * 2;
      const radius = 32;

      ctx.save();
      roundRect(ctx, cardX, cardY, cardW, cardH, radius);
      ctx.fillStyle = '#ffffff';
      ctx.fill();
      ctx.lineWidth = 3;
      ctx.strokeStyle = '#e2e8f0';
      ctx.stroke();
      ctx.clip();

      // Top Image Section
      ctx.fillStyle = '#0f172a';
      ctx.fillRect(cardX, cardY, cardW, imgDrawHeight);

      if (loadedImage) {
        const scale = Math.min(cardW / loadedImage.width, imgDrawHeight / loadedImage.height);
        const drawW = loadedImage.width * scale;
        const drawH = loadedImage.height * scale;
        const drawX = cardX + (cardW - drawW) / 2;
        const drawY = cardY + (imgDrawHeight - drawH) / 2;
        ctx.drawImage(loadedImage, drawX, drawY, drawW, drawH);
      } else {
        ctx.fillStyle = '#64748b';
        ctx.font = '600 30px "Noto Naskh Arabic", sans-serif';
        ctx.textAlign = 'center';
        ctx.fillText('چ وێنەیێن بەرهەمی نەهاتینە هەلبژارتن', cardX + cardW / 2, cardY + imgDrawHeight / 2);
      }

      // Details Section
      let curY = cardY + imgDrawHeight + 54;
      const rightX = cardX + cardW - 48;
      const leftX = cardX + 48;

      // Label: PRODUCT (Right) + Date (Left)
      ctx.textAlign = 'right';
      ctx.fillStyle = '#059669';
      ctx.font = '700 22px "Noto Naskh Arabic", sans-serif';
      ctx.fillText('بەرهەم', rightX, curY);

      ctx.textAlign = 'left';
      ctx.fillStyle = '#64748b';
      ctx.font = '600 22px "Noto Naskh Arabic", sans-serif';
      ctx.fillText(getTodayFormatted(), leftX, curY);

      curY += 52;
      ctx.textAlign = 'right';
      ctx.fillStyle = '#0f172a';
      ctx.font = '700 36px "Noto Naskh Arabic", sans-serif';
      const productText = productNameInput.value.trim() || 'ناڤێ بەرهەمی';
      ctx.fillText(truncateText(ctx, productText, cardW - 96), rightX, curY);

      // Divider
      curY += 32;
      ctx.strokeStyle = '#e2e8f0';
      ctx.lineWidth = 2;
      ctx.beginPath();
      ctx.moveTo(leftX, curY);
      ctx.lineTo(rightX, curY);
      ctx.stroke();

      // Highlight Box for Boxes, Price per Box, Total Money
      curY += 28;
      const boxH = 136;
      roundRect(ctx, leftX, curY, cardW - 96, boxH, 20);
      ctx.fillStyle = '#ecfdf5';
      ctx.fill();
      ctx.strokeStyle = '#a7f3d0';
      ctx.lineWidth = 2;
      ctx.stroke();

      const price = parseNumericValue(boxPriceInput.value);
      const boxes = Math.max(1, parseInt(boxAmountInput.value, 10) || 1);
      const currency = currencySelect.value;
      const total = price * boxes;

      const boxInnerW = cardW - 96;
      const colRightX = rightX - 32;
      const colMidX = rightX - boxInnerW * 0.36;
      const colLeftX = leftX + 32;

      // Col Right: Boxes
      ctx.textAlign = 'right';
      ctx.fillStyle = '#065f46';
      ctx.font = '600 22px "Noto Naskh Arabic", sans-serif';
      ctx.fillText('کارتۆن', colRightX, curY + 46);
      ctx.fillStyle = '#0f172a';
      ctx.font = '700 30px "Noto Naskh Arabic", sans-serif';
      ctx.fillText(formatBoxLabel(boxes), colRightX, curY + 98);

      // Col Middle: Price per Box
      ctx.textAlign = 'right';
      ctx.fillStyle = '#065f46';
      ctx.font = '600 22px "Noto Naskh Arabic", sans-serif';
      ctx.fillText('بهایێ کارتۆنێ', colMidX, curY + 46);
      ctx.fillStyle = '#0f172a';
      ctx.font = '700 28px "Noto Naskh Arabic", sans-serif';
      ctx.fillText(formatMoney(price, currency), colMidX, curY + 98);

      // Col Left: Total Money
      ctx.textAlign = 'left';
      ctx.fillStyle = '#047857';
      ctx.font = '700 22px "Noto Naskh Arabic", sans-serif';
      ctx.fillText('کویێ پارەی', colLeftX, curY + 46);
      ctx.fillStyle = '#064e3b';
      ctx.font = '700 32px "Noto Naskh Arabic", sans-serif';
      ctx.fillText(formatMoney(total, currency), colLeftX, curY + 98);

      // Buyer Name & Phone Row
      curY += boxH + 46;
      ctx.textAlign = 'right';
      ctx.fillStyle = '#64748b';
      ctx.font = '700 21px "Noto Naskh Arabic", sans-serif';
      ctx.fillText('ناڤێ کریاری', rightX, curY);

      ctx.textAlign = 'left';
      ctx.fillText('ژمارا تەلەفۆنێ (عێراق)', leftX, curY);

      curY += 46;
      const buyerText = buyerNameInput.value.trim() || '—';
      const phoneDigits = buyerPhoneInput.value.trim();
      const phoneText = phoneDigits ? `+964 ${phoneDigits}` : '+964 —';

      ctx.textAlign = 'right';
      ctx.fillStyle = '#0f172a';
      ctx.font = '700 30px "Noto Naskh Arabic", sans-serif';
      ctx.fillText(truncateText(ctx, buyerText, (cardW - 96) * 0.48), rightX, curY);

      ctx.textAlign = 'left';
      ctx.fillStyle = '#0f172a';
      ctx.font = '700 30px "Noto Naskh Arabic", sans-serif';
      ctx.fillText(phoneText, leftX, curY);

      ctx.restore();
      return canvas;
    }

    function roundRect(ctx, x, y, w, h, r) {
      ctx.beginPath();
      ctx.moveTo(x + r, y);
      ctx.arcTo(x + w, y, x + w, y + h, r);
      ctx.arcTo(x + w, y + h, x, y + h, r);
      ctx.arcTo(x, y + h, x, y, r);
      ctx.arcTo(x, y, x + w, y, r);
      ctx.closePath();
    }

    function truncateText(ctx, text, maxWidth) {
      if (ctx.measureText(text).width <= maxWidth) return text;
      let trimmed = text;
      while (trimmed.length > 0 && ctx.measureText(trimmed + '...').width > maxWidth) {
        trimmed = trimmed.slice(0, -1);
      }
      return trimmed + '...';
    }

    // Save Image Button
    saveBtn.addEventListener('click', () => {
      const canvas = renderReceiptCanvas();
      const safeName = (productNameInput.value.trim() || 'product-sale')
        .toLowerCase()
        .replace(/[^a-z0-9\u0600-\u06ff]+/g, '-')
        .replace(/^-|-$/g, '');

      canvas.toBlob((blob) => {
        if (!blob) return;
        const url = URL.createObjectURL(blob);
        const link = document.createElement('a');
        link.href = url;
        link.download = `${safeName || 'receipt'}-salesnap.png`;
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
        URL.revokeObjectURL(url);
        showToast('وێنە دگەل هەمی پێزانینێن بەرهەمی و کریاری هاتە خەزنکرن!');
      }, 'image/png');
    });

    // Share Button (Mobile / Supported Browsers)
    shareBtn.addEventListener('click', () => {
      const canvas = renderReceiptCanvas();
      canvas.toBlob(async (blob) => {
        if (!blob) return;
        const file = new File([blob], 'order-receipt.png', { type: 'image/png' });
        if (navigator.canShare && navigator.canShare({ files: [file] })) {
          try {
            await navigator.share({
              files: [file],
              title: productNameInput.value.trim() || 'داخوازیا بەرهەمی',
              text: `پێزانینێن داخوازیا کریاری: ${buyerNameInput.value.trim() || 'کریار'}`
            });
          } catch (err) {
            if (err.name !== 'AbortError') {
              showToast('لیستا هنارتنێ نەهاتە ڤەکرن. بکاربینە «خەزنکرنا وێنەی ب پێزانینا».', true);
            }
          }
        } else {
          // Fallback to download if Web Share with files isn't supported
          saveBtn.click();
        }
      }, 'image/png');
    });

    // Clear All
    resetBtn.addEventListener('click', () => {
      removePhotoBtn.click();
      productNameInput.value = '';
      boxPriceInput.value = '';
      boxAmountInput.value = '1';
      currencySelect.value = 'IQD';
      buyerNameInput.value = '';
      buyerPhoneInput.value = '';
      updatePreview();
      showToast('هەمی خانە هاتنە پاککرن.');
    });

    updatePreview();
  </script>
</body>
</html>
