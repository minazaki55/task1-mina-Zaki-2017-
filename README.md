# task1-mina-Zaki-2017-
#Model bulding

from cobra import *

model = Model('Test')

A = Metabolite('A', compartment='c')
B = Metabolite('B', compartment='c')
C = Metabolite('C', compartment='c')
D = Metabolite('D', compartment='c')
ATP = Metabolite('ATP', compartment='c')

######## r0 : ======> A
r0 = Reaction('r0')
r0.name = 'R0'
r0.lower_bound = 1
r0.upper_bound = 1

######## r1 : A ======> B
r1 = Reaction('r1')
r1.name = 'R1'
r1.lower_bound = 0
r1.upper_bound = 1000

######## r2 : B <======> C
r2 = Reaction('r2')
r2.name = 'R2'
r2.lower_bound = -1000
r2.upper_bound = 1000

######## r4 : C ======> D
r4 = Reaction('r4')
r4.name = 'R4'
r4.lower_bound = 0
r4.upper_bound = 1000

######## ATP_r : A ======> ATP
ATP_r = Reaction('ATP_r')
ATP_r.name = 'ATP_r'
ATP_r.lower_bound = 0
ATP_r.upper_bound = 1000

######## r3 : ATP ======>
r3 = Reaction('r3')
r3.name = 'R3'
r3.lower_bound = 0.75
r3.upper_bound = 0.75

######## M : D ======>
M = Reaction('M')
M.name = 'M'
M.lower_bound = 0
M.upper_bound = 1000

r0.add_metabolites({A: 1})
r1.add_metabolites({A: -1, B: 1})
r2.add_metabolites({B: -1, C: 1})
r4.add_metabolites({C: -1, D: 1})
M.add_metabolites({D: -1})
ATP_r.add_metabolites({A: -1, ATP: 1})
r3.add_metabolites({ATP: -1})

model.add_reactions([r0, r1, r2, r3, r4, M, ATP_r])
model.objective = 'M'
x = model.optimize()
print(x)

y = model.summary()
print(y)
