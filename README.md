# M-thodes_Explicit
Dans ce fichier nous retrouverons les méthodes de résolution d'équations différentielles temporelles telle que Euler et Range-Kutta

# Euler Explicite
 #coding:utf-8
"""
Nous cherchons ici à resoudre une équation différentielle d'ordre 1 du type :
y'(t)=F(t,y(t))
"""

import matplotlib.pyplot as plt
import math
import scipy as sc
import numpy as np 

global t 
global Temps1
global Temps2
Temps1=[]
Temps2=[]

def F(y,t):
	return 2*y+0*t

def Sol_Exacte(y0,t0,tf,n):
	t=t0
	y=y0
	global Temps2
	Temps2=[t0]
	Sol_Exacte=[y0]
	for i in range(n):
		t+=0.1
		y=np.exp(2*t)
		Temps2.append(t)
		Sol_Exacte.append(y)
  return Sol_Exacte

def Euler_explicit(f,t0,tf,y0,n):
	t=t0
	y=y0
	h=(tf-t0)/float(n)
	global Temps1
	Temps1=[t0]
	Approx_solution = [y0]
  for i in range(n):
		y += h*f(y,t)
		t += h 
		Approx_solution.append(y)
		Temps1.append(t)
    plt.xlabel("Temps")
	  plt.ylabel("y(t)")
	return Approx_solution, Temps1

Euler_explicit(F,0,5,1,200)
Sol_Exacte(1,0,5,50)

plt.plot(Temps1,Euler_explicit(F,0,5,1,200),'b',label="Sol_Aprox")
plt.plot(Temps2,Sol_Exacte(1,0,5,50),'r',label="Sol_Exacte")
plt.legend(loc='upper left')
plt.show()
