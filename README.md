### EX4 Implementation of Cluster and Visitor Segmentation for Navigation patterns
### DATE: 20-11-2026
### AIM: To implement Cluster and Visitor Segmentation for Navigation patterns in Python.
### Description:
<div align= "justify">Cluster visitor segmentation refers to the process of grouping or categorizing visitors to a website, 
  application, or physical location into distinct clusters or segments based on various characteristics or behaviors they exhibit. 
  This segmentation allows businesses or organizations to better understand their audience and tailor their strategies, marketing efforts, 
  or services to meet the specific needs and preferences of each cluster.</div>
  
### Procedure:
1) Read the CSV file: Use pd.read_csv to load the CSV file into a pandas DataFrame.
2) Define Age Groups by creating a dictionary containing age group conditions using Boolean conditions.
3) Segment Visitors by iterating through the dictionary and filter the visitors into respective age groups.
4) Visualize the result using matplotlib.

### Program:
```python
import pandas as pd
import matplotlib.pyplot as plt

# Read CSV file
df = pd.read_csv("clustervisitor.csv")

# Select Age feature
X = df["Age"].tolist()

# Number of clusters
k = 3

# Step 1: Choose initial centroids (first k values)
centroids = X[:k]

while True:
    clusters = [[] for _ in range(k)]
    labels = []

    # Step 2: Assign each data point to the nearest centroid
    for value in X:
        distances = [abs(value - c) for c in centroids]
        cluster = distances.index(min(distances))
        clusters[cluster].append(value)
        labels.append(cluster)

    # Step 3: Calculate new centroids
    new_centroids = []
    for cluster in clusters:
        if len(cluster) > 0:
            new_centroids.append(sum(cluster) / len(cluster))
        else:
            new_centroids.append(0)

    # Step 4: Stop if centroids do not change
    if new_centroids == centroids:
        break

    centroids = new_centroids

# Add cluster labels to DataFrame
df["Cluster"] = labels

# Display complete dataset
print("Complete Dataset")
print(df)

print("\nVisitor Segmentation (Cluster-wise)\n")

# Display cluster-wise output
for i in range(k):
    print(f"Cluster {i}")
    print(df[df["Cluster"] == i])
    print("-" * 50)




```
### Output:
<img width="1534" height="894" alt="image" src="https://github.com/user-attachments/assets/36f4897d-486a-4012-8aa9-f5023e416813" />

### Visualization:
```python
# Visualize clusters
plt.figure(figsize=(8, 6))

colors = ["red", "blue", "green"]

for i in range(k):
    cluster_data = df[df["Cluster"] == i]
    plt.scatter(
        cluster_data["Age"],
        cluster_data["Cluster"],
        color=colors[i],
        s=80,
        label=f"Cluster {i}"
    )

plt.xlabel("Age")
plt.ylabel("Cluster")
plt.title("Visitor Segmentation using K-Means")
plt.legend()
plt.grid(True)
plt.show()
```
### Output:
<img width="504" height="387" alt="image" src="https://github.com/user-attachments/assets/f2d189b0-8de9-4c70-94f2-16b6e6d3add4" />


### Result:
Thus the Cluster and Visitor Segmentation for Navigation patterns are executed successfully
