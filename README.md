# Person-and-Forklift-Recognition-and-Tracking-with-Image
Video görüntüsünde aynı anda bir insan ve bir forklifti algılayıp tanımlayacağız. Videoda bir insan olacak (kadın erkek fark etmez) bir de forklift olacak. İnsan ve aracın nerede durdukları önemli değil. Video akışında insanda insan yazacak araçta forklift yazacak. 

İnsan ve forklift için bir veri setinden faydalanıyoruz. Bu veri setini kaggle üzerinde indiriyoruz. ( https://www.kaggle.com/datasets/hakantaskiner/personforklift-dataset?resource=download ) 
İndirdiğimiz bu veri setini YOLOv5 ile eğitiyoruz. YOLOV5 Nesne Tespiti(Object Detection); fotoğraflardaki, videolardaki ve gerçek zamanlı görüntülerdeki nesneleri tespit etmeye odaklanan bilgisayarlı görü ve görüntü işleme ile ilgili bir bilgisayar teknolojisidir. 
 
https://github.com/ultralytics/yolov5 girdikten sonra Colab üzerinden çalışmaya devam ediyoruz. 
.......................................................................................................................................................................
- bu kısımı çalıştırıyoruz

!git clone https://github.com/ultralytics/yolov5  # clone
%cd yolov5
%pip install -qr requirements.txt  # install

import torch
import utils
display = utils.notebook_init()  # checks
.......................................................................................................................................................................
- veri setimizi zipliyoruz ve çalışma ortamımıza sürüklüyoruz
- zipten çıkartmak için;

!unzip -q ../train_data.zip -d ../

- zip dosyasını siliyoruz.
.......................................................................................................................................................................
-yolov5>data>coco128.yaml indiriyoruz  veri seti yolumuzu ve class içinde bulunmasını istediğimiz isimleri yazıyoruz. Daha sonra çalışma ortamına geri yüklüyoruz.
.......................................................................................................................................................................
!python train.py --img 640 --batch 2 --epochs 60 --data custom_data.yaml --weights yolov5s.pt --cache

custom_data.yaml -> bu başta düzenlediğimiz coco128.yaml dosyası siz ne isim verdiyseniz onu yazın.
epochs performası en iyi 60 da 
.......................................................................................................................................................................- videomuzu çalışma ortamımıza aktarıyoruz ve 
!python detect.py --weights runs/train/exp3/weights/last.pt --img 640 --conf 0.25 --source ../videos.mp4

weights runs/train/exp3/weights/last.pt -> epochs hesapladığımızda alt kısımdaki yolu kopyalıyoruz.
videos.mp4 -> sizin videonuzun ismini yazın.

- yolov5>data>runs>detect>exp>videos.mp4 -----> diyerek videoyu indirebilirsiniz.
