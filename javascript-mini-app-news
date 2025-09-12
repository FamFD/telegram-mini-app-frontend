// Initialize Telegram Web App
let tg = window.Telegram.WebApp;
tg.expand();
tg.enableClosingConfirmation();

// Crypto conversion rates (contoh)
const CRYPTO_RATES = {
    usdt: 15500,
    btc: 950000000,
    eth: 55000000,
    bnb: 8500000,
    xrp: 8500,
    ton: 35000
};

// Wallet connection functionality
document.querySelector('.wallet-connect').addEventListener('click', function() {
    tg.showPopup({
        title: 'Connect Wallet',
        message: 'Choose your wallet provider to connect to RPChanger',
        buttons: [
            {id: 'metaMask', type: 'default', text: 'MetaMask'},
            {id: 'trustWallet', type: 'default', text: 'Trust Wallet'},
            {id: 'walletConnect', type: 'default', text: 'WalletConnect'},
            {type: 'cancel'}
        ]
    });
});

// Calculate crypto amount when IDR input changes
document.getElementById('amount').addEventListener('input', function() {
    calculateCryptoAmount();
});

// Update calculation when crypto type changes
document.getElementById('crypto').addEventListener('change', function() {
    calculateCryptoAmount();
    updateCryptoType();
});

// Calculate crypto amount based on IDR input
function calculateCryptoAmount() {
    const idrAmount = parseFloat(document.getElementById('amount').value) || 0;
    const cryptoType = document.getElementById('crypto').value;
    const cryptoAmount = idrAmount / CRYPTO_RATES[cryptoType];
    document.getElementById('crypto-amount').textContent = cryptoAmount.toFixed(6);
    
    // Update conversion rate text
    document.querySelector('.conversion-rate').textContent = `1 ${cryptoType.toUpperCase()} = Rp ${formatRupiah(CRYPTO_RATES[cryptoType])}`;
}

// Update crypto type display
function updateCryptoType() {
    const cryptoType = document.getElementById('crypto').value;
    document.getElementById('crypto-type').textContent = cryptoType.toUpperCase();
}

// Pay button functionality
document.querySelector('.pay-btn').addEventListener('click', function() {
    const idrAmount = document.getElementById('amount').value;
    const cryptoType = document.getElementById('crypto');
    const cryptoText = cryptoType.options[cryptoType.selectedIndex].text;
    const cryptoAmount = document.getElementById('crypto-amount').textContent;
    const bank = document.getElementById('bank');
    const bankText = bank.options[bank.selectedIndex].text;
    const accountNumber = document.getElementById('account-number').value;
    const accountName = document.getElementById('account-name').value;
    
    // Validasi form
    if (!idrAmount || idrAmount < 10000) {
        tg.showPopup({
            title: 'Error',
            message: 'Nominal minimal adalah Rp 10,000',
            buttons: [{type: 'ok'}]
        });
        return;
    }
    
    if (!bank.value) {
        tg.showPopup({
            title: 'Error',
            message: 'Silakan pilih metode pembayaran',
            buttons: [{type: 'ok'}]
        });
        return;
    }
    
    if (!accountNumber) {
        tg.showPopup({
            title: 'Error',
            message: 'Silakan masukkan nomor rekening/e-wallet',
            buttons: [{type: 'ok'}]
        });
        return;
    }
    
    if (!accountName) {
        tg.showPopup({
            title: 'Error',
            message: 'Silakan masukkan nama pemilik rekening',
            buttons: [{type: 'ok'}]
        });
        return;
    }
    
    // Tampilkan konfirmasi pembayaran
    tg.showPopup({
        title: 'Konfirmasi Penukaran',
        message: `Anda akan menerima Rp ${formatRupiah(idrAmount)} dengan mengirim ${cryptoAmount} ${cryptoText} melalui ${bankText}. Lanjutkan?`,
        buttons: [
            {id: 'confirm', type: 'default', text: 'Konfirmasi'},
            {type: 'cancel'}
        ]
    });
    
    // Handle konfirmasi pembayaran
    tg.onEvent('popupClosed', function(popupData) {
        if (popupData.button_id === 'confirm') {
            // Proses penukaran
            processExchange(idrAmount, cryptoAmount, cryptoText, bank.value, accountNumber, accountName);
        }
    });
});

// Format Rupiah
function formatRupiah(amount) {
    return new Intl.NumberFormat('id-ID', {
        minimumFractionDigits: 0
    }).format(amount);
}

// Process exchange
function processExchange(idrAmount, cryptoAmount, cryptoText, bank, accountNumber, accountName) {
    // Simulasi proses penukaran
    tg.showPopup({
        title: 'Memproses Penukaran',
        message: 'Sedang memproses penukaran Anda...',
        buttons: []
    });
    
    // Simulasi delay proses
    setTimeout(function() {
        tg.showPopup({
            title: 'Penukaran Berhasil',
            message: `Penukaran ${cryptoAmount} ${cryptoText} ke Rp ${formatRupiah(idrAmount)} telah berhasil. Dana akan dikirim ke rekening Anda dalam 1-5 menit.`,
            buttons: [{type: 'ok'}]
        });
        
        // Reset form
        document.getElementById('amount').value = '';
        document.getElementById('crypto-amount').textContent = '0';
        document.getElementById('bank').selectedIndex = 0;
        document.getElementById('account-number').value = '';
        document.getElementById('account-name').value = '';
    }, 3000);
}

// Animate elements on scroll
function animateOnScroll() {
    const elements = document.querySelectorAll('.stat-card, .feature-card');
    
    elements.forEach(element => {
        const position = element.getBoundingClientRect();
        
        if(position.top < window.innerHeight - 100) {
            element.style.opacity = 1;
            element.style.transform = 'translateY(0)';
        }
    });
}

// Initialize animation properties
document.querySelectorAll('.stat-card, .feature-card').forEach(element => {
    element.style.opacity = 0;
    element.style.transform = 'translateY(20px)';
    element.style.transition = 'opacity 0.5s ease, transform 0.5s ease';
});

// Initialize page
document.addEventListener('DOMContentLoaded', function() {
    updateCryptoType();
    window.addEventListener('scroll', animateOnScroll);
    animateOnScroll();
});