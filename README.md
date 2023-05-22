# project
## Project Python
### Import các gói trước khi làm bài

import numpy as np

import pandas as pd

import matplotlib.pyplot as plt

import seaborn as sns
### Load dataset mẫu "taxis" trong gói seaborn vào biến df

df = sns.load_dataset("taxis")
### In ra 2 dòng đầu và 2 dòng cuối


df.head(2)

df.tail(2)
### Kiểm tra kiểu dữ liệu của từng cột

df.dtypes 

### Số lượng dòng và cột
df.shape
### Thời gian trải dài của Data 
df["pickup"].agg(["min", "max"])
### Lọc ra những chuyến xe có pickup time trong tháng 3 năm 2019 và lưu vào biến df_mar
cond = (df["pickup"] >= "2019-03-01") & (df["pickup"] < "2019-04-01")
df_mar = df[cond].copy()

### Kiểm tra lại xem kết quả có đúng như kỳ vọng
df_mar["pickup"].agg(["min", "max"])
### Số chuyến xe trong kết quả df_mar
df_mar.shape[0]
### Dùng df_mar đếm số chuyến xe cho mỗi ngày trong tuần
df_mar["pickup"].dt.day_name().value_counts()
## Các câu sau sử dụng biến df_mar
### Số lượng màu sắc cho các xe taxi và những màu nào?
df_mar["color"].nunique()

df_mar["color"].unique().tolist()
### Có những hình thức thanh toán nào?
df["payment"].unique().tolist()
### Tính tỉ trọng (%) số chuyến xe theo hình thức thanh toán 
df_mar["payment"].value_counts(normalize=True) * 100
### Tính trung bình tiền tip cho mỗi chuyến xe
df_mar["tip"].mean()
### Tính median  tiền tip cho mỗi chuyến xe

df_mar["tip"].median()
### Tính trung bình tiền tip cho mỗi chuyến xe theo từng hình thức payment
df_mar.groupby("payment")["tip"].mean() 
### Tính số lượng hành khách trung bình trên mỗi chuyến xe

df_mar["passengers"].mean()
### Tính tổng doanh thu trong tháng 3/2019

df_mar["fare"].sum()
### Xác định 5 khung giờ cao điểm (nhiều chuyến xe nhất)

df_mar["pickup"].dt.hour.value_counts().head(5)

df.head(2)
### Tạo cột same_borough có giá trị là 1 nếu cùng điểm pickup và dropoff, và nhận giá trị 0 nếu ngược lại

df_mar["same_borough"] =(df_mar["pickup_borough"] == df_mar["dropoff_borough"]).astype(int)

df_mar[["pickup_borough", "dropoff_borough", "same_borough"]].head()
### Đếm số chuyến xe có điểm pickup và dropoff 
### a) cùng borough 
### b) khác borough

df_mar["same_borough"].value_counts()
### Tính trung bình quãng đường di chuyển cho các chuyến xe xuất phát từ Manhattan

cond = df_mar["pickup_borough"] == "Manhattan"
df_mar.loc[cond, "distance"].mean()
### Tạo cột duration là thời gian giữa pickup và dropoff theo phút 

df_mar["duration"] = (df_mar["dropoff"] - df_mar["pickup"]).dt.total_seconds() / 60.
### Tính trung bình thời gian di chuyển cho mỗi chuyến xe có điểm pickup và dropoff 
### a) cùng borough và
### b) khác borough
df_mar.groupby("same_borough")["duration"].mean()
### Tạo cột pickup_hour là khung giờ pickup 

df_mar["pickup_hour"] = df_mar["pickup"].dt.hour
### Tạo cột km_per_min là số km đi được mỗi phút 

df_mar["km_per_min"] = df_mar["distance"] / df_mar["duration"]
### Tính tốc độ trung bình cho chuyến xe trong mỗi khung giờ pickup. Sắp xếp theo chiều tăng dần của
khung giờ

df_mar.groupby("pickup_hour")["km_per_min"].mean().sort_index() 
### Visualize kết quả 
#### Data to plot
plt_data = df_mar.groupby("pickup_hour")["km_per_min"].mean().sort_index()
#### Plot
fig, ax = plt.subplots(figsize=(7, 3))

plt_data.plot.bar(ax=ax)

ax.set_ylabel("Speed (km / min)")

ax.set_title("Average speed (km / min) by pickup hour")

plt.show()





## FIFA WORLD CUP 2018
### FIFA-World-Cup-Data-Analysis
FIFA world cup between 2018 data analysis using Power BI

#Transformation 
Downloading the dataset from the dataset online. CSV file and export it into the PowerBI. Tranferring the file into the Power Query Editor for transformation and verifying the data types and columns. Adjusting the columns and data data types where necessary. Appemding all the similar tables together inorder to have a complete table of the world cup dataset from 2018. After transformation, I closed and applied and created a rolling calender using DAX function from the data view.

I navigated to the model view and crested relationships with the data linking the facts tables to the dimension table.

Having modelled the data, I created measures with DAX and created my Dashboard. Joining several tiles together, measures and using slicers to navigate and filter through the dashboard.
### Story: FIFA Case Study - FIFA World Cup (2018)
The FIFA World Cup, commonly known simply as the FIFA World Cup, is an international football tournament contested by the senior men's national teams of members of the Football Confederation. International Football (FIFA), the sport's global governing body. Aggregate data set of statistics of players at Clubs in the 2017-2018 season before the players participated in the 2018 World Cup taking place in Russia.

The 2018 World Cup has 32 national teams, but the dataset only mentions 29 teams. The remaining 3 teams will be determined after the intercontinental Play-offs to determine the final 3 names to participate in the tournament in Russia. Germany is currently the highest-rated team capable of winning the tournament as they are the defending World Cup winners in 2014, topping the FIFA rankings and having players playing in the top clubs in Europe. Europe. Besides, teams such as England, France, Brazil, Argentina ... are also highly appreciated in this year's tournament for the chance to win the championship.
### Introduction
This project involved generating insight from a dataset containing information on the performance of the players present at the 2018 World Cup around the world before the tournament started. The following questions were asked to generate clear insight;

1. Ranking the team according to the FIFA index?
2. Top strongest teams based on player stats?
3. Top oldest and youngest football team?
4. Top teams with the best attack, the best defense, the best midfield?
5. Comparison between the big guys (top 1, 2 FIFA)?
6. Compare stats between superstars (Ronaldo, Messi)?
### Findings
In the given dataset, 29 national teams will participate in the FIFA World Cup and 3 teams will be determined after the intercontinental Play-off matches. 348 players from 151 clubs will participate in the World Cup held in Russia. Germany and Brazil are the 2 teams ranked 1st and 2nd in the FiFa Ranking. Germany has 1544 FIFA points and Brazil has 1384 FIFA points. Russia and Japan are the two teams with the lowest FIFA scores. Russia has 493 points and Japan has 528 points.The player with the most goals is Argentina's Messi with 34 goals, De Bruyne is the Belgian player with the most assists with 16 assists in the 2017-2018 season. Sergei Ignashevich is the oldest Russian player to attend the 2018 World Cup with 38 years old, the two youngest players are only 19 years old to attend the 2018 World Cup, Trent Alexander-Arnold of England and Kylian Mbappe of France.
### Team Germany
Germany before participating in the 2018 World Cup is the top 1 team in the FIFA rankings with 1544 points and is the defending champion of the 2014 World Cup. Germany before participating in the 2018 World Cup is being evaluated as a candidate team for the position. champions with a squad that is at the average age of 26 and has many excellent players playing at top European clubs such as: Ilkay Gundogan , Tony Kross , Marco Reus, ... Germany has a player in very high form, Timo Werners with 13 goals in the shirt of RB Leipzig is the player with the most goals in Germany in the 2017 season- 2018
### Team Brazil
Brazil before participating in the 2018 World Cup was the top 2 team in the FIFA rankings with 1384 points. Brazil before participating in the 2018 World Cup is being evaluated as a candidate team for the championship with a squad with an average age of 27.88 players and possessing many excellent players competing. Playing in the top European clubs such as: Neymar, Casemiro, Willian, ... Brazil has a player who is in very high form, Neymar with 19 goals in PSG's shirt is a player with many goals. Brazil's most successful team of the 2017-2018 season and will be expected to be the frontrunner in helping Brazil towards the championship. In the 2014 World Cup at home, Brazil was defeated by the Germans 7-1 and the Brazilians are looking forward to a chance to avenge the reigning World Cup champion.
### Lionel Messi
Lionel Messi is the captain of the Barcelona club as well as in the Argentina shirt. Despite turning 30 years old, the Argentine superstar still shows a destructive form with 30 goals and 12 assists in the 2017-2018 season. Messi is very much hoped by fans to lead the Argentine players in conquering the World Cup championship in Russia because he lost the championship 4 years ago when he lost to the Germans in the match. 2014 World Cup final This is a very difficult task because Argentina's squad besides Messi and Di Maria has no prominent names in the squad. 4 years ago Messi carried an Argentina team to the final and fans are hoping he will once again lead the team to the championship.
### Cristiano Ronaldo
Cristiano Ronaldo is the captain of the Portuguese team and is a player of Real Madrid. Despite turning 33 years old, the Portuguese superstar still shows a destructive form with 26 goals and 5 assists in the 2017-2018 season. Help Real club win 13th Champions League title and 3rd time in a row for this club. Ronaldo is very much hoped by fans to lead the Portuguese players in conquering the World Cup championship in Russia with the current form. Besides, Portugal is the reigning Euro champion with many superstars equally in all positions and is considered a bright candidate for the World Cup championship.
### OVERVIEW
<img width="782" alt="2023-05-22 (21)" src="https://github.com/maihoang2312001/project-power-bi/assets/114405595/813f7881-3f6c-4001-944e-74ede64b5dff">
<img width="775" alt="2023-05-22 (20)" src="https://github.com/maihoang2312001/project-power-bi/assets/114405595/ade5ae9a-a575-421b-a303-e8a09ba8ef51">
<img width="618" alt="2023-05-22 (19)" src="https://github.com/maihoang2312001/project-power-bi/assets/114405595/71406bb6-6594-4c61-9b67-9d5d7567e98c">


## BANK MARKETING ANALYST

### OVERVIEW
<img width="801" alt="2023-05-22 (12)" src="https://github.com/maihoang2312001/project-power-bi/assets/114405595/3e537a22-8bf9-4db1-9610-1cb26f9d0c34">
<img width="787" alt="2023-05-22 (13)" src="https://github.com/maihoang2312001/project-power-bi/assets/114405595/d365b458-35a0-4dd3-819c-dcf2a2773c0c">
<img width="787" alt="2023-05-22 (14)" src="https://github.com/maihoang2312001/project-power-bi/assets/114405595/ca410864-acf9-4cc8-b948-3d915cee9d27">
<img width="781" alt="2023-05-22 (15)" src="https://github.com/maihoang2312001/project-power-bi/assets/114405595/b1bc5edb-b19e-4072-b04a-7d906f54aa9e">
<img width="497" alt="2023-05-22 (16)" src="https://github.com/maihoang2312001/project-power-bi/assets/114405595/04b616d4-0374-4e3b-89f7-24b6d4400418">


