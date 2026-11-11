# FAST burchak detektori: jonli namoyish

Tasvirdagi muhim nuqtalarni (burchaklarni) **FAST** (Features from Accelerated Segment Test) algoritmi yordamida brauzerning o‘zida aniqlaydigan interaktiv dastur.

**🔗 Jonli sayt: https://fast-demo-pi.vercel.app/**

> «Kompyuter ko‘rishi» fani, 1-mustaqil ish: *«FAST algoritmi yordamida tasvirning muhim nuqtalarini ajratish»*
> Bajardi: **Sobirov Farrux**, 261-23 SIo‘ guruhi, Muhammad al-Xorazmiy nomidagi TATU

## Imkoniyatlari

- **Rasm yuklash** – istalgan JPG/PNG rasmni tanlash yoki oynaga sudrab tashlash.
- **Jonli parametrlar** – chegara `t` (threshold), ketma-ket piksellar soni `N` (9–12), NMS, Gauss shovqini va Gauss filtri. Har bir o‘zgarishda nuqtalar soni va ishlash vaqti darhol yangilanadi.
- **Lupa** – tasvirdagi istalgan pikselga bosilganda uning atrofidagi 16 pikselli Bresenham aylanasi ko‘rsatiladi: qizil – yorqinroq, ko‘k – qorong‘iroq, kulrang – o‘xshash. Shu yerda segment test shartining hisob-kitobi va xulosa («Burchak» / «Burchak emas») chiqadi.
- **Tezkor test statistikasi** – N = 12 da 1, 5, 9, 13-piksellar bo‘yicha tezkor tekshiruvdan o‘tgan piksellar ulushi.

## FAST qanday ishlaydi

1. Tekshirilayotgan **p** piksel atrofida radiusi 3 bo‘lgan 16 pikselli aylana olinadi.
2. Aylanadagi har bir piksel uch sinfdan biriga ajratiladi: `I > I_p + t` – yorqinroq, `I < I_p − t` – qorong‘iroq, aks holda – o‘xshash.
3. Aylanada **ketma-ket kamida N ta** piksel hammasi yorqinroq yoki hammasi qorong‘iroq bo‘lsa, **p – burchak**.
4. Bir burchak atrofidagi ortiqcha nuqtalar **Non-Maximum Suppression** (3×3 oynada eng katta javob) bilan olib tashlanadi. Javob: `V = max(Σ(I − I_p − t), Σ(I_p − I − t))`.

Algoritm JavaScript’da noldan yozilgan. Natijalari OpenCV’dagi `cv2.FastFeatureDetector` bilan tekshirilgan: NMS’siz holatda nuqtalar **100% mos** keladi (512×512 «camera» tasvirida, t = 25, N = 9: 4199 tadan 4199 ta).

## Ishga tushirish

Hech narsa o‘rnatish shart emas – `index.html` faylini brauzerda ochish kifoya. Dastur internetsiz ham ishlaydi (faqat shrift o‘zgaradi).

Sayt Vercel’da joylashtirilgan: https://fast-demo-pi.vercel.app/ (Framework Preset – `Other`, build buyrug‘i yo‘q).

## Manbalar

- E. Rosten, T. Drummond. *Machine Learning for High-Speed Corner Detection*. ECCV, 2006.
- E. Rosten, R. Porter, T. Drummond. *Faster and Better: A Machine Learning Approach to Corner Detection*. IEEE TPAMI, 2010.
- [OpenCV: FAST Algorithm for Corner Detection](https://docs.opencv.org/4.x/df/d0c/tutorial_py_fast.html)
