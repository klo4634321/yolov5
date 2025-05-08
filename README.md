


## 資料夾階層
```
my_datasets/
├── train/
│   ├── images/
│   └── labels/
├── valid/
│   ├── images/
│   └── labels/
yolov5/
├── custom_data.yaml
└── test_img.jpg
```

## 開始訓練模型
```
python train.py --img 640 --batch 16 --epochs 100 --data custom_data.yaml --weights yolov5s.pt --name my_yolo_model
```

參數解釋：
--img: 輸入影像尺寸（YOLO 支援 320~1280，常用 640）
--batch: 每個 batch 幾張圖
--epochs: 訓練多少輪
--data: 剛剛的 .yaml 檔
--weights: 初始權重，可選 yolov5s.pt, yolov5m.pt, yolov5l.pt, yolov5x.pt
--name: 輸出資料夾名稱（保存在 runs/train/ 下面）

## 訓練結果在哪裡？
完成後模型儲存在：
```
runs/train/my_yolo_model/weights/best.pt
```
你可以用這個檔來做推論（inference）。

## 單張圖片推論
```
python detect.py --weights runs/train/my_yolo_model/weights/best.pt --img 640 --conf 0.25 --source test_img.jpg #換成自己的檔名
```
## 一整個資料夾推論
```
python detect.py --weights runs/train/my_yolo_model/weights/best.pt --img 640 --conf 0.25 --source path/to/folder/
```
## 推論結果在哪裡？
```
runs/detect/exp/  # 或 exp2, exp3 ... 依照次數增加
```
### 如果你要評估 mAP、precision、recall 等指標：
```
python val.py --weights runs/train/my_yolo_model/weights/best.pt --data custom_data.yaml --img 640
```
這會根據你的驗證集進行完整評估，並在終端機輸出各類別的準確度（AP）與平均準確率（mAP@0.5 或 mAP@0.5:0.95）。
