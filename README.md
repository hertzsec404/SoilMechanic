# SoilMechanic
پروژه مکانیک خاک
یک مینی پروژه با پایتون برای رسم نمودار دانه بندی درشت دانه های محصول از آزمایش دانه بندی الک ها که شماره الک و وزن مانده روی هر الک داخل اسکریپت هارد کد شده است. برای اجرا مطمئن شوید که کتابخانه matplot را در محیط پایتون خود نصب کرده باشید. این اسکریپت بجز رسم نمودار - غیر لگاریتمی - درصد عبوری ها، آن را بصورت خروجی کنسول چاپ نیز میکند.


_____________________________________________________________________________________________________________________________________________________________________________________________
import subprocess
from math import *


def install_preneeds():
    try:
        subprocess.getoutput("pip install matplot c")
    except:
        print("Make sure u have installed \"matplotlib\" via pip\n>pip install matplot")


try:
    import matplotlib.pyplot as plt
except:
    install_preneeds()

plt.show()

# داده‌های نمونه
alak = [4.75, 2.00, 0.85, 0.425, 0.250, 0.180, 0.150, 0.075, 0]  # الک‌ها
jarame_mande = [0, 40, 60, 89, 140, 122, 210, 56, 12]  # جرم مانده روی هر الک

# محاسبه درصد عبوری ذرات
total_jarame_mande = fsum(jarame_mande)
print(f"Total germ = {total_jarame_mande}")
jerme_mande_tajamoee = list()
Z = 0
aboori = list()
number = 0
for jarame in jarame_mande:
    Z += 1
    number += jarame
    a = 100 * (1-(number / total_jarame_mande))
    aboori.append(a)
    darsad_tajamoee_oboori = round(100 * (number/total_jarame_mande), 2)
    jerme_mande_tajamoee.append(darsad_tajamoee_oboori)
    if darsad_tajamoee_oboori > 60:
        print(f"D60 [{darsad_tajamoee_oboori}]= {alak[-Z+1:]}", end="/")
    if darsad_tajamoee_oboori > 30:
        print(f"D30 [{darsad_tajamoee_oboori}]= {alak[-Z+1:]}", end="/")
    if darsad_tajamoee_oboori > 10:
        print(f"D10 [{darsad_tajamoee_oboori}]= {alak[-Z:]}", end="/")
    print("\n")
# ترسیم نمودار دانه بندی خاک و درصد عبوری ذرات
fig, ax1 = plt.subplots()
n = 0

for i in aboori:
    # try:
    print(
        f"Alacke [{alak[n]}] : Darsade Oboori [{i}] : JarmeMandeTajamoee [{jerme_mande_tajamoee[n]}]")
    n += 1
    # except:
    #     pass
ax1.plot(alak, aboori, marker='o', linestyle='-', color='b')
ax1.set_xlabel('ALAKHA')
ax1.set_ylabel('OBOORI')
ax1.invert_xaxis()

plt.title('Dane Bandi Zarat')

# نمایش نمودار
plt.show()
