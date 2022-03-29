from cgitb import text
from email.mime import image
from importlib.resources import path
from tkinter import *
from tkinter import filedialog
from turtle import title, width
from moviepy import *
from moviepy.editor import VideoFileClip
from pytube import YouTube 
import shutil #move files/folders to any directory

#Fun
def selectPath():
    path = filedialog.askdirectory() #enables user to select a file directory from the explorer
    path_lable.config(text=path)


def downloadFile():
    get_UserPath = link_field.get() 
    get_SelectedPath = path_lable.cget("text")
    screen.title('Downloading ... ')

    vid = YouTube(get_UserPath).streams.get_highest_resolution().download()
    vidvid = VideoFileClip(vid)
    vidvid.close()
    shutil.move(vid, get_SelectedPath)
    screen.title('Download Completed! ')

screen = Tk()

title = screen.title('YouTube Downloader')
canvas = Canvas(screen, width=600, height=600)
canvas.configure(bg='white')
canvas.pack()


logo=PhotoImage(file='Ylogo.png')

logo=logo.subsample(2,2) #resize the image
canvas.create_image(300, 200, image=logo)

link_field = Entry(screen, width=50, background='gainsboro')
link_label = Label(screen, text="Enter Download Link!", font=('Arial',15), background='white')


#selecting the path
path_lable = Label(screen, text="Select A Path For The Dowloaded video",font=('Arial',15),background='white')
Sbtn= Button(screen, text='Sellect', command=selectPath,)
#widges
canvas.create_window(300,450,window=path_lable)
canvas.create_window(300,490,window=Sbtn)

#widges
canvas.create_window(300,370, window=link_label)
canvas.create_window(300,400, window=link_field)

#btns
btn= Button(screen, text="Download File", command=downloadFile)

#add to canvas
canvas.create_window(300,550,window=btn)


screen.mainloop()
