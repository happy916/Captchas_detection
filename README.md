# Data analysis 
Prior to choosing the optimal algorithm for processing, an initial step involves basic data analysis.

This analysis revealed missing output pairs for input21.jpg and input100.jpg. Additionally, the corresponding input100.txt file was not found in the input folder. These data discrepancies have been manually rectified.

Subsequently, we will analyze the dimensions of all images and the frequency of all characters. 

# Detect using open-source Tesseract OCR and Easy OCR.
Initially, we evaluated the detection accuracy using the open-source libraries Tesseract OCR and EasyOCR. The accuracy on the overall dataset was 30% for Tesseract OCR and 38% for EasyOCR. To improve accuracy, we then employed PIL for image pre-processing before applying the detection functions. However, the accuracy remained at 23% for Tesseract OCR and 54% for EasyOCR after this pre-processing step. 

# Detect using image segmentation and linear regression 
To enhance accuracy, we split the dataset into training and testing sets. Subsequently, we segmented characters from the input images and associated them with corresponding labels. For each segmented image, we extracted feature vectors using CLIP image embeddings. Training a classifier with these features and labels proved difficult due to convergence issues, likely stemming from improper feature selection. We then switched to using the mean RGB value for each pixel as features, which resulted in smooth classifier convergence. However, the test accuracy remained low.

# Detect using imgae segmentation and image differences. 
Given the small dataset size, a complex model is unlikely to be effective. We are therefore employing a more direct method: using segmented images as templates and calculating the pixel-wise differences between the input image segments and these templates. The template corresponding to the lowest difference score is considered the match. However, experimentation revealed that this method struggles to accurately identify all characters in each input.

# Call a pretrained model (Web API) to detect (To save time)
To achieve a high accuracy and save the cost, we called the Web API AZcaptcha to test. On the whole dataset, the detection accrucy is 100%. 

Lastly, there are other open-source Captcha solving libraries and 3rd party captcha solving services can be employed and fine-tuned. 
For example, 
https://github.com/JackonYang/captcha-tensorflow
https://github.com/0b01/SimGAN-Captcha
https://github.com/PatrickLib/captcha_recognize
https://2captcha.com/
https://anti-captcha.com/

