import pandas as pd
import numpy as np

df = pd.read_csv("spotify (1).csv", encoding="latin1", on_bad_lines="skip")

print("FILAS_COLUMNAS:", df.shape)
print("INFO:")
df.info()

num = df.select_dtypes(include=[np.number])

print("\nRANGOS_MIN_MAX:")
print(num.agg(["min","max"]).T)

print("\nMEDIA_MEDIANA_DESVSTD:")
print(num.agg(["mean","median","std"]).T.round(6))

print("\nCONCLUSIONES_BREVES:")
for c in num.columns:
    s = num[c].dropna()
    if s.empty: 
        continue
    m, med, sd = s.mean(), s.median(), s.std()
    skew = "simétrica"
    if m > med: skew = "asimetría_derecha"
    elif m < med: skew = "asimetría_izquierda"
    print(f"{c}: media={m:.6f}, mediana={med:.6f}, desvstd={sd:.6f}, {skew}")
