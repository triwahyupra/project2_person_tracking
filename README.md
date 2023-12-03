# Project 2: Person Tracking (Object Detection)

Proyek ini menampilkan beragam percobaan arsitektur dan algoritma Convolitional Neural Network (CNN) dalam Computer Vision melalui implementasi object detection menggunakan dataset COCO2017. Dengan melakukan eksperimen berbagai varian dari algoritma Faster RCNN dan YOLO, model ini dilatih untuk mendeteksi kelas person pada datset COCO2017.

## 🚀 Sorotan Utama:

    Teknik: Menggunakan teknik computer vision dengan library Pytorch dan OpenCV.
    Model: Faster RCNN dengan backbone GoogleNet, MobileNet dan ResNet50. YOLO dengan versi 3,5 dan 8.
    Kinerja: Mencapai prediksi terbaik dengan backbone ResNet50 pada Faster RCNN dan YOLOv8 pada YOLO.

Jelajahi kode dan hasil untuk mendapatkan wawasan tentang object detection kelas person!

📝 Catatan: Proyek ini merupakan bagian dari Bootcamp Computer Vision oleh Indonesia AI dan dikerjakan secara kolaboratif oleh kelompok CV B -Oppenheimer dan CV D -Alan Turing

## ★ Introduction

### Background

Dalam era perkembangan teknologi komputer dan kecerdasan buatan, pemantauan objek dan deteksi manusia menjadi fokus utama dalam berbagai aplikasi, termasuk keamanan lingkungan, pemantauan lalu lintas, sampai dengan sektor industri dan perdagangan. Sistem pelacakan manusia yang efektif menjadi kunci untuk meningkatkan keamanan dan efisiensi di berbagai kondisi lingkungan.

### Problem Statement

Dalam deteksi objek khususnya person tracking, terdapat beberapa tantangan dikarenakan perubahan pose dan interaksi antar objek dalam satu frame. Eksplorasi algoritma Faster RCNN dan YOLO diharapkan memberikan solusi terkait deteksi manusia yang cepat dan akurat. Proyek ini bertujuan mengatasi kendala deteksi dalam kerumunan, perubahan pose, dan pemantauan real-time, mendukung pengembangan sistem pelacakan manusia yang lebih efisien.
  
## ★ Getting Started

### 1. Data collection & Preparation

#### 🔍 Dataset : [COCO (Common Objects in Context)](https://cocodataset.org/#explore)

<img align="left" src="https://cocodataset.org/images/coco-logo.png" alt="Deskripsi Gambar" width="300" height="180">
Dataset diambil dari COCO (Common Objects in Context) menggunakan library Fiftyone. Dataset merupakan kumpulan data gambar yang berisi sekitar 118.287 gambar pelatihan (train images) dan 5.000 gambar validasi (val images). Setiap gambar di dalam dataset ini memiliki beberapa anotasi objek, yang membuat total jumlah anotasi objek lebih dari 860.000. Dalam pemrosesan kami menyaring data sebanyak 5000 gambar dengan class ‘Person’ beserta label anotasi gambar yang memuat bounding box pada pixel yang menunjukkan kelas person pada gambar yang diambil. Kemudian melakukan split data menjadi data training sebanyak 4000, validation sebanyak 500 dan test sebanyak 500.

### 2. Model Development

### FASTER RCNN :
##### Backbone GoogLeNet:
- Menggunakan GoogleNet (Inception V1) & InceptionV3
- Mengaplikasikan augmentasi Normalization
- Mencoba Optimizer SGD dengan lr = 0.0001, momentum = 0.9, weight decay = 0.0001
- Mencoba Optimizer Adam dengan lr = 0.001
- Menambahkan LR scheduler (gamma=0.1)

##### Backbone MobileNet
- Menggunakan mobilenet_v3_large_fpn & mobilenet_v3_large_320_fpn
- Mengaplikasikan augmentasi Normalization
- Mencoba Optimizer SGD dengan lr = 0.005 dan 0.1, momentum = 0.9, weight decay = 0.0005 dan 0.0001
- Menambahkan LR scheduler (gamma=0.1)

##### Backbone ResNet50
- Menggunakan Resnet50 sebagai pretrained
- Mengaplikasikan augmentasi Normalization
- Mencoba Optimizer SGD dengan lr = 0.005, momentum = 0.9, weight decay = 0.0005
- Menambahkan LR scheduler (gamma=0.1)
 
### YOLO :
##### Versi yang diexplorasi:
- YOLO V3 : YOLO V3u
- YOLO V5 : YOLO V5s, YOLO V5x
- YOLO V8 : YOLOV8m, YOLOV8l, YOLOV8x

##### Hyperparameter yang digunakan:
- Epochs         : 50 dan 100
- Batch          : 8 dan 16
- Image Size     : 640x640
- Learning Rate  : lr0 = 0.01, lrf = 0.0001
- Momentum       : 0.937
- Weight Decay   : 0.0005
- Optimizer      : AdamW  

##### Augmentation yang diaplikasikan:
- Mosaic : 1.0
- Translate: 0.1
- Scale: 0.5
- fliplr: 0.5
- hsv_h (hue): 0.015
- hsv_s (saturation): 0.7
- hsv_v (value): 0.4

### 3. Training & Optimization

Pada tahap ini, dilakukan pelatihan dan optimasi model menggunakan beberapa arsitektur dan algoritma yang berbeda, yaitu Faster RCNN dengan Backbone GoogLeNet, MobileNet, ResNet50, dan YOLO dengan versi 3, 5, dan 8. Proses ini dilakukan untuk mencari arsitektur yang memberikan hasil terbaik pada dataset COCO untuk tujuan person detection.

#### * Evaluasi Hasil Training

Setelah pelatihan, model dievaluasi menggunakan dataset validasi untuk mengukur akurasi hasil prediksi. Metric evaluasi yang digunakan adalah Precision, Recall, dan mAP.

#### * Tabel Training & Evaluation (YOLO)

Berikut adalah tabel hasil training dari explorasi algoritma YOLO:
<img align="center" src="https://github.com/triwahyupra/project2_person_tracking/blob/e167ffb508007e3f6c04fe5a26daaf443d8e7acd/assets/tabel%20eval%20yolo.png" alt="tabel YOLO" width="1000" height="500">

### 4. Comparison
Setelah melakukan eksplorasi dan percobaan pada beragam model pada Faster RCNN dan YOLO, dilakukan komparasi untuk menemukan model terbaik untuk deteksi objek pada kelas person.
Berikut adalah tabel komparasi dari model yang diuji, khusus untuk hasil evaluasi YOLO diambil versi terbaik dari YOLOv3, YOLOv5, dan YOLOv8. Dari tabel berikut didapatkan bahwa ResNet50 adalah model terbaik dari kelompok Faster RCNN, dan YOLOv8 adalah model terbaik dari kelompok YOLO.
<img align="center" src="https://github.com/triwahyupra/project2_person_tracking/blob/e167ffb508007e3f6c04fe5a26daaf443d8e7acd/assets/tabel%20comparison.png" alt="tabel komparasi" width="1000" height="500">

## ★ The Results

### Inference Model Faster RCNN - ResNet50

Berikut adalaha hasil inference menggunakan video untuk model Faster RCNN dengan backbone ResNet50 sebagai model terbaik dari kelompok Faster RCNN 

<img align="center" src="https://github.com/triwahyupra/project2_person_tracking/blob/e167ffb508007e3f6c04fe5a26daaf443d8e7acd/assets/FasterRCNN-ResNet50.gif" alt="tabel komparasi" width="800" height="500">

### Inference Model YOLOv8

Berikut adalaha hasil inference menggunakan video pada model YOLOv8 sebagai model terbaik dari kelompok YOLO 

<img align="center" src="https://github.com/triwahyupra/project2_person_tracking/blob/e167ffb508007e3f6c04fe5a26daaf443d8e7acd/assets/yolov8.gif" alt="tabel komparasi" width="800" height="500">


## Notebook and Slides for Presentation

Project ini dikerjakan secara kolaboratif oleh kelompok CV D -Alan Turing, Beberapa Notebook yang dikerjakan oleh anggota Tim dapat diakses pada [FOLDER NOTEBOOK](https://github.com/triwahyupra/project2_person_tracking/tree/e167ffb508007e3f6c04fe5a26daaf443d8e7acd/notebook)

Notebook utama yang digunakan untuk merangkum performa setiap model dapat diakses pada 

[NOTEBOOK Faster RCNN - GoogleNet](https://github.com/triwahyupra/project2_person_tracking/blob/e167ffb508007e3f6c04fe5a26daaf443d8e7acd/notebook/Hendra_Project_2_Person_Tracking_(Faster_R_CNN_GoogLeNet).ipynb)

[NOTEBOOK Faster RCNN - MobileNet](https://github.com/triwahyupra/project2_person_tracking/blob/e167ffb508007e3f6c04fe5a26daaf443d8e7acd/notebook/fathurrahman_Mobile_net.ipynb)

[NOTEBOOK Faster RCNN - ResNet50](https://github.com/triwahyupra/project2_person_tracking/blob/e167ffb508007e3f6c04fe5a26daaf443d8e7acd/notebook/putu_ananta_fasterrcnn_resnet50.ipynb)

[NOTEBOOK YOLOv3](https://github.com/triwahyupra/project2_person_tracking/blob/e167ffb508007e3f6c04fe5a26daaf443d8e7acd/notebook/Satriaji_PersonDetection_trainingYOLOv3.ipynb)

[NOTEBOOK YOLOv5](https://github.com/triwahyupra/project2_person_tracking/blob/e167ffb508007e3f6c04fe5a26daaf443d8e7acd/notebook/triwahyu_yolov5_yolov3_coco_persontracking.ipynb)

[NOTEBOOK YOLOv8](https://github.com/triwahyupra/project2_person_tracking/blob/e167ffb508007e3f6c04fe5a26daaf443d8e7acd/notebook/Satriaji_PersonDetection_trainingYOLOv8.ipynb)

Untuk file presentasi (pptx file) dapat diakses pada [FILE PRESENTASI](https://www.canva.com/design/DAF1o5lBZf4/mWLQnlnXdohtt41iRELACA/edit)
  
## 📧 Contact

Jika Anda memiliki pertanyaan, masukan, atau ingin berkontribusi pada proyek ini, jangan ragu untuk menghubungi kontak berikut:

- Nama: [ Tri Wahyu Prabowo ]
- Email: [ triwahyu@reefgen.io ]
- LinkedIn: [ [triwahyupra](https://www.linkedin.com/in/triwahyupra) ]

Terima kasih atas dukungan dan kontribusi Anda!

