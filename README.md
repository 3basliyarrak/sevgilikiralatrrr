<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sevgili Kiralama Sitesi</title>
    <style>
        /* Genel Ayarlar */
        body {
            font-family: 'Poppins', sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(to bottom, #ffe6f0, #f3e6ff);
            color: #333;
        }

        /* Header */
        .header {
            background: linear-gradient(90deg, #ff8da1, #e88dff);
            color: white;
            text-align: center;
            padding: 30px 20px;
            font-size: 2rem;
            font-weight: bold;
            letter-spacing: 2px;
        }

        /* Menü */
        .menu {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 10px;
            background: #f9f9f9;
            padding: 15px 0;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        }
        .menu button {
            background-color: #ffdee9;
            border: none;
            padding: 10px 15px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: bold;
            color: #8a2be2;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        .menu button:hover {
            background-color: #e88dff;
            color: white;
        }

        /* Profil Kartları */
        .profiles {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            padding: 30px;
        }
        .profile-card {
            background: white;
            border: 2px solid #ff8da1;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .profile-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
        }
        .profile-card img {
            width: 90%;
            height: 300px;
            object-fit: cover;
        }
        .profile-card h3 {
            margin: 15px;
            font-size: 1.5rem;
            color: #ff4d6d;
        }
        .profile-card p {
            margin: 0 15px 5px;
            font-size: 0.9rem;
            color: #555;
        }
        .profile-card button {
            background-color: #ff8da1;
            color: white;
            border: none;
            padding: 10px;
            margin: 0 15px 15px;
            border-radius: 10px;
            font-size: 0.9rem;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        .profile-card button:hover {
            background-color: #e88dff;
        }

        /* Bakiye Bar */
        .balance-bar {
            background: #fff;
            padding: 10px;
            margin: 20px auto;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            text-align: center;
        }
        .balance-bar span {
            color: #8a2be2;
            font-weight: bold;
        }

         /* Hikaye Barı */
        .story-bar {
            display: flex;
            overflow-x: auto;
            padding: 10px 20px;
            background: #fff;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            margin: 20px auto;
            gap: 15px;
            scrollbar-width: none; /* Firefox */
        }
        .story-bar::-webkit-scrollbar {
            display: none; /* Chrome ve diğerleri */
        }

        .story-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            cursor: pointer;
            text-align: center;
        }
        .story-item img {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            border: 3px solid #ff4d6d;
            object-fit: cover;
            transition: transform 0.3s ease;
        }
        .story-item span {
            margin-top: 5px;
            font-size: 0.8rem;
            color: #333;
        }
        .story-item:hover img {
            transform: scale(1.1);
        }

        /* Modal */
        .story-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        .story-content {
            background: #fff;
            width: 80%;
            max-width: 500px;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            position: relative;
        }
        .story-content img {
            width: 100%;
            height: auto;
            border-radius: 10px;
        }
        .close-btn {
            position: absolute;
            top: 10px;
            right: 10px;
            background: #ff4d6d;
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 5px;
            cursor: pointer;
        }
        .close-btn:hover {
            background: #e60023;
        }


        /* IBAN Popup */
        .iban-popup {
            display: none;
            background: rgba(0, 0, 0, 0.7);
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            justify-content: center;
            align-items: center;
        }
        .iban-popup .content {
            background: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        }
        .iban-popup button {
            margin-top: 15px;
            padding: 10px 20px;
            border: none;
            background-color: #e88dff;
            color: white;
            border-radius: 5px;
            cursor: pointer;
        }
        .iban-popup button:hover {
            background-color: #ff4d6d;
        }

        /* Footer */
        .footer {
            text-align: center;
            padding: 20px;
            background-color: #ff8da1;
            color: white;
            font-size: 0.9rem;
            margin-top: 20px;
        }

        /* Responsive Tasarım */
        @media (max-width: 768px) {
            .menu button {
                padding: 10px 10px;
                font-size: 0.8rem;
            }
            .profile-card h3 {
                font-size: 1.2rem;
            }
            .profile-card p {
                font-size: 0.8rem;
            }
            .profile-card button {
                font-size: 0.8rem;
            }
        }

        .comments {
    display: none; /* Tüm yorumlar başlangıçta gizlenir */
        }

    </style>
</head>
<body>
    <div class="header">
        Sevgili Kirala
    </div>

    <div class="menu">
        <button onclick="showIBAN()">Bakiye Yükle</button>
        <button onclick="alert('Kiralananlarınız listeleniyor...')">Kiralananlar</button>
        <button onclick="alert('henüz birşey kiralamadınız.')">İade Talebi</button>
        <button onclick="alert('Şikayetlerinizi +62 821-2572-2628 WhatsApp adresine iletebilirsiniz.')">Şikayet</button>
        <button onclick="window.location.href='https://t.me/Kirala1237'">Destek</button>
        <button onclick="window.location.href='https://t.me/Kirala1237'">WhatsApp İletişim</button>
    </div>

    <div class="balance-bar">
        Mevcut Bakiyeniz: <span id="balance">0₺</span>
    </div>

    <div class="story-bar">
        <div class="story-item" onclick="showStory('cemile')">
            <img src="https://i.hizliresim.com/k928jsq.jpg" alt="Cemile Story">
            <span>Cemile</span>
        </div>
        <div class="story-item" onclick="showStory('ipek')">
            <img src="https://i.hizliresim.com/g6bwyv6.jpg" alt="İpek Story">
            <span>İpek</span>
        </div>
        <div class="story-item" onclick="showStory('eylül')">
            <img src="https://i.hizliresim.com/tju0o85.jpg" alt="Eylül Story">
            <span>Eylül</span>
        </div>
        <!-- Daha fazla hikaye -->
    </div>
    
    <!-- Hikaye Modal -->
    <div class="story-modal" id="storyModal">
        <div class="story-content">
            <button class="close-btn" onclick="closeStory()">X</button>
            <div class="story-images" id="storyImages"></div>
        </div>
    </div>
    

    <div class="profiles">
        <!-- Profil Kartları -->
        <div class="profile-card">
            <img src="https://i.hizliresim.com/k928jsq.jpg" alt="Profil Fotoğrafı">
            <h3>Cemile</h3>
            <p>Yaş: 25 | Boy: 1.72m | Kilo: 62kg | İl: Ankara</p>
            <p>Buluştuğu Kişi Sayısı: 3</p>
            <button onclick="kirala(3000)">Kirala (3000₺)</button>
            <button onclick="toggleComments(this)">Yorumları göster </button>
            <div class="comments" style="display: none;">
            <hr>
            <p>tirip falan çekemem diyene bire bir 👌</p>
            <hr>
            <p>dolandırılırım dıye korkuyordum gercekten geldı bulusmaya</p>
            <hr>
            <p>buluşma günü ıstanbula gıtmem gerekti iade talep etmeseydım ben de gorseydım bı nasıl afeet</p>
            <hr>
            <p>cinselik beklentisi olan avelere tavsiye etmıyorum 😂😂</p>
            <hr>
            </div>
        </div>
        <div class="profile-card">
            <img src="https://i.hizliresim.com/g6bwyv6.jpg" alt="Profil Fotoğrafı">
            <h3>İpek</h3>
            <p>Yaş: 22 | Boy: 1.64m | Kilo: 55kg İl: Kocaeli</p>
            <p>Buluştuğu Kişi Sayısı: 4</p>
            <button onclick="kirala(3000)">Kirala (3000₺)</button>
            <button onclick="toggleComments(this)">Yorumları göster </button>
            <div class="comments" style="display: none;">
            <hr>
            <p>iyi öpusuyor maaşım yatınca tekrar kiralıcam</p>
            <hr>
            <p>tırafık kazasında elımı kaybetım bu yuzden sevgılım benden ayrıldı yalnızlık çekiyordum güzel bir uygulama olmuş</p>
            <hr>
            <p>Satın alma yok mu kirala ne😂🤣😍</p>
            <hr>
            </div>
        </div>
        <div class="profile-card">
            <img src="https://i.hizliresim.com/tju0o85.jpg" alt="Profil Fotoğrafı">
            <h3>Eylül</h3>
            <p>Yaş: 26 | Boy: 1.67m | Kilo: 58kg İl: Antalya</p>
            <p>Buluştuğu Kişi Sayısı: 1</p>
            <button onclick="kirala(3000)">Kirala (3000₺)</button>
            <button onclick="toggleComments(this)">Yorumları göster </button>
            <div class="comments" style="display: none;">
            <hr>
            <p>uzman cavusum izinde güzel vakıt gecırdim çok guzel kız .</p>
            <hr>
            </div>
        </div>
        <div class="profile-card">
            <img src="https://i.hizliresim.com/4fpwpcs.jpg" alt="Profil Fotoğrafı">
            <h3>Beyza</h3>
            <p>Yaş: 23 | Boy: 1.70m | Kilo: 56kg İl: İzmir</p>
            <p>Buluştuğu Kişi Sayısı: 2</p>
            <button onclick="kirala(3000)">Kirala (3000₺)</button>
            <button onclick="toggleComments(this)">Yorumları göster </button>
            <div class="comments" style="display: none;">
            <hr>
            <p>eski sevgilimi kiralayacagım hıc aklıma gelmezdi</p>
            <hr>
            </div>
        </div>
        <div class="profile-card">
            <img src="https://i.hizliresim.com/1gw7pec.jpg" alt="Profil Fotoğrafı">
            <h3>Melis</h3>
            <p>Yaş: 24 | Boy: 1.66m | Kilo: 57kg İl: Manİsa</p>
            <p>Buluştuğu Kişi Sayısı: 1</p>
            <button onclick="kirala(3000)">Kirala (3000₺)</button>
            <button onclick="toggleComments(this)">Yorumları göster </button>
            <div class="comments" style="display: none;">
            <hr>
            <p>vermedi😒😁</p>
            <hr>
            </div>
        </div>
        <div class="profile-card">
            <img src="https://i.hizliresim.com/aucp93b.jpg" alt="Profil Fotoğrafı">
            <h3>Handan</h3>
            <p>Yaş: 23 | Boy: 1.67m | Kilo: 56kg İl: Konya</p>
            <p>Buluştuğu Kişi Sayısı: 0</p>
            <button onclick="kirala(3000)">Kirala (3000₺)</button>
            <button onclick="toggleComments(this)">Yorumları göster </button>
            <div class="comments" style="display: none;">
            </div>
        </div>
        <div class="profile-card">
            <img src="https://i.hizliresim.com/idmibut.jpg" alt="Profil Fotoğrafı">
            <h3>Elif</h3>
            <p>Yaş: 20 | Boy: 1.63m | Kilo: 54kg İl: Konya</p>
            <p>Buluştuğu Kişi Sayısı: 8</p>
            <button onclick="kirala(3000)">Kirala (3000₺)</button>
            <button onclick="toggleComments(this)">Yorumları göster </button>
            <div class="comments" style="display: none;">
            <hr>
            <p>konya şaşırtmıyor </p>
            <hr>
            <p>28 yaşina geldim ilk defa bır sevgilim oldu </p>
            <hr>
            <p>kırmızı don giyiyor </p>
            <hr>
            <p>iyi sikişiyor 💕😘</p>
            <hr>
            <p>tiktok ta buna benzer seyler gormustum ama ınanmamıstım gerçekmis </p>
            <hr>
            </div>
        </div>
        <div class="profile-card">
            <img src="https://i.hizliresim.com/3axegzm.jpg" alt="Profil Fotoğrafı">
            <h3>Fatma</h3>
            <p>Yaş: 30 | Boy: 1.68m | Kilo: 58kg İl: Istanbul</p>
            <p>Buluştuğu Kişi Sayısı: 3</p>
            <button onclick="kirala(3000)">Kirala (3000₺)</button>
            <button onclick="toggleComments(this)">Yorumları göster </button>
            <div class="comments" style="display: none;">
            <hr>
            <p>kizin evinde bulustuk güzel bir gundu 😁😍</p>
            <hr>
            <p>taş gibi karı</p>
            <hr>
            <p>benden daha isttekli cıktı 😜😊🤤</p>
            <hr>
            </div>
        </div>
    </div>


    <div class="footer">
        &copy; 2024 Sevgili Kiralama Sitesi - Tüm Hakları Saklıdır.
    </div>

    <div class="iban-popup" id="ibanPopup">
        <div class="content">
            <h3>Bakiye Yükleme Bilgileri</h3>
            <hr>
            <p>Ad Soyad: Enes BİNAN</p>
            <p>IBAN: <span id="iban">TR030001200951000001094961</span></p>
            <hr>
            <p>7/24 FAST</p>
            <button onclick="copyIBAN()">IBAN Kopyala</button>
            <button onclick="closeIBAN()">Kapat</button>
        </div>
    </div>

    <script>
        let bakiye = 0;

        // Tüm hikayeler
        const stories = {
            cemile: [
            "https://i.hizliresim.com/ry5y99d.jpg",
        ],
            ipek: [
                "https://i.hizliresim.com/b0gicin.jpeg?_gl=1*gz3a1b*_ga*Nzk0NzIxMzk5LjE3MzIxODIxNTk.*_ga_M9ZRXYS2YN*MTczMjU0NzU5NC40LjEuMTczMjU0NzkxOS41LjAuMA..",
                "https://example.com/story4.jpg"
        ],
            eylül: [
                "https://i.hizliresim.com/t56jdux.jpeg"
        ]
        };

        // Hikaye gösterme
            function showStory(name) {
            const storyModal = document.getElementById("storyModal");
            const storyImages = document.getElementById("storyImages");

        // Eski içerikleri temizle
            storyImages.innerHTML = "";

        // Yeni görselleri ekle
        if (stories[name]) {
            stories[name].forEach((src) => {
            const img = document.createElement("img");
            img.src = src;
            storyImages.appendChild(img);
        });
    }

        // Modal'ı göster
            storyModal.style.display = "flex";
        }

        // Hikaye kapatma
            function closeStory() {
            const storyModal = document.getElementById("storyModal");
            storyModal.style.display = "none";
        }


        function kirala(fiyat) {
            if (bakiye >= fiyat) {
                bakiye -= fiyat;
                document.getElementById("balance").innerText = `${bakiye}₺`;
                alert("Kiralama işlemi başarılı! İyi günler dileriz.");
            } else {
                alert("Yetersiz bakiye! Lütfen bakiye yükleyin.");
            }
        }

        function showIBAN() {
            document.getElementById("ibanPopup").style.display = "flex";
        }

        function closeIBAN() {
            document.getElementById("ibanPopup").style.display = "none";
        }

        function copyIBAN() {
            const ibanText = document.getElementById("iban").innerText;
            navigator.clipboard.writeText(ibanText).then(() => {
                alert("IBAN başarıyla kopyalandı!");
            }).catch(() => {
                alert("IBAN kopyalanamadı. Lütfen tekrar deneyin.");
            });
        }

        function toggleComments(button) {
    var comments = button.nextElementSibling; // Butonun hemen sonrasındaki yorum kısmını seçiyoruz

    // Yorumları açma/gizleme işlemi
    if (comments.style.display === "none" || comments.style.display === "") {
        comments.style.display = "block"; // Yorumları göster
        button.textContent = "Yorumları gizle"; // Buton metnini güncelle

        // Eğer "Yorum Yap" butonu yoksa oluştur
        if (!comments.querySelector(".comment-btn")) {
            var commentButton = document.createElement("button");
            commentButton.textContent = "Yorum Yap";
            commentButton.className = "comment-btn";
            commentButton.style.marginTop = "10px"; // Biraz boşluk eklemek için
            commentButton.onclick = function () {
                alert("Daha önce kiraladığınız bir kullanıcıya yorum yapabilirsiniz.");
            };
            comments.appendChild(commentButton);
        }
    } else {
        comments.style.display = "none"; // Yorumları gizle
        button.textContent = "Yorumları göster"; // Buton metnini güncelle
    }
        }

        function addAnonPrefix() {
    // Tüm yorum elemanlarını seç
    const comments = document.querySelectorAll('.comments p');
    
    // Her yorumun başına "Anon: " ekle
    comments.forEach(comment => {
        if (!comment.innerText.startsWith("Anon:")) {
            comment.innerText = "Anonim kullanıcı: " + comment.innerText;
        }
    });
}

// Sayfa yüklendiğinde "Anon:" eklemek için çağır
window.onload = function() {
    addAnonPrefix();
};


    </script>
</body>
</html>
