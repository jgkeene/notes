What exactly is a list comprehension?

It's just a quick way to make a list, by itterating over another sequence.

All list comprehensions have the form:

[ EXPR for TARGET in ITTERABLE ...]

All list comprehensions can be re-writen as just a regular FOR loop

Take this list comprehension:

[(x,y,z) for x in range(1,30) for y in range(x,30) for z in range(y,30) if x**2 + y**2 == z**2]
# [(3, 4, 5), (5, 12, 13), (6, 8, 10), (7, 24, 25), (8, 15, 17), (9, 12, 15), (10, 24, 26), (12, 16, 20), (15, 20, 25), (20, 21, 29)]

It's equivalent is this FOR loop:

for x in range(1,30):
    for y in range(x,30):
        for z in range(y,30):
            if x**2 + y**2 == z**2:
                l.append((x,y,z))
# [(3, 4, 5), (5, 12, 13), (6, 8, 10), (7, 24, 25), (8, 15, 17), (9, 12, 15), (10, 24, 26), (12, 16, 20), (15, 20, 25), (20, 21, 29)]


Here's another list comprehension

[':#04}'.format(x) for x in range(256) if x%2==0]
# ['0000', '0002', '0004', '0006', '0008', '0010', '0012', '0014', '0016', '0018', '0020', '0022', '0024', '0026', '0028', '0030', '0032', '0034', '0036', '0038', '0040', '0042', '0044', '0046', '0048', '0050', '0052', '0054', '0056', '0058', '0060', '0062', '0064', '0066', '0068', '0070', '0072', '0074', '0076', '0078', '0080', '0082', '0084', '0086', '0088', '0090', '0092', '0094', '0096', '0098', '0100', '0102', '0104', '0106', '0108', '0110', '0112', '0114', '0116', '0118', '0120', '0122', '0124', '0126', '0128', '0130', '0132', '0134', '0136', '0138', '0140', '0142', '0144', '0146', '0148', '0150', '0152', '0154', '0156', '0158', '0160', '0162', '0164', '0166', '0168', '0170', '0172', '0174', '0176', '0178', '0180', '0182', '0184', '0186', '0188', '0190', '0192', '0194', '0196', '0198', '0200', '0202', '0204', '0206', '0208', '0210', '0212', '0214', '0216', '0218', '0220', '0222', '0224', '0226', '0228', '0230', '0232', '0234', '0236', '0238', '0240', '0242', '0244', '0246', '0248', '0250', '0252', '0254']

Ant it's its equivalent, as a simple FOR loop

for x in range(256):
    if x%2==0:
        l.append(':#04}'.format(x))
# ['0000', '0002', '0004', '0006', ..]



What's a generator comprehension then?

They are simply a generator expression, that is wraped in a pair of parenthesis

Otherwise, the syntax and the way of working is like list comprehension,

But a generator comprehension returns a generator instead of a list:

x = (x **2 for x in range(20))
type(x)
# generator 

type([x])
# list


What exactly is a lambda?

It's an inline function, with 1 expression, that gets evaluated when the function is called

All lambdas have the form:

lambda ARGUMENTS : EXPRESSION

All lambdas functions can be re-writen as a regular FUNCTION

Take this lambda for example:

f = lambda x,y : x+y
f(2,2)
# 4

It's equivalent is this regular FUNCTION:

def f(x,y):
    return x+y
f(2,2)
# 4

