# project

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = sns.load_dataset("taxis")

df.head(2)

df.tail(2)

df.dtypes 


df.shape

df["pickup"].agg(["min", "max"])

cond = (df["pickup"] >= "2019-03-01") & (df["pickup"] < "2019-04-01")
df_mar = df[cond].copy()


df_mar["pickup"].agg(["min", "max"])

df_mar.shape[0]

df_mar["pickup"].dt.day_name().value_counts()

df_mar["color"].nunique()

df_mar["color"].unique().tolist()

df["payment"].unique().tolist()

df_mar["payment"].value_counts(normalize=True) * 100

df_mar["tip"].mean()

df_mar["tip"].median()

df_mar.groupby("payment")["tip"].mean() 

df_mar["passengers"].mean()

df_mar["fare"].sum()

df_mar["pickup"].dt.hour.value_counts().head(5)

df.head(2)

df_mar["same_borough"] =(df_mar["pickup_borough"] == df_mar["dropoff_borough"]).astype(int)

df_mar[["pickup_borough", "dropoff_borough", "same_borough"]].head()

df_mar["same_borough"].value_counts()

cond = df_mar["pickup_borough"] == "Manhattan"
df_mar.loc[cond, "distance"].mean()

df_mar["duration"] = (df_mar["dropoff"] - df_mar["pickup"]).dt.total_seconds() / 60.

df_mar.groupby("same_borough")["duration"].mean()

df_mar["pickup_hour"] = df_mar["pickup"].dt.hour

df_mar["km_per_min"] = df_mar["distance"] / df_mar["duration"]

df_mar.groupby("pickup_hour")["km_per_min"].mean().sort_index() 

# Data to plot
plt_data = df_mar.groupby("pickup_hour")["km_per_min"].mean().sort_index()
# Plot
fig, ax = plt.subplots(figsize=(7, 3))
plt_data.plot.bar(ax=ax)
ax.set_ylabel("Speed (km / min)")
ax.set_title("Average speed (km / min) by pickup hour")
plt.show()





FIFA WORLD CUP 2018

OVERVIEW
<img width="960" alt="2023-04-05" src="https://user-images.githubusercontent.com/114405595/229874476-03af0411-e0c7-44c1-8776-209c6f55c78b.png">

<img width="960" alt="2023-04-05 (1)" src="https://user-images.githubusercontent.com/114405595/229870060-d2e312c5-cdf0-4bf3-9ff8-d6dbc29c3d86.png">
<img width="960" alt="2023-04-05 (2)" src="https://user-images.githubusercontent.com/114405595/229870135-b84b096c-c256-43f3-9dbb-372a4d00c58a.png">
<img width="960" alt="2023-04-05 (3)" src="https://user-images.githubusercontent.com/114405595/229870172-24202367-ddc2-4230-a20f-84aeba2ea9d8.png">
<img width="960" alt="2023-04-05 (4)" src="https://user-images.githubusercontent.com/114405595/229870205-be9e274e-d66f-41db-b724-ba96265a557f.png">
<img width="960" alt="2023-04-05 (5)" src="https://user-images.githubusercontent.com/114405595/229870243-7b6b73df-497a-42fe-b2c0-9680447194a9.png">
<img width="960" alt="2023-04-05 (6)" src="https://user-images.githubusercontent.com/114405595/229870258-01bbd14a-0632-41da-94f0-ad3b43626773.png">
<img width="960" alt="2023-04-05 (8)" src="https://user-images.githubusercontent.com/114405595/229871153-884a8c8e-bfb3-4ff5-8356-df5cc8c33e7e.png">
<img width="960" alt="2023-04-05 (9)" src="https://user-images.githubusercontent.com/114405595/229871172-948fcb3d-6331-4f28-810d-02e78708c550.png">


BANK MARKETING ANALYST

OVERVIEW
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

