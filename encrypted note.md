# encrypted-note
#write a note and create password
import xlrd
import os
import json
import xlwt
import time
note_address_xls='note_number.xls'
password_address='password.json'
name_address='name.json'
try:
    with open(name_address,'r') as r:
        name=json.load(r)
except FileNotFoundError:
    with open(name_address,'w') as w:
        print("enter your name::::")
        name=input()
        json.dump(name,w)
#1
def new_password():
    print("Enter a new password:::::")
    passwordget=input()
    with open(password_address,'w') as w:
        password=json.dump(passwordget,w)
        print("if you want to see your new password press *see* else press another key")
        key=input()
        if key=='see':
            time.sleep(0.5)
            print(f"your password is:::  {password}")
            return True
        else:
            return True
#2      
def password1():
    try:
        print("Enter your password:")
        passwordget=input()
        with open(password_address,'r') as r:
            password=json.load(r)  
            if passwordget==password:
                return True
            else:
                return False
    except FileNotFoundError:
        new_password()
#3     
def note_address():
    try:
        note_address=[]
        a=xlrd.open_workbook(note_address_xls)
        b=a.sheet_by_index(0)
        for i in range(b.nrows):
            note_address.append(b.cell_value(i,0))
        return note_address
    except FileNotFoundError:
        note_address_new()
    
def note_address1():
    try:
        note_address1=[]
        a=xlrd.open_workbook(note_address_xls)
        b=a.sheet_by_index(0)
        for i in range(b.nrows):
            note_address1.append(b.cell_value(i,0))

        return note_address1
    except FileNotFoundError:
        return note_address_new()
#4      
def note_address_new():
    try:
        note_address=[]
        a=xlrd.open_workbook(note_address_xls)
        b=a.sheet_by_index(0)
        for i in range(b.nrows):
            note_address.append(b.cell_value(i,0))
        note_address.append(note_address[-1]+'+')
        
        os.remove(note_address_xls)
        a=xlwt.Workbook()
        b=a.add_sheet("address sheet")
        for i in range(len(note_address)):
            b.write(i,0,note_address[i])
        a.save(note_address_xls)
        return note_address
    except FileNotFoundError:
        note_address=['a']
        a=xlwt.Workbook()
        b=a.add_sheet("sheet address")
        b.write(0,0,'a')
        a.save(note_address_xls)
        return note_address
#5    
def changing_note(note_address):
    address=note_address+'.txt'
    time.sleep(0.5)
    print("if you want to add a note press *add* and you want to delete note an write new note press *new*")
    key=input()
    if key=='new':
          time.sleep(0.5)
          print("write a new note")
          text=input()
          with open(address,'w') as w:
              w.write(text,w)
              print("SUCCESS")
    elif key=='add':
        time.sleep(0.5)
        print("write a text")
        text=input()
        with open(address,'a') as a:
            a.write(text)
            print("a text added")
    else:
        print("wrong key try again::::")
        changing_note()
#6    
def writing_new_note(note_address):
    address=note_address+'.txt'
    time.sleep(0.5)
    with open(address,'w') as w:
        print("write your text:::::")
        text=input()
        w.write(text)
        time.sleep(0.5)
        print("*SUCCESS*")
        
#7
def see_and_change_name():
    with open(name_address,'r') as r:
        name=json.load(r)
    print(f"your name is {name}")
    time.sleep(0.9)
    print('\n'*3)
    print("if you want to change your name press c else press another key")
    key=input()
    if key=='c':
        with open(name_address,'w') as w:
            print("enter your name::::")
            name=input()
            json.dump(name,w)
            print("SUCCESS")
    else:
        return name
    
#8
def counter_note():
    try:
        note_address=[]
        a=xlrd.open_workbook(note_address_xls)
        b=a.sheet_by_index(0)
        for i in range(b.nrows):
            note_address.append(b.cell_value(i,0))
        print(f"you have a {len(note_address)} note now")
        return len(note_address)
    except FileNotFoundError:
        print("you have not a note yet")
        

try:
    with open(password_address,'r') as r:
        password=json.load(r)
        password
except FileNotFoundError:
    print("Enter your favourite password::::")
    password=input()
    with open(password_address,'w') as w:
        password=json.dump(password,w)
        
            
print(f"HELLO  {name}")
time.sleep(0.6)
print('\n'*3)
print("welcome")
time.sleep(1)
print('\n'*6)


for i in range(3):
    time.sleep(0.60)
    print(f"you have {3-i} more chance")
    if password1() is True:
        key='s'
        while(key!='quit'):
            print("***************MENU********************")
            print('\n'*3)
            time.sleep(0.5)
            print("**if you want to see and change your name press-------------------------------------------->> name <<")
            print("**if you want write a new note press-------------------------------------------->> new <<")
            print("**if you want to see a past note press-------------------------------------------->> past <<")
            print("**if you want to see a number of note press-------------------------------------------->> number <<")
            print("**if you want to change your password press-------------------------------------------->> pass <<")
            print("**if you want to exit this app press-------------------------------------------->> quit <<")
            key=input()
            if key=='name':
                see_and_change_name()
            
            elif key=='new':
                note_address=note_address_new()
    
                address=note_address[-1]
                writing_new_note(address)
            
            elif key=='past':
                time.sleep(0.6)
                note_address=note_address1()
                print("your notes address is::::")
                time.sleep(0.8)
                for i in range(len(note_address)):
                    print(f"{i}={note_address[i]}")
                    time.sleep(0.2)
                print("if you see a note enter the number of note")
    
                time.sleep(0.8)
                print('\n'*2)
                print("and if you want to delete a note press del")
                key=input()
                if key=='del':
                    print("press the number of note::::")
                    l=input()
                    if int(l) in range(len(note_address)):
                        try:
                            os.remove(note_address[int(l)]+'.txt')
                        except FileNotFoundError:
                            time.sleep(0.5)
                            print("file is empty")
                    else:
                        time.sleep(0.2)
                        print("you presssed keu incurectly")
                elif int(key) in range(len(note_address)):
                    print("your note is::::")
                    time.sleep(0.5)
                    try:
                        with open(note_address[int(key)]+'.txt','r') as r:
                             print(r.read())
                    except FileNotFoundError:
                        print("file is empty")
                    print("if you want to change this note press ch else press another key")
                    lo=input()
                    if lo=='ch':
                        changing_note(note_address[int(key)])
                    else:
                        None
                else:
                    time.sleep(0.6)
                    print("**you pressed wrong key**")
                    
            
            elif key=='number':
                counter_note()
            
            elif key=='pass':
                with open(password_address,'r') as r:
                    password=json.load(r) 
                print(f"your password is {password}")
                time.sleep(0.8)
                print('\n'*2)
                print("if you want to change your password press *ch* else press another key")
                key=input()
                if key=='ch':
                    new_password()
                    time.sleep(0.3)
                    print('\n'*2)
                    print("SUCCESS")
            
            else:
                key=='quit'
        break
        
    else:
        time.sleep(0.6)
        print("**WRONG**")
