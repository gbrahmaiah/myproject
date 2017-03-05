# myproject
import cx_Oracle
conn=cx_Oracle.connect("scott","tiger","localhost")
cursor=conn.cursor()
d={1:'insert',2:'update',3:'select',4:'delete',5:'exit'}
print "*"*5,"DATABASE MANIPULATION","*"*5 
for i in d.keys():
    print i,".",d[i]
#x=input("enter your choice from [1-5]:")
xloop=True
while xloop:
    x=input("enter your choice from [1-5]:")
    if d.has_key(x):
        y=d[x]
        if y=="insert":
            iloop=True
            while iloop:
                insert=raw_input("do you want to insert the date:Y/N:")
                if insert=='Y':
                    dept_name=raw_input("enter dept_name:")
                    cursor.execute("insert into dept2(dept_name)values('%s')"%(dept_name))
                    conn.commit()
                    cursor.close()
                    conn.close()
                    print "value is inserted sucessfully"
                elif insert=='N':
                    iloop=False                 
                #xloop=False
        elif y=="update":
            old_dept_name=raw_input("enter old_dept_name:")
            new_dept_name=raw_input("enter new_dept_name:")
            cursor.execute("update dept2 set dept_name='%s' where dept_name='%s'"%(new_dept_name,old_dept_name))
            conn.commit()
            cursor.close()
            conn.close()
            print "sucessfully updated"
            xloop=False 
        elif y=="select":
            dept_name=raw_input("enter table name:")
            cursor.execute("select * from %s"%(dept_name))
            for row in cursor:
                print row
            conn.commit()
            cursor.close()
            conn.close()
            print "data successfully fetched:"
            xloop=False
        elif y=="delete":
            dloop=True
            while dloop:
                delete=raw_input("do you want to delete:Y/N:")
                if delete=='Y':
                    table_name=raw_input("enter table_name:")
                    dept_name=raw_input("enter col_name:")
                    cursor.execute("delete from %s where dept_name='%s'"%(table_name,dept_name))
                    conn.commit()
                    cursor.close()
                    conn.close()
                    print "the row deleted"
                elif delete=='N':
                    print "sucessfully exit from the data base connection:"
                    dloop=False
                    xloop=Falsess
        else:
            print "exit successfully"
            xloop=False
    else:
        print "your entered invalid choice please enter the valid choice between 1 to 5"
    
   
