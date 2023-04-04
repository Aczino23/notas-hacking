# MacroHard WeakEdge

## Descripción: 
I've hidden a flag in this file. Can you find it? [Forensics is fun.pptm](https://mercury.picoctf.net/static/2e739f9e0dc9f4c1556ea6b033c3ec8e/Forensics%20is%20fun.pptm)

**Pistas:**

## Solución:
1. En este reto se nos da un archivo de Microsoft PowerPoint 2007:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/MacroHard_WeakEdge]
└─$ ls
'Forensics is fun.pptm'

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/MacroHard_WeakEdge]
└─$ file Forensics\ is\ fun.pptm 
Forensics is fun.pptm: Microsoft PowerPoint 2007+

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/MacroHard_WeakEdge]
└─$ 
```

2. Descomprimimos el archivo:

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/MacroHard_WeakEdge]
└─$ unzip Forensics\ is\ fun.pptm 
Archive:  Forensics is fun.pptm
  inflating: [Content_Types].xml     
  inflating: _rels/.rels             
  inflating: ppt/presentation.xml    
  inflating: ppt/slides/_rels/slide46.xml.rels  
  inflating: ppt/slides/slide1.xml   
  inflating: ppt/slides/slide2.xml   
  inflating: ppt/slides/slide3.xml   
  inflating: ppt/slides/slide4.xml   
  inflating: ppt/slides/slide5.xml   
  inflating: ppt/slides/slide6.xml   
  inflating: ppt/slides/slide7.xml   
  inflating: ppt/slides/slide8.xml   
  inflating: ppt/slides/slide9.xml   
  inflating: ppt/slides/slide10.xml  
  inflating: ppt/slides/slide11.xml  
  inflating: ppt/slides/slide12.xml  
  inflating: ppt/slides/slide13.xml  
  inflating: ppt/slides/slide14.xml  
  inflating: ppt/slides/slide15.xml  
  inflating: ppt/slides/slide16.xml  
  inflating: ppt/slides/slide17.xml  
  inflating: ppt/slides/slide18.xml  
  inflating: ppt/slides/slide19.xml  
  inflating: ppt/slides/slide20.xml    
  ...                                               
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/MacroHard_WeakEdge]
└─$ ls
'[Content_Types].xml'   docProps  'Forensics is fun.pptm'   ppt   _rels

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/MacroHard_WeakEdge]
└─$ 
```

3. Haciendo una búsqueda por los archivos encontramos que en u archivo existe una cadena codificada en base64 la cual parce ser la flag: 

```bash
┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/MacroHard_WeakEdge]
└─$ ls
'[Content_Types].xml'   docProps  'Forensics is fun.pptm'   ppt   _rels

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/MacroHard_WeakEdge]
└─$ cd ppt 

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/MacroHard_WeakEdge/ppt]
└─$ ls
presentation.xml  _rels         slideMasters  tableStyles.xml  vbaProject.bin
presProps.xml     slideLayouts  slides        theme            viewProps.xml

┌──(kali㉿kali)-[~/picoCTF-Practice/forensics/MacroHard_WeakEdge/ppt]
└─$ cd slideMasters   

┌──(kali㉿kali)-[~/…/forensics/MacroHard_WeakEdge/ppt/slideMasters]
└─$ ls
hidden  _rels  slideMaster1.xml

┌──(kali㉿kali)-[~/…/forensics/MacroHard_WeakEdge/ppt/slideMasters]
└─$ cat hidden     
Z m x h Z z o g c G l j b 0 N U R n t E M W R f d V 9 r b j B 3 X 3 B w d H N f c l 9 6 M X A 1 f Q                                                                                            
┌──(kali㉿kali)-[~/…/forensics/MacroHard_WeakEdge/ppt/slideMasters]
└─$ echo "Z m x h Z z o g c G l j b 0 N U R n t E M W R f d V 9 r b j B 3 X 3 B w d H N f c l 9 6 M X A 1 f Q " | tr -d " "
ZmxhZzogcGljb0NURntEMWRfdV9rbjB3X3BwdHNfcl96MXA1fQ

┌──(kali㉿kali)-[~/…/forensics/MacroHard_WeakEdge/ppt/slideMasters]
└─$ echo "Z m x h Z z o g c G l j b 0 N U R n t E M W R f d V 9 r b j B 3 X 3 B w d H N f c l 9 6 M X A 1 f Q " | tr -d " " | base64 -d
flag: picoCTF{D1d_u_kn0w_ppts_r_z1p5}base64: entrada inválida

┌──(kali㉿kali)-[~/…/forensics/MacroHard_WeakEdge/ppt/slideMasters]
└─$ 
```

### Flag: picoCTF{D1d_u_kn0w_ppts_r_z1p5}

## Notas adicionales:

Los archivos con el formato **PPTM** se utilizan para indicar los archivos de presentación habilitados para macros creadas por de Microsoft PowerPoint, un software bien conocido usado para crear presentaciones con el uso de presentaciones de diapositivas. Microsoft PowerPoint también es compatible con el uso de diferentes objetos multimedia, como imágenes, archivos de audio y video, hipervínculos y otros objetos multimedia que se pueden organizar libremente.

## Referencias:
- https://www.reviversoft.com/es/file-extensions/pptm
