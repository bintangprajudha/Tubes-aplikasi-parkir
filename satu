package main

import (
	"fmt"
)

type kendaraan struct {
	plat   string
	jm, jk waktu //jm = jam masuk, jk = jam keluar
	jenis  int
}

type waktu struct {
	jam, menit int
}

const kapasitasParkir = 40

type tabParkir [kapasitasParkir]kendaraan

func pilihOpsiParkir(opsi *int) {
	var n int
	fmt.Println("Selamat datang di parkiran")
	fmt.Println("Pilih opsi di bawah ini: ")
	fmt.Println("1. Masuk untuk parkir")
	fmt.Println("2. Keluar parkir")
	fmt.Println("3. Keluar aplikasi")
	fmt.Scan(&n)
	*opsi = n
}

func pilihJenisKendaraan() string {
	var k string
	fmt.Println("Masukkan jenis kendaraan (mobil/motor) atau tekan titik (.) untuk keluar:")
	fmt.Scan(&k)
	return k
}

func bacaIdentitasKendaraan(K *tabParkir, i int) {
		fmt.Println("Masukkan plat nomor kendaraan anda")
		fmt.Scan(&K[i].plat)

		fmt.Println("Masukkan waktu masuk (jam menit):")
		fmt.Scan(&K[i].jm.jam, &K[i].jm.menit)
}

func cetakTiket(jenis string, K tabParkir, i int) {
	fmt.Printf("kendaraan berjenis %v dengan plat nomor %v nomor nomor parkir", jenis, K[i].plat, 100 + i)
}

func cariIndexPlat(A tabParkir, plat string) int {
	var idx int
	idx = -1
	for i := 0; i < kapasitasParkir; i++ {
		if A[i].plat == plat {
			idx = i
		}
	}
	return idx
}

func hitungTarif(kendaraan string, durasi int) int {
	var tarif int
		if kendaraan == "mobil" {
			if durasi > 60 {
				tarif = 5000 + (durasi - 60)/60 * 2000
			} else {
				tarif = 5000
			}
		} else if kendaraan == "motor" {
			if durasi > 60 {
				tarif = 2000 + (durasi - 60)/60 * 500
			} else {
				tarif = 2000
			}
		}
		return tarif
}

func hitungWaktu(A tabParkir, i int) int {
	var durasi, jamMasuk, jamKeluar int
	jamMasuk = (A[i].jm.jam*60 + A[i].jm.menit)
	jamKeluar = (A[i].jk.jam*60 + A[i].jk.menit)
	durasi = jamMasuk - jamKeluar //dalam satuan menit
	return durasi
}

func cetakBuktiPembayaran(A tabParkir, tarif, uang int) {
	i := 0
	fmt.Println("PT Modar Jaya (PERSERO)")
	fmt.Println("Jalan Telekomunikasi No.1")
	fmt.Println("==========================")
	fmt.Println("No kendaraan:", A[i].plat)
	fmt.Println("Masuk:", A[i].jm.jam, A[i].jm.menit)
	fmt.Println("Keluar:", A[i].jk.jam, A[i].jk.menit)
	fmt.Println("Tarif:", tarif)
	fmt.Println("Bayar:", uang)
	fmt.Println("Kembali:", tarif - uang)
	fmt.Println("==========================")
	fmt.Println("Terima kasih - selamat jalan")
	
}

func main() {
	var mobil tabParkir
	var motor tabParkir
	var pendapatanMobil, pendapatanMotor, jumlahMobil, jumlahMotor, tarif int
	var kendaraan string
	var opsi int
	i := 0
	for {
		pilihOpsiParkir(&opsi)
		if opsi == 1 {
			//memilih masuk parkir
			kendaraan = pilihJenisKendaraan()
			if pilihJenisKendaraan() == "mobil" {
				bacaIdentitasKendaraan(&mobil, i)
				jumlahMobil++
				cetakTiket(kendaraan, mobil, i)				
			} else if kendaraan == "motor" {
				bacaIdentitasKendaraan(&motor, i)
				jumlahMotor++
				cetakTiket(kendaraan, motor, i)
			}
		} else if opsi == 2 {
			//memilih opsi keluar parkir
			var plat string
			var idx, durasi, money int
			kendaraan = pilihJenisKendaraan()
			fmt.Println("Masukkan plat nomor kendaraan anda")
			fmt.Scan(&plat)
			if kendaraan == "mobil" {
				idx = cariIndexPlat(mobil,plat)
				durasi = hitungWaktu(mobil, idx)
				tarif = hitungTarif(kendaraan, durasi)
				fmt.Println("Tarif parkir:", tarif)
				fmt.Println("Masukan nominal uang anda!")
				fmt.Scan(&money)
				cetakBuktiPembayaran(mobil, tarif, money)
			} else if kendaraan == "motor" {
				idx = cariIndexPlat(motor, plat)	
				durasi = hitungWaktu(motor, idx)
				tarif = hitungTarif(kendaraan, durasi)
				fmt.Println("Tarif parkir:", tarif)
				fmt.Println("Masukan nominal uang anda!")
				fmt.Scan(&money)
				cetakBuktiPembayaran(mobil, tarif, money)
			}
		} else if opsi == 3 {
				break
		} else if opsi == 4 {
			//ini fitur rahasia buat pengelola parkir
			fmt.Printf("Total pendapatan dari mobil: %d\n", pendapatanMobil)
			fmt.Printf("Total pendapatan dari motor: %d\n", pendapatanMotor)
			fmt.Printf("Jumlah mobil: %d\n", jumlahMobil)
			fmt.Printf("Jumlah motor: %d\n", jumlahMotor)
		}
		//ini kurang ngasih fitur buat pengelola aja sih
	}
}
