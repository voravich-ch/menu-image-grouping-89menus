## **Overview**

This project is an extension of menu-image-grouping project. The goal is to improve the performance of the classification algorithm by implementing state-of-the-art model: EfficientNet in place of VGG-16. EfficientNet-B6 succeeded in increasing the number of distinguishable classes to 89 menus while maintaining a precision above 90% on the test set.


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
-   `01_crop-and-clean_image.ipynb` -> Select, clean, and crop images according to the bounding box.
-   `02_create_data_nclasses.ipynb` -> Distributed images to train/validation/test folders preparing data for model training and evaluation.
-   `03_train_model.ipynb` -> Train EfficientNet-B6 model.
-   `04_evaluation.ipynb` -> Evaluate result on test set.
   

