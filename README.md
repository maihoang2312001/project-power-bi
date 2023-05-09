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
FIFA world cup between 2002 - 2018 data analysis using Power BI

#Transformation Downloading the dataset from the dataset online. CSV file and export it into the PowerBI. Tranferring the file into the Power Query Editor for transformation and verifying the data types and columns. Adjusting the columns and data data types where necessary. Appemding all the similar tables together inorder to have a complete table of the world cup dataset from 2002-2018. After transformation, I closed and applied and created a rolling calender using DAX function from the data view.

I navigated to the model view and crested relationships with the data linking the facts tables to the dimension table.

Having modelled the data, I created measures with DAX and created my Dashboard. Joining several tiles together, measures and using slicers to navigate and filter through the dashboard.
### The Story: FIFA - Football World Cup Case Study ( Year 2002 -2018)
The FIFA World Cup, often simply called the World Cup, is an international association football competition contested by the senior men's national teams of the members of the Fédération Internationale de Football Association (FIFA), the sport's global governing body. The championship has been awarded every four years since the inaugural tournament in 1930, except in 1942 and 1946 when it was not held because of the Second World War. The current champion is France, which won its second title at the 2018 tournament in Russia.

The 21 World Cup tournaments have been won by eight national teams. Brazil have won five times, and they are the only team to have played in every tournament. The other World Cup winners are Germany and Italy, with four titles each; Argentina, France, and inaugural winner Uruguay, with two titles each; and England and Spain, with one title each.
### Introduction
This project involves generating insight from 5 years dataset of the FIFA world cup tournament participated by 59 countries from different continents of the world. The following questions was asked to generate clear insight;

How many countries have played in the world cup (5 Years)?
Get the total games played; win, loss, Goals for/against.
The country with the highest and lowest appearance in the last five years?
The country with the highest and lowest games played.
The country with the highest and lowest games won.
The country with the highest and lowest games lost.
The country with the highest and lowest goals for?
The country with the highest and lowest goals against?
The country with the highest and lowest goals difference?
The country with the highest and lowest points?
### Findings
In the given dataset, 59 countries played the FIFA world cup. 640 games were played, win and loss games were 247 games respectively and total goals were 793. The countries with the highest and lowest games played were; Germany played 13 games while Angola and 13 other countries played total games of 3 each. The countries with the highest and lowest games won were Germany and Angola with total games won in 5years as 22 and 0 respectively. The countries with the highest and lowest games lost were South Korea and Angola, 9 and 1 respectively. The countries with the highest and lowest number of goals were Germany with 64 goals and Angola with 1 goal. Brazil has the highest number of goals against with a total number of 27 and Angola has the lowest goals-against against 2. Germany has the highest points of 69 while China PR has the lowest point of 0.
### Tailored Analysis
The total goal scored in the 5 years FIFA world cup dataset was 793 goals, of which; the highest and lowest goals was scored in 2014 and 2010 total goals of 171 and 145 respectively. However, in 2018, 2002, and 2006 goals scored were 169, 161, and 147 respectively.
### Team France
France got the most points in 2018 with a total of 19 points, most goals were scored in the same year with 14 goals, 6 games were won and 1 draw out of the 7 games played. In the last 5 years, France had downward and upward trends between 2002 and 2018. The downward trend in 2002 and 2010, out of the 3 games played in 2002, loss 2 and draw 1 while in 2010, they played 3 games loss 2 and draw 1. In other words, they did not win any game in 2002 and 2010.

The upward trend was in 2006, 2014, and 2018. In 2014, they played 5 games, won 3, lost 1, and also had a draw. While in 2006 and 2018 they played in 7 games, won 4 and 3 draws in 2006, and also won 6 games and a draw in 2018.
### Team Nigeria
Nigeria’s performance in the last 5 years; in 2002 and 2010 they played 3 games, won none of the matches, lost 2, and also had a draw. In 2014, they played 4 games, won 1, lost 2, and also had a draw. In 2018, they played 3 games. Won none, loss 2 and 2 draw. In 2006, Nigeria did not participate in the FIFA world cup.
### Analysis of countries that won and lost the world cup Between 2002 and 2018
Brazil won the cup in 2002; they won all the 7 games played with a total of 21 points, a total of 18 goals. However, the 5 teams that lost most were; China PR, Croatia, Ecuador, and France. In 2006 Germany won the FIFA world cup, they won 5 games out of the 7 games played, lost 1 and also had a draw. They scored 14 goals with a total of 16 points. However, the 3 teams that lost most that are; underperformed teams were Costa Rica, Serbia & Montenegro, and Togo. In 2010, Netherland won the FIFA world cup. In all the 7 games played, they won 6 and lost 1 game with a total of 18 points. They scored 12 goals. Algeria, North Korea, and Cameroon had the most loss matches. In 2010, Netherland won the FIFA world cup. In all the 7 games played, they won 6 and lost 1 game with a total of 18 points. They scored 12 goals. Algeria, North Korea, and Cameroon had the most loss matches. In 2014, Germany won the FIFA world cup for the second time after 2006. Out of the 7 games played, they won 6 and also had a draw with a total of 19 points. They scored 18 goals, higher than the total number of goals scored in 2006. Australia, Cameroon, and Honduras had the most loss matches. Finally, in 2018 France won the FIFA world cup. Out of the 7 games played, they won 6 games and lost 1 of the game with a total of 19 points and 16 goals scored. Egypt, England, and Panama had the most loss matches.
### OVERVIEW
<img width="960" alt="2023-04-05" src="https://user-images.githubusercontent.com/114405595/229874476-03af0411-e0c7-44c1-8776-209c6f55c78b.png">

<img width="960" alt="2023-04-05 (1)" src="https://user-images.githubusercontent.com/114405595/229870060-d2e312c5-cdf0-4bf3-9ff8-d6dbc29c3d86.png">
<img width="960" alt="2023-04-05 (2)" src="https://user-images.githubusercontent.com/114405595/229870135-b84b096c-c256-43f3-9dbb-372a4d00c58a.png">
<img width="960" alt="2023-04-05 (3)" src="https://user-images.githubusercontent.com/114405595/229870172-24202367-ddc2-4230-a20f-84aeba2ea9d8.png">
<img width="960" alt="2023-04-05 (4)" src="https://user-images.githubusercontent.com/114405595/229870205-be9e274e-d66f-41db-b724-ba96265a557f.png">
<img width="960" alt="2023-04-05 (5)" src="https://user-images.githubusercontent.com/114405595/229870243-7b6b73df-497a-42fe-b2c0-9680447194a9.png">
<img width="960" alt="2023-04-05 (6)" src="https://user-images.githubusercontent.com/114405595/229870258-01bbd14a-0632-41da-94f0-ad3b43626773.png">
<img width="960" alt="2023-04-05 (8)" src="https://user-images.githubusercontent.com/114405595/229871153-884a8c8e-bfb3-4ff5-8356-df5cc8c33e7e.png">
<img width="960" alt="2023-04-05 (9)" src="https://user-images.githubusercontent.com/114405595/229871172-948fcb3d-6331-4f28-810d-02e78708c550.png">


## BANK MARKETING ANALYST

### OVERVIEW
<img width="960" alt="2023-04-05 (10)" src="https://user-images.githubusercontent.com/114405595/229871492-cfdbc45c-1660-4b0d-a4d6-1079f0e517c5.png">

<img width="960" alt="2023-04-05 (11)" src="https://user-images.githubusercontent.com/114405595/229871519-7b948858-d173-4938-9dea-02d151d4e49f.png">
<img width="960" alt="2023-04-05 (12)" src="https://user-images.githubusercontent.com/114405595/229871536-567108d8-901b-4f69-9874-8d21364dcff5.png">
<img width="960" alt="2023-04-05 (13)" src="https://user-images.githubusercontent.com/114405595/229871558-9bbb89a2-3968-4583-b24e-9f33bcd3399f.png">
<img width="960" alt="2023-04-05 (14)" src="https://user-images.githubusercontent.com/114405595/229871575-619590ad-bcf5-4b23-8b66-d17836b5bf95.png">
<img width="960" alt="2023-04-05 (15)" src="https://user-images.githubusercontent.com/114405595/229871603-230c336d-35f4-45c5-aa87-68bf5f9bf12c.png">
<img width="960" alt="2023-04-05 (16)" src="https://user-images.githubusercontent.com/114405595/229871632-eb81f294-1602-4149-8540-edc69ad11b86.png">
<img width="960" alt="2023-04-05 (17)" src="https://user-images.githubusercontent.com/114405595/229871658-cf4d300f-d103-4abc-97e1-7703b0d8678b.png">
<img width="960" alt="2023-04-05 (18)" src="https://user-images.githubusercontent.com/114405595/229871684-55fc60a1-62be-41ad-a2b8-a063d6de262c.png">
<img width="960" alt="2023-04-05 (19)" src="https://user-images.githubusercontent.com/114405595/229871703-a5e47350-fe80-4e45-a155-52978102aa5e.png">

