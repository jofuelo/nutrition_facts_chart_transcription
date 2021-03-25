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
The target of this task is to obtain the above mentioned 8 nutritional information values per 100g from the image itself. To that purpose, we used [Google's transcription engine Tesseract](https://github.com/tesseract-ocr/tesseract) and [our nutrition facts chart detector](https://github.com/jofuelo/nutrition_facts_chart_detection). Several preprocessing and post processing algorithms are also applied to finally get the information structured and as correct as possible. As a metric we use the number of errors made in each image, obtaining the following results:

<table class="tg">
<thead>
  <tr>
    <th class="tg-0pky" rowspan="2"></th>
    <th class="tg-c3ow" colspan="10">Number of errors</th>
  </tr>
  <tr>
    <td class="tg-0pky">0</td>
    <td class="tg-0pky">1</td>
    <td class="tg-0pky">2</td>
    <td class="tg-0pky">3</td>
    <td class="tg-0pky">4</td>
    <td class="tg-0pky">5</td>
    <td class="tg-0pky">6</td>
    <td class="tg-0pky">7</td>
    <td class="tg-0pky">8</td>
    <td class="tg-0pky">Total</td>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">Number of transcriptions</td>
    <td class="tg-0pky">144 (23%)</td>
    <td class="tg-0pky">95 (15%)</td>
    <td class="tg-0pky">105 (17%)</td>
    <td class="tg-0pky">71 (11%)</td>
    <td class="tg-0pky">62 (10%)</td>
    <td class="tg-0pky">58 (9%)</td>
    <td class="tg-0pky">46 (7%)</td>
    <td class="tg-0pky">18 (3%)</td>
    <td class="tg-0pky">34 (5%)</td>
    <td class="tg-0pky">633</td>
  </tr>
</tbody>
  
We also calculated the accuracy per nutritional value. In the following table, we show the number of errors per each one of them.
<table class="tg">
<thead>
  <tr>
    <th class="tg-0pky"></th>
    <th class="tg-0pky">Energy (kJ)</th>
    <th class="tg-0pky">Energy (kcal)</th>
    <th class="tg-0pky">Fat (g)</th>
    <th class="tg-0pky">Saturated fat (g)</th>
    <th class="tg-0pky">Carbohydrates (g)</th>
    <th class="tg-0pky">Sugar (g)</th>
    <th class="tg-0pky">Protein (g)</th>
    <th class="tg-0pky">Salt (g)</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">Number oferrors</td>
    <td class="tg-0pky">137 (22%)</td>
    <td class="tg-0pky">139 (22%)</td>
    <td class="tg-0pky">226 (36%)</td>
    <td class="tg-0pky">232 (37%)</td>
    <td class="tg-0pky">225 (36%)</td>
    <td class="tg-0pky">227 (36%)</td>
    <td class="tg-0pky">285 (45%)</td>
    <td class="tg-0pky">259 (41%)</td>
  </tr>
</tbody>
</table>

