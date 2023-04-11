### School-Management-System

import getpass
import os
def addStudent(id,name,grade,m1,m2,m3,m4,m5):
    try:
        f=open("C:\\Users\\RUTU\\Desktop\\student.txt","a")
        log=open("C:\\Users\\RUTU\\Desktop\\login.txt","a")
        f.write(id+"\t"+name+"\t"+grade+"\t"+m1+"\t"+m2+"\t"+m3+"\t"+m4+"\t"+m5+"\n")
        log.write(id+"\t"+"password"+"\t"+"S"+"\n")
    finally:
        f.close()
        log.close()
def addTeacher(id,name,sub,clas):
    try:    
        f=open("C:\\Users\\RUTU\\Desktop\\Teacher.txt","a")
        log=open("C:\\Users\\RUTU\\Desktop\\login.txt","a")
        log.write(id+"\t"+"password"+"\t"+"T"+"\n")
        f.write(id+"\t"+name+"\t"+sub+"\t"+clas+"\n")
    finally:    
        f.close()
        log.close()
def searchStudent(id):
    try:    
        flag = 0
        file=open("C:\\Users\\RUTU\\Desktop\\student.txt","r")
        for i in file:
            lis = []
            lis = i.split()
            if(lis[0] == id):
                print(i)
                flag = 1
                break
        if not flag:
            print("Student id not found")
    finally:
        file.close()        
def searchTeacher(id):
    try:    
        flag = 0
        file=open("C:\\Users\\RUTU\\Desktop\\Teacher.txt","r")
        for i in file:
            lis = []
            lis = i.split()
            if(lis[0] == id):
                print(i)
                flag = 1
                break
        if not flag:
                print("Teacher id not found")
    finally:
        file.close()            
def update(id,m1,m2,m3,m4,m5):
    file=open("C:\\Users\\RUTU\\Desktop\\student.txt","r")
    fi= open("C:\\Users\\RUTU\\Desktop\\temp.txt","w")
    for i in file:
        l=[]
        l=i.strip().split()
        if l[0]==id :
            fi.writelines(l[0]+"\t"+l[1]+"\t"+l[2]+"\t"+m1+"\t"+m2+"\t"+m3+"\t"+m4+"\t"+m5+"\n")
        else:
            fi.writelines(i)
    file.close()
    fi.close()
    os.remove("C:\\Users\\RUTU\\Desktop\\student.txt")
    os.rename("C:\\Users\\RUTU\\Desktop\\temp.txt","C:\\Users\\RUTU\\Desktop\\student.txt")
    print("Student Record Updated!") 

def del_record(file_name,id):
    file=open(file_name,"r")
    fi= open("C:\\Users\\RUTU\\Desktop\\temp.txt","w")
    log=open("C:\\Users\\RUTU\\Desktop\\login.txt","r")
    t1=open("C:\\Users\\RUTU\\Desktop\\temp1.txt","w")
    for i in file:
        l=[]
        l=i.strip().split()
        if l[0]==id :
            print("Record Deleted!")
            pass
        else:
            fi.writelines(i)
    for j in log:
        l=[]
        l=j.strip().split()
        if l[0]==id :
            pass
        else:
            t1.writelines(j)        
    file.close()
    fi.close()
    log.close()
    t1.close()
    os.remove(file_name)
    os.rename("C:\\Users\\RUTU\\Desktop\\temp.txt",file_name)
    os.remove("C:\\Users\\RUTU\\Desktop\\login.txt")
    os.rename("C:\\Users\\RUTU\\Desktop\\temp1.txt","C:\\Users\\RUTU\\Desktop\\login.txt")
     
def adminmenu():
    while(True):
        print("\n\n1-Add Student\n2-Search Student\n3-Add Teacher\n4-Search Teacher\n5-Delete Student\n6-Delete Teacher\n0-Exit\n")
        ch=int(input("Enter the choice:"))
        if(ch==1):
            id=input("Enter ID:")
            name=input("Enter name:")
            grade=input("Enter grade:")
            m1,m2,m3,m4,m5=input("Enter marks with space:").split()
            addStudent(id,name,grade,m1,m2,m3,m4,m5)
        elif(ch==2):
            id=input("Enter student ID")
            searchStudent(id)  
        elif(ch==3):
            id=input("Enter ID:")
            name=input("Enter name:")
            sub=input("Enter subject:")
            clas=input("Enter Class:")
            addTeacher(id,name,sub,clas)
        elif(ch==4):
            id=input("Enter ID:")
            searchTeacher(id)
        elif(ch==5):
            filename="C:\\Users\\RUTU\\Desktop\\student.txt"
            id=input("Enter ID:")
            del_record(filename,id)
        elif(ch==6):
            filename="C:\\Users\\RUTU\\Desktop\\Teacher.txt"
            id=input("Enter ID:")
            del_record(filename,id)   
        elif(ch==0):
            break
def teachermenu():
    while(True):
        ch=int(input("\n\n1-Search Student\n2-Update Marks\n3-Change Password\n0-Exit\n"))
        if(ch==1):
            id=input("Enter student ID:")
            searchStudent(id)
        elif(ch==2):
            id=input("Enter ID:")
            m1,m2,m3,m4,m5=input("Enter marks with space:").split()
            update(id,m1,m2,m3,m4,m5) 
        elif(ch==3):
            u=input("Enter ID:")
            p=input("Enter Old Password:")
            createnewpass(u,p)
        elif(ch==0):
            break
        else:
            print("Invalid Choice!")
def studentmenu():
    while(True):
        ch=int(input("\n\n1-Change Password\n2-Search Student\n0-Exit\n"))
        if(ch==1):
            u=input("Enter ID:")
            p=input("Enter Old Password:")
            createnewpass(u,p)
        elif(ch==2):
            id=input("Enter ID:")
            searchStudent(id)
        elif(ch==0):
            break
        else:
            print("Invalid Choice!")                  
def password():
    username=input("Enter ID:")
    password=getpass.getpass()
    if(username=="admin" and password=="admin"):
        adminmenu()
    f1=open("C:\\Users\\RUTU\\Desktop\\login.txt","r")
    for i in f1.readlines():
        l=list(i.strip().split())
        if l[0]==username:
            if l[1]==password and l[2]=="T":
                f1.close()
                teachermenu()
            elif l[1]==password and l[2]=="S":
                f1.close()
                studentmenu()
            else:
                print("ID not Found")
def createnewpass(u,p):
    log=open("C:\\Users\\RUTU\\Desktop\\login.txt","r+")
    lg=open("C:\\Users\\RUTU\\Desktop\\temp.txt","w")
    s_alpha=l_alpha=digit=chrt=0
    for i in log.readlines():
        l=[]
        i=i.strip()
        l=i.split()
        if(l[0]==u and l[1]==p):
            l[1]=input("Enter New Password:")
            for k in l[1]:
                if k in "abcdefghijklmnopqrstuvwxyz":
                    s_alpha+=1
                elif k in "ABCDEFGHIJKLMNOPQRSTUVWXYZ":
                    l_alpha+=1
                elif k in "0123456789":
                    digit+=1
                elif k in "!@#$":
                    chrt+=1
            if s_alpha>=1 and l_alpha>=1 and digit>=1 and chrt>=1 and len(l[1])>=6 and len(l[1])<=12:        
                lg.writelines(l[0]+"\t"+l[1]+"\t"+l[2]+"\n")
                print("Password Changed!")
            else:
                print("Inavlid Password!\nPassword should contain 6-12 characters\nShould contain atleast 1 Capital letter\nShould contain one character [!@#$]\nTry Again\n")
        else:
            lg.writelines(i+"\n")    
    log.close()
    lg.close()
    if (len(l[1])>=8):
        os.remove("C:\\Users\\RUTU\\Desktop\\login.txt")
        os.rename("C:\\Users\\RUTU\\Desktop\\temp.txt","C:\\Users\\RUTU\\Desktop\\login.txt")                
print("SCHOOL MANAGEMENT SYSTEM")
while(True):
    jk=int(input("\n\n1-Login\n2-Logout\n"))
    if jk==1:
        password()
    elif jk==2:
        print("Logged Out\nThank You!")
        exit()       

