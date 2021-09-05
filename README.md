# Russian Caption system

This project was implemented as part of an internship at Odnoklassniki.

The system makes captions to images for blind and visually impaired people. The architecture consists of two models:

- [YOLOv3](https://github.com/experiencor/keras-yolo3) - state-of-the-art, real-time object detection system.
- [Sber ru-GPT models](https://github.com/sberbank-ai/ru-gpts) - autoregressive transformer language models.

For the first model, weights were taken from the YOLOv3 neural network and trained in 80 classes from a dataset [MS COCO](https://cocodataset.org/#home).

For the second model, the weights of two models were taken: **ruGPT3Small** and **ruGPT3Medium**. Then they were fine-tuned on a dataset of russion language, containing labels and capltion from them.

Thus, 3 models were developed: ruGPT3Small trained on 2 and 10 epochs, ruGPT3Medium trained on 5 epochs. The **ruGPT3Small(2 epochs)** model worked best on tests, but ruGPT3Medium makes more eloquent captions.

![](/readme_pics/example.png)

## Installing

To install the dependencies, run

```bash
pip install -r requirements.txt
```

Also you should download weights for YOLOv3, GPT2:

- Grab the pretrained weights of yolo3 from <https://pjreddie.com/media/files/yolov3.weights>
- Weight of GPT model from <https://drive.google.com/drive/folders/1WFpM3jFpGHSq3GESIKMnTzyRZvdRf9mN?usp=sharing>

And for the GPU to work, make sure you've got the drivers installed beforehand (CUDA).

It has been tested to work with Python 3.7.11

## Caption

Select model, image and run:

```bash
python caption.py -m choosen_models -i your_image.jpg
```

## Models Timings

Time estimated on CPU Intel Core i5.

<table><tbody>
<!-- START TABLE -->
<!-- TABLE HEADER -->
<th valign="bottom">Name</th>
<th valign="bottom">Download</th>
<th valign="bottom">Time @ 1 image.</th>
<!-- TABLE BODY -->
 <tr><td align="left">Small (2 epochs)</td>
<td align="center"><a href="https://drive.google.com/file/d/1pbGBRhVJqJiXzo9_dUp2855MXQ8ryoMf/view?usp=sharing">model</a></td>
<td align="center">7.2 s</td>
</tr>
 <tr><td align="left">Small (10 epochs)</td>
<td align="center"><a href="https://drive.google.com/file/d/1lZpUO6mSxNOAcvNbWRk_hLf34qjuVcYJ/view?usp=sharing">model</a></td>
<td align="center">6.6 s</td>
</tr>
 <tr><td align="left">Meduim (5 epochs)</td>
<td align="center"><a href="https://drive.google.com/file/d/1XiZV8HPPHUK-AZowF0WqRQYXeMSs126K/view?usp=sharing">model</a></td>
<td align="center">10.9 s</td>
</tr>
</tbody></table>

## Captions Examples

![](/readme_pics/example2.png)

<table><tbody>
<!-- START TABLE -->
<!-- TABLE HEADER -->
<th valign="bottom">Name</th>
<th valign="bottom">vase.jpg</th>
<th valign="bottom">man.jpg</th>
<th valign="bottom">sofa.jpg</th>
<th valign="bottom">cats.jpg</th>
<!-- TABLE BODY -->
<tr><td align="left">Small (2 epochs)</td>
<td align="center">Ваза и чашка на столе</td>
<td align="center">Человек с мобильным телефоном и галстуком</td>
<td align="center">Человек сидит на диване с мобильным телефоном</td>
<td align="center">Два кота смотрят на человека на завтраке за столом со стулом и чашей</td>
</tr>

<tr><td align="left">Small (10 epochs)</td>
<td align="center">Маленькая вазочка со стеклянной кружкой на столе</td>
<td align="center">Человек, стоящий перед мобильным телефоном в галстуке</td>
<td align="center">Люди на диване с мобильными телефонами</td>
<td align="center">Два больших коричневых кота смотрят на человека на столе со стулом в чаше</td>
</tr>

<tr><td align="left">Meduim (5 epochs)</td>
<td align="center">Белая керамическая ваза с розами и белая чашка на деревянном столе</td>
<td align="center">Мужчина в костюме с мобильным телефоном и галстуком на шее</td>
<td align="center">Мужчина сидит на диване и разговаривает по мобильному телефону</td>
<td align="center">Две серые кошки сидят напротив человека, обедающего на кухонном столе возле стульев и чаши</td>
</tr>

</tbody></table>
