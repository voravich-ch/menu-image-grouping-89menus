## **Overview**

This project is an extension of menu-image-grouping project. The goal is to improve the performance of the classification algorithm by implementing state-of-the-art model: EfficientNet in place of VGG-16. EfficientNet-B6 succeeded in increasing the number of distinguishable classes to 89 menus while maintaining a precision above 90% on the test set.

### Link to
-   [Google Slide Deck](https://docs.google.com/presentation/d/1h847Ayu3bea-TxJRxq6LftJx4XlU4Czsu9nQhgiwng0/edit?fbclid=IwAR3RqJjAgEXoN6vtOuqgODp8BNNHht4Uc5tEyvqg3XeECTYG0NQKODAUhdE#slide=id.g6f8ee14405_5_7)
-   [Google Sheet (Dashboard)](https://docs.google.com/spreadsheets/d/1kPVHFn06Jqwp1vr5lF1mlLwxh3E53jjH7wTWKInFy60/edit#gid=947057979)


## **Directory Structure**


```
        EfficientNet-B6_89menus
        ├── README.md
        ├── food_cleaned.csv
        ├── new_random_sample_out.csv
        ├── requirements.txt
        ├── best_model
        │   ├── B6_89classes-54-1.20.h5
        │   ├── B6_89classes_acc.png
        │   ├── B6_89classes_loss.png
        │   └── B6_eval.png
        └── dev
            ├── 00_download_image.ipynb
            ├── 01_crop-and-clean_image.ipynb
            ├── 02_create_data_nclasses.ipynb
            ├── 03_train_model.ipynb
            └── 04_evaluation.ipynb
```

## File Description
-   `food_cleaned.csv` -> Table containing information of cleaned data including: \
aesthetic_score, photo_eid, pic_url, product_id, product_name, res_id, res_name, number_of_object, bbox_ratio, real_x1, real_x2, real_y1, real_y2.
-   `new_random_sample_out.csv` -> Table containing random sample for testing (Not used: data cleaning is needed)

### best_model
-   `B6_89classes-54-1.20.h5` -> EfficientNet-B6 weights for 89 classes. 
-   `B6_89classes_acc.png` -> Plot of training accuracy and validation accuracy.
-   `B6_89classes_loss.png` -> Plot of training loss and validation loss.
-   `B6_eval.png` -> Plot of evaluation result on the test set.

### dev
-   `00_download_image.ipynb` -> Download images data from Google Cloud Storage.
-   `01_crop-and-clean_image.ipynb` -> Select, clean, and crop images according to the bounding box. Create `food_cleaned_cropped.csv` while will be used in `02_create_data_nclasses.ipynb`
-   `02_create_data_nclasses.ipynb` -> Distributed images to train/validation/test folders preparing data for model training and evaluation.
-   `03_train_model.ipynb` -> Train EfficientNet-B6 model.
-   `04_evaluation.ipynb` -> Evaluate result on test set.

## Model

The weight of the model: `best_model/B6_89classes-54-1.20.h5`. When setting a threshold at 0.3, the model can label 78.60% of the food images while sustaining 97.23% precision on the test set (`test_photo_eid_89classes.csv`).\
**There is a trade-off between precision and collection when changing the threshold*

## 89 Menu names

```
['Pizza' 'Salmon Sashimi' 'honey toast' 'กระเพาะปลา' 'กุ้งอบวุ้นเส้น'
 'กุ้งเผา' 'กุ้งแช่น้ำปลา' 'ก๋วยจั๊บ' 'ก๋วยจั๊บญวน' 'ก๋วยเตี๋ยวคั่วไก่'
 'ก๋วยเตี๋ยวต้มยำ' 'ก๋วยเตี๋ยวเรือ' 'ขนมจีน' 'ขนมจีบ' 'ขนมปัง'
 'ขนมปังปิ้ง' 'ขาหมูเยอรมัน' 'ข้าวขาหมู' 'ข้าวคลุกกะปิ' 'ข้าวซอยไก่'
 'ข้าวผัด' 'ข้าวผัดกระเทียม' 'ข้าวมันไก่' 'ข้าวหน้าเนื้อ' 'ข้าวหน้าเป็ด'
 'ข้าวหมกไก่' 'ข้าวหมูกรอบ' 'ข้าวหมูแดง' 'ข้าวเหนียวมะม่วง' 'คอหมูย่าง'
 'ชาบู' 'ตับหวาน' 'ติ่มซำ' 'ต้มยำ' 'ต้มเลือดหมู' 'ต้มแซ่บกระดูกอ่อน'
 'ทอดมันกุ้ง' 'ทอดมันปลากราย' 'ทาโกะยากิ' 'น้ำตกหมู' 'น้ำพริกไข่ปู'
 'บะหมี่แห้ง' 'ปลากระพงทอดน้ำปลา' 'ปลากระพงนึ่งมะนาว' 'ปลาหมึกผัดไข่เค็ม'
 'ปอเปี๊ยะทอด' 'ปูนิ่มทอดกระเทียม' 'ปูผัดผงกะหรี่' 'ปูม้านึ่ง'
 'ผักโขมอบชีส' 'ผัดไทกุ้งสด' 'ยำถั่วพลู' 'ยำปลาดุกฟู' 'ยำวุ้นเส้น'
 'ยำสาหร่าย' 'ยำหมูยอ' 'ยำแซลมอน' 'ลาบ' 'สปาเก็ตตี้ขี้เมาทะเล'
 'สปาเก็ตตี้คาโบนาร่า' 'สลัด' 'สเต็กหมู' 'ส้มตำ' 'หมูกรอบ' 'หมูมะนาว'
 'หมูสะเต๊ะ' 'หมูแดดเดียว' 'หอยนางรม' 'หอยแครงลวก' 'ออส่วน' 'ฮะเก๋า'
 'เกี๊ยวซ่า' 'เกี๊ยวทอด' 'เนื้อย่าง' 'เป็ดปักกิ่ง' 'เป็ดพะโล้' 'เป็ดย่าง'
 'เย็นตาโฟ' 'แกงคั่วหอยขม' 'แกงส้มชะอมกุ้ง' 'แหนมเนือง' 'ใบเหลียงผัดไข่'
 'ไก่ทอด' 'ไก่ย่าง' 'ไข่กระทะ' 'ไข่ตุ๋น' 'ไข่เจียว' 'ไส้อั่ว' 'ไอศกรีม']

```

## To-do Task

-   Create a test set which can better represent the real data. It should include all classes in the database, labeling classes other than these 89 menus as 'อื่นๆ'\
 
-   Clean the training data.\
    ```There are some label mistakes in the `food_cleaned.csv` file; hence, cleaning it may increase performance. (Though it might not worth the time spent)```

-   Add more images to classes with fewer numbers of images.\
    ```The maximum number of images in each class in the training set was set to be 450. Therefore, it would be best to have a balanced training set having 450 images in each class.```

-   Increase the number of classes\
    ```The performance did not drop much when scaling from 62 menus to 89 menus; thus, scaling to a larger number of menus seems feasible.```

-   Develop a better object detection model\
    ```The current object detection can only detect one object, and sometimes a non-target object is detected instead.```
    ```There are some errors in the bounding box coordinates.```

## Reference

### Efficient net
-   [EfficientNet: Improving Accuracy and Efficiency through AutoML and Model Scaling](https://ai.googleblog.com/2019/05/efficientnet-improving-accuracy-and.html) 
-   [EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks](https://arxiv.org/abs/1905.11946)
-   [EfficientNet Explained!](https://www.youtube.com/watch?v=3svIm5UC94I)

### CNN
-   [Neural Network that Changes Everything - Computerphile](https://www.youtube.com/watch?v=py5byOOHZM8)
-   [How Blurs & Filters Work - Computerphile](https://youtu.be/C_zFhWdM4ic)
-   [Understand the architecture of CNN](https://towardsdatascience.com/understand-the-architecture-of-cnn-90a25e244c7)

### Transfer learning
-   [A Comprehensive Hands-on Guide to Transfer Learning with Real-World Applications in Deep Learning](https://towardsdatascience.com/a-comprehensive-hands-on-guide-to-transfer-learning-with-real-world-applications-in-deep-learning-212bf3b2f27a)
-   [How to do Transfer learning with Efficientnet](https://www.dlology.com/blog/transfer-learning-with-efficientnet/)

### Evaluation (Precision-Recall)
-   [Precision and recall](https://en.wikipedia.org/wiki/Precision_and_recall)
-   [What is a good classifier?](https://skilja.com/what-is-a-good-classifier-1-4/)

