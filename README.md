# Img2Text
### Image Caption Generator 
    Using CNN-RNN Merge Architecture with Glove Embedding

### Let's take a look:
||||
:-------------------------:|:-------------------------:|:-------------------------:
![](personal_test_image/Profile.jpg) man in black jacket is standing in front of large building | ![](personal_test_image/1002674143_1b742ab4b8.jpg) little girl in pink shirt is sitting in front of rainbow painting | ![](personal_test_image/gang.jpeg) group of people are standing in front of fence


## Model and Hyperparameter:
| | |
|-|-|
| CNN   | InceptionV3 |
| RNN   | CuDNNLSTM |
| Word Embedding | Glove |
| Loss | sparse_categorical_crossentropy |
| Optimizer | Adam |
| Embedding Dimension | 300 |
| Embedding Trainable | True |
| Layer Size | 256 |
| Dropout Rate | 0.5 |
| Max Epochs | 20 |
| Early stopping | monitor='val_loss', min_delta=0.01, patience=10 |
| Model Checkpoint | monitor='val_loss', save_best_only=True |
| Batch Size | 2048 |

## Performance:
### 1. Crossentropy Loss (Lower the better)
|       | With Glove | Without Glove |
|:-----:|:------:| :------:|
| Train | 2.6006 | 2.6338 |
| Dev   | 3.0556 | 3.1157 |
### 2. CIDEr Score (Test Set)

<table border=0 cellpadding=0 cellspacing=0 width=672 style='border-collapse:
 collapse;table-layout:fixed;width:503pt'>
 <col width=121 style='mso-width-source:userset;mso-width-alt:3882;width:91pt'>
 <col width=183 style='mso-width-source:userset;mso-width-alt:5845;width:137pt'>
 <col width=107 style='mso-width-source:userset;mso-width-alt:3413;width:80pt'>
 <col width=87 span=3 style='width:65pt'>
 <tr height=21 style='height:16.0pt'>
  <td height=21 class=xl63 width=121 style='height:16.0pt;width:91pt'></td>
  <td class=xl63 width=183 style='width:137pt'></td>
  <td class=xl63 width=107 style='width:80pt'>
  <meta charset=utf-8>
  CIDEr</td>
 </tr>
 <tr height=21 style='height:16.0pt'>
  <td rowspan=2 height=42 class=xl63 style='height:32.0pt'>With Glove</td>
  <td class=xl63>Greedy Search</td>
  <td class=xl64>0.44643053</td>
 </tr>
 <tr height=21 style='height:16.0pt'>
  <td height=21 class=xl63 style='height:16.0pt'>Beam Search (B = 3)</td>
  <td class=xl64>0.48076379</td>
 </tr>
 <tr height=21 style='height:16.0pt'>
  <td rowspan=2 height=42 class=xl63 style='height:32.0pt'>Without Glove</td>
  <td class=xl63>Greedy Search</td>
  <td class=xl64>0.46058652</td>
 </tr>
 <tr height=21 style='height:16.0pt'>
  <td height=21 class=xl63 style='height:16.0pt'>Beam Search (B = 3)</td>
  <td class=xl64>0.49261228</td>
 </tr>
</table>


### 3. BLEU Score (Test Set)

<table border=0 cellpadding=0 cellspacing=0 width=662 style='border-collapse:
 collapse;table-layout:fixed;width:495pt'>
 <col width=127 style='mso-width-source:userset;mso-width-alt:4053;width:95pt'>
 <col width=187 style='mso-width-source:userset;mso-width-alt:5973;width:140pt'>
 <col width=87 span=4 style='width:65pt'>
 <tr height=21 style='height:16.0pt'>
  <td height=21 class=xl65 width=127 style='height:16.0pt;width:95pt'></td>
  <td class=xl65 width=187 style='width:140pt'></td>
  <td class=xl65 width=87 style='width:65pt'>BLEU-1</td>
  <td class=xl65 width=87 style='width:65pt'>BLEU-2</td>
  <td class=xl65 width=87 style='width:65pt'>BLEU-3</td>
  <td class=xl65 width=87 style='width:65pt'>BLEU-4</td>
 </tr>
 <tr height=21 style='height:16.0pt'>
  <td rowspan=2 height=42 class=xl65 style='height:32.0pt'>With Glove</td>
  <td class=xl65>Greedy Search</td>
  <td class=xl66>0.594145</td>
  <td class=xl66>0.373877</td>
  <td class=xl66>0.242624</td>
  <td class=xl66>0.152859</td>
 </tr>
 <tr height=21 style='height:16.0pt'>
  <td height=21 class=xl65 style='height:16.0pt'>Beam Search (B = 3)</td>
  <td class=xl66>0.604485</td>
  <td class=xl66>0.393628</td>
  <td class=xl66>0.267615</td>
  <td class=xl66>0.177017</td>
 </tr>
 <tr height=21 style='height:16.0pt'>
  <td rowspan=2 height=42 class=xl65 style='height:32.0pt'>Without Glove</td>
  <td class=xl65>Greedy Search</td>
  <td class=xl66>0.612248</td>
  <td class=xl66>0.391558</td>
  <td class=xl66>0.254003</td>
  <td class=xl66>0.16078</td>
 </tr>
 <tr height=21 style='height:16.0pt'>
  <td height=21 class=xl65 style='height:16.0pt'>Beam Search (B = 3)</td>
  <td class=xl66>0.619149</td>
  <td class=xl66>0.405042</td>
  <td class=xl66>0.27374</td>
  <td class=xl66>0.179306</td>
 </tr>
</table>


## Conclusion:

1. Use InceptionV3 to encode image.
2. Beam Search is better then Greedy Search by 10% on both CIDEr and BLEU Score.
3. Use large Batch with early stopping and checkpoints can achieve lower crossentropy loss
4. Fine-tune a pre-trained embedding maynot always gives better result.