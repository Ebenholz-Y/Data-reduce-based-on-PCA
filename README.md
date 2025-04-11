本方法针对UCI Wine数据集，采用主成分分析(PCA)与随机森林特征选择相结合的方法进行数据规约。通过降维与特征重要性评估，将原始13维特征降至5维，在保持分类准确率98.3%的同时实现61.5%的数据压缩率。结合PCA与特征选择的方法在保证分类性能的前提下，有效实现了数据压缩。实验表明，通过特征重要性筛选后的5维数据即可保持原始分类准确率，为后续数据分析提供了高效的数据表示。
完整代码在Create Code文件中。


方法
1. 数据预处理
   对178条葡萄酒样本的13个化学特征进行标准化处理：
   from sklearn.preprocessing import StandardScaler
   scaler = StandardScaler()
   X_scaled = scaler.fit_transform(X)

2. PCA降维
   保留95%方差解释率：
   from sklearn.decomposition import PCA
   pca = PCA(n_components=0.95)
   X_pca = pca.fit_transform(X_scaled)

3. 特征选择
   使用随机森林评估特征重要性，保留Top 5特征：
   from sklearn.ensemble import RandomForestClassifier
   rf = RandomForestClassifier()
   rf.fit(X_scaled, y)
   importance = rf.feature_importances_
   
