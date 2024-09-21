package com.mycompany.penjadwalanotomatis;

import java.util.ArrayList;
import java.util.Scanner;

public class PenjadwalanOtomatis {

    static class Jadwal {
        String mataKuliah;
        String hari;
        String jamMulai;
        String jamSelesai;

        public Jadwal(String mataKuliah, String hari, String jamMulai, String jamSelesai) {
            this.mataKuliah = mataKuliah;
            this.hari = hari;
            this.jamMulai = jamMulai;
            this.jamSelesai = jamSelesai;
        }
    }

    private static final ArrayList<Jadwal> jadwalKuliah = new ArrayList<>();
    private static final Scanner scanner = new Scanner(System.in);

    public static void tambahJadwalKuliah() {
        System.out.print("Masukkan Mata Kuliah: ");
        String mataKuliah = scanner.nextLine();
        System.out.print("Masukkan Hari: ");
        String hari = scanner.nextLine();   
        System.out.print("Masukkan Jam Mulai (format HH:MM): ");
        String jamMulai = scanner.nextLine();
        System.out.print("Masukkan Jam Selesai (format HH:MM): ");
        String jamSelesai = scanner.nextLine();

        if (jamMulai.compareTo(jamSelesai) >= 0) {
            System.out.println("Waktu mulai tidak boleh sama atau lebih dari waktu selesai. Jadwal tidak ditambahkan.");
            return;
        }

        jadwalKuliah.add(new Jadwal(mataKuliah, hari, jamMulai, jamSelesai));
        System.out.println("Jadwal kuliah berhasil ditambahkan.");
    }

    public static void lihatJadwal() {
        if (jadwalKuliah.isEmpty()) {
            System.out.println("Belum ada jadwal yang ditambahkan.");
            return;
        }

        String[] hariArray = {"Senin", "Selasa", "Rabu", "Kamis", "Jumat"};
        System.out.println("Jadwal Kuliah:");
        System.out.println("----------------------------------------------------------");

        for (String hari : hariArray) {
            System.out.println("Hari: " + hari);
            System.out.printf("%-20s %-15s\n", "Mata Kuliah", "Waktu");
            System.out.println("----------------------------------------------------------");
            boolean adaJadwal = false;

            for (Jadwal jadwal : jadwalKuliah) {
                if (jadwal.hari.equalsIgnoreCase(hari)) {
                    adaJadwal = true;
                    System.out.printf("%-20s %-15s\n", 
                        jadwal.mataKuliah, 
                        jadwal.jamMulai + " - " + jadwal.jamSelesai);
                }
            }

            if (!adaJadwal) {
                System.out.println("Tidak ada jadwal untuk hari ini.");
            }
            System.out.println();
        }
    }

    public static void hapusJadwal() {
        lihatJadwal();
        System.out.print("Masukkan indeks jadwal yang ingin dihapus (mulai dari 0): ");
        int index = scanner.nextInt();
        scanner.nextLine();  // Mengatasi newline setelah input angka

        if (index < 0 || index >= jadwalKuliah.size()) {
            System.out.println("Indeks tidak valid.");
            return;
        }

        Jadwal jadwalYangDihapus = jadwalKuliah.remove(index);
        System.out.println("Jadwal " + jadwalYangDihapus.mataKuliah + " pada hari " + jadwalYangDihapus.hari + " telah dihapus.");
    }

    public static void editJadwal() {
    System.out.print("Masukkan hari untuk melihat jadwal yang akan diedit: ");
    String hari = scanner.nextLine();

    boolean adaJadwal = false;
    for (Jadwal jadwal : jadwalKuliah) {
        if (jadwal.hari.equalsIgnoreCase(hari)) {
            adaJadwal = true;
            break;
        }
    }

    if (!adaJadwal) {
        System.out.println("Tidak ada jadwal kuliah pada hari " + hari + ".");
        return;
    }

    lihatJadwal();

    System.out.print("Masukkan indeks jadwal yang ingin diedit (mulai dari 0): ");
    int index = scanner.nextInt();
    scanner.nextLine(); // Mengatasi newline setelah input angka

    if (index < 0 || index >= jadwalKuliah.size()) {
        System.out.println("Indeks tidak valid.");
        return;
    }

    Jadwal jadwalYangDipilih = jadwalKuliah.get(index);
    System.out.println("Jadwal yang dipilih: " + jadwalYangDipilih);

    System.out.print("Masukkan Mata Kuliah baru (tekan Enter untuk tetap sama): ");
    String mataKuliahBaru = scanner.nextLine();
    System.out.print("Masukkan Jam Mulai baru (format HH:MM, tekan Enter untuk tetap sama): ");
    String jamMulaiBaru = scanner.nextLine();
    System.out.print("Masukkan Jam Selesai baru (format HH:MM, tekan Enter untuk tetap sama): ");
    String jamSelesaiBaru = scanner.nextLine();

    if (!mataKuliahBaru.isEmpty()) {
        jadwalYangDipilih.mataKuliah = mataKuliahBaru;
    }
    if (!jamMulaiBaru.isEmpty() && !jamSelesaiBaru.isEmpty()) {
        jadwalYangDipilih.jamMulai = jamMulaiBaru;
        jadwalYangDipilih.jamSelesai = jamSelesaiBaru;
    }

    System.out.println("Jadwal berhasil diupdate: " + jadwalYangDipilih);
}
    
    public static void main(String[] args) {
        jadwalKuliah.add(new Jadwal("DDPL", "Senin", "09:10", "10:40"));
        jadwalKuliah.add(new Jadwal("DMJK", "Senin", "10:50", "12:20"));
        jadwalKuliah.add(new Jadwal("TEKPER", "Senin", "13:00", "14:30"));
        
        jadwalKuliah.add(new Jadwal("MLTI", "Selasa", "13:00", "14:30"));
        
        jadwalKuliah.add(new Jadwal("DBD", "Rabu", "07:30", "09:00"));
        jadwalKuliah.add(new Jadwal("PBO", "Rabu", "09:10", "10:40"));
        jadwalKuliah.add(new Jadwal("DMPB", "Rabu", "10:50", "12:30"));
        
        jadwalKuliah.add(new Jadwal("BDL", "Kamis", "07:30", "09:00"));
        
        jadwalKuliah.add(new Jadwal("RO", "Jumat", "08:00", "09:30"));
        jadwalKuliah.add(new Jadwal("IMK", "Jumat", "10:00", "11:30"));

        int pilihan;

        do {
            System.out.println("\nMenu Jadwal Sederhana:");
            System.out.println("1. Tambah Jadwal Kuliah");
            System.out.println("2. Lihat Jadwal Kuliah");
            System.out.println("3. Edit Jadwal");
            System.out.println("4. Hapus Jadwal");
            System.out.println("5. Keluar");
            System.out.print("Pilih menu: ");
            pilihan = scanner.nextInt();
            scanner.nextLine();  // Mengatasi newline setelah input angka
            switch (pilihan) {
                case 1 -> tambahJadwalKuliah();
                case 2 -> lihatJadwal();
                case 3 -> editJadwal();
                case 4 -> hapusJadwal();
                case 5 -> System.out.println("Keluar dari program.");
                default -> System.out.println("Pilihan tidak valid, coba lagi.");
            }
        } while (pilihan != 5);
    }
}
