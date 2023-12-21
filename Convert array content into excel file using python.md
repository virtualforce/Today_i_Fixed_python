## Problem
...  
If you want to convert array contents into an excel file then you can use the following code.  ...

## Environment
... Visual Studio Code, Python ...

## How you fix it
... We use openpyxl library of python and then first give the column headers name. Then use date time to fill in values in our columns of updated at and created at. finally, we express the name of the meal items and use rows and columns to insert and save data in an excel file.
 ...

## Solution
```import openpyxl

# Create a new Excel file.
wb = openpyxl.Workbook()

# Create a worksheet.
ws = wb.create_sheet()

# Set the column headers.
headings = ["Name", "Ingredients", "Diet_Category", "CreatedAt", "UpdatedAt"]
for i in range(len(headings)):
    ws.cell(row=1, column=i+1).value = headings[i]

# Get the current date and time.
import datetime
now = datetime.datetime.now()

# Set the current date and time in the CreatedAt and UpdatedAt columns.
for i in range(3, 123):
    ws.cell(row=i, column=4).value = now
    ws.cell(row=i, column=5).value = now

# Insert the meal item names into the Name column.
meal_item_names = """
Berries
Daal
fish curry
Aloo chaat
Hard-boiled egg
Saag
Grilled chicken breast
Cauliflower
Whole wheat Chapati
Tinday sabzi
Paratha
Naan
Butter chicken
Aloo gosht
Tandoori chicken
Gajar sabzi
Baingan sabzi
Whole-wheat cereal
Salad
Lentil soup
White Chana masala
Yakhni pulao
Dum aloo
salted Lassi
potato cutlet
Biryani
haleem
Daal makhani
Karela sabzi
Shami kebab
Brown rice
Chicken qeema
Chicken Nihari
Chana masala
Malai boti
Vegetable soup
Gobi sabzi
Seasonal Fruit
Aloo sabzi
Tea
Milk
Chicken korma
Baingan bharta
Qeema aloo
steamed fish
grilled fish
mutton kebab
Nuts
Zarda
Chicken biryani
Vegetable biryani
mint raita
zeera raita
bhindi sabzi
Tori sabzi
Khichdi
Seekh kebab
chicken Kebab
Yogurt
Kofta curry
band Gobi sabzi
Haleem
Black Chana masala
Oatmeal
Fish curry
Shimla mirch sabzi
Fried rice
boiled rice
brown rice
vegetable curry
Chicken kebabs
Peshawari chapli kebab
channa chaat
Broccoli
Black coffee
multigrain chapatti
Multigrain bread slice
scrambled egg
vegetables
Minced Chicken
Mixed Daal
Whole grain biscuits
Steamed chicken
fist of nuts
cooked lentils
Chamomile Tea
Zeera qehwa
Chia Seeds Water
Flaxseed Water
Cinnamon Water
Tea without sugar
Tea with Jaggery
fist of unsalted nuts
green tea
peppermint tea
lemongrass tea
ginger tea
fennel seeds tea
cinnamon tea
licorice tea
moringa tea
skinless chicken
kidney beans gravy
soaked figs
vegetable omelette
beans kabab
caesar salad
beans salad
fruit salad
pasta
roasted chickpeas
chickpea rice
vegetable chicken salad
chicken curry
milk coffee
multigrain pasta
chia seeds pudding
chicken sandwich
iced coffee

""".split("\n")

for i in range(3, 123):
    ws.cell(row=i, column=1).value = meal_item_names[min(i-3, len(meal_item_names)-1)] if i <= 122 else None

# Save the Excel file.
wb.save("meal_items.xlsx")
print("file saved")
```
