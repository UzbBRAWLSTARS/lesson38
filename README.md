# lesson39
from googletrans import Translator

tarjimon = Translator()

msg = "Tarjima uchun so'z kiriting (chiqib ketish uchun \"q\" deb yozing): "
msg = 'Tarjima uchun so\'z kiriting (chiqib ketish uchun "q" deb yozing): '
while True:
    text = input(msg)
    if text == "q":
        break
    else:
        tarjima = tarjimon.translate(text, src='uz', dest='en')
        print(tarjima.text)    
        tarjima = tarjimon.translate(text, src="uz", dest="en")
        print(tarjima.text)
  16 changes: 9 additions & 7 deletions16  
39-pip-pypi/darslar-openCV.py
@@ -16,8 +16,10 @@
import cv2

cap = cv2.VideoCapture(0)
face_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + 'haarcascade_frontalface_default.xml')
eye_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + 'haarcascade_eye.xml')
face_cascade = cv2.CascadeClassifier(
    cv2.data.haarcascades + "haarcascade_frontalface_default.xml"
)
eye_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + "haarcascade_eye.xml")

while True:
    ret, frame = cap.read()
@@ -26,16 +28,16 @@
    faces = face_cascade.detectMultiScale(gray, 1.3, 5)
    for (x, y, w, h) in faces:
        cv2.rectangle(frame, (x, y), (x + w, y + h), (255, 0, 0), 5)
        roi_gray = gray[y:y+w, x:x+w]
        roi_color = frame[y:y+h, x:x+w]
        roi_gray = gray[y : y + w, x : x + w]
        roi_color = frame[y : y + h, x : x + w]
        eyes = eye_cascade.detectMultiScale(roi_gray, 1.3, 5)
        for (ex, ey, ew, eh) in eyes:
            cv2.rectangle(roi_color, (ex, ey), (ex + ew, ey + eh), (0, 255, 0), 5)

    cv2.imshow('frame', frame)
    cv2.imshow("frame", frame)

    if cv2.waitKey(1) == ord('q'):
    if cv2.waitKey(1) == ord("q"):
        break

cap.release()
cv2.destroyAllWindows()
cv2.destroyAllWindows()
  12 changes: 7 additions & 5 deletions12  
39-pip-pypi/darslar-pywebio.py
@@ -2,10 +2,12 @@
from pywebio.output import put_text
from math import pi


def doira():
    r = input("Doira radiusini kiriting：", type=FLOAT)    
    yuza = pi*(r**2)
    per = 2*pi*r    
    put_text(f"Doira yuzi {yuza}ga,\nperimetri {per}ga teng")  
    r = input("Doira radiusini kiriting：", type=FLOAT)
    yuza = pi * (r ** 2)
    per = 2 * pi * r
    put_text(f"Doira yuzi {yuza}ga,\nperimetri {per}ga teng")


doira()
doira()
  2 changes: 1 addition & 1 deletion2  
39-pip-pypi/darslar-requests.py
@@ -23,4 +23,4 @@
r = requests.get(url)
r_json = r.json()[0]
# print(r_json.keys())
print(r_json['capital'])
print(r_json["capital"])
  35 changes: 19 additions & 16 deletions35  
39-pip-pypi/darslar-wordcloud.py
@@ -13,30 +13,33 @@
import requests

from bs4 import BeautifulSoup
from wordcloud import WordCloud 
import matplotlib.pyplot as plt 
from wordcloud import WordCloud
import matplotlib.pyplot as plt


sahifa = "https://kun.uz/news/main"
r = requests.get(sahifa)
# pprint(r.text)

soup = BeautifulSoup(r.text, 'html.parser')
soup = BeautifulSoup(r.text, "html.parser")
# print(soup.prettify())
news = soup.find_all(class_="news-title")
matn=""
matn = ""
for n in news:
    matn += n.text

stopwords = ["учун","бўйича","лекин","билан","ва","бор","ҳам","хил","йил"]
wordcloud = WordCloud(width = 1000, height = 1000, 
                background_color ='white', 
                stopwords = stopwords, 
                min_font_size = 20).generate(matn) 

# plot the WordCloud image                        
plt.figure(figsize = (8, 8), facecolor = None) 
plt.imshow(wordcloud) 
plt.axis("off") 
plt.tight_layout(pad = 0) 
plt.show() 
stopwords = ["учун", "бўйича", "лекин", "билан", "ва", "бор", "ҳам", "хил", "йил"]
wordcloud = WordCloud(
    width=1000,
    height=1000,
    background_color="white",
    stopwords=stopwords,
    min_font_size=20,
).generate(matn)

# plot the WordCloud image
plt.figure(figsize=(8, 8), facecolor=None)
plt.imshow(wordcloud)
plt.axis("off")
plt.tight_layout(pad=0)
plt.show()
  38 changes: 20 additions & 18 deletions38  
39-pip-pypi/darslar-wxPython.py
@@ -14,33 +14,35 @@
from googletrans import Translator

tarjimon = Translator()
class MyFrame(wx.Frame):    


class MyFrame(wx.Frame):
    def __init__(self):
        super().__init__(parent=None, title='Oʻzbek-Ingliz Lugʻat')
        panel = wx.Panel(self)        
        my_sizer = wx.BoxSizer(wx.VERTICAL)        
        super().__init__(parent=None, title="Oʻzbek-Ingliz Lugʻat")
        panel = wx.Panel(self)
        my_sizer = wx.BoxSizer(wx.VERTICAL)
        self.text_ctrl = wx.TextCtrl(panel)
        my_sizer.Add(self.text_ctrl, 0, wx.ALL | wx.EXPAND, 5)        
        
        my_btn = wx.Button(panel, label='TARJIMA')
        my_sizer.Add(self.text_ctrl, 0, wx.ALL | wx.EXPAND, 5)

        my_btn = wx.Button(panel, label="TARJIMA")
        my_btn.Bind(wx.EVT_BUTTON, self.on_press)
        my_sizer.Add(my_btn, 0, wx.ALL | wx.CENTER, 5)        
        
        self.text_out = wx.TextCtrl(panel,style = wx.TE_READONLY)        
        my_sizer.Add(self.text_out, 0, wx.ALL | wx.EXPAND, 5)         
        panel.SetSizer(my_sizer)        
        my_sizer.Add(my_btn, 0, wx.ALL | wx.CENTER, 5)

        self.text_out = wx.TextCtrl(panel, style=wx.TE_READONLY)
        my_sizer.Add(self.text_out, 0, wx.ALL | wx.EXPAND, 5)
        panel.SetSizer(my_sizer)
        self.Show()

    def on_press(self, event):
        value = self.text_ctrl.GetValue()
        if not value:                       
        if not value:
            self.text_out.SetValue("Soʻz kiritmadingiz")
        else:
            tarjima = tarjimon.translate(value, src='uz', dest='en')
            self.text_out.SetValue(tarjima.text.capitalize()) 
    
            tarjima = tarjimon.translate(value, src="uz", dest="en")
            self.text_out.SetValue(tarjima.text.capitalize())


if __name__ == '__main__':
if __name__ == "__main__":
    app = wx.App()
    frame = MyFrame()
    app.MainLoop()
    app.MainLoop()
