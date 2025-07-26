# 📊 Análisis de Ventas 

Este proyecto muestra cómo analizar datos de ventas de varias tiendas y crear gráficos con Python.

---

## ✅ Pasos principales

### 1. **Importar datos**
```python
import pandas as pd

url1 = "https://.../tienda_1.csv"
url2 = "https://.../tienda_2.csv"
url3 = "https://.../tienda_3.csv"
url4 = "https://.../tienda_4.csv"

tienda1 = pd.read_csv(url1)
tienda2 = pd.read_csv(url2)
tienda3 = pd.read_csv(url3)
tienda4 = pd.read_csv(url4)
```

---

### 2. **Unir datos**
```python
tienda1['Tienda'] = 'Tienda 1'
tienda2['Tienda'] = 'Tienda 2'
tienda3['Tienda'] = 'Tienda 3'
tienda4['Tienda'] = 'Tienda 4'

df = pd.concat([tienda1, tienda2, tienda3, tienda4], ignore_index=True)
```

---

### 3. **Calcular métricas**
- **Facturación por tienda:**
```python
facturacion = df.groupby('Tienda')['Precio'].sum().reset_index(name='Facturación Total')
```

- **Promedio de calificación:**
```python
calificacion = df.groupby('Tienda')['Calificación'].mean().reset_index(name='Promedio Calificación')
```

- **Categoría más vendida:**
```python
ventas_cat = df.groupby(['Tienda','Categoría del Producto']).size().reset_index(name='Cantidad')
```

---

### 4. **Gráficos con matplotlib**
- **Barras:**
```python
import matplotlib.pyplot as plt
plt.bar(facturacion['Tienda'], facturacion['Facturación Total'], color='skyblue')
plt.title('Facturación por Tienda')
plt.show()
```

- **Línea:**
```python
plt.plot(facturacion['Tienda'], facturacion['Facturación Total'], marker='o')
plt.title('Facturación por Tienda')
plt.show()
```

- **Circular (Pie):**
```python
tienda1 = df[df['Tienda']=='Tienda 1'].sort_values('Producto_Vendido',ascending=False).head(10)
plt.pie(tienda1['Producto_Vendido'], labels=tienda1['Producto'], autopct='%1.1f%%')
plt.title('Top 10 Productos - Tienda 1')
plt.show()
```
---
