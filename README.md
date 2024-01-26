import random
import tkinter


def draw(event):
    global y0
    global x0
    if event.keysym == 'Up':
        canvas.move(oval, 0, -10)
        y0 -= 10
    if event.keysym == 'Down':
        canvas.move(oval, 0, 10)
        y0 += 10
    if event.keysym == 'Right':
        canvas.move(oval, 10, 0)
        x0 += 10
    if event.keysym == 'Left':
        canvas.move(oval, -10, 0)
        x0 -= 10
    if event.keysym == '1':
        canvas.itemconfig(oval, fill='red')
    if event.keysym == '2':
        canvas.itemconfig(oval, fill='blue')
    if event.keysym == '3':
        canvas.itemconfig(oval, fill='green')
    if event.keysym == 'c':
        color = '#%02x%02x%02x' % (random.randint(0, 255), random.randint(0, 255), random.randint(0, 255))
        canvas.itemconfig(oval, fill=color)
    if event.keysym == 'p':
        x0 = random.randint(0, 600)
        y0 = random.randint(0, 600)
        canvas.coords(oval, x0 - 100, y0 - 100, x0 + 100, y0 + 100)
    if x0 > 600:
        canvas.move(oval, -601, 0)
        x0 = 0
    if y0 > 600:
        canvas.move(oval, 0, -601)
        y0 = 0
    if x0 < 0:
        canvas.move(oval, 601, 0)
        x0 = 600
    if y0 < 0:
        canvas.move(oval, 0, 601)
        y0 = 600
    label.config(text=('Центр: ' + str(x0) + ', ' + str(y0)))

main = tkinter.Tk()
x0 = 300
y0 = 300
screensize = (600, 600)
canvas = tkinter.Canvas(main, bg='white', height=screensize[1], width=screensize[0])
oval = canvas.create_oval((200, 200), (400, 400), fill='yellow', width=3, outline='black')
canvas.pack()
label = tkinter.Label(main, text=('the centre: ' + str(x0) + ', ' + str(y0)))
label.pack()
main.bind('<KeyPress>', draw)
main.mainloop()
