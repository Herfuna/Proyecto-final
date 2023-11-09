# Universidad Mariano Gálves de Guatemala
## Centro regional Boca del Monte
## _Curso de Algoritmos_

[![N|Solid](https://www.universidadesonline.com.gt/logos/thumb/logo-universidad-mariano-galvez-de-guatemala.png)](https://umg.edu.gt/miumg/)
## Conversiones de unidades de longitud
## _Proyecto Final:_
'''Aplicacion Grafica que puede leer un archivo de texto'''
import sys
from tkinter import *
from tkinter import messagebox
from tkinter import filedialog
import webbrowser
ventana = Tk()
ventana.geometry('650x510+500+200')
archivo_abierto = None

def acercade():
    messagebox.showinfo('Proyecto Final', '''Practamente esta aplicacion es un mini editor de texto asi como notepad, el cual muestra las funciones mas basicas posibles.
Licencia de Usuario Final (EULA) para la Aplicación web "HERFUNA.
                        Version: 1.20"''')

def actualizar():
    messagebox.showwarning('Actualizacion', '''Actualizacion Disponible
debe actualizar el sistema visite:www.microsoft.com ''')

def salir():
    seleccion=messagebox.askokcancel('Salir', 'Desea salir de la aplicacion?')
    if seleccion==True:
        sys.exit()

def abrir():
    global archivo_abierto
    archivo_abierto = filedialog.askopenfilename(initialdir='C', filetypes=(('Ficheros Excel', '*.xlsx'), ('Fichero de texto', '*.txt'), ('Ficheros de c++', '*.cpp'), ('Fichero Py', '*.py'), ('Todos los Archivos', '*.*')))
    with open(archivo_abierto, 'r') as archivo:
        contenido = archivo.read()
        caja_principal.delete(1.0, END) 
        caja_principal.insert(INSERT, contenido)
   


def guardar():
    global archivo_abierto
    if archivo_abierto:
        contenido = caja_principal.get("1.0", "end-1c")
        with open(archivo_abierto, 'w') as archivo:
            archivo.write(contenido)
    else:
        guardarcomo()


def guardarcomo():
    contenido = caja_principal.get("1.0", "end-1c")
    nombre_archivo = filedialog.asksaveasfilename(defaultextension=".txt", filetypes=[("Archivos de texto", "*.txt")])

    if nombre_archivo:
        with open(nombre_archivo, 'w') as archivo:
            archivo.write(contenido)

def leer():
    archivo = open('cartain.txt', 'r')
    contenido = archivo.read()
    caja_principal.insert(INSERT, contenido)
    archivo.close()

def rehacer():
    caja_principal.edit_redo()

def deshacer():
    caja_principal.edit_undo()

def copy():
    caja_principal.focus()
    global seleccion
    seleccion = ventana.clipboard_get()

def pegar():
     if seleccion:
        caja_principal.insert(INSERT, seleccion)
def nuevo():
    caja_principal.delete(1.0, END)
def soporte():
    url = "https://imgur.com/a/LhtC55d"  
    webbrowser.open(url)

    
ventana.config(bg='#F9CF7A')
ventana.title('Proyecto Final')
ventana.resizable(width = False, height=False)
ventana.iconbitmap('gato.ico')

def integrantes():
    messagebox.showinfo('Participantes', '''Juan de Jesús Fuentes Hernández
7690-23-12943
Seccion: D
Grupo 7 ''')
    #Menus
barramenu=Menu(ventana)
ventana.config(menu=barramenu, width=600, height=900)
menuarchivo=Menu(barramenu, tearoff=0)
menuarchivo.add_command(label='Nuevo', command=nuevo)
menuarchivo.add_command(label='Leer', command=leer)
menuarchivo.add_command(label='Abrir', command=abrir)
menuarchivo.add_command(label='Guardar', command=guardar)
menuarchivo.add_command(label='Guardar como..', command=guardarcomo)
menuarchivo.add_separator()
menuarchivo.add_command(label='Cerrar', command=salir)

barramenu.add_cascade(label='Archivo', menu=menuarchivo)
#Menu parte 2
menuedit=Menu(barramenu, tearoff=0)
menuedit.add_cascade(label='Copiar', menu=copy)
menuedit.add_cascade(label='Pegar', menu=pegar)
menuedit.add_cascade(label='Deshacer', menu=deshacer)
menuedit.add_cascade(label='Rehacer', menu=rehacer)
barramenu.add_cascade(label='Edicion', menu=menuedit)
#Menu parte 3
menuayuda=Menu(barramenu, tearoff=0)
menuayuda.add_cascade(label='Soporte', command=soporte)
menuayuda.add_cascade(label='Actualizaciones', command=actualizar)
menuayuda.add_cascade(label='Integrantes', command=integrantes)
menuayuda.add_cascade(label='Acerca de..', command=acercade)
barramenu.add_cascade(label='Ayuda', menu=menuayuda)

#Ventana y cuadro
caja_principal=Text(ventana, font=('arial', 10), undo=True, wrap=WORD)
caja_principal.grid(row=1, column=0, padx=30, pady=25)
vertical=Scrollbar(ventana, command=caja_principal.yview)
vertical.grid(row=1, column=1, sticky='nsew')
caja_principal.config(yscrollcommand=vertical.set)
imagen = PhotoImage(file='dico.png')
Label(ventana, image=imagen).place(x=570, y=438)
mensaje = Label(ventana, text='Algortimos 2023', fg='darkred', font=('verdana', 10))
mensaje.grid(row=0, column=0)
ventana.mainloop()
