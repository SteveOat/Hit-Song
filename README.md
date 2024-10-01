```bash
import seaborn as sns
import matplotlib.pyplot as plt

# Assuming 'df' is your original DataFrame and 'Popularity' is the target column
popularity_corr = df.corr()[['Streams']]  # Select only the 'Popularity' row

plt.figure(figsize=(10, 8))  # Adjust figure size as needed
sns.heatmap(popularity_corr, annot=True, cmap='coolwarm', fmt=".2f")
plt.title("Pearson Correlation with Streams")
plt.show()
```
