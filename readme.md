# Ödev 3

## Demo: [Uygulama Demosu](https://responsive-product.netlify.app/)

## Sıfırdan Responsive Ürün Vitrini

Bu projede HTML ve CSS kullanarak sıfırdan responsive (duyarlı) bir ürün listeleme vitrini oluşturdum. Her ürün, resim, isim, fiyat ve “Sepete Ekle” butonundan oluşan bir kart yapısında tasarlandı.

Uygulama içinde CSS değişkenlerini `:root` içerisinde tanımladım ve bu değişkenleri stil dosyamın farklı bölümlerinde kullanarak bütünlüklü ve yönetilebilir bir yapı oluşturdum. Renk teması olarak ağırlıklı olarak `grey` tonlarını tercih ettim.

Tüm kartları, CSS Grid sistemiyle ve `grid-template-columns` özelliğini kullanarak responsive olacak şekilde düzenledim. Böylece 6 ürünü farklı ekran boyutlarına göre dinamik şekilde gösterebilen bir yapı ortaya çıkmış oldu.

---

### Sayfa Başlığı (Responsive H1)

```css
#page-title {
  font-weight: 600;
  color: var(--grey-600);
  font-size: clamp(2rem, 5vw, 4rem);
  margin-bottom: 2rem;
}
```

```html
<h1>Yeni Ürün Listesi</h1>
```

Sayfa başlığını `h1` etiketi ile oluşturdum. Font boyutunu farklı ekran boyutlarına göre uyarlamak için `clamp()` fonksiyonunu kullandım. Bu sayede `font-size`, mobilde küçük, büyük ekranlarda ise daha büyük ama kontrollü bir şekilde ölçekleniyor oldu.

---

### Ürünleri Grid ile Yerleştirme

```css
.product-grid {
  display: grid;
  gap: 2rem;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  max-width: var(--view-width);
}
```

Bu CSS bloğu ile ürünleri bir grid düzeni içinde responsive şekilde yerleştirdim.

- `auto-fit`, ekran genişliğine sığabildiği kadar sütun yerleştirir.
- `minmax(350px, 1fr)`, her sütunun minimum 350px genişliğinde olmasını, uygun yer varsa 1fr kadar büyümesini sağlar.
- `max-width: 90vw` ile gridin genişliğini sınırlayarak sayfanın kenar boşluklarını korudum.

Böylece ekran küçüldükçe kartlar alta geçiyor, büyüdükçe yan yana diziliyor oldu.

---

### Ürün Kart Tasarımı

```css
.product-card {
  width: var(--view-width);
  max-width: 350px;
  border: 0.001rem solid var(--grey-300);
  border-radius: var(--borderRadius-100);
  box-shadow: var(--shadow-2);
  overflow: hidden;
  transition: 0.3s;
  margin: 15px auto;
  cursor: pointer;
}

.product-card:hover {
  transform: translateY(-4px);
  box-shadow: var(--shadow-4);
}
```

Ürün kartlarının genişliğini `max-width: 350px` ile sınırladım. Kartlara gölge (box-shadow), yuvarlatılmış kenarlar (border-radius) ve hover efekti verdim. Hover anında yukarı hafifçe yükseliyor ve gölgesi artıyor. Bu da kullanıcı deneyimini artırıyor.

---

### Ürün Görseli ve Badge

```css
.product-image {
  height: 200px;
  overflow: hidden;
  position: relative;
}

.product-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: all 0.5s;
  border-top-left-radius: var(--borderRadius-100);
  border-top-right-radius: var(--borderRadius-100);
}

.product-card:hover .product-image img {
  transform: scale(1.05);
}

.product-image .badge {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background-color: var(--red-100);
  border: 1px solid var(--red-50);
  padding: 0.625rem;
  border-radius: var(--borderRadius-50);
  box-shadow: var(--shadow-3);
}

.badge .badge-text {
  color: var(--grey-700);
  font-weight: 600;
  font-size: var(--small-text);
}
```

```html
<div class="product-image">
  <img
    src="https://images.unsplash.com/photo-1514342959091-2bffd8a7c4ba?w=500&auto=format&fit=crop&q=60"
  />
  <div class="badge">
    <p class="badge-text">Tükendi</p>
  </div>
</div>
```

Kartın üst kısmında ürün görseli yer alıyor. Resme `object-fit: cover` vererek taşma olmadan tüm alanı kaplamasını sağladım. Ayrıca hover anında hafif büyüme efekti verdim. "Tükendi" badge’ini resmin sağ üst köşesine `absolute` konumlandırarak yerleştirdim.

---

### Ürün Bilgileri ve Sepete Ekle Butonu

```css
.product-info {
  padding: 0.825rem 1.125rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.product-info h3 {
  font-weight: 600;
  color: var(--grey-600);
}

.price-text {
  font-size: var(--normal-text);
  font-weight: bold;
  color: var(--grey-600);
}

.price-btn {
  margin-top: 0.5rem;
  padding: 0.625rem;
  background: linear-gradient(45deg, var(--grey-400), var(--grey-500));
  border-radius: var(--borderRadius-50);
  border: none;
  color: var(--white);
  cursor: pointer;
  font-size: var(--small-text);
  transition: var(--transition);
}

.price-btn:hover {
  background: linear-gradient(45deg, var(--grey-500), var(--grey-600));
  transform: translateY(-4px);
  box-shadow: var(--shadow-3);
}
```

```html
<div class="product-info">
  <h3>MacBook Pro</h3>
  <p class="price-text">64.000,00 TL</p>
  <button class="price-btn">Sepete Ekle</button>
</div>
```

Ürün adını, fiyatını ve sepete ekle butonunu dikey şekilde hizalamak için `flex-direction: column` kullandım. Butonun arka planında `linear-gradient` kullandım, hover efektinde arka planı koyulaştırdım ve gölge verdim. Ayrıca `transform` ile butonun hover anında yukarı hareket etmesini sağladım.

---

## Uygulama Görseli

![Ürün Vitrini Ekran Görüntüsü](/images/product.png)

## Not

Bu uygulamada **media query kullanmadan**, sadece `clamp()` ve `grid-template-columns` gibi modern CSS özelliklerini kullanarak responsive bir yapı oluşturmaya çalıştım. Hem görsel hem de kod yapısı olarak sade ve etkili bir vitrin hazırlamış oldum.

---

## Kullandığım Kaynaklar

- [`clamp()` hakkında detaylı bilgi – MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/clamp)
- [CSS Grid ve `minmax()` kullanımı – Ahmad Shadeed](https://ishadeed.com/article/css-grid-minmax/)
- [Gradient renkler için faydalı araç – CSS Gradient](https://cssgradient.io/)
