import pandas as pd
import numpy as np

df = pd.read_csv("spotify (1).csv", encoding="latin1", on_bad_lines="skip")

print("Cantidad de datos:", df.shape)
print("\nTipos de variables:")
print(df.dtypes)

num = df.select_dtypes(include=[np.number])

print("\nRangos (mínimo y máximo):")
print(num.agg(["min", "max"]).T)

print("\nMedia, mediana y desviación estándar:")
print(num.agg(["mean", "median", "std"]).T.round(3))
