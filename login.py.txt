import mysql.connector
mycon=mysql.connector.connect(host="localhost",user="root",passwd="root",database="cs")
cursor=mycon.cursor()
r="s"
while r=="s":
    print("Welcome to Employee Management System")
    print("1.Employee")
    print("2.Admin")
    print("3.Forgot Password")
    print("4.Exit")
    login=int(input("login as:"))
    if login==2:
        a=0
        while a<3:
            l=int(input("enter id:"))  
            L=[]
            P=[]
            y=""
            L.append(l)
            cursor.execute("select Id from employee where job ='Admin';")
            t=cursor.fetchall()
            if tuple(L) in t:
                p=int(input("enter password:"))
                f="select password from employee where Id='"+str(l)+"'"
                P.append(p)
                cursor.execute(f)
                F=cursor.fetchall()
                if tuple(P) in F:
                    print("welcome")
                    y="a"
                    a=4
                else:
                    print("Wrong password!")
                    a+=1
            else:
                print("employee id doesn't exists")
                a+=1
        if a==3:
            y="b"
        while y=="a":
            print("1.Add employee details")
            print("2.Delete employee details")
            print("3.Promote employee")
            print("4.View employee details:")
            print("5.update")
            print("6.Notice")
            print("7.Logout")
            ch=int(input("enter your choice:"))
            if ch==1:
                Name = input("Enter Employee Name : ")
                dept=input("enter department :")
                Post = input("Enter Employee Post : ")
                Salary = int(input("Enter Employee Salary : "))
                Id=int(input("enter id :"))
                cursor.execute("select Id from employee")
                iD=cursor.fetchall()
                lis=[Id]
                if tuple(lis) in iD:
                    print("this employee id already exists")
                else:
                    email=input("enter email address :")
                    passwd=int(input("enter password :"))
                    doj=input("enter date of joining :")
                    data = (Id, Name,doj,dept,Post, Salary,email,passwd)
                    sql = "insert into employee values(%s,%s,%s,%s,%s,%s,%s,%s)"
                    cursor.execute(sql,data)
                    mycon.commit()
                    print("new record inserted")
            elif ch==2:
                e=int(input("enter employee Id to be deleted:"))
                li=[e]
                cursor.execute("select Id from employee")
                fetc=cursor.fetchall()
                cursor.execute("select lcase(job) from employee where Id="+str(e))
                fg=cursor.fetchone()
                adm=("admin")
                if adm in fg:
                    print("can't delete")
                    
                elif tuple(li) in fetc:
                    dele="delete from employee where id='"+str(e)+"'"
                    cursor.execute(dele)
                    print("employee deleted")
                    mycon.commit()
                else:
                    print("employee Id does not exist")
            elif ch==3:
                I=int(input("enter employee id :"))
                Li=[I]
                cursor.execute("select Id from employee")
                fet=cursor.fetchall()
                if tuple(Li) in fet:
                    p=input("enter new post:")
                    z=int(input("enter increment:"))
                    Z=(z,I)
                    P=(p,I)
                    inc="update employee set salary= salary+%s where Id=%s;"
                    cursor.execute(inc,Z)
                    po="update employee set job=%s where Id=%s;"
                    cursor.execute(po,P)
                    print("Employee promoted")
                    mycon.commit()
                else:
                    print("entered empolyee id does not exist")
            elif ch==4:
                print("1.view all employees")
                print("2.view employees by department")
                print("3.view employees by job")
                j=int(input("enter your choice :"))
                if j==1:
                    cursor.execute("select * from employee;")
                    DATA=cursor.fetchall()
                    for row in DATA:
                        print(row)
                elif j==2:
                    d=input("enter department :")
                    D="select * from employee where department='"+d+"'"
                    cursor.execute(D)
                    depar=cursor.fetchall()
                    for row in depar:
                        print(row)
                elif j==3:
                    c=input("enter job:")
                    cursor.execute("select * from employee where job='"+c+"'")
                    joe=cursor.fetchall()
                    for row in joe:
                        print(row)
                else:
                    print("enter your choice correctly!")
            elif ch==5:
                print("1.update email id")
                print("2.update password")
                print("3.update name")
                print("4.update department")
                print("5.update salary")
                up=int(input("enter your choice:"))
                if up==1:
                    em=input("enter email id:")
                    k=int(input("enter employee id:"))
                    li=[k]
                    cursor.execute("select Id from employee")
                    fetc=cursor.fetchall()
                    if tuple(li) in fetc:
                        cursor.execute("update employee set email='"+em+"'where Id='"+str(k)+"'")
                        mycon.commit()
                        print("email id updated")
                    else:
                         print("entered employee id does not exist")
                elif up==2:
                    emp=int(input("enter employee id:"))
                    pas=int(input("previous password:"))
                    pn=int(input("new password:"))
                    i=[emp]
                    cursor.execute("select Id from employee")
                    fetc=cursor.fetchall()
                    if tuple(i) in fetc:
                        ln="select password from employee where Id='"+str(emp)+"'"
                        cursor.execute(ln)
                        ti=cursor.fetchone()
                        if pas in ti:
                            cursor.execute("update employee set password='"+str(pn)+"'where Id='"+str(emp)+"'")
                            mycon.commit()
                            print("password updated")
                        else:
                            print("incorrect password!")
                    else:
                        print("employee ID does not exists")
                elif up==3:
                    EMP=int(input("enter employee id:"))
                    i=[EMP]
                    cursor.execute("select Id from employee")
                    fetc=cursor.fetchall()
                    if tuple(i) in fetc:
                        NamE=input("enter new name:")
                        cursor.execute("update employee set Name='"+NamE+"'where Id='"+str(EMP)+"'")
                        print("name updated")
                        mycon.commit()
                    else:
                        print("employee id entered does not exist")
                elif up==4:
                    EmP=int(input("enter employee id:"))
                    li=[EmP]
                    cursor.execute("select Id from employee")
                    fetc=cursor.fetchall()
                    if tuple(li) in fetc:
                        de=input("enter new department:")
                        cursor.execute("update employee set department='"+de+"' where Id='"+str(EmP)+"'")
                        print("department updated")
                        mycon.commit()
                    else:
                        print("entered employee id does not exist")
                elif up==5:
                    ee=int(input("enter employee id:"))
                    li=[ee]
                    cursor.execute("select Id from employee")
                    fetc=cursor.fetchall()
                    if tuple(li) in fetc:
                        sala=int(input("enter new salary:"))
                        cursor.execute("update employee set salary='"+str(sala)+"' where Id='"+str(ee)+"'")
                        mycon.commit()
                        print("salary has been updated")
                    else:
                        print("entered employee id does not exist")
            elif ch==6:
                W=open("aim.txt","w")
                w=input("enter notice:")
                W.write(w)
                W.close()
                        
            elif ch==7:
                break
            else:
                print("invalid choice")

                
    elif login==1:
        b=0
        while b<3:
            G=int(input("enter id:"))  
            g=[]
            Y=[]
            C="c"
            z=""
            Y.append(G)
            u="select Id from employee;"
            cursor.execute(u)
            m=cursor.fetchall()
            if tuple(Y) in m:
                R=int(input("enter password:"))
                q="select password from employee where Id='"+str(G)+"'"
                g.append(R)
                cursor.execute(q)
                Fet=cursor.fetchall()
                if tuple(g) in Fet:
                    print("welcome")
                    b=1
                    C="a"
                else:
                    print("Wrong password!")
                    b+=1
                      
            else :
                print("employee id doesn't exists")
                b+=1
            if b==3:
                C="b"
            while C=="a":
                print("1.View my Info")
                print("2.Change my Password")
                print("3.Update my Info")
                print("4.View Notice")
                print("5.Logout")
                cho=int(input("enter your choice:"))
                if cho==1:
                    cursor.execute("select * from employee where Id='"+str(G)+"'")
                    print(cursor.fetchall())
                elif cho==2:
                    passw=int(input("previous password:"))
                    pasn=int(input("new password:"))
                    ln="select password from employee where Id='"+str(G)+"'"
                    cursor.execute(ln)
                    tI=cursor.fetchone()
                    if passw in tI:
                        cursor.execute("update employee set password='"+str(pasn)+"'where Id='"+str(G)+"'")
                        print("password changed")
                        mycon.commit()
                    else:
                        print("incorrect password!")
                elif cho==3:
                    print("1.Update my Name")
                    print("2.Update my Email Id")
                    print("3.Update my Department")
                    upd=int(input("enter your choice:"))
                    if upd==1:
                        nav=input("enter new name:")
                        cursor.execute("update employee set Name='"+nav+"'where Id='"+str(G)+"'")
                        print("Name updated")
                        mycon.commit()
                    elif upd==2:
                        ema=input("enter new email id:")
                        cursor.execute("update employee set email ='"+ema+"'where Id='"+str(G)+"'")
                        print("Email Id updated")
                        mycon.commit()
                    elif upd==3:
                        dep=input("enter new department:")
                        cursor.execute("update employee set department ='"+dep+"'where Id='"+str(G)+"'")
                        print("department changed")
                        mycon.commit()
                elif cho==4:
                    file=open("aim.txt","r")
                    line=file.readline()
                    print(line)
                    file.close()
                elif cho==5:
                    C="b"
                    b=4
    elif login==3:
        Id=int(input("enter id:"))
        Name=input("enter name:")
        sal=int(input("enter salary:"))
        email=input("enter email:")
        t=(Id,Name.lower(),sal,email.lower())
        l=[t]
        cursor.execute("select Id,Name,salary,email from employee where Id='"+str(Id)+"'")
        s=cursor.fetchall()
        if l==s:
            newpass=int(input("enter new password:"))
            cursor.execute("update employee set password='"+str(newpass)+"' where Id='"+str(Id)+"'")
            mycon.commit()
            print("password has been changed")
            print("try to login using new password")
        else:
            print("entered details do not match the actual details")
            print("try again")
                
    elif login==4:
        r="t"
        break
    else:
        print("invalid choice")
mycon.close()
#create table employee(Id int primary key,Name varchar(20),DOJ date,department varchar(20),job varchar(20),salary int,email varchar(20), password int);


