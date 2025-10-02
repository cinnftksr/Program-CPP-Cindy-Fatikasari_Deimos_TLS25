# Program-CPP-Cindy-Fatikasari_Deimos_TLS25
**2. Lost and Found**

    #include <iostream>
    using namespace std;

    // hitung panjang string 
    int panjang(string s) {
    int n = 0;
    while (s[n] != '\0') n++;
    return n;
    }

    // membalik string 
    string balik(string s) {
    int n = panjang(s);
    string hasil = "";
    for (int i = n - 1; i >= 0; i--) {
        hasil += s[i];
    }
    return hasil;
    }

    // cek huruf vokal 
    bool vokal(char c) {
    return (c=='a' || c=='i' || c=='u' || c=='e' || c=='o' ||
            c=='A' || c=='I' || c=='U' || c=='E' || c=='O');
    }

    // membuat sandi dari kata
    string buatSandi(string kata) {
    // buang huruf vokal
    string konsonan = "";
    for (int i = 0; kata[i] != '\0'; i++) {
        if (!vokal(kata[i])) konsonan += kata[i];
    }

    // membalik huruf konsonan yang tersisa
    string rev = balik(konsonan);

    // ambil kode ASCII pada huruf pertama
    int ascii = (int)kata[0];

    // sisipkan kode ASCII di tengah
    int n = panjang(rev);
    int pos = n / 2;
    string hasil = "";
    for (int i = 0; i < n; i++) {
        if (i == pos) hasil += to_string(ascii);
        hasil += rev[i];
    }
    if (n == 0) hasil += to_string(ascii);
    return hasil;
    }

    // membuat kata dari sandi
    string buatKata(string sandi) {
    string angka = "", huruf = "";
    for (int i = 0; sandi[i] != '\0'; i++) {
        if (sandi[i] >= '0' && sandi[i] <= '9') angka += sandi[i];
        else huruf += sandi[i];
    }

    // mengubah angka yang merupakan kode ASCII menjadi huruf
    int ascii = 0;
    for (int i = 0; angka[i] != '\0'; i++) {
        ascii = ascii * 10 + (angka[i] - '0');
    }
    char first = (char)ascii;

    // membalik huruf-huruf
    string rev = balik(huruf);

    // agar tidak terjadi huruf pertama berjumlah ganda
    if (panjang(rev) > 0 && rev[0] == first) return rev;
    else return rev;
    }

    int main() {
    while (true) {
        cout << "1. Buat sandi\n";
        cout << "2. Buat kata dari sandi\n";
        cout << "3. Selesai\n";
        cout << "Pilihan: ";

        int pilih; cin >> pilih;
        if (pilih == 1) {
            string kata;
            cout << "Masukkan kata: ";
            cin >> kata;
            cout << "Sandi: " << buatSandi(kata) << "\n";
        } else if (pilih == 2) {
            string sandi;
            cout << "Masukkan sandi: ";
            cin >> sandi;
            cout << "Kata: " << buatKata(sandi) << "\n";
            cout << "(Tambahkan huruf vokal dan tentukan kata asli yang paling rasional dan sesuai clue!)\n";
        } else if (pilih == 3) {
            cout << "Selesai.\n";
            break;
        } else {
            cout << "Pilihan salah!\n";
        }
    }
    }

**3. Strange Traffic Lights**

    #include <iostream>
    using namespace std;

    string warnaLampu(int detik) {
    // urutan warna lampu: kuning -> merah -> hijau
    int durasi[3] = {3, 80, 20};
    string warna[3] = {"Kuning", "Merah", "Hijau"};

    int mulai = 45;   // mulai dari lampu kuning
    int idx = 0;      // index 0 = kuning, 1 = merah, 2 = hijau

    int waktu = (detik - mulai);
    if (waktu < 0) return "?"; // sebelum 45 tidak terdefinisi

    // geser maju sesuai durasi
    while (waktu >= durasi[idx]) {
        waktu -= durasi[idx];      // kurangi sisa waktu
        idx = (idx + 1) % 3;       // pindah ke lampu berikutnya
    }

    return warna[idx];
    }

    int main() {
    int detik[] = {80, 135, 150, 212};
    for (int t : detik) {
        cout << "Pada detik ke-" << t << " lampu berwarna " << warnaLampu(t) << endl;
    }
    return 0;
}


