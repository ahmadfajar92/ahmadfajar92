# Quick Guide to Observer Pattern

Observer pattern sudah sangat umum dipakai sekarang. faktanya, sudah banyak library pattern ini tersedia di berbagai macam bahasa pemprograman. 
Dan ketika masuk kedalam dunia industri, pattern ini banyak di custom secara khusus untuk menunjang kebutuhan bisnis industri nya. mau tau kek gimana pattern ini ? scroll terus kebawah ye 😏.

## Apa itu Observer Pattern
Observer pattern ini merupakan design pattern yg menggambarkan hubungan antar 1 object (**Observable**) dengan banyak object (**Observer**) yang dimana ketika 1 object melakukan perubahan status, object - object yang terhubung dengan object tersebut akan mendapatkan pemberitahuan dan melakukan tindakan secara otomatis. agar lebih gampang di cerna mari kita bahas secara simple dan detail dalam 2 langkah.

## Step 1 : Keywords
Apaan si keywords ini, keywords ini method yang sangat simple biar kelean paham pattern ini dan bisa membedakan pattern ini dengan yang lain dan kalau bisa tulis di kertas, bakar lalu minum biar ingat terus 😛 wkwkwk.

### Keyword "Subject"
**Subject** ini adalah object (**Observable**) yang kita anggap sebagai sumber data, pengolah data, atau bisnis logic kita.

### Keyword "Register/Attach"
Register/attach ini merupakan fungsi yang dipakai object (**Observer**) untuk mendaftarkan diri mereka sendiri ke subject (**Observable**).

### Keyword "Notify"
Melakukan pemberitahuan kepada object (**Observer**), si subject (**Observable**) ini bisa melakukan "*push*" atau si object (**Observer**) yang melakukan "*poll*" semua tergantung seperti apa implementasi nya.

### Keyword "Update"
Object (**Observer**) melakukan perubahan status setelah mendapat "*Notify*" dari si subject (**Observable**).

## Step 2 : Jump to the Code

**note** : *disini sample code nya pakai bahasa pemprograman [Golang](https://golang.org/) ya biar kekinian* 😁

```
// Interfaces

// Observable interface
type Observable interface {
    Register()
    Notify()
}

// Observer interface
type Observer interface {
    Update(data interface{}) error
}


// Implementation

// TukangSayur struct implement Observable
type TukangSayur struct {
    Emaks []Observer
}

// NewTukangSayur func to initiate TukangSayur
func NewTukangSayur() Observable {
    return new(TukangSayur)
}

// Register func for emak connected with tukang sayur
func (ts *TukangSayur) Register(emak Observer) {
    ts.Emaks = append(ts.Emaks, emak)
}

// Notify func to notify emak that tukang sayur is have a fresh sayur
func (ts *TukangSayur) Notify(data interface) error {
    err := nil
    for _, emak := range ts.Emaks {
        err = emak.Update(data)
        if err != nil {
            break
        }
    }

    return err
}


type Emak struct {
    money Int
}

func NewEmak(money int) Observer {
    emak = new (Emak)
    emak.money = money

    return emak
}

func (emak *Emak) Update(sayur interface) error {
    err := nil
    // your emak logic here

    return nil
}

kangSayur = NewTukangSayur()
emakPopon = NewEmak(10000)
emakIjah = NewEmak(2000)

kangSayur.Register(emakPopon)
kangSayur.Register(emakIjah)

// logic to get fresh sayur then notify to all emak
// notify all emak
kangSayur.Notify(map[string]interface{}{
    "bayam": 5000,
    "tomat": 3000
})
```

Jadi dalam pattern ini terdapat 2 object utama yaitu *TukangSayur* (**Observable**) dan *Emak* (**Observer**) yang dimana *Emak* ini mendaftarkan dirinya ke *TukangSayur* untuk dapat update secara langsung tanpa harus selalu bertanya kepada *TukangSayur*. 
sekarang faham kan ? ga usah di jelasin kali ya detil code nya, cape boi 😌 mending kelean copy paste code itu terus run di IDE kelean. 

kalau mau lebih jelas soal Observer Pattern ini kaya apa kelean bisa cek [disini](https://refactoring.guru/design-patterns/observer) aja ya boi 😁

oke mungkin cukup disini penjelasan nya, semoga kelean minimal faham kek gimana pattern ini. Tengkyu boi 😘.
