---
author: tulakann
layout: post
title: บันทึกการใช้คลาส IEEEtran บน LaTeX สำหรับ IEEE conference paper [2]
description: "ต่อจากบล็อกที่แล้ว ว่าด้วยเรื่องการอ้างอิงในเปเปอร์โดยใช้ BibTeX"
tags: [Latex, IEEE, Conference, Paper]
image:
  feature: post/latexieee/featurebst.jpg
  credit: IEEE
  creditlink: http://ctan.megagod.net/tex-archive/macros/latex/contrib/IEEEtran/bibtex/IEEEtran_bst_HOWTO.pdf
comments: true
share: true
date: 2016-10-10 15:30:00
---

ในบล็อกนี้เราก็จะมาพูดถึงการอ้างอิงกันล้วนๆ เลย อย่างที่ได้กล่าวไปในบล็อกที่แล้วว่าเราจะใช้ BibTeX และ Mendeley กัน แต่ก่อนอื่นเรามารู้จักกับการเขียน Bibliography ใน LaTeX กันก่อนดีกว่า ถ้ายังไม่ได้อ่านบล็อกที่แล้วพวกโค้ดที่ใช้ยกตัวอย่างอาจจะไม่เหมือนกันทุกประการ ลองกลับไปอ่านได้ที่นี่เลย [บันทึกการใช้คลาส IEEEtran ตอนที่ 1](http://tupleblog.github.io/latex-ieeetran/)

## LaTeX Bibliography
การเขียน references ใน LaTeX นั้นไม่ได้จำกัดว่าต้องใช้ BibTeX เท่านั้น แต่เรายังสามารถเขียนเองได้ด้วย ลองมาดูตัวอย่างกันในไฟล์ my_conf_paper.tex ที่เราเขียนค้างไว้จากบล็อกที่แล้วที่บรรทัดประมาณ 600 หน่อยๆ จะเจอกับตัวอย่างที่เค้าใส่ไว้ให้ตามนี้

```tex
\begin{thebibliography}{1}

\bibitem{IEEEhowto:kopka}
H.~Kopka and P.~W. Daly, \emph{A Guide to \LaTeX}, 3rd~ed.\hskip 1em plus
  0.5em minus 0.4em\relax Harlow, England: Addison-Wesley, 1999.

\end{thebibliography}
```

อันนี้ก็เป็นรูปแบบการเขียน Bibliography พื้นฐานของ LaTeX เลย ประกอบไปด้วย

- `\begin{thebibliography}{1}` ประกาศเปิดการเขียน references ด้วยจำนวนแหล่งอ้างอิงทั้งหมด ใช้เพื่อคำนวณพื้นที่ที่จะใช้ ถ้ามี 20 แหล่งอ้างอิงก็ใช้ `{20}`
- `\bibitem{IEEEhowto:kopka}` ประกาศ bibliography item โดยใช้คีย์ชื่อว่า `IEEEhowto:kopka` เวลาจะอ้างถึงอันนี้จะใช้คำสั่ง `\cite{IEEEhowto:kopka}`

- ส่วนแต่ละ item ก็จะมีการปรับแต่่งตามที่เห็น มีทั้งการใช้ `~`, `\emph{}`, `\hskip` และ `\relax` ซึ่งคำสั่งเหล่านี้ช่วยจัดให้การเรนเดอร์ดูสวยงามขึ้น แต่ความต่างนั้นเล็กน้อยมากจนแทบสังเกตไม่เห็น

ลองนึกภาพถ้าเราจะอ้างอิง 10 แหล่งข้อมูล เราก็ต้องมาพิมพ์แบบนี้ 10 ครั้ง ซึ่งมันก็คงจะน่าเบื่อไม่น้อย และนี่ก็คือจุดที่ BibTeX จะมาช่วยเรานั่นเอง

## BibTeX
BibTeX เป็นเครื่องมือที่ใช้ช่วยในการอ้างอิงสื่อหรือบทความต่างๆ เข้าใจว่าน่าจะทำงานในลักษณะเดียวกับ Endnote นะ แต่เราไม่เคยใช้ Endnote ก็เลยบอกไม่ได้ว่าเหมือนกันแค่ไหน ก่อนที่เราจะมาสร้างไฟล์ `.bib` ของตัวเองกันเราจะลองมาดูกันก่อนว่าการใช้งาน BibTeX ทำยังไง และเรนเดอร์ออกมาแล้วหน้าตาเป็นยังไง

จากบล็อกที่แล้วที่ให้ copy ไฟล์มาไว้ในโฟลเดอร์โปรเจค จะเห็นว่ามีไฟล์ชื่อ `IEEEexample.bib` อยู่ เราจะมาลองใช้ไฟล์นี้กันเพื่อให้เห็นภาพรวมก่อน ก่อนอื่นให้คอมเมนต์โค้ดเมื่อกี้ให้หมดก่อนแล้วเติมเข้าไปตามนี้

```tex
% \begin{thebibliography}{1}
%
% \bibitem{IEEEhowto:kopka}
% H.~Kopka and P.~W. Daly, \emph{A Guide to \LaTeX}, 3rd~ed.\hskip 1em plus
%   0.5em minus 0.4em\relax Harlow, England: Addison-Wesley, 1999.
%
% \end{thebibliography}

\bibliographystyle{IEEEtran}
\bibliography{IEEEabrv,IEEEexample}
```

แล้วก็ลองไป cite ใน `\section{Conclusion}` ที่บรรทัดประมาณ 580

```tex
\section{Conclusion}
The conclusion goes here. Now, I will try to cite these two sources
\cite{IEEEexample:biblatex} \cite{IEEEexample:phdurl} and you can see how
the result looks like.
```

จะได้ผลออกมาหน้าตาแบบนี้

<figure><center>
  <img width="450px" src="/images/post/latexieee/refrendered.png" data-action="zoom"/>
</center></figure>

จะเห็นว่าจำนวน references ที่ขึ้นมามีจำนวนเท่ากับแหล่งอ้างอิงที่เรา cite ไป แต่ถ้าอยากรู้ว่าในไฟล์ `IEEEexample.bib` มีแหล่งอ้างอิงอยู่ทั้งหมดเท่าไหร่ก็ลองให้เรนเดอร์ดูทั้งหมดก็ได้โดยเพิ่มคำสั่ง `\nocite{*}` เข้าไป

```tex
\nocite{*}
\bibliographystyle{IEEEtran}
\bibliography{IEEEabrv,IEEEexample}
```

references ที่อยู่ใน `IEEEexample.bib` ทั้งหมดจะถูกแสดง สำหรับไฟล์ตัวอย่างนี้มีเยอะมากจนหน้าเดียวไม่พออย่างที่เห็น

_**Note** ตอน build อาจเจอปัญหาเล็กน้อยเนื่องจากใน `.bib` มี `{% raw %}{{\BibTeX}}{% endraw %}` อยู่ แต่ไม่รู้ทำยังไงเหมือนกันอยู่ดีๆ ก็ build ผ่าน_

<figure><center>
  <img src="/images/post/latexieee/allref.png" data-action="zoom"/>
</center></figure>

เห็นภาพกันแล้วทีนี้ก็ลองมาดูว่าการจัดรูปแบบโดย `IEEEtran` นั้นรองรับแหล่งอ้างอิงชนิดไหนบ้าง จากบทความ [How to Use the IEEEtran BibTeX Style](http://ctan.megagod.net/tex-archive/macros/latex/contrib/IEEEtran/bibtex/IEEEtran_bst_HOWTO.pdf) ในเซคชัน _V. SUPPORTED ENTRY TYPES_ ชนิดแหล่งอ้างอิงที่รองรับได้แก่

- Article
- Book
- Inbook
- Incollection
- Booklet
- Manual
- Inproceedings/Conference
- Proceedings
- Mastersthesis
- Phdthesis
- Techreport
- Unpublished
- Electronic
- Patent
- Misc

ซึ่งอันที่น่าจะได้ใช้กันบ่อยๆ ก็น่าจะเป็น Article, Book แล้วก็ Electronic ที่ไว้อ้างอิงสื่อออนไลน์ในอินเทอร์เนต แต่เอาเข้าจริงๆ แล้วกรณีที่เราจะต้องมาสร้าง BibTeX entry เองน่าจะมีน้อยมาก เช่น หนังสือที่ไม่มีอยู่ในฐานข้อมูลทั่วไป หรือพวกแหล่งอ้างอิงออนไลน์ตามอินเทอร์เนต เป็นต้น เพราะส่วนใหญ่เปเปอร์ที่เราจะอ้างอิงน่าจะสามารถหาได้จากตัวช่วยของเรา หรือก็คือ Mendeley นั่นเอง

## Mendeley
Mendeley เป็นโปรแกรมจัดการสื่ออ้างอิงที่ได้รับความนิยมมากตัวหนึ่ง การใช้งานก็ถือว่าค่อนข้างสะดวก สามารถค้นหาเปเปอร์หรือบทความต่างๆ ได้เยอะระดับนึง สำหรับใครที่ไม่เคยใช้บล็อกนี้ก็จะมาแนะนำการใช้งานเบื้องต้นให้ดูกัน จากตรงนี้ไปขอลิสต์เป็นข้อๆ ละกัน

- สร้างไฟล์ `.bib` ของเราไว้ก่อน เช่น `abcde_conf.bib` แล้วก็เปิดไฟล์รอไว้เลย
- จากนั้นก็เปิด Mendeley ขึ้นมาแล้วก็สร้างโฟลเดอร์ไว้รวบรวมแหล่งอ้างอิงที่เราจะใช้ในงานนี้
- ไปที่ Literature Search เพื่อค้นหาเปเปอร์

<figure><center>
  <img src="/images/post/latexieee/mendeleymenu.png" data-action="zoom"/>

  <figcaption>
    <a title="#">
      สร้างโฟลเดอร์ abcde_conf แล้วมาค้นหาที่ Literature Search
    </a>
  </figcaption>
</center></figure>

เราจะมายกตัวอย่างกันสักสองสามอัน อันแรกเลยลองค้นว่า "abc of emg" พอผลการค้นหาขึ้นมาก็คลิกอันบนสุด (Peter Konrad) แล้วลากไปใส่โฟลเดอร์ที่สร้างไว้เมื่อกี้ ต่อไปลองค้นว่า "latex" แล้วก็ลากอันแรกไปไว้ในโฟลเดอร์อีก พอได้สองอันนี้มาแล้ว ต่อไปเราจะดึงข้อมูลที่จะเอาไปใส่ไฟล์ `.bib` กัน ข้อมูลนี้เรียกว่า BibTeX entry สามารถดึงมาได้โดยคลิกขวาแล้วเลือก `Copy As` > `BibTeX Entry` เสร็จแล้วก็เอาไปแปะในไฟล์ `abcde_conf.bib` ที่เปิดรอไว้ก็จะได้ BibTeX entry หน้าตาแบบนี้

```tex
@article{Downes2002,
  author = {Downes, M.},
  doi = {10.1.1.96.645},
  isbn = {1581139306},
  issn = {1581139306},
  journal = {American Mathematical Society},
  mendeley-groups = {abcde{\_}conf},
  pages = {1--17},
  title = {% raw %} {{Short Math Guide for LATEX}}, {% endraw %}
  year = {2002}
}
@article{Konrad2005,
  author = {Konrad, Peter},
  doi = {10.1016/j.jacc.2008.05.066},
  isbn = {0977162214},
  issn = {15583597},
  journal = {A practical introduction to kinesiological {\ldots}},
  mendeley-groups = {abcde{\_}conf},
  number = {April},
  pages = {1--60},
  pmid = {19130982},
  title = {% raw %} {{The abc of emg}}, {% endraw %}
  url = {http://demotu.org/aulas/controle/ABCofEMG.pdf},
  year = {2005}
}
```

ในโค้ดตัวอย่างนี้ขอเอา attribute abstract ออก เพราะมันยาวเหลือเกิน ลองสังเกตดูก็จะพบว่าทั้งสองอันเป็นเป็นบทความทั้งหมด (`@article`) และมีคีย์คือ `Downes2002` แล้วก็ `Konrad2005` ก่อนจะไปลอง `\cite{}` ให้ลองเพิ่มอีกอันนึงเข้าไป คือการอ้างอิงจากเว็บไซต์ ตามนี้เลย

```tex
@electronic{who.int,
  author = {% raw %}{{WHO | World Health Organization}}{% endraw %},
  title = {Types of cardiovascular disease},
  url = {http://www.who.int/cardiovascular\_diseases/en/cvd\_atlas\_01\_types.pdf},
  date = 13,
  month = Sep,
  year = 2013
}
```

โดยที่ `who.int` คือคีย์ที่จะใช้ในคำสั่ง `\cite{}` ตรงนี้จะตั้งว่าอะไรก็ได้แล้วแต่เราเลย เอาล่ะทีนี้เราลองไป cite กัน อย่าลืมเปลี่ยนไฟล์ `.bib` เป็นไฟล์ของเราด้วย

```tex
Next we will cite Downes2002, Konrad2005 and who.int
here \cite{Downes2002} \cite{Konrad2005} \cite{who.int}.
.
.
\bibliography{IEEEabrv,abcde_conf}
```

ก็จะเรนเดอร์ได้แบบนี้ จะเห็นได้ว่าที่เรา cite ไปตอนแรกกลายเป็น `[?]` เพราะเราเปลี่ยนไฟล์ `.bib` แล้วนั่นเอง

<figure><center>
  <img src="/images/post/latexieee/citemybib.png" data-action="zoom"/>
</center></figure>

หลักๆ ที่ได้ใช้มาก็มีเท่านี้ ก็น่าจะจบการบันทึกการใช้งาน LaTeX class นี้ได้ซะที บล็อกนี้ดูเหมือนจะยาวไปสักหน่อยเพราะใช้รูปและโค้ดประกอบการอธิบายไปเรื่อยๆ ค่อนข้างละเอียดในระดับนึง ไม่ใช่อะไรแต่กลัวเรานี่แหละจะลืมเอง 😅

ก็ขอจบบล็อกนี้ไว้ตรงนี้ ถ้าใครผ่านมาได้อ่านและมีข้อเสนอแนะหรือคำถามอะไรก็ติดต่อผมมาได้ทางอีเมล์หรือ[ทวิตเตอร์](https://twitter.com/tulakann)เลยนะครับ สวัสดี
