<template>
    <Parent>
        <div class="row">
            <div class="col-12">
                <div class="page-title-box d-sm-flex align-items-center justify-content-between">
                    <h4 class="mb-sm-0 font-size-18">Input Data</h4>
                    <div class="page-title-right">Input / Input Data</div>
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col-12 my-3">
                <div class="row justify-content-center align-items-center">
                    <div class="col-lg-2">
                        <label for="inputPassword6" class="col-form-label">Banyak Sistem Antrian</label>
                    </div>
                    <div class="col-4 col-lg-2">
                        <input type="text" class="form-control" v-model="banyaknya">
                    </div>
                    <div class="col-auto">
                        <button class="btn btn-success" @click="banyakAntrian"><i class="bx bx-send"></i>Tambah</button>
                    </div>
                </div>
            </div>
        </div>
        <div class="card" v-for="(index, i) in banyak" :key="index">
            <div class="card-body">
                <div class="accordion accordion-flush" id="accordionFlushExample">
                    <div class="accordion-item">
                        <h2 class="accordion-header" id="flush-headingOne">
                            <button class="accordion-button fw-medium collapsed" type="button" data-bs-toggle="collapse"
                                :data-bs-target="'#flush-collapseOne' + i" aria-expanded="false"
                                aria-controls="flush-collapseOne">
                                Sistem {{ index }}
                            </button>
                        </h2>
                        <div :id="'flush-collapseOne' + i" class="accordion-collapse collapse"
                            aria-labelledby="flush-headingOne" data-bs-parent="#accordionFlushExample" style="">
                            <div class="accordion-body text-muted">
                                <div class="row mt-5">
                                    <div class="col-12 text-center">
                                        <div class="row g-3 justify-content-center align-items-center">
                                            <div class="col-4 col-lg-1"><label for="inputPassword6"
                                                    class="col-form-label">Jumlah Pelanggan</label>
                                            </div>
                                            <div class="col-4 col-lg-2">
                                                <input type="text" class="form-control" v-model="countSPelanggan[i]">
                                            </div>
                                            <div class="col-auto"><button class="btn btn-success"
                                                    @click="tambahPelanggan(i)"><i class="bx bx-send"></i>Tambah</button>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                <div class="row">
                                    <div class="col-12">
                                        <div class="table-responsive">
                                            <table
                                                class="align-middle table table-hover table-striped table-bordered text-center">
                                                <thead class="bg-white align-middle">
                                                    <tr>
                                                        <th>Pelanggan</th>
                                                        <th>Waktu Kedatangan</th>
                                                        <th>Mulai Pelayanan</th>
                                                        <th>Selesai Pelayanan</th>
                                                        <th>Lama Pelayanan</th>
                                                        <th>Pelanggan Menunggu</th>
                                                        <th>Petugas Diam</th>
                                                    </tr>
                                                </thead>
                                                <tbody>
                                                    <tr v-for="(index, item) in pelaggans[i]" :key="index">
                                                        <td>{{ index }}</td>
                                                        <td>
                                                            <div class="row justify-content-center">
                                                                <div class="col-5">
                                                                    <input type="text" name="waktu_kedatangan"
                                                                        id="waktu_kedatangan"
                                                                        class="form-control text-center"
                                                                        v-model="waktuKedatangan[i][item]"
                                                                        @change="hitungWaktu(i, item)">
                                                                </div>
                                                            </div>
                                                        </td>
                                                        <td>
                                                            <div class="row justify-content-center">
                                                                <div class="col-5">
                                                                    <input type="text" name="waktu_pelayanan"
                                                                        id="waktu_pelayanan"
                                                                        class="form-control text-center"
                                                                        v-model="waktuMulai[i][item]"
                                                                        @change="hitungWaktu(i, item)">
                                                                </div>
                                                            </div>
                                                        </td>
                                                        <td>
                                                            <div class="row justify-content-center">
                                                                <div class="col-5">
                                                                    <input type="text" name="waktu_selasaipelayanan"
                                                                        id="waktu_selasaipelayanan"
                                                                        class="form-control text-center"
                                                                        v-model="waktuSelesai[i][item]"
                                                                        @change="hitungWaktu(i, item)">
                                                                </div>
                                                            </div>
                                                        </td>
                                                        <td>
                                                            <div class="row justify-content-center">
                                                                <div class="col-5">
                                                                    <input type="text" name="waktu_lama" id="waktu_lama"
                                                                        class="form-control text-center"
                                                                        v-model="waktuLama[i][item]" disabled>
                                                                </div>
                                                            </div>
                                                        </td>
                                                        <td>
                                                            <div class="row justify-content-center">
                                                                <div class="col-5">
                                                                    <input type="text" name="waktu_meunggu"
                                                                        id="waktu_meunggu" class="form-control text-center"
                                                                        v-model="waktuMenunggu[i][item]" disabled>
                                                                </div>
                                                            </div>
                                                        </td>
                                                        <td>
                                                            <div class="row justify-content-center">
                                                                <div class="col-5">
                                                                    <input type="text" name="waktu_diam" id="waktu_diam"
                                                                        class="form-control text-center"
                                                                        v-model="waktuDiam[i][item]" disabled>
                                                                </div>
                                                            </div>
                                                        </td>
                                                    </tr>
                                                </tbody>
                                            </table>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col-12 text-center">
                <button class="btn btn-primary" @click="hitung"><i class="bx bx-send"></i> Hitung</button>
            </div>
        </div>
        <div class="alert alert-info mt-5">
            Waktu Antar Kedatangan: {{ waktuAntarKedatangan }} orang perjam
            <br>
            Waktu Pelayanan: {{ waktuPelayanan }} orang perjam
            <br>
            Utilitas Sistem: {{ utilitasSistem }}
            <br>
            Probabilitas Petugas Menganggur: {{ probabilitas }}
            <br>
            Rata - Rata Pelanggan Menunggu: {{ meanWq }}
            <br>
            Rata - Rata Pelanggan Dalam Sistem: {{ meanW }}
            <br>
            Rata - Rata Pelanggan Dalam Antrian: {{ meanLq }}
            <br>
            Rata - Rata Pelanggan Dalam Sistem: {{ meanL }}

        </div>
    </Parent>
</template>

<!-- import -->
<script setup lang="ts">
import { ref } from 'vue';
import Parent from './Parent.vue';

//Variabel Reaktif Vue 3
const banyaknya = ref();
const banyak = ref<number>();

//Fungsi untuk mengatur nilai 'banyak antrian'
function banyakAntrian() {
    banyak.value = parseInt(banyaknya.value);
}

//array yang di gunakan untuk menyimpan data setiap sistem antrian
const pelaggans = ref<any[]>([]);
const countSPelanggan = ref<[]>([]);
const waktuKedatangan = ref<any[][]>([]);
const waktuMulai = ref<any[][]>([]);
const waktuSelesai = ref<any[][]>([]);
const waktuLama = ref<any[][]>([]);
const waktuMenunggu = ref<any[][]>([]);
const waktuDiam = ref<any[][]>([]);

// Fungsi untuk menambah pelanggan ke sistem antrian
function tambahPelanggan(index: number) { //Mengisialisasi array berdasarkan jumlah pelanggan
    pelaggans.value[index] = parseInt(countSPelanggan.value[index]);
    waktuKedatangan.value[index] = [];
    waktuMulai.value[index] = [];
    waktuSelesai.value[index] = [];
    waktuLama.value[index] = [];
    waktuMenunggu.value[index] = [];
    waktuDiam.value[index] = [];
    for (let i = 0; i < countSPelanggan.value[index]; i++) {
        waktuKedatangan.value[index][i] = '';
        waktuMulai.value[index][i] = '';
        waktuSelesai.value[index][i] = '';
        waktuLama.value[index][i] = '';
        waktuMenunggu.value[index][i] = '';
        waktuDiam.value[index][i] = '';
    }
}

//Variabel untuk menyimpan waktu penyelesaian pelayanan
const selesai_pelayanan = ref<number>();

// Fungsi untuk menghitung berbagai metrik waktu untuk seorang pelanggan dalam sistem antrian
function hitungWaktu(index: number, item: number) {
    waktuLama.value[index][item] = waktuSelesai.value[index][item] - waktuMulai.value[index][item];
    waktuMenunggu.value[index][item] = waktuMulai.value[index][item] - waktuKedatangan.value[index][item];
    waktuDiam.value[index][item - 1] = waktuMulai.value[index][item] - waktuSelesai.value[index][item - 1];
    waktuDiam.value[index][item] = 0;
    selesai_pelayanan.value = waktuSelesai.value[index][item];
}

// Variabel untuk menyimpan metrik kinerja untuk sistem secara keseluruhan
const waktuAntarKedatangan = ref<number>(0);
const waktuPelayanan = ref<number>();
const utilitasSistem = ref<number>();
const probabilitas = ref<number>();
const meanLq = ref<number>();
const meanL = ref<number>();
const meanWq = ref<number>();
const meanW = ref<number>();

// Fungsi untuk melakukan perhitungan dan memperbarui metrik
function hitung() {
    let totalPelanggan = countSPelanggan.value!.reduce((a: any, b: any) => parseInt(a) + parseInt(b), 0);
    antarKedatangan(selesai_pelayanan.value!, banyak.value!, totalPelanggan);
    let totalPelayanan = lamaPelayanan();

    waktuPelayanan.value = Math.floor((totalPelayanan * 60) / totalPelanggan);
    waktuPelayanan.value = Math.floor(3600 / waktuPelayanan.value);
    utilitasSistem.value = Number((waktuAntarKedatangan.value / (banyak.value! * waktuPelayanan.value)).toFixed(2));

    probabilitas.value = probabilitasPelangganMenunggu(waktuAntarKedatangan!.value, waktuPelayanan.value, banyak.value!);

    meanLq.value = Number(lq(waktuAntarKedatangan!.value, waktuPelayanan.value, banyak.value!).toFixed(2));
    meanL.value = Number(l(waktuAntarKedatangan!.value, waktuPelayanan.value, banyak.value!).toFixed(2));
    meanWq.value = Number(wq(waktuAntarKedatangan!.value, waktuPelayanan.value, banyak.value!).toFixed(2));
    meanW.value = Number(W(waktuAntarKedatangan!.value, waktuPelayanan.value, banyak.value!).toFixed(2));
}

// Fungsi pembantu untuk menghitung waktu antar kedatangan
function antarKedatangan(selesai_pelayanan: number, banyak: number, totalPelanggan: number) {
    let result = 0;
    result = selesai_pelayanan * banyak;
    result = result * 60;
    result = result / totalPelanggan;
    waktuAntarKedatangan.value = Math.floor(3600 / result);
}

// Fungsi pembantu untuk menghitung total waktu layanan
function lamaPelayanan() {
    let totalPelayanan = 0;
    for (let i = 0; i < banyak.value!; i++) {
        totalPelayanan += waktuLama.value[i].reduce((a: any, b: any) => parseInt(a) + parseInt(b), 0);
    }
    return totalPelayanan;
}

// Fungsi pembantu untuk menghitung probabilitas seorang pelanggan menunggu
function probabilitasPelangganMenunggu(waktuAntarKedatangan: number, waktuPelayanan: number, bayakPetugas: number) {
    let result = 0;
    for (let i = 0; i < bayakPetugas; i++) {
        result += Math.pow(waktuAntarKedatangan / waktuPelayanan, i) / faktorial(i);
    }
    result += Math.pow(waktuAntarKedatangan / waktuPelayanan, bayakPetugas) / (faktorial(bayakPetugas) * (1 - (waktuAntarKedatangan / (bayakPetugas * waktuPelayanan))));
    return result;
}

function faktorial(n: number): number {
    if (n == 0) {
        return 1;
    } else {
        return n * faktorial(n - 1);
    }
}

// Fungsi pembantu untuk menghitung Lq (rata-rata jumlah pelanggan dalam antrian)
function lq(waktuAntarKedatangan: number, waktuPelayanan: number, bayakPetugas: number) {
    let result = 0;
    result = Math.pow(waktuAntarKedatangan / waktuPelayanan, bayakPetugas) * (waktuAntarKedatangan / (faktorial(bayakPetugas) * Math.pow(bayakPetugas * waktuPelayanan - waktuAntarKedatangan, 2)));
    return result;
}

// Fungsi pembantu untuk menghitung L (rata-rata jumlah pelanggan dalam sistem)
function l(waktuAntarKedatangan: number, waktuPelayanan: number, bayakPetugas: number) {
    let result = 0;
    result = lq(waktuAntarKedatangan, waktuPelayanan, bayakPetugas) + (waktuAntarKedatangan / waktuPelayanan);
    return result;
}

// Fungsi pembantu untuk menghitung Wq (rata-rata waktu seorang pelanggan menunggu)
function wq(waktuAntarKedatangan: number, waktuPelayanan: number, bayakPetugas: number) {
    let result = 0;
    result = lq(waktuAntarKedatangan, waktuPelayanan, bayakPetugas) / (waktuAntarKedatangan / waktuPelayanan);
    return result;
}

// Fungsi pembantu untuk menghitung W (rata-rata waktu seorang pelanggan dalam sistem)
function W(waktuAntarKedatangan: number, waktuPelayanan: number, bayakPetugas: number) {
    let result = 0;
    result = wq(waktuAntarKedatangan, waktuPelayanan, bayakPetugas) + (1 / waktuPelayanan);
    return result;
}
</script>