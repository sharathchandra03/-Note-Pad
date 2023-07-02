# -Note-Pad
# -GUI project about how to create Note pad like Application
from tkinter import *
from PIL import ImageTk,Image
from tkinter import StringVar,IntVar,scrolledtext,END,filedialog
import tkinter.messagebox as msg


root=Tk()
root.geometry("600x600")
root.title("Note Pad")
root.resizable(0,0)
root.iconbitmap("pad.ico")

#colors
root_color="white"
menu_color="yellow"
text_color="black"
root.config(bg=root_color)
#creating Frames
menu_frame=Frame(root,bg=menu_color)
text_frame=Frame(root,bg=text_color)
menu_frame.pack()
text_frame.pack()

#defining functions

def change_font(event):
    if style_font.get()=='none':
        my_font = ((font_family.get()),(size_family.get()))
    else:
        my_font = ((font_family.get()),(size_family.get()),(style_font.get()))

    #changing text in text box
    text_box.config(font=my_font)


def close_window():
    box=msg.askyesno("Close Note","Are You Sure You Want To Close The Note ?")
    if box==1:
        root.destroy()


def new_note():
    new=msg.askyesno("New Note","Are You Sure You Want a New Note ?")
    if new==1:
        text_box.delete(1.0,END)


def save_file():
    save_name = filedialog.asksaveasfilename(initialdir="./",title="Save Note",filetypes=(("Text File","*.txt"),("All Files","*.*")))
    with open(save_name,'w') as f:
        f.write(text_box.get("1.0",END))


def open_file():
    open_name=filedialog.askopenfilename(initialdir="./",title="Open File",filetypes=(("Text File","*.txt"),("All Files","*.*")))
    with open(open_name,"r") as f:
        text_box.delete("1.0",END)
        change_font(1)
        text=f.read()
        text_box.insert("1.0",text)



#creating Buttons
new_image=ImageTk.PhotoImage(Image.open("final open file.png"))
new_file=Button(menu_frame,text="New File",image=new_image,command=new_note)
new_file.grid(row=0,column=0,padx=5,pady=5)

open_image=ImageTk.PhotoImage(Image.open("final file icon .png"))
open_file=Button(menu_frame,text="New File",image=open_image,command=open_file)
open_file.grid(row=0,column=1,padx=5,pady=5)

save_image=ImageTk.PhotoImage(Image.open("final save file.png"))
save_file=Button(menu_frame,text="New File",image=save_image,command=save_file)
save_file.grid(row=0,column=2,padx=5,pady=5)

close_image=ImageTk.PhotoImage(Image.open("final close file.png"))
close_file=Button(menu_frame,text="New File",image=close_image,command=close_window)
close_file.grid(row=0,column=3,padx=5,pady=5)

#creating drop box
fonts=['Terminal','calibri','Times New Roman','Wingdings']
font_family=StringVar()
font_family_drop=OptionMenu(menu_frame,font_family,*fonts,command=change_font)
font_family_drop.grid(row=0,column=4,padx=5,pady=5)
font_family.set('Terminal')
font_family_drop.config(width=15)

sizes=[8,12,14,16,18,20,24,57,76]
size_family=IntVar()
size_family_drop=OptionMenu(menu_frame,size_family,*sizes,command=change_font)
size_family_drop.grid(row=0,column=5,padx=5,pady=6)
size_family.set(12)
size_family_drop.config(width=3)

style=['none','italic','bold','underline']
style_font=StringVar()
style_font_drop=OptionMenu(menu_frame,style_font,*style,command=change_font)
style_font_drop.grid(row=0,column=6,padx=5,pady=5)
style_font.set('none')
style_font_drop.config(width=9)

#creating Text box
my_font=((font_family.get()),(size_family.get()))
text_box=scrolledtext.ScrolledText(text_frame,width=500,height=500,font=my_font)
text_box.pack()

root=mainloop()
