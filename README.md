const textInput = document.getElementById('textInput');
const fontSelect = document.getElementById('fontSelect');
const fontSize = document.getElementById('fontSize');
const preview = document.getElementById('preview');
const fontNameBadge = document.getElementById('fontNameBadge');
const copyBtn = document.getElementById('copyBtn');
const clearBtn = document.getElementById('clearBtn');
const sampleBtn = document.getElementById('sampleBtn');

const sampleText = `العقلُ هو خيرُ رفيقٍ، والجهدُ هو مفتاحُ النجاحِ.\n\nإذا أردت أن ترقى في حياتك، فابدأ اليومَ بخطوةٍ صغيرةٍ،\nثم اجعلها عادةً، ثم صِرْ قادراً على تحقيق ما تريده.`;

const fontMap = {
  Amiri: 'Amiri',
  'Noto Naskh Arabic': 'Noto Naskh Arabic',
  Tajawal: 'Tajawal',
  Cairo: 'Cairo',
  'Aref Ruqaa': 'Aref Ruqaa',
  Lateef: 'Lateef',
  'Scheherazade New': 'Scheherazade New',
  'Reem Kufi': 'Reem Kufi',
  'IBM Plex Sans Arabic': 'IBM Plex Sans Arabic'
};

function applyPreview() {
  const content = textInput.value.trim() || 'اكتب هنا';
  const selectedFont = fontSelect.value;
  preview.textContent = content;
  preview.style.fontFamily = '"' + selectedFont + '", "Segoe UI", sans-serif';
  preview.style.fontSize = `${fontSize.value}px`;
  fontNameBadge.textContent = fontMap[selectedFont] || selectedFont;
}

fontSelect.addEventListener('change', applyPreview);
fontSize.addEventListener('input', applyPreview);
textInput.addEventListener('input', applyPreview);

sampleBtn.addEventListener('click', () => {
  textInput.value = sampleText;
  applyPreview();
});

copyBtn.addEventListener('click', async () => {
  const text = textInput.value.trim();

  if (!text) {
    return;
  }

  try {
    await navigator.clipboard.writeText(text);
    copyBtn.textContent = 'تم النسخ';
    setTimeout(() => {
      copyBtn.textContent = 'نسخ النص';
    }, 1200);
  } catch (error) {
    copyBtn.textContent = 'فشل النسخ';
    setTimeout(() => {
      copyBtn.textContent = 'نسخ النص';
    }, 1200);
  }
});

clearBtn.addEventListener('click', () => {
  textInput.value = '';
  applyPreview();
  textInput.focus();
});

applyPreview();
