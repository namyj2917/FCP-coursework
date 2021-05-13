# FCP-coursework


import turtle
import random

tur=[]
pos_x=[]
pos_y=[]
covid_list=[]
covid_dt=[]
day=1
N=1000
n=2
p=0.3
nMin=1
nMax=6

i=0
while True:
    t1= turtle.Turtle()
    if i==0:
        screen=t1.getscreen()
        screen.setup(600,600)
        t1.shape("circle")
        t1.speed("fastest")
        t1.penup()
        
        tmp_x= random.randint(-250,250)
        tmp_y= random.randint(-250,250)
        t1.goto(tmp_x,tmp_y)
        
        close_fg= False
        p_cnt= len(pos_x)
        for i in range(p_cnt):
            ds=t1.distance(pos_x[i],pos_y[i])
            if ds<1:
                close_fg= True
            
        if close_fg:
            t1. hideturtle()
            print("proximity occurence")
            continue
        
        tur.append(t1)
        pos_x.append(tmp_x)
        pos_y.append(tmp_y)
        i+= 1
        print("t"+str(i), end=" ")
        
        if i >= N-1:
            break
        print(tmp_x,tmp_y)
        
        
for i in range(n):
    rnum=random.randrange(0,N)
    if covid_list.count(rnum):
        n+=1
        continue
    tur[rnum].color("red")
    print("Num of infection in Day1:",rnum)
    covid_list.append(rnum)
    covid_dt.append(1)
    

day_covid_list=covid_list[:]
print("day_covid_list:", day_covid_list)
print("covid_list:", covid_list)

while True:
    for i in day_covid_list:
        print("Infection:", i)
        idx=i
        f=random.randrange(nMin,nMax+1)
        print("Contact:",f)
        
        ds_list=[]
        ds_list.clear()
        for j in range(0,N):
            ds=tur[idx].distance(pos_x[j],pos_y[j])
            ds_list.append(ds)
        ds_list[idx]=10000
        d=0
        for j in range(0,N):
            tmp_idx= ds_list.index(min(ds_list))
            if covid_list.count(tmp_idx):
                ds_list[tmp_idx]=10000
                d += 1
                continue
        else:
            print("Contact:",idx,",",tmp_idx)
            ds_list[tmp_idx]=10000
            
            rp=random.randrange(0,100)
            if rp<p*100:
                covid_list.apppend(tmp_idx)
                tur[tmp_idx].color("blue")
                covid_dt.append(day)
                print("Infection:", tmp_idx)
                
            d +=1
        if d >= f:
            break
    
    day_covid_list=covid_list[:]
    print("day_covid_list:", day_covid_list)
    print("covid_list:",covid_list)
    
    if len(covid_list)>= N-1:
        break
    
print(covid_list)
print(covid_dt)

turtle.mainloop()
