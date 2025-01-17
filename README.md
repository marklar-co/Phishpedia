# Phishpedia A Hybrid Deep Learning Based Approach to Visually Identify Phishing Webpages

<div align="center">

![Dialogues](https://img.shields.io/badge/Proctected\_Brands\_Size-277-green?style=flat-square)
![Dialogues](https://img.shields.io/badge/Phishing\_Benchmark\_Size-30k-green?style=flat-square)


</div>
<p align="center">
  <a href="https://www.usenix.org/conference/usenixsecurity21/presentation/lin">Paper</a> •
  <a href="https://sites.google.com/view/phishpedia-site/">Website</a> •
  <a href="https://www.youtube.com/watch?v=ZQOH1RW5DmY">Video</a> •
   <a href="https://drive.google.com/file/d/12ypEMPRQ43zGRqHGut0Esq2z5en0DH4g/view?usp=drive_link">Dataset</a> •
  <a href="#citation">Citation</a>
</p>

- This is the official implementation of "Phishpedia: A Hybrid Deep Learning Based Approach to Visually Identify Phishing Webpages" USENIX'21 [link to paper](https://www.usenix.org/conference/usenixsecurity21/presentation/lin), [link to our website](https://sites.google.com/view/phishpedia-site/), [link to our dataset](https://drive.google.com/file/d/12ypEMPRQ43zGRqHGut0Esq2z5en0DH4g/view?usp=drive_link).

- Existing reference-based phishing detectors:
  - :x: Lack of interpretability
  - :x: Lack of generalization performance in the wild
  - :x: Lack of a large-scale phishing benchmark dataset
    
- The contributions of our paper:
   - :white_check_mark: We propose a phishing identification system Phishpedia, which has high identification accuracy and low runtime overhead, outperforming the relevant state-of-the-art identification approaches. 
   - :white_check_mark: Our system provides explainable annotations which increase users' confidence in model prediction
   - :white_check_mark: We conducted a phishing discovery experiment on emerging domains fed from CertStream and discovered 1,704 real phishing, out of which 1133 are zero-days   

## Framework
    
<img src="./datasets/overview.png" style="width:2000px;height:350px"/>

```Input```: A URL and its screenshot ```Output```: Phish/Benign, Phishing target
- Step 1: Enter <b>Deep Object Detection Model</b>, get predicted logos and inputs (inputs are not used for later prediction, just for explanation)

- Step 2: Enter <b>Deep Siamese Model</b>
    - If Siamese report no target, ```Return  Benign, None```
    - Else Siamese report a target, ```Return Phish, Phishing target``` 
    
## Project structure
```
- logo_recog.py: Deep Object Detection Model
- logo_matching.py: Deep Siamese Model 
- configs.yaml: Configuration file
- phishpedia.py: Main script
```

## Instructions
Requirements: 
- Anaconda installed, please refer to the official installation guide: https://docs.anaconda.com/free/anaconda/install/index.html 

1. Create a local clone of Phishpedia
```bash
git clone https://github.com/lindsey98/Phishpedia.git
```

2. Setup
```bash
chmod +x ./setup.sh
./setup.sh
```

3. 
```
conda activate phishpedia
```

4. Run in bash 
```bash
python phishpedia.py --folder <folder you want to test e.g. ./datasets/test_sites>
```

The testing folder should be in the structure of:

```
test_site_1
|__ info.txt (Write the URL)
|__ shot.png (Save the screenshot)
test_site_2
|__ info.txt (Write the URL)
|__ shot.png (Save the screenshot)
......
```

## Miscellaneous
- In our paper, we also implement several phishing detection and identification baselines, see [here](https://github.com/lindsey98/PhishingBaseline)
- The logo targetlist described in our paper includes 181 brands, we have further expanded the targetlist to include 277 brands in this code repository 
- For the phish discovery experiment, we obtain feed from [Certstream phish_catcher](https://github.com/x0rz/phishing_catcher), we lower the score threshold to be 40 to process more suspicious websites, readers can refer to their repo for details
- We use Scrapy for website crawling 

## Citation 
If you find our work useful in your research, please consider citing our paper by:

```bibtex
@inproceedings{lin2021phishpedia,
  title={Phishpedia: A Hybrid Deep Learning Based Approach to Visually Identify Phishing Webpages},
  author={Lin, Yun and Liu, Ruofan and Divakaran, Dinil Mon and Ng, Jun Yang and Chan, Qing Zhou and Lu, Yiwen and Si, Yuxuan and Zhang, Fan and Dong, Jin Song},
  booktitle={30th $\{$USENIX$\}$ Security Symposium ($\{$USENIX$\}$ Security 21)},
  year={2021}
}
```

## Contacts
If you have any issues running our code, you can raise an issue or send an email to liu.ruofan16@u.nus.edu, lin_yun@sjtu.edu.cn, and dcsdjs@nus.edu.sg
