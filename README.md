# Karnaugh Maze Game

Java ile yazılmış konsol tabanlı bir labirent oyunu. Oyuncu labirentte gezinerek mantık sembolleri (değişkenler ve operatörler) toplar, bunları bir **ikili ağaç (binary tree)** yapısında birleştirerek boolean bir ifade oluşturur ve son olarak bu ifadeyi bir **Karnaugh haritası** çözücüsüyle sadeleştirir.

Bu proje, bir okul dersi kapsamında (veri yapıları / nesne yönelimli programlama) proje ödevi olarak geliştirilmiştir.

## Oyun Akışı

Oyun üç ekran arasında geçiş yapar:

1. **Labirent Ekranı** — Oyuncu (`P`) labirentte dolaşır, mantık sembolleri (`A`, `B`, `C`, `D`, operatörler vb.) ve ateş topu (`@`) eşyalarını toplar. Labirentte oyuncuyu avlayan robotlar (`X`) da bulunur; robotlar zaman zaman rastgele gezinir, zaman zaman en yakın eşyaya doğru hareket eder.
2. **Ağaç Ekranı** — Toplanan semboller, tam ikili bir ağaç (31 düğümlü, derinlik 5) üzerinde yerleştirilir. Oyuncu ağaçta gezinip düğüm ekleyebilir, çıkarabilir ve sırt çantası (backpack) ile ağaç arasında sembol transfer edebilir.
3. **Tablo / Karnaugh Ekranı** — Tamamlanan ifade geçerliyse (doğru operatör/operand yapısı, yeterli derinlik ve değişken sayısı), doğruluk tablosu ve Karnaugh haritası hesaplanıp gösterilir; harita üzerinden ifade sadeleştirilir.

## Kontroller

### Labirent Ekranı
| Tuş | Aksiyon |
|---|---|
| ↑ ↓ ← → | Hareket |
| `M` | Depolama modunu değiştir (Ağaç / Sırt Çantası) |
| `Space` | Ateş topu fırlat |
| `1` | Labirent ekranına geç |
| `2` | Ağaç ekranına geç |

### Ağaç Ekranı
| Tuş | Aksiyon |
|---|---|
| `W` | Üst (ebeveyn) düğüme git |
| `A` | Sol çocuğa git |
| `D` | Sağ çocuğa git |
| `T` | Sırt çantasından sembolü ağaca yerleştir |
| `R` | Ağaçtaki sembolü sırt çantasına geri al |
| `F` | İfadeyi bitir ve Karnaugh ekranına geç (koşullar sağlanıyorsa puan kazandırır) |

## Proje Yapısı

- `GameEngine.java` — Ana oyun döngüsü, girdi işleme ve ekran yönetimi
- `GameElement.java` — Oyun nesneleri için temel sınıf (konum, sembol)
- `Player.java` — Oyuncu; can puanı, skor, ateş topu sayısı ve eşya toplama mantığı
- `XRobot.java` — Oyuncuyu avlayan/rastgele gezen robot davranışı
- `Symbol.java` — Mantık sembolleri (literal ve operatörler: `~ ^ v + > =`)
- `Expression.java` — İkili ağaçtan türetilen boolean ifade yapısı ve hesaplama mantığı
- `Tree.java` — 31 düğümlü sabit boyutlu ikili ağaç; ifade doğrulama ve infix/postfix çıktı üretimi
- `Backpack.java` — LIFO (yığın) mantığıyla çalışan sınırlı kapasiteli sembol deposu
- `DoublyLinkedList.java` — Skor tablosu için sıralı çift yönlü bağlı liste
- `Karnaugh.java` — Doğruluk tablosundan Karnaugh haritası oluşturma ve grup bulma (sadeleştirme) algoritması

## Nasıl Çalıştırılır

Proje, konsol tabanlı bir grafik kütüphanesi (`enigma.console`) kullanmaktadır. Dersin sağladığı proje şablonu/kütüphanesiyle birlikte derlenip çalıştırılmalıdır.

```bash
javac *.java
java GameEngine
```

## Notlar

- Bu proje eğitim amaçlıdır ve bir ders ödevi kapsamında geliştirilmiştir.
- Kod, ders kapsamında verilen "enigma.console" kütüphanesine bağımlıdır; bu kütüphane olmadan derlenemeyebilir.
