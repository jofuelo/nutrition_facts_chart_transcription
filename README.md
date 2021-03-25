# Nutrition facts chart transcription
This page contains a small dataset for the task of recovering structured precise nutritional information from an image of a product.

## Dataset description
##### Size: 
This dataset contains **633** images.
##### Data description:
The images are natural close-up photographs of one side of food products with the nutritional facts box clearly visible.
All of them are of spanish products.
##### Examples
![Example1](/examples/imgs/ex1.jpg)
![Example2](/examples/imgs/ex2.jpg)

## Ground truth description
All images have been labeled by hand with the ground truth value of 8 nutritional values: energy (kJ), energy (kcal), fat (g), saturated fat (g), carbohydrates (g), sugar (g), protein (g) and salt (g). Other nutritional values may be present in the annotations but we didn't take them into account, as they did not appear in the nutrition facts chart for most products.
As all the products are spanish and the charts in the images are in spanish, the ground truth is provided in spanish. The correspondence in english is the following:
- energía_kj = energy (kJ)
- energía_kcal = energy (kcal)
- grasa = fat
- saturada = saturated fat
- hidratos = carbohydrates
- azúcar = sugar
- proteínas = protein
- sal = salt

These annotations are provided in the following way: one `csv` file per image contains all the information. This file may contain two or three columns depending on how much information appears in the product. The first one is always a list of the nutritional values that appear in the image. The second one contains the quantity of those fields per 100g of product. The third one, if present, contains the quantity of those fields per serving. This column isn't always present in the product labeling, so it is provided when present.

##### Example
| energía_kj   | 802 | 3246 |
|--------------|-----|------|
| energía_kcal | 190 | 770  |
| grasa        | 4.5 | 18   |
| saturada     | 2.7 | 11   |
| hidratos     | 28  | 112  |
| azúcar       | 3.4 | 14   |
| proteínas    | 8.5 | 34   |
| sal          | 1.2 | 5.1  |
| fibra        | 2.1 | 8.6  |

## Data download
You can download the images from [here](https://drive.google.com/file/d/15vnCd0pTIv489j_VpIx_cyTRuQYFTVUC/view?usp=sharing) and the ground truth from [here](https://drive.google.com/file/d/15vnCd0pTIv489j_VpIx_cyTRuQYFTVUC/view?usp=sharing)

## Data extraction task
The target of this task is to obtain the above mentioned 8 nutritional information values per 100g from the image itself. To that purpose, we used Google's transcription engine `Tesseract` and [our nutrition facts chart detector](https://github.com/jofuelo/nutrition_facts_chart_detection). Several preprocessing and post processing algorithms are also applied to finally get the information structured and as correct as possible. As a metric we use the number of errors made in each image, obtaining the following results:

<table class="tg">
<thead>
  <tr>
    <th class="tg-0pky" rowspan="2">   <br>    </th>
    <th class="tg-c3ow" colspan="10">   <br>Number of   errors   </th>
  </tr>
  <tr>
    <td class="tg-0pky">   <br>0   </td>
    <td class="tg-0pky">   <br>1   </td>
    <td class="tg-0pky">   <br>2   </td>
    <td class="tg-0pky">   <br>3   </td>
    <td class="tg-0pky">   <br>4   </td>
    <td class="tg-0pky">   <br>5   </td>
    <td class="tg-0pky">   <br>6   </td>
    <td class="tg-0pky">   <br>7   </td>
    <td class="tg-0pky">   <br>8   </td>
    <td class="tg-0pky">   <br>Total   </td>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">   <br>Number of transcriptions   </td>
    <td class="tg-0pky">   <br>144 (23%)   </td>
    <td class="tg-0pky">   <br>95<br>   <br>(15%)   </td>
    <td class="tg-0pky">   <br>105 (17%)   </td>
    <td class="tg-0pky">   <br>71 (11%)   </td>
    <td class="tg-0pky">   <br>62 (10%)   </td>
    <td class="tg-0pky">   <br>58 (9%)   </td>
    <td class="tg-0pky">   <br>46 (7%)   </td>
    <td class="tg-0pky">   <br>18 (3%)   </td>
    <td class="tg-0pky">   <br>34 (5%)   </td>
    <td class="tg-0pky">   <br>633   </td>
  </tr>
</tbody>

