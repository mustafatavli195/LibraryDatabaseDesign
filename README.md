# Kütüphane Yönetim Sistemi

Bu proje, SQL kullanarak oluşturulmuş bir ilişkisel kütüphane veritabanı şeması ve bu veritabanıyla etkileşimde bulunmak için yazılmış bazı prosedür ve görünümleri içerir. Veritabanı, kütüphaneler için kitap, yazar, üye, ödünç verme, rezervasyon gibi çeşitli bilgileri yönetmeye yönelik tasarlanmıştır.

## İçindekiler

- [Özellikler](#özellikler)
- [Veritabanı Şeması](#veritabanı-şeması)
- [İlişkiler](#ilişkiler)
- [Prosedürler](#prosedürler)
- [Görünümler](#görünümler)
- [Kurulum](#kurulum)
- [Kullanım](#kullanım)
- [Yazarlar](#yazarlar)

## Özellikler

- **Adresler**: Kütüphane adres bilgilerini saklar.
- **Yayıncılar**: Kitapların yayıncı bilgilerini içerir.
- **Kategoriler**: Kitap kategorilerini tanımlar.
- **Yazarlar**: Kitap yazarlarının bilgilerini saklar.
- **Kitaplar**: Kütüphanedeki kitapları yönetir.
- **Kitap-Yazar İlişkileri**: Bir kitabın bir veya birden fazla yazarla ilişkisini belirler.
- **Üyeler**: Kütüphane üyelerinin bilgilerini tutar.
- **Kütüphane Personeli**: Kütüphane personelinin bilgilerini içerir.
- **Ödünç Verme**: Kitap ödünç verme işlemlerini yönetir.
- **Rezervasyonlar**: Kitap rezervasyonlarını takip eder.
- **Cezalar**: Gecikme cezalarını hesaplar ve kaydeder.

## Veritabanı Şeması

Veritabanı, aşağıdaki tabloları içerir:

- **Addresses**: Adres bilgileri.
- **Publishers**: Yayıncılar ve adres ilişkileri.
- **Categories**: Kitap kategorileri.
- **Authors**: Yazarlar.
- **Books**: Kitaplar, yayıncılar ve kategorilerle ilişkili.
- **BookAuthors**: Kitap ve yazar ilişkileri.
- **Members**: Üye bilgileri ve adres ilişkileri.
- **LibraryStaff**: Kütüphane personel bilgileri ve adres ilişkileri.
- **Loans**: Kitap ödünç verme bilgileri.
- **Reservations**: Kitap rezervasyon bilgileri.
- **Fines**: Geç teslim edilen kitaplar için cezalar.

## İlişkiler

Veritabanındaki tablolar arasındaki ilişkiler aşağıdaki gibidir:

- **Addresses** tablosu:
  - **Publishers** tablosu ile `AddressId` üzerinden ilişkilidir.
  - **Members** tablosu ile `AddressId` üzerinden ilişkilidir.
  - **LibraryStaff** tablosu ile `AddressId` üzerinden ilişkilidir.

- **Publishers** tablosu:
  - **Books** tablosu ile `PublisherId` üzerinden ilişkilidir.

- **Categories** tablosu:
  - **Books** tablosu ile `CategoryId` üzerinden ilişkilidir.

- **Authors** tablosu:
  - **BookAuthors** tablosu ile `AuthorId` üzerinden ilişkilidir.

- **Books** tablosu:
  - **BookAuthors** tablosu ile `BookId` üzerinden ilişkilidir.
  - **Loans** tablosu ile `BookId` üzerinden ilişkilidir.
  - **Reservations** tablosu ile `BookId` üzerinden ilişkilidir.

- **BookAuthors** tablosu:
  - **Books** tablosu ile `BookId` üzerinden ilişkilidir.
  - **Authors** tablosu ile `AuthorId` üzerinden ilişkilidir.

- **Members** tablosu:
  - **Loans** tablosu ile `MemberId` üzerinden ilişkilidir.
  - **Reservations** tablosu ile `MemberId` üzerinden ilişkilidir.

- **LibraryStaff** tablosu:
  - (Bu tabloda doğrudan ilişki kurulan başka bir tablo bulunmamaktadır.)

- **Loans** tablosu:
  - **Books** tablosu ile `BookId` üzerinden ilişkilidir.
  - **Members** tablosu ile `MemberId` üzerinden ilişkilidir.
  - **Fines** tablosu ile `LoanId` üzerinden ilişkilidir.

- **Reservations** tablosu:
  - **Books** tablosu ile `BookId` üzerinden ilişkilidir.
  - **Members** tablosu ile `MemberId` üzerinden ilişkilidir.

- **Fines** tablosu:
  - **Loans** tablosu ile `LoanId` üzerinden ilişkilidir.

## Prosedürler

Aşağıdaki saklı prosedürler tanımlanmıştır:

- **`BorrowBook`**: Bir kitabı ödünç verme işlemini gerçekleştirir.
- **`ReturnBook`**: Bir kitabın geri verilmesini ve gecikme cezasını hesaplar.
- **`GetBookAuthors`**: Bir kitabın yazarlarını listeler.

## Görünümler

Aşağıdaki görünümler tanımlanmıştır:

- **`BookStatus`**: Kitapların mevcut durumunu (ödünçte mi, mevcut mı) gösterir.
- **`MemberLoans`**: Üyelerin ödünç aldıkları kitapları ve detaylarını listeler.
- **`BooksByCategory`**: Kategorilere göre kitap sayısını gösterir.

## Kurulum

1. Veritabanını oluşturmak için SQL sorgularını çalıştırın.
2. Saklı prosedürleri ve görünümleri veritabanına ekleyin.

```sql
-- Veritabanını oluştur ve kullan
CREATE DATABASE IF NOT EXISTS LibraryDB;
USE LibraryDB;

-- Tablo ve prosedürleri ekleyin (sizin verdiğiniz SQL kodlarını burada kullanın)
