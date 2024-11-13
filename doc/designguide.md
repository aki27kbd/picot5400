# Design Guide

picot5400を用いたキーボードのデザインガイドになります。picot5400を用いることで、トラックボール付キーボードの設計がしやすくなります。  
picot5400を採用したキーボードであるpicot_O44を例に挙げます。下図はpicot_O44の全体構成概略図になります。  
![picot_o44_diagram](/images/design/picot_o44_diagram.jpg)  

picot_O44では、picot5400をケースに固定し、同じくケースに固定したUnified DaughterboardとJSTケーブルで接続します。  
キーマトリクス基板（PCB）はpicot5400とフレキシブルフラットケーブルで接続されます。  
このデザインガイドでは、キーマトリクス基板とケースの設計について留意すべき点を中心にまとめています。一般的なキーボード用PCBやケースデザインの基礎については他資料を参照してください。

## PCB Design

キーボードを設計する際は、picot5400とフレキシブルフラットケーブルを介して接続するキーマトリクス基板が必要になります。マイコン（RP2040）およびセンサー（PMW3360）は全てpicot5400側に搭載されているので、キーマトリクス基板はGPIOと電源線のみで構成することが可能です。

### Circuit Design
回路図には、左側のFFCコネクタと右側のキーマトリクスが必要です。  
[picot_o44_schematics.pdf](https://github.com/aki27kbd/picot_o44/blob/main/doc/picot_o44_schematics.pdf)  
![picot_o44_schematics](/images/design/picot_o44_schematics.jpg)

FFCコネクタは、使用するケーブルの種類（ストレート・反転）に応じて、ピンの配置を反転させてください。picot_O44では、ストレートタイプのケーブルを用いて、基板底面にコネクタを配置しています。下図のように、***ストレートタイプのケーブルを用いる場合はpicot5400とキーマトリクス基板でコネクタのピンアサインが反転することに注意してください。***  
![picot5400_ffc_connector](/images/design/picot5400_ffc_connector.jpg)

コネクタのピンアサインを誤って逆にしてしまった場合でも、ケーブルを折り曲げることで対応可能です。  
![FFC_reversed](/images/design/FFC_03.jpg)

キーマトリクス側は、通常のキーボードと同様に設計してください。FFCケーブルで接続した場合、最大21本のGPIOを使用することが可能なので、キー数の多いキーボードやロータリーエンコーダにも十分に対応可能です。  
![Keymatrix](/images/design/picot_o44_keymatrix.jpg)

### PCB Design
キーマトリクス基板側のFFCコネクタは、キーの間に設置することが可能です。スイッチソケットを扱う場合もキー間に設置可能です。  
![picot_o44_ffc_connector](/images/design/picot_o44_ffc_connector.jpg)


picot_O44のようにキーボードの中央にトラックボールを設ける場合、キーマトリクス基板の該当箇所に必要な開口を設けてください。  
![PCB](/images/design/picot_o44_pcb.jpg)

picot_O44のPCBには、picot5400のUSB Type-Cとの干渉を避けるための切り欠きが設けられています。設計上はPCBとUSB Type-Cは干渉しませんが、PCBが想定以上に撓んだ場合を想定して該当箇所を切り欠いています。  
![PCB_USB](/images/design/picot_o44_pcb_usb.jpg)

また、picot_O44のようにスタビライザーを固定するためにPCBが開口側にはみ出す場合もあります。その場合はボールケース（ベース）の切り欠きがある側をスタビライザー側になるように設計してください。
![PCB_stabilizer](/images/design/picot_o44_stabilizer.jpg)

## Case Design
picot5400は、キーボードのケースやボトムプレートなど、キーマトリクス基板から独立したものに固定することを推奨しています。これはキーの押下に伴う基板の揺れがセンサーとボールに伝わりにくくするためです。

picot_O44では、picot5400を直接キーボードのケースに固定し、キーマトリクス基板はケースを介して間接的に接触する設計としています。
断面図での各パーツの構成は下図の通りです。  
![picot_o44_section1](/images/design/picot_o44_section1.jpg)  

![picot_o44_section2](/images/design/picot_o44_section2.jpg)  


キーボードのケースやボトムプレートに固定する際のねじ穴寸法は、下の寸法図を参考にしてください。  
![picot5400_dimension](/images/design/picot5400_dimension.jpg)  

また、3DプリンタやCNCで製造する立体的なケースを設計する際は、下記資料内の[picot5400_case_sample](/resources/picot5400_case_sample.step)を参照してください。  
下記ポイントに注意して設計を進めてください。
- picot5400の下部にセンサーが出っ張るため干渉を避ける必要があります
- USB Type-Cコネクタが基板外径線からはみ出しているので、基板をケースに埋め込む際はコネクタと干渉しないよう切り欠きを設ける必要があります
- FFCケーブル、JSTケーブルは基板上面のコネクタに接続するので、基板をケースに埋め込む際はケーブルルート用の切り欠きを設ける必要があります

USBコネクタは、picot5400に搭載されているものを用いない場合はJSTケーブルでUnified Daughterboardと接続することになります。  
Unified Daughterboardに関する設計は[公式ドキュメント](https://unified-daughterboard.github.io/#/?id=unified-daughterboard)を参照してください。

## Resources
[picot5400_schematics](/resources/picot5400_schematics.pdf)  
![picot5400_scematics](/images/design/picot5400_schematics.jpg)  

[picot5400_step](/resources/picot5400.step)  
![picot5400_step_preview](/images/design/picot5400_step_preview.jpg)  

[picot5400_case_sample](/resources/picot5400_case_sample.step)
![picot5400_case_sample](/images/design/picot5400_case_sample.jpg)  
