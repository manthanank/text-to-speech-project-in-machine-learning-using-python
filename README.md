# Text-to-Speech-project-in-Machine-Learning-using-python
Converting text to speech using python in Machine Learning


from tkinter.ttk import *
from gtts import gTTS
import tkinter
import tkinter as tk
import os
from tkinter import filedialog
from tkinter import *
from tkinter import messagebox
import pandas as pd
import csv
import sys
#from PIL import Image, ImageTk

window=Tk()
window.geometry('350x350')
window.title('Text to Speech')

a=Label(window,text='Text to Speech Convertor',bg='white',font=('arial 20 bold'),fg='black').pack()
window.config(background='white')
#a.place(x=150,y=100)

#b=Label(window,text='Enter text',bg='white',font=('arial 16 bold'),fg='black').pack()
#mytext=StringVar()
#b.place(x=100,y=200)

#def task():
    #window.filename=filedialog.askopenfilename(initialdir="/",title="Select file",filetypes=(("text files",".txt"),("all files","*.*")))
#p=ttk.Button(window,width=10,command=task)
#photo=PhotoImage(file="photo.png")
#p.config(image=photo)
#p.place(x=50,y=350)

def task1():
    j=tk.messagebox.askquestion('Exit','Are you sure',icon='warning')
    if j=='yes':
        window.destroy()
    else:
        tk.messagebox.showinfo('Return','Back')
j=Button(window,text='Exit',width=10,height=1,bg='red',command=task1)
j.place(x=250,y=140)

#def task():
abc=pd.read_csv("Student.csv")
print(abc)
#g>>abc

def fetch():
    mytext=" "
    language='en'
    for datas in abc.values:
        #f1="Hi you have a mail from" +datas[-4]+ " subject is " +datas[-3]+ "content is  "+datas[-2]+"  mail sent on "+datas[-1]
        #f1 = ["Reg no is" +datas[-8]+ " name is  " +datas[-7]+ "has attendence  " +datas[-6]+ " in subject " +datas[-5]+ " and secured "+datas[-1]+ "  final IA marks in subject "+datas[-5]]
        f1 = " name is  " +datas[-3]+ "has grade" +datas[-1]+ " in subject " +datas[-2]
        for x in f1:
            mytext+=x
            myobj=gTTS(text=mytext, lang=language, slow=False)
        myobj.save('Voice3.mp3')
    
def play():
    from pygame import mixer
    mixer.init()
    mixer.music.load("Voice3.mp3")
    mixer.music.play()
    
#m=Entry(window,text=mytext).pack()
#m.place(x=200,y=200)
    
n=Button(window,text='convert',width=10,bg='green',command=fetch)
n.place(x=50,y=140)

o=Button(window,text='play file',width=10,bg='green',command=play)
o.place(x=150,y=140)

with open('Student.csv') as csv_file:
    csv_reader = csv.reader(csv_file, delimiter=',')
    line_count = 0
    for row in csv_reader:
        if line_count == 0:
            print(f'Column names are {", ".join(row)}')
            line_count += 1
        else:
            #print(f'\tReg no is {row[0]} and name is {row[1]} has attendence {row[2]} in subject {row[3]} and secured {row[7]} in {row[3]}.')    
            print(f'\tname is {row[0]} has grade {row[2]} in subject {row[1]}.')
            line_count += 1
    print(f'Processed {line_count} lines.')
    
window.mainloop()
